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
| `%r` | zaimek zwrotny | siebie |
| `%S %O %P %Q %R` | jak wyzej, ale z wielkiej litery (na poczatek zdania) | Ona, Ja, Jej, Jej, Siebie |
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

**Zaimki** (`%s/%o/%p/%q/%r`) pokrywaja w praktyce:
- mianownik (`%s`: on/ona/ono/oni),
- biernik (`%o`: go/ja/je/ich),
- dopelniacz w funkcji dzierzawczej (`%p`/`%q`: jego/jej/ich -- to naprawde forma dopelniacza uzyta jako "jego/jej", tak jak w prawdziwym polskim).

**Brakuje**: celownika (komu/czemu -- "jemu/jej/im"), narzednika (z kim/czym -- "nim/nia/nimi"), miejscownika (o kim/czym -- "nim/niej/nich"). Jesli twoj komunikat potrzebuje jednej z tych form zaimka, **napisz zdanie tak, zeby ich unikac** (patrz przyklady nizej), albo popros o rozszerzenie `$gender_utils` o brakujace przypadki (to wykonalne -- male, zamkniete tabele -- ale wymaga swiadomej decyzji, bo dotyka wspoldzielonej infrastruktury).

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

- Brak pelnej odmiany przez 7 przypadkow (patrz sekcja 5).
- Brak rozroznienia rodzaju meskoosobowego/niemeskoosobowego w liczbie mnogiej (prawdziwy polski rozroznia "oni"/"one" w zaleznosci od tego, czy w grupie jest mezczyzna -- tu zawsze "oni").
- Brak zgodnosci rodzaju w czasie przeszlym (polski czasownik w czasie przeszlym odmienia sie przez rodzaj, np. "zrobil"/"zrobila" -- to nie jest obslugiwane; komunikaty unikaja czasu przeszlego z podmiotem o zmiennym rodzaju, uzywajac np. czasu terazniejszego albo przeformulowania zdania).
- Przymiotniki stanu obiektu (otwarty/zamkniety/pusty) zawsze w formie nijakiej, niezaleznie od prawdziwego rodzaju rzeczownika.
- Zero diakrytykow, wszedzie (patrz sekcja 1).

## 9. Checklist przed dodaniem nowej tresci

- [ ] Zero znakow spoza ASCII (`grep -cP '[^\x00-\x7F]' plik` powinno dawac 0 -- ten test wylapie kazdy polski znak diakrytyczny, niezaleznie od tego, ktory to konkretnie).
- [ ] Jesli uzywasz `%<czasownik>` dla zwyklego czasownika (nie "ma"/"jest") -- podaj obie formy przez `/`.
- [ ] Jesli komunikat odnosi sie do nazwy obiektu w innym przypadku niz mianownik -- sprawdz, czy da sie przeformulowac zdanie (sekcja 5), zamiast zakladac, ze odmiana zadziala automatycznie.
- [ ] Liczby czegokolwiek -- uzyj `$polish_utils:count()`, nie doklejaj "-y"/"-ow" na sztywno.
- [ ] Przetestuj na zywo z kilkoma roznymi `@gender` (przynajmniej `nijaki`, `meski`, `zenski`, `mnogi`), zeby zobaczyc realny wynik podstawiania.
