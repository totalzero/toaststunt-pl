# Tworzenie tresci po polsku w toaststunt-pl

Ten dokument opisuje, jak pisac nowa tresc MOO (pokoje, przedmioty, komunikaty, komendy) w tym forku tak, zeby poprawnie dzialala z polskim systemem jezykowym wbudowanym w baze `toastcore.db`. Jest przeznaczony dla programistow i budowniczych (wizardow/programistow MOO), nie dla zwyklych graczy.

Jesli szukasz szybkiej wersji tego samego materialu bezposrednio w grze, wpisz `help polski-tworcy` po zalogowaniu.

## Spis tresci

1. [Zasada ASCII-only i dlaczego istnieje](#1-zasada-ascii-only-i-dlaczego-istnieje)
2. [System rodzaju: `$gender_utils`](#2-system-rodzaju-gender_utils)
3. [Podstawianie zaimkow: `pronoun_sub` i `%s/%o/%p/%q/%r`](#3-podstawianie-zaimkow-pronoun_sub-i-sopqr)
4. [Odmiana czasownikow: `%<czasownik>` i pulapka `get_conj`](#4-odmiana-czasownikow-czasownik-i-pulapka-get_conj)
5. [Odmiana przez przypadki -- co dziala, a co nie](#5-odmiana-przez-przypadki----co-dziala-a-co-nie)
6. [Liczebniki i rzeczowniki: `$polish_utils:count()`](#6-liczebniki-i-rzeczowniki-polish_utilscount)
7. [Aliasy komend](#7-aliasy-komend)
8. [Znane, swiadome uproszczenia](#8-znane-swiadome-uproszczenia)
9. [Checklist przed dodaniem nowej tresci](#9-checklist-przed-dodaniem-nowej-tresci)
10. [Status prac i co zostalo do zrobienia](#10-status-prac-i-co-zostalo-do-zrobienia)

---

## 1. Zasada ASCII-only i dlaczego istnieje

Cala tresc w tym forku -- komunikaty silnika, baza `toastcore.db`, ta dokumentacja -- jest pisana w jezyku polskim **bez znakow diakrytycznych** (a/e/l/n/o/s/z/z zamiast ich odpowiednikow z ogonkami/kreskami). To nie jest tylko kwestia stylu.

Silnik MOO (LambdaMOO/Stunt/ToastStunt) reprezentuje stringi jako **surowe ciagi bajtow**, nie jako sekwencje znakow Unicode. Funkcje takie jak `length()`, `index()` czy wycinanie podlancuchow (`string[a..b]`) licza i tna po **bajtach**, nie po znakach. Prawdziwy polski znak diakrytyczny w UTF-8 (np. `a` z ogonkiem) zajmuje 2 bajty -- dla silnika to "dwa znaki", nie jeden. Oznacza to, ze:

- `length("wiadomosc")` (bez polskich znakow) zwroci poprawna liczbe liter,
- ale `length()` na stringu z prawdziwymi diakrytykami policzy bajty, nie litery -- np. slowo z trzema znakami z ogonkami/kreskami "urosnie" o kilka dodatkowych jednostek dlugosci,
- a jakakolwiek operacja przycinania/dzielenia stringa (np. formatowanie szerokosci kolumny, `%(property)` w `pronoun_sub`, wlasne funkcje formatujace tekst) moze rozciac wielobajtowy znak w polowie, dajac uszkodzony (nieczytelny) wynik.

Zeby uniknac calej tej klasy bledow -- raz na zawsze, dla kazdej tresci napisanej w ten sposob -- ten projekt uzywa transliteracji ASCII zamiast prawdziwych diakrytykow. To dziala poprawnie z kazdym istniejacym kodem MOO, ktory operuje na dlugosci/podlancuchach stringow, bez zadnych wyjatkow czy pulapek.

**Zasada dla nowej tresci: pisz po polsku, ale zawsze zamieniaj znaki diakrytyczne na ich ASCII-owe odpowiedniki:**

| Polska litera (nazwa) | Zamiennik ASCII |
|---|---|
| a z ogonkiem | a |
| c z kreska | c |
| e z ogonkiem | e |
| l przekreslone | l |
| n z kreska | n |
| o z kreska | o |
| s z kreska | s |
| z z kropka | z |
| z z kreska | z |

(Wielkie litery analogicznie.)

Ten sam dokument, jak widac, jest napisany zgodnie z ta zasada -- nie znajdziesz w nim ani jednego prawdziwego polskiego znaku diakrytycznego, tylko ich nazwy opisane slownie tam, gdzie trzeba je rozroznic.

Surowe bajty UTF-8 od gracza (np. gdyby ktos mimo wszystko wpisal prawdziwe polskie znaki w czacie) przejda przez siec bez problemu i wyswietla sie poprawnie -- problem dotyczy tylko **kodu MOO**, ktory manipuluje takim stringiem programistycznie. Jesli kiedys zdecydujesz sie dopuscic prawdziwe diakrytyki w tresci pisanej przez graczy (nie w kodzie silnika), pamietaj o tym ograniczeniu i unikaj operacji dlugosciowych/podlancuchowych na takim tekscie.

## 2. System rodzaju: `$gender_utils`

Kazdy obiekt (typowo gracz) moze miec ustawiona wlasciwosc `.gender`, ktora steruje doborem zaimkow i odmiany czasownikow w komunikatach. Gracz ustawia to poleceniem:

```
@gender <rodzaj>
```

Dostepne wartosci (`$gender_utils.genders`):

| Wartosc | Znaczenie | Zaimek (mianownik) |
|---|---|---|
| `nijaki` | rodzaj nijaki (domyslny) | ono |
| `meski` | rodzaj meski | on |
| `zenski` | rodzaj zenski | ona |
| `dowolny` | dowolny/oba (forma "on/ona") | on/ona |
| `mnogi` | mnogi (liczba mnoga) | oni |
| `spivak`, `gwiazdka` | neutralne zaimki (rzadko uzywane) | ono (zastepczo) |
| `egotystyczny` | zart -- "ja" | ja |
| `krolewski` | zart -- "my" (krolewskie my) | my |
| `drugoosobowy` | odnosi sie do "ty" (np. obiekt "You") | ty |

`spivak`/`gwiazdka` to odpowiedniki angielskich neopronoun-schematow (Spivak/`*e`), ktore nie maja ustalonego polskiego odpowiednika -- zamiast wymyslac neologizm, uzywaja tych samych form co `nijaki`. To swiadome uproszczenie.

## 3. Podstawianie zaimkow: `pronoun_sub` i `%s/%o/%p/%q/%r`

Wiekszosc komunikatow w bazie przechodzi przez `$string_utils:pronoun_sub(tekst, kto)`, ktora podmienia specjalne znaczniki procentowe:

| Znacznik | Znaczenie | Przyklad (rodzaj `zenski`) |
|---|---|---|
| `%s` | zaimek w mianowniku | ona |
| `%o` | zaimek w bierniku | ja |
| `%p` | zaimek dzierzawczy | jej |
| `%q` | zaimek dzierzawczy (forma absolutna) | jej |
| `%c` | zaimek w celowniku | jej |
| `%z` | zaimek w narzedniku | nia |
| `%m` | zaimek w miejscowniku | niej |
| `%r` | zaimek zwrotny | siebie |
| `%S %O %P %Q %C %Z %M %R` | jak wyzej, ale z wielkiej litery (na poczatek zdania) | Ona, Ja, Jej, Jej, Jej, Nia, Niej, Siebie |
| `%n` `%d` `%i` `%t` `%l` | odpowiednio: kto/dobj/iobj/thing/location | (nazwa obiektu) |

Przyklad:

```
$string_utils:pronoun_sub("%S siedzi i czyta %p ksiazke.", player)
```

dla gracza `zenski` da: `"Ona siedzi i czyta jej ksiazke."` (patrz sekcja 5 -- "jej ksiazke" powinno gramatycznie brzmiec "swoja ksiazke", ale zaimki dzierzawcze 3-osobowe nie sa tu odmieniane przez przypadek rzeczownika, ktory nastepuje).

**Znana homografia warta zapamietania**: `%o` dla rodzaju `zenski` to string `"ja"`. W prawdziwej polszczyznie biernik zaimka "ona" to "ja" z ogonkiem na koncowym "a" -- po zdjeciu ogonka (zasada ASCII-only, sekcja 1) wychodzi dokladnie to samo, co zaimek pierwszoosobowy "ja" (ja/mnie). To nieunikniona konsekwencja transliteracji, nie blad -- kontekst zdania (pozycja podmiotu vs. dopelnienia po czasowniku) zwykle rozstrzyga znaczenie, ale warto o tej homografii wiedziec przy pisaniu i czytaniu tresci.

## 4. Odmiana czasownikow: `%<czasownik>` i pulapka `get_conj`

Wewnatrz tekstu przekazywanego do `pronoun_sub` mozesz uzyc `%<czasownik>`, zeby czasownik automatycznie dostosowal sie do liczby/rodzaju "kto":

```
$string_utils:pronoun_sub("%S %<krzyczy/krzycza> gniewnie.", player)
```

**Skladnia `%<forma_pojedyncza/forma_mnoga>`** (ukosnik oddziela dwie formy) jest zawsze bezpieczna -- dziala poprawnie niezaleznie od rodzaju "kto", bo obie formy sa podane explicite.

**Pulapka, o ktorej trzeba wiedziec**: jesli podasz **tylko jedno slowo** bez ukosnika (np. `%<ma>`), mechanizm `get_conj` uzyje go **doslownie bez zadnej zmiany**, jesli rodzaj "kto" jest jednym z pojedynczych (`nijaki`/`meski`/`zenski`/`dowolny`/`spivak`/`gwiazdka`) -- czyli w **najczestszym przypadku**. Tabela odmiany (`$gender_utils.have`/`.be`) jest sprawdzana **tylko** wtedy, gdy trzeba wyprowadzic **przeciwna** liczbe (np. gdy "kto" akurat ma rodzaj `mnogi`/`egotystyczny`/`krolewski`/`drugoosobowy`).

Oznacza to w praktyce:

- `%<ma>` -- dziala poprawnie dla typowego (pojedynczego) gracza (`ma` uzyte doslownie, poprawnie), **i** poprawnie dla rzadkiego przypadku liczby mnogiej (automatycznie zamieni na `maja`). To jest wlasciwy sposob pisania.
- `%<has>` (stary angielski wyzwalacz) -- dziala **przypadkowo** poprawnie dla liczby mnogiej (bo tabela rozpoznaje rowniez stare angielskie slowa jako synonimy, dla zgodnosci wstecznej), ale dla zwyklego pojedynczego gracza wypisze doslowne angielskie "has" w polskim zdaniu. **Nie pisz nowej tresci w ten sposob.**
- Dla zwyklych czasownikow (nie "miec"/"byc") **zawsze podawaj obie formy jawnie** przez `/`, np. `%<otwiera/otwieraja>`, `%<idzie/ida>` -- nie ma zadnego mechanizmu automatycznego wyprowadzania jednej formy z drugiej dla dowolnego polskiego czasownika (dziala to tylko dla "ma"/"jest" jako wbudowanych nieregularnych przypadkow).

Ta sama zasada dotyczy bezposredniego wywolania `$gender_utils:get_conj(specyfikacja, obiekt)`.

## 5. Odmiana przez przypadki -- co dziala, a co nie

To najwazniejsze ograniczenie do zrozumienia, jesli piszesz bardziej rozbudowana tresc.

**Zaimki** (`%s/%o/%p/%q/%c/%z/%m/%r`) pokrywaja wszystkie 7 przypadkow:
- mianownik (`%s`: on/ona/ono/oni),
- biernik (`%o`: go/ja/je/ich),
- dopelniacz w funkcji dzierzawczej (`%p`/`%q`: jego/jej/ich -- to naprawde forma dopelniacza uzyta jako "jego/jej", tak jak w prawdziwym polskim),
- celownik (`%c`: jemu/jej/im -- komu/czemu),
- narzednik (`%z`: nim/nia/nimi -- z kim/czym),
- miejscownik (`%m`: nim/niej/nich -- o kim/czym),
- zwrotny (`%r`: zawsze "siebie", niezaleznie od rodzaju/liczby).

Dodane 2026-07-16 -- wczesniej brakowalo celownika/narzednika/miejscownika; rozszerzono `$gender_utils` o trzy dodatkowe pary wlasciwosci (`.pc`/`.pz`/`.pm` + wersje z wielkiej litery), zdefiniowane raz na wspoldzielonym obiekcie-przodku (`#94`, Generic Gendered Object) i dziedziczone przez wszystkie obiekty z gestem/`.gender`, dokladnie tak samo jak istniejace `.ps`/`.po`/`.pp`.

**Nadal brakuje**: odmiany **rzeczownikow** (nazw obiektow/przedmiotow) przez przypadek -- to swiadome, pozostajace ograniczenie (patrz nizej), niezalezne od tego, ile przypadkow maja teraz zaimki.

**Rzeczowniki (nazwy obiektow/przedmiotow) nie sa odmieniane w ogole.** Nazwa przedmiotu (`.name`) zawsze pojawia sie w formie, w jakiej zostala zapisana -- typowo mianownik. Automatyczna odmiana dowolnego polskiego rzeczownika przez przypadek to zadanie na skale silnika jezykowego (NLP), nie na skale skryptu MOO -- polska deklinacja ma zbyt wiele wzorcow i wyjatkow, zeby dalo sie ja niezawodnie zautomatyzowac bez slownika form dla kazdego rzeczownika z osobna.

**Jak pisac komunikaty, zeby to ograniczenie nie bylo widoczne**: formuluj zdania tak, zeby nazwa obiektu zawsze mogla stac w mianowniku (albo w formie identycznej z mianownikiem), zamiast wymagac innego przypadka:

| Zamiast (wymaga biernika/celownika) | Napisz (nazwa w mianowniku) |
|---|---|
| "Bierzesz skrzynie." (D. "skrzynie" to biernik "skrzyni") | "Oto skrzynia: bierzesz ja." -- lub prosciej: uzyj zaimka zamiast nazwy: "Bierzesz to." |
| "Dajesz mieczowi polysk." (celownik) | "Miecz nabiera polysku." |

W praktyce najbezpieczniejszy wzorzec to unikanie umieszczania `%d`/`%i`/nazwy obiektu w pozycji wymagajacej przypadka innego niz mianownik -- albo pogodzenie sie z lekka niepoprawnoscia gramatyczna nazwy przedmiotu (to samo rozwiazanie, jakiego uzywa istniejaca tresc w tej bazie: przymiotniki stanu obiektu, np. "otwarte"/"zamkniete", zawsze uzywaja formy nijakiej niezaleznie od prawdziwego rodzaju rzeczownika -- swiadome uproszczenie, nie blad).

## 6. Liczebniki i rzeczowniki: `$polish_utils:count()`

Polski ma trzy formy rzeczownika w zaleznosci od liczby (1 / 2-4 / 5+, z wyjatkiem 12-14 ktore licza sie jak 5+). Do tego sluzy:

```
$polish_utils:count(n, forma_1, forma_2_4, forma_5plus)
```

Przyklad:

```
tostr(n, " ", $polish_utils:count(n, "miecz", "miecze", "mieczy"))
```

daje: `1 miecz`, `2 miecze`, `5 mieczy`, `22 miecze`, `12 mieczy`.

Uzyj tego **zawsze**, gdy wyswietlasz liczbe czegokolwiek graczowi (przedmioty w ekwipunku, wiadomosci, minuty/godziny itp.) -- to jedyny poprawny sposob na polska liczbe mnoga, angielski wzorzec "dodaj s" nie ma tu zastosowania.

## 7. Aliasy komend

Wiele standardowych komend ma juz polskie aliasy (np. `wez`/`poloz` obok `take`/`drop`) -- sprawdz `@list <obiekt>:<czasownik>` na obiekcie takim jak `$thing`, zeby zobaczyc wszystkie nazwy/aliasy danego czasownika. Jesli dodajesz nowa komende, ktora ma byc naturalnym elementem polskiej rozgrywki, rozwaz dodanie polskiego aliasu obok oryginalnej angielskiej nazwy (ta sama konwencja co reszta bazy) -- ale **nie tlumacz** nazw komend systemowych/administracyjnych typu `@programmer`, `@toad`, ktore pozostaja po angielsku celowo (to literalne polecenia, ktore trzeba wpisac, tlumaczenie ich zmieniloby skladnie, nie tylko opis).

## 8. Znane, swiadome uproszczenia

Te ograniczenia sa celowe (nie przeoczeniem) i nie powinny byc "naprawiane" bez swiadomej decyzji:

- Zaimki maja pelna odmiane przez wszystkie 7 przypadkow (od 2026-07-16); rzeczowniki (nazwy obiektow) nie sa odmieniane wcale i to zostaje tak celowo (patrz sekcja 5).
- Brak rozroznienia rodzaju meskoosobowego/niemeskoosobowego w liczbie mnogiej (prawdziwy polski rozroznia "oni"/"one" w zaleznosci od tego, czy w grupie jest mezczyzna -- tu zawsze "oni").
- Brak zgodnosci rodzaju w czasie przeszlym (polski czasownik w czasie przeszlym odmienia sie przez rodzaj, np. "zrobil"/"zrobila" -- to nie jest obslugiwane; komunikaty unikaja czasu przeszlego z podmiotem o zmiennym rodzaju, uzywajac np. czasu terazniejszego albo przeformulowania zdania).
- Przymiotniki stanu obiektu (otwarty/zamkniety/pusty) zawsze w formie nijakiej, niezaleznie od prawdziwego rodzaju rzeczownika.
- Zero diakrytykow, wszedzie (patrz sekcja 1).
- Angielskie nazwy dni/miesiecy w wyjsciu `ctime()` (np. "Wed Jul 15...") -- swiadoma decyzja uzytkownika (2026-07-16), zeby tego NIE naprawiac. `ctime()` w `src/numbers.cc` uzywa `strftime()` w locale "C", a zadna tresc bazy tego nie zmienia.
- Czas trwania w opcjach mail (`@mailoption expire`) i sekwencje `@unsend`/`unsend_sequences` (before/after/since/until/subject/body/last) -- pozostaja po angielsku, bo parser rozpoznaje doslownie te angielskie slowa kluczowe (`$time_utils:parse_english_time_interval`, itp.); przetlumaczenie samego opisu bez zmiany parsera wprowadziloby gracza w blad co do tego, co naprawde da sie wpisac.
- **Pulapka "sklejonego slowa-klucza"** (ten sam wzorzec, co `prep_list` z Fazy 1, ale odkryty pozniej na `@blacklist`/`@toad`): kilka wizardowskich narzedzi (`@blacklist`/`@graylist`/`@redlist`/`@spooflist`, `@toad`) wyznacza angielskie slowo (np. `"blacklist"`) na podstawie nazwy wywolanej komendy (`$login:listname(...)`), a nastepnie **jednoczesnie** (a) wkleja to slowo bezposrednio w tekst komunikatu dla gracza ("is already blacklisted") i (b) uzywa tej samej zmiennej do wywolania czasownika po nazwie (`$login:(which + "_add")`). Przetlumaczenie samego tekstu bez nadania `$login` rownoleglych polskich nazw czasownikow albo zepsuloby wywolanie, albo zostawiloby angielskie slowo wklejone w srodek polskiego zdania. W `@blacklist` przetlumaczono wszystkie samodzielne komunikaty, a te "sklejone" zdania zostawiono jak byly (udokumentowane, nie przeoczone). **Jesli dodajesz nowy kod w tym stylu (budowanie nazwy czasownika/wlasciwosci z tej samej zmiennej, co widoczny dla gracza tekst) -- rozdziel od razu te dwie role (osobna zmienna do wyswietlania, osobna do dispatchu), zeby uniknac tej samej pulapki.**

## 9. Checklist przed dodaniem nowej tresci

- [ ] Zero znakow spoza ASCII (`grep -cP '[^\x00-\x7F]' plik` powinno dawac 0 -- ten test wylapie kazdy polski znak diakrytyczny, niezaleznie od tego, ktory to konkretnie).
- [ ] Jesli uzywasz `%<czasownik>` dla zwyklego czasownika (nie "ma"/"jest") -- podaj obie formy przez `/`.
- [ ] Jesli komunikat odnosi sie do nazwy obiektu w innym przypadku niz mianownik -- sprawdz, czy da sie przeformulowac zdanie (sekcja 5), zamiast zakladac, ze odmiana zadziala automatycznie.
- [ ] Liczby czegokolwiek -- uzyj `$polish_utils:count()`, nie doklejaj "-y"/"-ow" na sztywno.
- [ ] Przetestuj na zywo z kilkoma roznymi `@gender` (przynajmniej `nijaki`, `meski`, `zenski`, `mnogi`), zeby zobaczyc realny wynik podstawiania.

## 10. Status prac i co zostalo do zrobienia

Stan na 2026-07-15 (koniec sesji). Lokalizacja jest prowadzona jako wyczerpujacy przeglad calej bazy: diagnoza (szukanie angielskiej tresci) -> tlumaczenie -> test na zywo -> commit. Ponizej lista tego, co jeszcze zostalo, zeby kolejna sesja mogla zaczac dokladnie w tym miejscu.

**W trakcie (etap "Generic Wizard", #57)** -- pozostale czasowniki do sprawdzenia i przetlumaczenia (kazdy ma tylko 1-4 trafien angielskiej tresci w ostatnim przegladzie): `mcd_2`, `@chown`, `@untoad`, `@new-password`, `@temp-newt`, `@lock-login`, wlasciwosci `toad_msg`/`toad_victim_msg`/`programmer_msg`/itp. (jeszcze nie sprawdzone -- moga juz byc po polsku, tak jak nieoczekiwanie okazalo sie z baza pomocy edytora, `#44`), `@newt`, `@log`, `@make-guest`, `@grant`, `@shutdown`, `@who-calls`, `@quota`, `@grepcore`, `@make-player`, `@unnewt`, `@guests`, `@corify`, `@deprogrammer`, `toad_cleanup`. Po zakonczeniu #57, warto zrobic jeszcze jeden przeglad #57 i #58 od zera -- metoda szukania angielskiej tresci po numerach linii jest zawodna, bo numery przesuwaja sie po kazdej edycji; skuteczniejsze jest przeszukiwanie tresci czasownikow bezposrednio (patrz uwaga w sekcji 1 o naturze bajtowej stringow -- ta sama ostroznosc dotyczy zaslepych przeszukiwan po linii).

**Kolejne, wieksze kieszenie tresci do sprawdzenia** (z ostatniego pelnego przegladu bazy): Frand's Player Class (`#88`, ~22 trafien -- poczta/teleportacja poza juz naprawionymi), mniejsze kieszenie 1-4 trafien na obiektach poczty (`#40`/`#14`/`#11`), News (`#61`), ANSI PC (`#100`), Housekeeper (`#71`), Registration Database (`#16`) i inne.

**Nowe zadanie zgloszone przez uzytkownika (2026-07-15), jeszcze nie zaczete**: w `docs/README.md`, sekcja polska (~linia 160) linkuje zewnetrznie do przewodnika dla poczatkujacych: `https://lisdude.com/moo/toaststunt_newbie.txt`. Trzeba:
1. Pobrac tresc tego pliku (`WebFetch` albo `curl`),
2. Przetlumaczyc na polski (ASCII-only, jak reszta tresci),
3. Zapisac jako nowy plik w `docs/` (np. `docs/PRZEWODNIK-DLA-POCZATKUJACYCH.md`),
4. Zmienic link w polskiej sekcji README tak, zeby wskazywal na ten nowy lokalny plik zamiast na zewnetrzna strone.
Sekcja angielska w README (~linia 23, "Getting Started Guide") ma zostac BEZ ZMIAN -- to dotyczy tylko polskiej sekcji.

**Po zakonczeniu calego przegladu**: zbudowac przykladowy, przechodni MOO (kilka/kilkanascie polaczonych lokacji, kilka przedmiotow, kilka NPC), zeby uzytkownik mogl sie zalogowac, stworzyc postac i osobiscie sprawdzic dzialanie lokalizacji w praktyce -- to byl warunek koncowy calego zadania (dopiero po potwierdzeniu, ze tlumaczenie jest kompletne).
