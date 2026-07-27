# Poradnik: budowa wlasnego swiata MOO od zera

*To jest oryginalny, praktyczny poradnik (nie tlumaczenie zewnetrznego zrodla), pisany od razu dla tego forka ToastStunt. Tak jak reszta polskiej dokumentacji w tym repozytorium, tresc jest ASCII-only (bez polskich znakow diakrytycznych) -- celowo, zobacz sekcje "Polski" w [README.md](README.md) po wyjasnienie. Kod (polecenia, nazwy wlasciwosci i czasownikow, fragmenty programow MOO) zostaje wpisywany doslownie -- kopiuj go bez zmian, tlumaczeniu podlega tylko tekst wyjasniajacy.*

Ten poradnik odpowiada na pytanie "mam juz dzialajacy, pusty serwer -- co dalej?". Pokazuje, krok po kroku i na jednym, ciaglym przykladzie, jak zbudowac prawdziwy, grywalny kawalek swiata: od pierwszego `@dig`, przez kilkadziesiat polaczonych ze soba lokacji, przedmioty i NPC-e, az po efekty specjalne takie jak zamki, cykl dnia i nocy, ekonomia czy proste zadania. Wszystko na przykladzie jednego, spojnego settingu -- ale kazda technika pokazana tutaj przenosi sie 1:1 na dowolny inny temat (wspolczesne miasto, statek kosmiczny, cokolwiek).

## Do kogo jest ten poradnik i czego wymaga

Zakladam, ze:

- Masz juz dzialajacy serwer ToastStunt z zaladowana baza (np. `toastcore.db`) -- jesli nie, zacznij od [Przewodnika dla poczatkujacych](PRZEWODNIK-DLA-POCZATKUJACYCH.md), ktory prowadzi od kompilacji serwera do pierwszego logowania.
- Masz konto gracza z uprawnieniami budowniczego (Generic Builder) lub programisty -- patrz [Podstawy dla Czarodziei](PODSTAWY-DLA-CZARODZIEI.md), jesli potrzebujesz taki status komus nadac.
- Znasz podstawy skladni jezyka MOO (zmienne, `if`/`for`, wywolania czasownikow) albo jestes gotowy zerkac do [Podrecznika Programisty](PODRECZNIK-PROGRAMISTY.md) przy okazji -- ten poradnik tlumaczy kazdy nowy element jezyka przy pierwszym uzyciu, ale nie jest pelnym kursem skladni od zera.

Nie zakladam nic ponad to. W szczegolnosci nie zakladam, ze budujesz na produkcyjnym, "zywym" serwerze -- wrecz przeciwnie, w Rozdziale 2 pierwsza rzecz, jaka robimy, to przygotowanie bezpiecznego miejsca do eksperymentow.

## Jak korzystac z tego poradnika

Kazdy rozdzial zaklada, ze poprzednie zostaly przerobione -- swiat budowany jest przyrostowo, tak jak robilbys to naprawde. Kod w blokach jest gotowy do wklejenia do klienta MOO (telnet/klient MUD) w takiej postaci, w jakiej jest -- tam, gdzie musisz podstawic swoj wlasny numer obiektu czy nazwe, jest to jasno opisane w tekscie przed blokiem kodu.

Spis tresci:

1. [Koncepcja swiata](#rozdzial-1-koncepcja-swiata)
2. [Przygotowanie warsztatu budowniczego](#rozdzial-2-przygotowanie-warsztatu-budowniczego)
3. [Pierwsza lokacja recznie](#rozdzial-3-pierwsza-lokacja-recznie)
4. [Budowa calej mapy](#rozdzial-4-budowa-calej-mapy)
5. [Przedmioty](#rozdzial-5-przedmioty)
6. [NPC-e i dialogi](#rozdzial-6-npc-e-i-dialogi)
7. [Efekty atmosferyczne](#rozdzial-7-efekty-atmosferyczne)
8. [Zamki, sekrety i pulapki](#rozdzial-8-zamki-sekrety-i-pulapki)
9. [Ekonomia](#rozdzial-9-ekonomia)
10. [Prosty system questow](#rozdzial-10-prosty-system-questow)
11. [Pomoc w grze dla wlasnej zawartosci](#rozdzial-11-pomoc-w-grze-dla-wlasnej-zawartosci)
12. [Testowanie i dalsze kierunki](#rozdzial-12-testowanie-i-dalsze-kierunki)

## Rozdzial 1: koncepcja swiata

Zanim wpiszesz pierwsze `@dig`, warto miec na kartce (albo w pliku tekstowym obok) odpowiedz na trzy pytania: **gdzie** to sie dzieje, **kto** tu mieszka i **co gracz moze tu robic**. Bez tego latwo skonczyc z dziesiecioma bezimiennymi "pokojami" bez charakteru. Ponizej jest odpowiedz na te trzy pytania dla przykladu, ktory bedziemy budowac przez caly poradnik -- ale potraktuj to jako szablon do wypelnienia wlasnym pomyslem (miasto wspolczesne, statek kosmiczny, cokolwiek), nie jako jedyna sluszna tresc.

### Nazwa i ton

Nasz przykladowy swiat to **Dolina Kruczych Wzgorz** -- niewielka, na wpol odizolowana kraina: wioska w dolinie, otaczajacy ja las, rzeka z mlynem, wzgorza z opuszczona kopalnia i stary kurhan (kopiec grobowy) skrywajacy cos starszego niz sama wioska. To swiadomie skromna skala -- **jedna wioska plus cztery sasiadujace tereny**, nie caly kontynent. Dzieki temu da sie ja realnie zbudowac w tym poradniku (30-40 lokacji) i wciaz miec miejsce na przedmioty, NPC-e i efekty, zamiast utonac w samej geografii.

Ton: nizinny, "ziemisty" fantasy bez wielkiej magii na pokaz -- blizej ludowych opowiesci i ballad niz eposu. Wybralam ten ton celowo: nie wymaga wymyslania calej kosmologii czy panteonu, zeby dzialal, a jednoczesnie daje pretekst do wszystkiego, co chcemy pokazac w kolejnych rozdzialach (zamkniete drzwi, cos w lesie, kopiec, ktorego nikt nie odwiedza).

Jesli wolisz zupelnie inny temat -- wspolczesne miasto, stacje kosmiczna, cokolwiek -- struktura ponizej (regiony -> lokacje -> punkty zaczepienia dla NPC/questow) przenosi sie bezposrednio, zmieniaja sie tylko nazwy i opisy.

### Geografia: piec regionow

| # | Region | Charakter | Orientacyjna liczba lokacji |
|---|--------|-----------|------------------------------|
| 1 | Kruczy Brod (wioska) | centrum swiata: rynek, gospoda, kuznia, swiatynia, domostwa | ok. 10 |
| 2 | Las Szepczacych Debow | dzicz na polnoc od wioski, sciezki, chata pustelnika | ok. 7 |
| 3 | Rzeka i Most Kruczy | granica wschodnia, rybacy, mlyn wodny | ok. 5 |
| 4 | Kurhan Kruczych Wzgorz | stary kopiec grobowy na poludniu, wewnetrzny "mini-dungeon" | ok. 8 |
| 5 | Wzgorza i Opuszczona Kopalnia | teren na zachodzie, obozowisko zbojcow, krysztalowa grota | ok. 7 |

Razem: okolo 37 lokacji -- w widelkach 20-50, ktore mielismy zbudowac, z zapasem, by w kolejnych rozdzialach cos jeszcze dopisac (sekretne przejscie, dodatkowy pokoj na potrzeby questu), bez przekraczania gornej granicy.

Dokladna lista pokoj-po-pokoju, z ich polaczeniami, jest w Rozdziale 4 -- tutaj chodzi tylko o szkielet, do ktorego bedziemy sie odwolywac przy projektowaniu przedmiotow i NPC-ow.

### Frakcje i punkty zaczepienia fabularnego

Cztery grupy/postacie, na ktorych oprzemy pozniejsze rozdzialy (NPC-e w Rozdziale 6, ekonomia w Rozdziale 9, questy w Rozdziale 10):

- **Rada Starszych Kruczego Brodu** -- zarzadza wioska, siedziba w Domu Starosty. Zrodlo pierwszych zadan dla gracza.
- **Kaplani Trzech Ksiezycow** -- niewielka swiatynia w wiosce, wiedza o kurhanie i o tym, czego lepiej tam nie ruszac. Zrodlo lore i questu w Rozdziale 4/10.
- **Pustelnik z Lasu Szepczacych Debow** -- neutralna postac na uboczu, handluje ziolami/informacjami, alternatywne zrodlo wskazowek.
- **Zbojcy z Wzgorz** -- antagonisci zajmujacy opuszczona kopalnie, zrodlo konfliktu/zagrozenia w Rozdziale 5 (przedmioty -- np. skradziony towar) i 8 (zamki/pulapki -- ich obozowisko jest strzezone).

Nie musisz w tym momencie znac szczegolow -- one wyklarowuja sie naturalnie w kolejnych rozdzialach, w miare jak dopisujemy NPC-e i zadania. Wazne jest tylko, zeby juz teraz miec te cztery "zaczepy", zeby pozniejsze lokacje, przedmioty i postacie nie byly przypadkowe, tylko skladaly sie w jedna calosc.

### Jak przeniesc to na wlasny temat

Jesli budujesz cos innego niz wioska fantasy, ten sam szablon dziala tak:

1. Wybierz skale, ktora realnie skonczysz -- jedna dzielnica miasta, jeden statek, jedna baza, nie "caly swiat". 20-50 lokacji to dobry, sprawdzony rozmiar na pierwszy projekt.
2. Podziel ja na 3-6 regionow/stref o wyraznie roznym charakterze (tak jak wyzej: wioska / las / rzeka / kurhan / wzgorza) -- to naturalnie zapobiega monotonii opisow.
3. Dla kazdego regionu zapisz orientacyjna liczbe lokacji -- nie musi byc dokladna, to tylko budzet, zeby caly projekt nie rozrosl sie w nieskonczonosc.
4. Wypisz 3-5 frakcji/postaci, ktore beda zrodlem NPC-ow i zadan -- gracz zawsze bardziej zapamieta miejsce przez pryzmat postaci niz przez sam opis pokoju.

Majac to na kartce, przechodzimy do Rozdzialu 2 -- przygotowania bezpiecznego miejsca, w ktorym faktycznie to zbudujemy.

## Rozdzial 2: przygotowanie warsztatu budowniczego

### Nie buduj na produkcyjnej bazie

Zanim wpiszesz cokolwiek, upewnij sie, ze polaczyles sie z baza, ktora mozesz bezkarnie zepsuc. Jesli dopiero skonfigurowales serwer wedlug [Przewodnika dla poczatkujacych](PRZEWODNIK-DLA-POCZATKUJACYCH.md), prawdopodobnie uzywasz swiezego `toastcore.db` na wlasnym komputerze -- to idealne miejsce, bo jestes na nim jedynym graczem i jedynym czarodziejem. Jesli natomiast masz dostep do juz dzialajacego, wspoldzielonego MOO (np. jako budowniczy na cudzym serwerze), **nie eksperymentuj tam z technikami z tego poradnika bez zgody adminow** -- poprosic o osobna, testowa baze albo przynajmniej o odizolowany obszar do budowania jest dobra praktyka, a nie przesadna ostroznoscia.

Sposob najprostszy, jesli budujesz sam dla siebie: skopiuj swiezy `toastcore.db` do osobnego katalogu roboczego i uruchom na nim drugi, lokalny serwer na innym porcie, wylacznie do przerabiania tego poradnika. Nic, co tu zbudujesz, nie musi trafic na produkcyjny serwer -- to poligon cwiczebny. Jesli pozniej zechcesz przeniesc gotowy fragment swiata na prawdziwy MOO, `@dump`/`@create ... with create` (patrz `help @dump`) pozwala wyeksportowac obiekty do formatu, ktory da sie wkleic gdzie indziej.

### Uprawnienia: budowniczy albo programista

Do wiekszosci tego poradnika (kopanie pokoi, tworzenie przedmiotow z gotowych klas) wystarczy status **budowniczego** (Generic Builder) -- to on daje dostep do `@dig`, `@create`, `@recycle` i pokrewnych. Do pisania wlasnych czasownikow (a zrobimy to od Rozdzialu 5 w gore) potrzebujesz statusu **programisty** (Generic Programmer), ktory obejmuje uprawnienia budowniczego i doklada mozliwosc pisania kodu.

Jesli jestes czarodziejem na swoim wlasnym serwerze testowym (najczesciej tak wlasnie bedzie, jesli szedles za Przewodnikiem dla poczatkujacych), nadaj to sobie samemu:

```
@programmer me
```

(albo `@programmer <twoja-nazwa-gracza>`, jesli wolisz podac nazwe wprost). Jesli budujesz na cudzym serwerze, popros czarodzieja o to samo polecenie na twoim koncie -- zobacz [Podstawy dla Czarodziei](PODSTAWY-DLA-CZARODZIEI.md#jak-tworzyc-programistow) po ich stronie procesu.

### Limit obiektow (quota) -- sprawdz to, zanim zaczniesz

Kazdy nowy programista dostaje domyslny limit **7 obiektow** (wlasciwosc `size_quota`) -- to znaczy, ze bez podniesienia limitu nie zbudujesz nawet jednego regionu z naszej mapy, nie mowiac o calych ~37 lokacjach plus przedmiotach i NPC-ach. Wyjatkiem sa czarodzieje -- oni nie sa ograniczani limitem quota.

Sprawdz swoj aktualny limit:

```
@quota me
```

Jesli budujesz jako zwykly programista (nie czarodziej), popros czarodzieja o podniesienie limitu, zanim przejdziesz dalej -- np. do 100, z zapasem na caly przyklad z tego poradnika plus wlasne eksperymenty:

```
@quota <twoja-nazwa-gracza> 100
```

(to polecenie moze wykonac tylko czarodziej -- zobacz `help @quota`). Jesli jestes czarodziejem budujacym na wlasnym serwerze testowym, mozesz ten krok pominac.

W trakcie budowy warto od czasu do czasu sprawdzic, ile obiektow juz zuzyles:

```
@count
```

a pelna liste tego, co juz stworzyles, pokazuje:

```
@audit
```

Obie komendy przydadza sie zwlaszcza w Rozdziale 4, gdzie tworzymy dziesiatki obiektow pod rzad.

### Konwencja nazewnictwa

MOO nie ma nazwanych stalych -- kazdy obiekt, ktory stworzysz, dostaje numer (np. `#1503`), a nie nazwe, do ktorej mozesz sie odwolac w kodzie. To oznacza, ze **musisz sam prowadzic notatki**, ktory numer to ktora lokacja, bo inaczej po dwudziestym `@dig` stracisz orientacje.

Zalecana konwencja na potrzeby tego poradnika:

- Kazda lokacja dostaje pelna, opisowa nazwe gracza-widzialna (np. `"Rynek w Kruczym Brodzie"`) -- to trafia do `@dig`/`@rename` i jest tym, co gracze widza.
- Rownolegle prowadz **poza MOO**, w zwyklym pliku tekstowym, tabele: region / nazwa lokacji / numer obiektu / polaczenia. Dokladnie taka tabele budujemy razem w Rozdziale 4 -- potraktuj ja jako szablon.
- Dla wlasnych klas obiektow (custom parenty, ktore zaczniemy tworzyc od Rozdzialu 5) dobrze sprawdza sie prefiks tematyczny w nazwie, np. `"Krucza Kolczuga"` zamiast po prostu `"Kolczuga"` -- ulatwia to pozniej odnalezienie "swoich" obiektow poleceniem `@audit` czy `@find`, zwlaszcza gdy baza rosnie.
- Nazwy czasownikow (verb names) zapisuj po angielsku i w liczbie pojedynczej rdzenia, tak jak reszta bazy ToastCore (`take`, `drop`, `read`) -- to standardowa konwencja calego silnika, a jesli chcesz dodac polskie aliasy obok, zobacz [Tworzenie tresci po polsku](TWORZENIE-TRESCI-PO-POLSKU.md).

### WAZNE: specjalne slowa i przyimki w tym forku

Zanim zaczniesz wpisywac polecenia -- ten fork tlumaczy na polski nie tylko tresc bazy, ale takze **kilka rzeczy wbudowanych bezposrednio w silnik (C++), nie w baze danych**. To znaczy, ze zwykle angielskie MOO-owe nawyki tu nie zadzialaja, i **zweryfikowalam to live na dzialajacym serwerze**, zeby miec pewnosc, zanim to napisze:

- Specjalne slowa oznaczajace "ja sam" i "moja obecna lokalizacja" to **`ja`** i **`tu`**/**`tutaj`** -- nie angielskie `me`/`here`. Np. `@move ja do #1500` dziala, `@move me to #1500` zwroci `Nie widze tu "me".`.
- Podstawowe przyimki, ktorych silnik uzywa do dopasowywania polecen (dopelnien czasownikow), sa rowniez polskie: `jako` (nie `as`), `za pomoca`/`przy uzyciu`/`uzywajac` (nie `with`), `w`/`wewnatrz` (nie `in`), `z`/`spod` (nie `from`), `u`/`do` (nie `to`), `o`/`dla` (nie `about`/`for`), oraz `na`, `nad`, `przez`, `pod`, `za`, `obok`, `ze` -- pelna liste pokazuje `help prepositions`. Dotyczy to zarowno polecen wbudowanych (`@describe X jako "..."`, nie `@describe X as "..."`), jak i **czasownikow, ktore sami piszemy** -- np. `@verb obiekt:"cos" any about any` zwroci wprost `"about" is not a valid preposition.` przy probie stworzenia takiego czasownika; trzeba uzyc `any o any`.
- Slowa-specyfikatory w samym poleceniu `@verb` (`none`, `this`, `any`) **zostaja po angielsku** -- to nie sa przyimki, tylko oddzielna skladnia samego polecenia `@verb`, i dzialaja dokladnie tak, jak pokazuje `help @verb`.
- Wywolanie czasownika w postaci `obiekt:czasownik()` (np. `kowal:start()`) **nie jest zwyklym poleceniem gracza** -- to wyrazenie jezyka MOO, wiec zawsze wymaga poprzedzenia `;` (skrot na `eval`, patrz `help eval`). Co wiecej, wewnatrz `eval` nazwy takie jak `kowal` **nie sa dopasowywane do obiektow tak jak w zwyklych poleceniach** -- to zwykle zmienne jezyka MOO, wiec `;kowal:start()` zwroci blad "Nie znaleziono zmiennej". W `eval` uzywaj numeru obiektu wprost (`;#1561:start()`) -- wyjatkiem sa odwolania `$nazwa` (jak `$room` czy `$zegar_swiata`), ktore dzialaja w `eval` bezposrednio, bo `$nazwa` to czesc skladni samego jezyka, nie zwykla zmienna.
- Niektore polecenia administracyjne (`@move`, `@dig`, `@corify`, `@set`) same, w swoim kodzie, jawnie rozpoznaja oba warianty przyimka (`do`/`to`, `jako`/`as`) -- to wyjatek, nie regula; nie zakladaj tego dla innych polecen czy wlasnych czasownikow bez sprawdzenia. Co wiecej, dwa konkretne polecenia -- `@quota` i `@programmer` -- gdy odnosza sie do ciebie samego, wymagaja akurat **angielskiego** `me`, nie `ja` (to najpewniej przeoczenie z wczesniejszego tlumaczenia, nie swiadoma decyzja, ale tak to dzis dziala) -- oba przypadki sa poprawnie napisane w przykladach ponizej, ale to dobry dowod, ze **kazde** polecenie warto zweryfikowac osobno, zamiast zakladac spojnosc w calej bazie.

Kazdy przyklad w reszcie tego poradnika juz uwzglednia te zasade -- ale jesli kiedys kopiujesz skladnie z innego, angielskiego zrodla o MOO, to jest dokladnie ten szczegol, ktory cie zaskoczy.

Majac uprawnienia, limit i notatnik gotowe, mozemy wykopac pierwszy pokoj -- Rozdzial 3.

## Rozdzial 3: pierwsza lokacja recznie

Zaczynamy od centrum naszego swiata -- rynku w Kruczym Brodzie. To bedzie jedyny pokoj w calym poradniku, ktory budujemy krok po kroku z pelnym komentarzem do kazdego polecenia; od Rozdzialu 4 wiemy juz, co robimy, wiec tempo przyspiesza.

### Kopiemy pokoj

```
@dig "Rynek w Kruczym Brodzie"
```

Serwer odpowie czyms w rodzaju:

```
Rynek w Kruczym Brodzie (#1500) utworzony.
```

**Twoj numer bedzie inny** -- kazda baza ma inny stan licznika obiektow, wiec u ciebie moze to byc `#88`, `#3502`, cokolwiek. W dalszej czesci tego rozdzialu uzywam `#1500` jako przykladu -- wszedzie, gdzie go widzisz, podstaw swoj wlasny numer. (To zreszta dokladnie po to prowadzimy notatnik z Rozdzialu 2 -- zapisz go tam juz teraz.)

Ta forma `@dig` (bez `to`) tworzy pokoj **niepolaczony z niczym** -- wisi w probni, dokladnie tak jak mowi help @dig (`help @dig`, jesli chcesz przypomniec sobie skladnie). To celowe: polaczenia (exits) budujemy systematycznie dla calej mapy w Rozdziale 4, zeby nie robic tego kawalkami.

### Przenosimy sie tam

Nowy pokoj nie ma jeszcze zadnego wejscia, wiec zwykle chodzenie nic nie da -- teleportujemy sie poleceniem `@move`:

```
@move ja do #1500
```

Powinienes zobaczyc nazwe pokoju i (na razie) pusty, domyslny opis.

### Opisujemy pokoj

Opis to najwazniejsza pojedyncza rzecz, jaka gracz widzi w kazdej lokacji -- wart czasu. Ustawiamy go przez `@describe`:

```
@describe tu jako "Nierowny bruk, wytarty tysiacami stop. Posrodku stoi kamienna studnia z zadaszeniem z poszarzalej dachowki. Wokol niej kilka drewnianych straganow, teraz pustych -- targ zaczyna sie dopiero rano. Z rynku widac gospode, kuznie i sciezki wiodace w strone lasu oraz wzgorz."
```

Uzylam `tu`, bo po `@move` jestesmy juz w tym pokoju -- mozna tez podac numer wprost (`@describe #1500 jako "..."`). Wpisz `look`, zeby zobaczyc efekt.

Technicznie `@describe` po prostu ustawia wlasciwosc `.description` na obiekcie -- `@describe tu jako "..."` to skrot dla `@set tu.description do "..."`. Warto to wiedziec, bo w Rozdziale 7 bedziemy ta wlasciwosc odczytywac i modyfikowac z poziomu kodu (np. zeby opis zmienial sie w zaleznosci od pory dnia).

Zauwaz cos waznego w tresci opisu: wspomina "sciezki wiodace w strone lasu oraz wzgorz", mimo ze tych wyjsc jeszcze fizycznie nie ma. To swiadomy zabieg -- opis pokoju to najlepsze miejsce, by *zapowiedziec* graczowi, dokad moze pojsc, zanim jeszcze sprawdzi liste wyjsc. Miej to na uwadze przy pisaniu opisow reszty mapy w Rozdziale 4.

### Pierwszy wlasny czasownik: `nasluchuj`

Zanim przejdziemy do budowy reszty mapy, zobaczmy pelny cykl pisania kodu na czyms malym -- czasownik, ktory dodaje odrobine klimatu, gdy gracz wpisze `nasluchuj` stojac na rynku.

Tworzymy nowy czasownik na naszym pokoju:

```
@verb #1500:"nasluchuj listen" none none none
```

`none none none` oznacza czasownik-polecenie bez zadnych dopelnien -- gracz wpisuje sam `nasluchuj`, bez podawania jakiegokolwiek obiektu (patrz `help @verb`, jesli chcesz przypomniec sobie, co oznaczaja `dobj`/`prep`/`iobj`; jest tam tez skrot `tnt` na `this none this`, ale to co innego -- oznacza czasownik, ktory **nie jest** wywolywany jako polecenie gracza, tylko wylacznie z kodu, i uzyjemy go pozniej, np. przy NPC-ach w Rozdziale 6). Podajemy dwie nazwy na raz (`nasluchuj` i angielskie `listen`), zeby dzialalo niezaleznie od tego, w jakim jezyku gracz wpisuje polecenia -- tak jak reszta bazy ToastCore.

Teraz wchodzimy w tryb edycji kodu:

```
@program #1500:nasluchuj
```

Serwer przelacza sie w tryb wpisywania linii kodu. Wpisz (kazda linia osobno, Enter po kazdej):

```
dzwieki = {"Skrzypienie szyldu gospody na wietrze.", "Gdzies szczeka pies.", "Kroki kogos, kto przeszedl przez rynek i zniknal w bocznej uliczce.", "Cisza -- nawet studnia nie skrzypi."};
player:tell(dzwieki[random(length(dzwieki))]);
.
```

Ostatnia, samotna kropka konczy tryb programowania i instaluje czasownik (dokladnie tak, jak opisuje `help @program`). Jesli serwer zglosi blad skladni, wroc do `@program #1500:nasluchuj` i popraw.

Wypisz w grze `nasluchuj` kilka razy -- za kazdym razem powinienes dostac inny, losowy komunikat. To najprostszy mozliwy przyklad interaktywnosci: wlasciwosc (tutaj: lokalna zmienna `dzwieki`) plus czasownik reagujacy na polecenie gracza. Dokladnie ten sam wzorzec -- zmienna/wlasciwosc z danymi plus czasownik, ktory je odczytuje -- bedziemy powtarzac przez reszte poradnika, tylko na coraz ciekawszych przykladach: przedmiotach (Rozdzial 5), NPC-ach (Rozdzial 6) i efektach atmosferycznych (Rozdzial 7).

### Co dalej

Mamy jeden, w pelni opisany i lekko interaktywny pokoj. W Rozdziale 4 robimy to samo systematycznie dla calej reszty mapy -- tym razem z gotowa tabela lokacji i pelnymi sekwencjami `@dig`, zamiast tlumaczyc kazdy krok od nowa.

## Rozdzial 4: budowa calej mapy

### Konwencja kierunkow

Ten fork rozpoznaje polskie nazwy kierunkow obok angielskich skrotow -- `polnoc`/`n`, `poludnie`/`s`, `wschod`/`e`, `zachod`/`w`, `polnocny-wschod`/`ne`, `poludniowy-wschod`/`se`, `poludniowy-zachod`/`sw`, `polnocny-zachod`/`nw`, `gore`/`u`, `na dol`/`d` (mozesz to zweryfikowac samemu -- to zaszyta w kodzie tabela w `$string_utils` uzywana m.in. do generowania wyjsc). **Uwaga:** `na dol` to dwa slowa, a polecenia w MOO sa dopasowywane po pierwszym slowie -- dwuwyrazowy alias wyjscia nigdy nie zadziala jako wpisywane polecenie (zweryfikowane live: nawet recznie dodany alias `"na dol"` nie reaguje na wpisanie `na dol`). Dlatego w tym poradniku dla kierunku "w dol" uzywamy jednowyrazowego aliasu **`dol`** zamiast `na dol` -- to jedyna zmiana wzgledem tabeli z `$string_utils`. W kazdym `@dig` z tego rozdzialu podaje oba warianty (pelne slowo i skrot) naraz, tak jak w przykladzie z `help @dig` (`west,w|east,e,out`) -- gracz bedzie mogl wpisac dowolny z nich.

### Sposob pracy: kop, potem idz, potem kop dalej

`@dig` **nie przenosi cie** do nowo wykopanego pokoju -- zostajesz tam, gdzie bytes, a nowy pokoj jest tylko polaczony wyjsciem. Zeby kopac dalej *z* nowego pokoju, trzeba do niego normalnie wejsc -- tym samym wyjsciem, ktore sie wlasnie stworzylo. To zreszta dobra rzecz: przy okazji od razu sprawdzasz, ze wyjscie faktycznie dziala tak, jak bedzie dzialac dla gracza.

Ponizej sekwencje polecen zakladaja, ze wykonujesz je jedno po drugim, w podanej kolejnosci, zaczynajac stojac w Rynku (`#1500` w naszym przykladzie z Rozdzialu 3 -- **podstaw swoj wlasny numer**). Po kazdym `@dig` z instrukcja "przejdz" wpisz podany kierunek jako zwykle polecenie ruchu.

### Pelna mapa -- tabela referencyjna

Zanim zaczniemy kopac, oto caly szkielet na raz -- warto skopiowac go do notatnika z Rozdzialu 2 i dopisywac tam rzeczywiste numery obiektow w miare budowy.

**Region 1: Kruczy Brod** (wioska, centrum swiata)

| Lokacja | Polaczenie | Uwaga |
|---|---|---|
| Rynek w Kruczym Brodzie | (start, zbudowany w Rozdziale 3) | hub calego regionu |
| Gospoda "Pod Zlamana Podkowa" | zachod od Rynku | punkt startowy questow, patrz Rozdzial 10 |
| Kuznia Kowala Borna | polnoc od Rynku | tu pozniej NPC-kowal, Rozdzial 6 |
| Brama Polnocna Kruczego Brodu | polnoc od Kuzni | wyjscie do Regionu 2 (las) |
| Uliczka Swiatynna | wschod od Rynku | |
| Swiatynia Trzech Ksiezycow | wschod od Uliczki Swiatynnej | zrodlo lore o kurhanie |
| Cmentarzyk przy Swiatyni | poludnie od Swiatyni | |
| Dom Starosty Wlodzimierza | polnocny-zachod od Rynku | zrodlo pierwszych questow |
| Chatka Zielarki Jagny | zachod od Domu Starosty | sprzedaje ziola/mikstury, Rozdzial 9 |
| Brama Poludniowa Kruczego Brodu | poludnie od Rynku | wyjscie do Regionu 3 (rzeka) |

**Region 2: Las Szepczacych Debow**

| Lokacja | Polaczenie | Uwaga |
|---|---|---|
| Skraj Lasu | polnoc od Bramy Polnocnej | |
| Zrodlo Lesne | wschod od Skraju Lasu | slepy zaulek, dobry na detal atmosfery |
| Gesty Gaszcz | polnoc od Skraju Lasu | |
| Chata Pustelnika | zachod od Gestego Gaszczu | NPC-pustelnik, Rozdzial 6 |
| Polana z Kregiem Grzybow | polnoc od Gestego Gaszczu | magiczny detal, Rozdzial 7 |
| Jaskinia Niedzwiedzia | polnoc od Polany | slepy zaulek/zagrozenie |
| Stary Dab Piorunem Rozlupany | wschod od Polany | landmark, zaczep pod Rozdzial 8 (sekret) |

**Region 3: Rzeka i Most Kruczy**

| Lokacja | Polaczenie | Uwaga |
|---|---|---|
| Brzeg Rzeki | poludnie od Bramy Poludniowej | |
| Przystan Rybacka | wschod od Brzegu Rzeki | |
| Wodny Mlyn | zachod od Brzegu Rzeki | |
| Most Kruczy | poludnie od Brzegu Rzeki | |
| Drugi Brzeg Rzeki | poludnie od Mostu Kruczego | wyjscie do Regionu 4 (kurhan) |

**Region 4: Kurhan Kruczych Wzgorz** (mini-dungeon)

| Lokacja | Polaczenie | Uwaga |
|---|---|---|
| Wejscie do Kurhanu | poludnie od Drugiego Brzegu Rzeki | |
| Korytarz Kurhanu | dol od Wejscia do Kurhanu | |
| Krypta Pierwsza | wschod od Korytarza | |
| Krypta Druga | zachod od Korytarza | ukryte polaczenie z Regionem 5, Rozdzial 8 |
| Sala z Pulapka | poludnie od Korytarza | fizyczna pulapka, Rozdzial 8 |
| Komnata Straznika | poludnie od Sali z Pulapka | NPC-straznik/mini-boss, Rozdzial 6 |
| Skarbiec | dol od Komnaty Straznika | zamkniete, Rozdzial 8 |
| Tajne Przejscie | (ukryty exit z Krypty Drugiej) | prowadzi do Regionu 5 |

**Region 5: Wzgorza i Opuszczona Kopalnia**

| Lokacja | Polaczenie | Uwaga |
|---|---|---|
| Podnoze Wzgorz | zachod od Tajnego Przejscia | |
| Szlak Gorski | polnoc od Podnoza Wzgorz | |
| Szczyt Wzgorza | polnoc od Szlaku Gorskiego | slepy zaulek, widok/atmosfera |
| Wejscie do Opuszczonej Kopalni | poludnie od Podnoza Wzgorz | |
| Kopalnia -- Poziom Pierwszy | dol od Wejscia do Kopalni | |
| Grota Krysztalowa | wschod od Poziomu Pierwszego | skarb/ekonomia, Rozdzial 9 |
| Kopalnia -- Poziom Drugi (Obozowisko Zbojcow) | dol od Poziomu Pierwszego | siedziba antagonistow, Rozdzial 6 i 8 |

Razem: 10 + 7 + 5 + 8 + 7 = **37 lokacji**, zgodnie z planem z Rozdzialu 1.

### Budujemy Region 1 (reszta wioski)

Zakladamy, ze stoisz w Rynku (`#1500` w przykladzie). Wykonuj po kolei:

```
@dig zachod,w|wschod,e to "Gospoda \"Pod Zlamana Podkowa\""
@dig polnoc,n|poludnie,s to "Kuznia Kowala Borna"
```

Przejdz `polnoc`, zeby wejsc do Kuzni, i wykop z niej dalej brame:

```
@dig polnoc,n|poludnie,s to "Brama Polnocna Kruczego Brodu"
```

Wroc do Rynku (`poludnie`, albo po prostu `@move ja do #1500`, jesli wolisz nie liczyc krokow) i wykop wschodnia odnoge:

```
@dig wschod,e|zachod,w to "Uliczka Swiatynna"
```

Przejdz `wschod`, wejdz do Uliczki Swiatynnej, i kop dalej:

```
@dig wschod,e|zachod,w to "Swiatynia Trzech Ksiezycow"
```

Przejdz `wschod` do Swiatyni i wykop cmentarzyk:

```
@dig poludnie,s|polnoc,n to "Cmentarzyk przy Swiatyni"
```

Wroc do Rynku (`zachod`, `zachod`, albo po prostu `@move ja do #1500`, jesli wolisz nie liczyc krokow) i wykop pozostale dwie odnogi:

```
@dig polnocny-zachod,nw|poludniowy-wschod,se to "Dom Starosty Wlodzimierza"
```

Przejdz `polnocny-zachod` do Domu Starosty i wykop chatke zielarki:

```
@dig zachod,w|wschod,e to "Chatka Zielarki Jagny"
```

Wroc do Rynku i wykop brame poludniowa -- nasze wyjscie z wioski w strone rzeki:

```
@dig poludnie,s|polnoc,n to "Brama Poludniowa Kruczego Brodu"
```

Region 1 gotowy -- 10 lokacji, wszystkie polaczone. Sprawdz `@count`, powinienes miec teraz okolo 11 obiektow (10 pokoi + wyjscia sa liczone osobno od pokoi, wiec dokladna liczba bedzie wyzsza -- `@audit` pokaze pelna liste).

### Budujemy Region 2 (Las Szepczacych Debow)

Region 1 zostawil cie w Rynku -- wejdz do Bramy Polnocnej (`polnoc` do Kuzni, potem `polnoc` do Bramy -- albo `@move ja do <numer Bramy Polnocnej z notatnika>`) i kop dalej w las:

```
@dig polnoc,n|poludnie,s to "Skraj Lasu"
```

Przejdz `polnoc`, i z Skraju Lasu wykop dwie odnogi:

```
@dig wschod,e|zachod,w to "Zrodlo Lesne"
```

Wciaz stojac w Skraju Lasu (nie weszliscie do Zrodla Lesnego, tylko je wykopaliscie z zewnatrz), idz dalej w glab lasu:

```
@dig polnoc,n|poludnie,s to "Gesty Gaszcz"
```

Przejdz `polnoc` do Gestego Gaszczu i wykop chate pustelnika oraz dalsza sciezke:

```
@dig zachod,w|wschod,e to "Chata Pustelnika"
```

Wciaz stojac w Gestym Gaszczu (ta sama sytuacja co przy Zrodle Lesnym):

```
@dig polnoc,n|poludnie,s to "Polana z Kregiem Grzybow"
```

Przejdz `polnoc` na Polane i wykop ostatnie dwa pokoje regionu:

```
@dig polnoc,n|poludnie,s to "Jaskinia Niedzwiedzia"
```

Wciaz stojac na Polanie (ta sama sytuacja co poprzednio -- nie weszliscie do Jaskini):

```
@dig wschod,e|zachod,w to "Stary Dab Piorunem Rozlupany"
```

Region 2 gotowy -- 7 lokacji.

### Budujemy Region 3 (Rzeka i Most Kruczy)

Wroc do Rynku (`@move ja do #1500` jest najprostsze, bo z Polany do Rynku jest kilka krokow) i wejdz przez Brame Poludniowa (`poludnie`):

```
@dig poludnie,s|polnoc,n to "Brzeg Rzeki"
```

Przejdz `poludnie` na Brzeg Rzeki i wykop trzy odnogi:

```
@dig wschod,e|zachod,w to "Przystan Rybacka"
```

Wciaz stojac nad Brzegiem Rzeki (nie weszliscie do Przystani):

```
@dig zachod,w|wschod,e to "Wodny Mlyn"
```

Nadal w tym samym miejscu:

```
@dig poludnie,s|polnoc,n to "Most Kruczy"
```

Przejdz `poludnie` na Most i wykop drugi brzeg:

```
@dig poludnie,s|polnoc,n to "Drugi Brzeg Rzeki"
```

Region 3 gotowy -- 5 lokacji.

### Budujemy Region 4 (Kurhan Kruczych Wzgorz)

Jestes wciaz na Moscie Kruczym (nie weszliscie na Drugi Brzeg) -- przejdz `poludnie`, zeby tam wejsc, i wykop wejscie do kurhanu:

```
@dig poludnie,s|polnoc,n to "Wejscie do Kurhanu"
```

Przejdz `poludnie` i zejdz pod ziemie:

```
@dig dol,d|gore,u to "Korytarz Kurhanu"
```

(zauwaz, ze tu wyjscie *w dol* prowadzi do nowego pokoju, wiec para wyjsc to `dol,d|gore,u` -- z korytarza wraca sie `gore`, nie `polnoc`; kierunki nie musza trzymac sie geografii na powierzchni, gdy budujesz cos podziemnego. Uwaga: uzywamy `dol`, nie `na dol` -- patrz przypomnienie na poczatku tego rozdzialu).

Przejdz `dol` do Korytarza i wykop trzy odnogi plus komnate straznika w linii prostej:

```
@dig wschod,e|zachod,w to "Krypta Pierwsza"
```

Wciaz stojac w Korytarzu (nie weszliscie do Krypty Pierwszej):

```
@dig zachod,w|wschod,e to "Krypta Druga"
```

Nadal w Korytarzu:

```
@dig poludnie,s|polnoc,n to "Sala z Pulapka"
```

Przejdz `poludnie` i kop dalej w glab:

```
@dig poludnie,s|polnoc,n to "Komnata Straznika"
```

Przejdz `poludnie` i wykop skarbiec pod komnata:

```
@dig dol,d|gore,u to "Skarbiec"
```

Ostatni pokoj tego regionu -- **Tajne Przejscie** -- celowo nie kopiemy teraz. To ukryte polaczenie miedzy Krypta Druga a Regionem 5, ktore wymaga mechanizmu ukrywania wyjscia (obiekt wyjscia istnieje, ale nie jest widoczny w zwyklym `look`) -- to dokladnie material Rozdzialu 8. Zanotuj sobie tylko w notatniku, ze Krypta Druga bedzie potrzebowac takiego polaczenia, i wroc do tego w Rozdziale 8.

Region 4 gotowy -- 7 z 8 zaplanowanych lokacji (ostatnia doczeka Rozdzialu 8).

### Budujemy Region 5 (Wzgorza i Opuszczona Kopalnia)

Ten region z zalozenia laczy sie z reszta mapy przez Tajne Przejscie z Regionu 4 -- skoro jeszcze go nie ma, na razie zbudujemy Region 5 jako osobna, chwilowo niepolaczona grupe pokoi (`@dig` bez `to`), a po Rozdziale 8 dostanie polaczenie. To dobra okazja, by przypomniec: pokoj bez wyjsc wejsciowych to nie blad -- to normalny, przejsciowy stan podczas budowy.

```
@dig "Podnoze Wzgorz"
```

Zapisz numer, ktory zwroci serwer, i przejdz tam recznie: `@move ja do <numer>`.

```
@dig polnoc,n|poludnie,s to "Szlak Gorski"
```

Przejdz `polnoc`:

```
@dig polnoc,n|poludnie,s to "Szczyt Wzgorza"
```

Wroc na Podnoze Wzgorz (`poludnie` -- albo `@move`):

```
@dig poludnie,s|polnoc,n to "Wejscie do Opuszczonej Kopalni"
```

Przejdz `poludnie` i zejdz do kopalni:

```
@dig dol,d|gore,u to "Kopalnia -- Poziom Pierwszy"
```

Przejdz `dol` i wykop dwie ostatnie lokacje:

```
@dig wschod,e|zachod,w to "Grota Krysztalowa"
```

Wciaz na Poziomie Pierwszym (nie weszliscie do Groty):

```
@dig dol,d|gore,u to "Kopalnia -- Poziom Drugi (Obozowisko Zbojcow)"
```

Region 5 gotowy -- 7 lokacji, na razie odizolowanych od reszty mapy (celowo, patrz wyzej).

### Opisy

Kazdy z powyzszych pokoi ma teraz nazwe i polaczenia, ale wciaz domyslny (pusty) opis. Wzorzec z Rozdzialu 3 (`@describe tu jako "..."`) jest identyczny dla kazdego z nich -- zamiast przepisywac 36 kolejnych przykladow, potraktuj to jako cwiczenie: przejdz sie po calej mapie i opisz przynajmniej te lokacje, ktore beda mialy znaczenie w kolejnych rozdzialach (Gospoda, Kuznia, Swiatynia, Chata Pustelnika, Polana z Kregiem Grzybow, Komnata Straznika, Obozowisko Zbojcow -- wszystkie pojawiaja sie ponownie przy przedmiotach, NPC-ach lub efektach). Reszte mozesz dopisac w dowolnym momencie -- pusty opis nie przeszkadza w dalszej pracy nad mechanika.

### Co dalej

Mamy szkielet calego swiata -- 36 zbudowanych lokacji plus jedna (Tajne Przejscie) odlozona do Rozdzialu 8, i caly Region 5 czekajacy na spiecie z reszta mapy. W Rozdziale 5 zaczynamy wypelniac te lokacje trescia: przedmiotami, ktore gracz moze podniesc, uzyc i (czasem) zjesc.

## Rozdzial 5: przedmioty

### Cztery standardowe klasy

`help @create` wymienia cztery gotowe "standardowe klasy", od ktorych mozesz od razu dziedziczyc: `$note`, `$letter`, `$thing` i `$container`. Kazda przydaje sie do czegos innego:

- `$thing` -- najbardziej ogolna klasa. Mozna ja podniesc, upuscic, przeniesc. Baza pod wszystko, co nie pasuje do pozostalych trzech.
- `$note` -- przedmiot z tekstem do przeczytania (wlasciwosc `.text`, lista linii). Idealny na liscik, zapiski, karteczki.
- `$letter` -- podobny do `$note`, ale pomyslany pod system pocztowy (adresat, mozliwosc wyslania) -- na potrzeby tego poradnika bedziemy uzywac gownie `$note`.
- `$container` -- przedmiot, do ktorego mozna wlozyc inne przedmioty (`put X w Y`) i z ktorego mozna je wyjac (`take X z Y`). Ma tez wbudowana obsluge opcjonalnego zamka (wlasciwosc `.key`) -- wykorzystamy to w Rozdziale 8.

### Pierwszy przedmiot: zapiski w Chacie Pustelnika

Przejdz do Chaty Pustelnika (Rozdzial 4, Region 2) i stworz tam notatke:

```
@create $note named "wyplowiale zapiski,zapiski,notatka"
```

Serwer zwroci numer nowego obiektu (przykladowo `#1540` -- podstaw swoj). Opisz go z zewnatrz i ustaw tresc do przeczytania:

```
@describe #1540 jako "Kawalek pergaminu, pokryty niewprawnym pismem."
@set #1540.text do {"Jesli czytasz te slowa, pustelnik chyba pozwolil ci tu zostac.", "Trzy Ksiezyce widza wiecej, niz kaplani chca przyznac -- pytaj o Kurhan.", "-- P."}
```

Nowy obiekt wciaz jest w twoim ekwipunku (tworzenie `@create` nie umieszcza go automatycznie w pokoju) -- upusc go tam, gdzie ma lezec:

```
drop wyplowiale zapiski
```

Kazdy gracz, ktory wejdzie do Chaty Pustelnika, moze teraz podniesc notatke (`take zapiski`) i przeczytac ja (`read zapiski`) -- oba czasowniki sa juz gotowe, odziedziczone z `$note`.

### Kontener: skrzynia w Skarbcu

Przejdz do Skarbca (Region 4) i stworz tam zamykana (na razie jeszcze nie zamknieta -- to Rozdzial 8) skrzynie:

```
@create $container named "stara okuta skrzynia,skrzynia,kufer"
@describe skrzynia jako "Ciezka, debowa skrzynia okuta zelazem, pociemniala od wilgoci."
drop stara okuta skrzynia
```

Do srodka mozesz od razu wlozyc pierwszy "skarb" -- na razie zwykly `$thing`. Nowo stworzony kontener jest domyslnie **zamkniety**, wiec najpierw go otwieramy (zweryfikowane live: `put` do zamknietego kontenera po prostu sie nie uda):

```
@create $thing named "garsc starych srebrnych monet,monety,srebro"
@describe monety jako "Garsc poczernialych ze staroscia monet z profilem wladcy, ktorego nikt juz nie pamieta."
open skrzynia
put monety w skrzynia
```

Gracz, ktory dotrze do Skarbca, moze `open skrzynia`, `look w skrzynia` i `take monety z skrzynia` -- znowu, cala ta mechanika jest juz wbudowana w `$container`, nie napisalismy do niej ani linijki kodu (pamietaj o zasadzie z Rozdzialu 2: przyimki tego forka sa polskie -- `w`/`z`, nie angielskie `in`/`from`).

### Wlasna klasa: przedmioty jadalne

Zadna standardowa klasa nie obsluguje jedzenia -- to dobra okazja, by pokazac, jak stworzyc **wlasna klase-rodzica**, z ktorej pozniej beda dziedziczyc wszystkie podobne przedmioty (tu: kazdy kolejny posilek w grze, bez pisania kodu od nowa za kazdym razem).

Tworzymy klase (nie konkretny przedmiot -- prototyp, po ktorym beda dziedziczyc inne):

```
@create $thing named "Klasa: Przedmiot Jadalny,edible class"
```

Zeby mozna bylo tworzyc dzieci tej klasy, musi byc **plodna** (fertile) -- inaczej `@create` z tym rodzicem odmowi dzialania (`help @chmod`, jesli chcesz przypomniec sobie znaczenie bitow uprawnien):

```
@chmod #1550 +f
```

(znow: `#1550` to przykladowy numer, u ciebie bedzie inny -- to na tyle wazny obiekt, ze warto zapisac go w notatniku pod nazwa `$edible`, bedziemy go uzywac ponownie).

Teraz dopisujemy czasownik `zjedz`/`eat`, ktory bedzie dzialal na kazdym przedmiocie dziedziczacym po tej klasie:

```
@verb #1550:"zjedz eat" this none none
```

```
@program #1550:zjedz
if (this.location != player)
player:tell("Najpierw musisz to podniesc.");
else
player:tell("Zjadasz ", this.name, ". ", (this.smak_opis || "Smakuje calkiem niezle."));
this.location:announce_all_but({player}, player.name + " zjada " + this.name + ".");
recycle(this);
endif
.
```

Kilka nowosci w tym kodzie, wyjasnione: `this` to zawsze obiekt, na ktorym uruchomiono czasownik (tu: konkretny posilek); `player` to gracz, ktory wydal polecenie; `this.location != player` sprawdza, czy przedmiot faktycznie jest w rekach gracza (a nie np. wciaz lezy w pokoju); `this.smak_opis || "..."` to wzorzec "wartosc domyslna, jesli wlasciwosc jest pusta/nieustawiona", ktory bedziemy uzywac wielokrotnie w kolejnych rozdzialach; `this.location:announce_all_but({player}, ...)` informuje wszystkich innych w pokoju (ale nie samego gracza -- on juz widzial swoj wlasny `player:tell`) -- `:announce` z Rozdzialu 3 mowi do wszystkich bez wyjatku, `:announce_all_but` pozwala kogos pominac; `recycle(this)` niszczy przedmiot po zjedzeniu -- zjedzony bochenek chleba nie powinien zostac w ekwipunku. **Uwaga:** to musi byc `recycle(this)` (funkcja wbudowana), nie `this:recycle()` (wywolanie czasownika) -- to drugie zweryfikowane live nie niszczy obiektu, tylko cicho zwraca 0.

Zauwaz, ze `zjedz` odwoluje sie do wlasciwosci `smak_opis`, ktorej klasa `$edible` jeszcze nie ma -- dodajmy ja, z sensowna domyslna wartoscia pustego stringu:

```
@property #1550.smak_opis "" rc
```

(`rc` to uprawnienia wlasciwosci -- readable i "chown-owned", czyli standardowe, patrz `help @property`).

Teraz tworzymy konkretny przedmiot dziedziczacy po tej klasie -- bochenek chleba w Gospodzie:

```
@create #1550 named "bochenek razowego chleba,chleb,bochenek"
@describe chleb jako "Jeszcze cieply, razowy bochenek, pachnacy kminkiem."
@set chleb.smak_opis do "Chrupiaca skorka i cieply, gesty miekisz -- najlepszy chleb w calej dolinie."
```

(uzylam nazwy `chleb`, nie `tu` jak w Rozdziale 3 -- **`@create` zostawia nowy obiekt w twoim ekwipunku, nie w pokoju, a `tu` zawsze oznacza pokoj, nigdy przedmiot w rekach, bez wzgledu na to, gdzie stoisz** -- zweryfikowane live: uzycie `tu` w tym miejscu po cichu opisuje pokoj zamiast przedmiotu, co latwo przeoczyc, bo `@describe` i tak zglasza "Opis ustawiony." Dla swiezo stworzonych przedmiotow w ekwipunku uzywaj wiec ich nazwy albo aliasu -- albo numeru wprost, jesli wolisz: `@describe #1551 jako "..."`).

Przejdz do Gospody (`@move ja do <numer Gospody z notatnika>`) i upusc tam chleb -- zostawiamy go jako element wyposazenia lokacji dla innych graczy. Zeby sprawdzic, czy czasownik dziala (nie musisz tego robic dla kazdego przyszlego przedmiotu, ale warto zobaczyc raz, jak to wyglada), podnies go z powrotem (`take chleb`) i sprobuj `zjedz chleb` (albo `eat chleb`) -- powinienes zobaczyc opis smaku i znikniecie przedmiotu z ekwipunku. (Bez ponownego podniesienia czasownik odpowie "Najpierw musisz to podniesc." -- `this.location != player` w kodzie wyzej dziala dokladnie tak, jak powinno).

### Dlaczego to sie oplaca

Ten sam wzorzec -- klasa-rodzic z jedna wspolna logika plus wiele lekkich "dzieci" roznia sie tylko wartosciami wlasciwosci -- powtorzymy jeszcze kilka razy: dla kluczy w Rozdziale 8 i dla towaru na sprzedaz w Rozdziale 9. Zamiast pisac czasownik `zjedz` od nowa dla kazdego kolejnego posilku w grze, wystarczy stworzyc kolejny `@create #1550 named "..."` i ustawic dwie-trzy wlasciwosci. To sedno programowania obiektowego w MOO, i najwiekszy dzwig produktywnosci przy budowaniu wiekszego swiata.

Rozstaw po swiecie kilka wlasnych przedmiotow jadalnych jako cwiczenie (np. co widac na Rynku podczas targu, co podaje pustelnik) -- w Rozdziale 6 zaczynamy zaludniac ten swiat postaciami, ktore beda te przedmioty rozdawac, sprzedawac i o nich rozmawiac.

## Rozdzial 6: NPC-e i dialogi

### Czym jest NPC w MOO

W MOO nie ma osobnego "typu" postaci niezaleznej (NPC) -- to po prostu zwykly obiekt (najczesciej dziedziczacy po `$thing`), ktory wyglada i zachowuje sie jak postac, bo my sami napisalismy mu opis i czasowniki reagujace na polecenia gracza. Nie jest zalogowanym graczem i nic nie robi "sam z siebie", chyba ze zaplanujemy to jawnie -- albo przez czasowniki wywolywane na zadanie (np. `porozmawiaj z kowalem`), albo przez samo-planujace sie zadanie w tle (`fork`), ktore od czasu do czasu cos robi bez udzialu gracza. Zbudujemy oba mechanizmy na jednym przykladzie, a potem powielimy go na reszte postaci.

### Wlasna klasa: $npc

Tak jak w Rozdziale 5, zaczynamy od plodnej klasy-rodzica. Stworz ja gdziekolwiek (np. w Rynku) i zanotuj numer jako `$npc`:

```
@create $thing named "Klasa: NPC,npc class"
@chmod #1560 +f
```

Dwie wlasciwosci, ktorych bedzie potrzebowac kazdy NPC z tej klasy -- lista kwestii do wygadywania od czasu do czasu i "sciaga" odpowiedzi na pytania:

```
@property #1560.gadanie {} rc
@property #1560.odpowiedzi [] rc
@property #1560.heartbeat_task 0 rc
```

`odpowiedzi` bedzie mapa (typ danych MOO zapisywany `[klucz -> wartosc, ...]`) laczaca slowo-klucz z odpowiedzia -- np. `["kurhan" -> "Nie chodz tam po zmroku, chlopcze."]`. `heartbeat_task` przechowuje numer zaplanowanego zadania w tle, zebysmy mogli je pozniej zatrzymac (`kill_task`) zamiast zostawiac je dzialajace w nieskonczonosc, gdy np. NPC zostanie zrecyklowany.

### Czasownik dialogowy: `zagadnij`/`zapytaj`

```
@verb #1560:"zagadnij zapytaj ask" any o any
```

```
@program #1560:zagadnij
temat = strsub(iobjstr, " ", "");
if (temat in mapkeys(this.odpowiedzi))
this:announce_line(this.odpowiedzi[temat]);
else
this:announce_line(this.odpowiedzi["_domyslna"] || "...wzrusza ramionami.");
endif
.
```

(`this:announce_line` jeszcze nie istnieje -- dopisujemy go od razu, zeby nie powtarzac tego samego `player:tell`/`announce` w kazdym kolejnym czasowniku NPC-a):

```
@verb #1560:announce_line this none this
```

```
@program #1560:announce_line
tekst = args[1];
player:tell("\"", tekst, "\" -- mowi ", this.name, ".");
.
```

Skladnia polecenia gracza wyglada teraz tak: `zagadnij kowal o kurhan` albo `ask kowal o kurhan` (imiona/nazwy obiektow w poleceniach zawsze podajemy w formie podstawowej/mianownikowej, bez odmiany przez przypadki -- ten fork celowo nie wspiera odmiany rzeczownikow w dopasowywaniu obiektow, wiec `kowala` by nie zadzialalo) (nazwa czasownika moze byc angielska lub polska -- to tylko alias -- ale przyimek musi byc `o`, nie angielskie `about`; przypomnienie z Rozdzialu 2: przyimki wbudowane w silnik tego forka sa polskie, `help prepositions` pokazuje pelna liste). Jesli chcesz sprawdzic albo rozszerzyc polskie aliasy komend w calej bazie, zajrzyj do [Tworzenia tresci po polsku](TWORZENIE-TRESCI-PO-POLSKU.md).

### Losowe kwestie w tle (`fork`)

Zeby NPC czasem odzywal sie sam z siebie (nie tylko w odpowiedzi na pytanie), potrzebujemy zadania, ktore samo siebie planuje na przyszlosc. To pierwsze uzycie `fork` w tym poradniku -- pelny opis skladni jest w [Podreczniku Programisty](PODRECZNIK-PROGRAMISTY.md), tu pokazuje tylko dzialajacy wzorzec:

```
@verb #1560:heartbeat this none this
```

```
@program #1560:heartbeat
this.heartbeat_task = 0;
if ((this.gadanie != {}) && (random(4) == 1))
this.location:announce(this.name, " mowi: \"", this.gadanie[random(length(this.gadanie))], "\"");
endif
fork zadanie (30 + random(60))
this:heartbeat();
endfork
this.heartbeat_task = zadanie;
.
```

```
@verb #1560:start this none this
```

```
@program #1560:start
if (this.heartbeat_task == 0)
this:heartbeat();
endif
.
```

```
@verb #1560:stop this none this
```

```
@program #1560:stop
if (this.heartbeat_task != 0)
kill_task(this.heartbeat_task);
this.heartbeat_task = 0;
endif
.
```

Kazde wywolanie `:heartbeat` z jednej czwartej szans wygaduje losowa kwestie do calego pokoju (`this.location:announce(...)`, ta sama wbudowana metoda co przy komunikatach polaczenia z Rozdzialu 3), a potem **samo planuje swoje kolejne wywolanie** za 30-90 sekund (`30 + random(60)`) i zapamietuje numer zaplanowanego zadania w `.heartbeat_task`. `:stop` zabija to zaplanowane zadanie -- **zawsze wywolaj `:stop` przed `@recycle` takiego NPC-a**, inaczej zaplanowane zadanie zostanie osierocone (bedzie probowalo wywolac czasownik na juz nieistniejacym obiekcie i zakonczy sie bledem w logu serwera, ale i tak lepiej tego unikac).

### Pierwszy NPC: Kowal Born

```
@create #1560 named "Kowal Born,kowal,born"
@describe kowal jako "Postawny mezczyzna o rekach jak balki, w skorzanym fartuchu poznaczonym iskrami. Pilnuje pieca, jakby to bylo najcenniejsze, co ma."
@set kowal.gadanie do {"Uwazaj na iskry, jesli podejdziesz blizej.", "Dobra stal wymaga cierpliwosci, tak samo jak dobre zycie."}
@set kowal.odpowiedzi do ["kurhan" -> "Nie chodz tam po zmroku, chlopcze. Kaplani cos wiedza, ale nie mowia.", "_domyslna" -> "Kowal mruczy cos pod nosem i wraca do pracy."]
```

Przejdz do Kuzni (`@move ja do <numer Kuzni z notatnika>`) i tam go upusc -- to jego docelowe miejsce:

```
drop kowal
```

Uruchom mu gadanie w tle. Wywolanie czasownika w postaci `obiekt:czasownik()` **nie jest zwyklym poleceniem gracza** -- to wyrazenie jezyka MOO, wiec trzeba je poprzedzic `;` (skrot na `eval`, patrz `help eval`). Co wiecej, w `eval` nazwy takie jak `kowal` nie sa automatycznie dopasowywane do obiektow (tak jak w zwyklych poleceniach) -- to zwykle zmienne, i jesli nie istnieje zmienna `kowal`, dostaniesz blad "Nie znaleziono zmiennej". Dlatego w `eval` uzywamy numeru obiektu wprost (`#1561` w naszym przykladzie -- podstaw swoj):

```
;#1561:start()
```

Poczekaj minute w Kuzni i sprobuj `zapytaj kowal o kurhan`.

### Reszta obsady

Ten sam trzyczesciowy wzorzec (klasa `$npc` + `@create #1560 named "..."` + ustawienie `.gadanie`/`.odpowiedzi` + `:start()`) powtarzamy dla pozostalych postaci z Rozdzialu 1:

- **Starosta Wlodzimierz** (Dom Starosty) -- `.odpowiedzi` zawiera wskazowke o pierwszym zadaniu (rozwijamy je w Rozdziale 10).
- **Pustelnik** (Chata Pustelnika) -- neutralne, zagadkowe odpowiedzi; zna `zapiski` z Rozdzialu 5, bo sam je napisal.
- **Straznik Kurhanu** (Komnata Straznika, Region 4) -- zamiast losowych kwestii, `.odpowiedzi["_domyslna"]` moze ostrzegac gracza przed dalsza wedrowka -- w Rozdziale 8 dodamy mu realna mechanike blokowania przejscia.
- **Zbojcy z Obozowiska** (Region 5) -- kilka instancji tej samej klasy z bardziej wrogim `.gadanie`, np. `"Nie widziales nas."`, `"To nie miejsce dla ciebie."`.

Nie musisz pisac ani linijki nowego kodu dla zadnej z tych postaci -- caly wysilek programistyczny poszedl w klase `$npc`; kazda kolejna postac to tylko dane (opis + dwie listy tekstu). To ten sam dzwig produktywnosci, co przy przedmiotach jadalnych w Rozdziale 5, tylko na wiekszej skali.

W Rozdziale 7 zajmiemy sie czyms innym: efektami, ktore nie naleza do zadnego konkretnego obiektu, tylko do calego swiata -- pora dnia i pogoda.

## Rozdzial 7: efekty atmosferyczne

### Jeden obiekt trzymajacy stan calego swiata

Pora dnia i pogoda to nie wlasciwosci pojedynczego pokoju -- to stan globalny, ktory wiele pokoi powinno moc odczytac. Zamiast duplikowac go wszedzie, tworzymy jeden obiekt-zegar i odwolujemy sie do niego z kazdego miejsca, ktore go potrzebuje:

```
@create $thing named "Zegar Swiata,zegar,zegar swiata"
@property #1575.pora_dnia "rano" rc
@property #1575.pogoda "pogodnie" rc
@property #1575.tick_task 0 rc
```

(`#1575` to znowu przykladowy numer -- podstaw swoj). Ten obiekt nigdy nie musi byc "widziany" przez gracza -- to czysto techniczny magazyn stanu, wiec nie przejmuj sie tym, ze wciaz lezy w twoim ekwipunku.

### Samo-planujace sie zadanie: `:tick`

Ten sam wzorzec `fork`/`kill_task` co przy NPC-ach w Rozdziale 6, tylko tym razem zadanie przesuwa cykl dnia i losuje pogode zamiast wygadywac kwestie:

```
@verb #1575:tick this none this
```

```
@program #1575:tick
this.tick_task = 0;
cykl = {"rano", "dzien", "wieczor", "noc"};
teraz = 1;
for i in [1..length(cykl)]
if (cykl[i] == this.pora_dnia)
teraz = i;
endif
endfor
this.pora_dnia = cykl[(teraz % length(cykl)) + 1];
los = random(10);
if (los <= 2)
this.pogoda = "deszcz";
elseif (los == 3)
this.pogoda = "mgla";
else
this.pogoda = "pogodnie";
endif
fork zadanie (300)
this:tick();
endfork
this.tick_task = zadanie;
.
```

```
@verb #1575:start this none this
```
```
@program #1575:start
if (this.tick_task == 0)
this:tick();
endif
.
```
```
@verb #1575:stop this none this
```
```
@program #1575:stop
if (this.tick_task != 0)
kill_task(this.tick_task);
this.tick_task = 0;
endif
.
```

Kazde wywolanie `:tick` przesuwa `.pora_dnia` o jeden krok w cyklu rano->dzien->wieczor->noc->rano..., losuje nowa `.pogoda` (20% szans na deszcz, 10% na mgle, reszta pogodnie) i planuje sie ponownie za 300 sekund (5 minut) -- wystarczajaco czesto, by gracz zauwazyl zmiane w rozsadnym czasie gry, ale nie na tyle czesto, zeby zasypac serwer zadaniami.

Zeby moc odwolywac sie do zegara z dowolnego miejsca w bazie bez pamietania jego numeru, skorowujemy go (wymaga uprawnien wizarda -- `help @corify`, jesli chcesz przypomniec sobie szczegoly):

```
@corify zegar jako zegar_swiata
```

Od teraz `$zegar_swiata` dziala wszedzie, tak samo jak `$room` czy `$thing`. Uruchamiamy zegar -- pamietaj o `;` przed wywolaniem czasownika (przypomnienie z Rozdzialu 6: `obiekt:czasownik()` to wyrazenie MOO, nie polecenie gracza, wiec wymaga `eval`/`;`; w przeciwienstwie do `kowal` z Rozdzialu 6, `$zegar_swiata` dziala tu bezposrednio -- skladnia `$nazwa` to czesc samego jezyka MOO, nie zwykla zmienna):

```
;$zegar_swiata:start()
```

### Podpiecie opisow pokoi pod stan zegara

To najciekawsza czesc tego rozdzialu: chcemy, zeby `look` w pokoju na zewnatrz doklejal zdanie o porze dnia i pogodzie do opisu, ktory juz napisalismy w Rozdziale 4 -- bez przepisywania tego opisu za kazdym razem. [Podrecznik Programisty](PODRECZNIK-PROGRAMISTY.md#programowanie-obiektowe) opisuje dokladnie ten wzorzec: kazdy obiekt ma czasownik `:description()`, ktory domyslnie zwraca `this.description`, a `look` wywoluje wlasnie ten czasownik (nie czyta wlasciwosci bezposrednio). Jesli nadpiszemy `:description()` na obiekcie-dziecku, mozemy wywolac oryginalna wersje funkcja `pass()` i dopisac cos od siebie.

My nadpisujemy `:description()` nie na jednym pokoju, ale **na samym `$room`** -- czyli rodzicu kompletnie kazdej lokacji w calej bazie, wlaczajac wszystkie 36+ pokoi z Rozdzialu 4. To swiadoma decyzja, nie pomylka: dzieki temu piszemy ten kod raz, a dziala wszedzie. Zeby nie doklejac pogody do wnetrza Kuzni czy Krypty w Kurhanie, dodajemy przelacznik, ktory kazdy pokoj musi jawnie wlaczyc:

```
@property $room.na_zewnatrz 0 rc
```

```
@verb $room:description this none this
```

```
@program $room:description
opis = pass();
if (!this.na_zewnatrz)
return opis;
endif
if (typeof(opis) == STR)
opis = {opis};
endif
return {@opis, "", this:opis_pogody()};
.
```

```
@verb $room:opis_pogody this none this
```

```
@program $room:opis_pogody
pora = $zegar_swiata.pora_dnia;
pogoda = $zegar_swiata.pogoda;
zdania_pory = ["rano" -> "Poranne slonce ledwo wspina sie ponad dachy.", "dzien" -> "Slonce stoi wysoko, dzien jest w pelni.", "wieczor" -> "Niebo barwi sie na pomaranczowo -- zbliza sie wieczor.", "noc" -> "Ciemno, jedynie gwiazdy daja cokolwiek swiatla."];
linia = zdania_pory[pora];
if (pogoda == "deszcz")
linia = linia + " Mzy drobny deszcz.";
elseif (pogoda == "mgla")
linia = linia + " Nad ziemia snuje sie gesta mgla.";
endif
return linia;
.
```

(indeksowanie mapy `zdania_pory[pora]` zaklada, ze `pora` zawsze jest jedna z czterech kluczy tej mapy -- a tak jest, bo sami kontrolujemy mozliwe wartosci `.pora_dnia` w `:tick`, wiec nie musimy tu dodatkowo obslugiwac brakujacego klucza).

Teraz wlacz efekt na kilku lokacjach na zewnatrz -- np.:

```
@set #1500.na_zewnatrz do 1
```

(Rynek), a analogicznie dla Skraju Lasu, Brzegu Rzeki, Podnoza Wzgorz i innych lokacji "pod golym niebem" z Rozdzialu 4. Lokacje wewnatrz budynkow i pod ziemia (Gospoda, Kuznia, caly Kurhan, wnetrze kopalni) zostaw z domyslnym `.na_zewnatrz` rownym `0` -- tam pogoda nie ma racji bytu.

Wpisz `look` na Rynku o roznych porach (albo po prostu poczekaj kilka cykli `:tick`) -- opis powinien teraz konczyc sie zmieniajaca sie linia o porze dnia i pogodzie, podczas gdy sam tekst opisu z Rozdzialu 3 pozostaje nietkniety.

### Ten sam wzorzec gdzie indziej

Dokladnie ta sama technika -- nadpisanie `:description()`, `pass()` po oryginalny tekst, dopisanie czegos na koncu -- dziala na dowolnym obiekcie, nie tylko na `$room`: NPC moze wygladac inaczej w zaleznosci od tego, czy akurat pracuje (Kowal Born przy dzien moglby miec dopisane "wlasnie pracuje przy palenisku", a noca "spi na sienniku w kacie"). Zostawiam to jako cwiczenie -- masz juz caly potrzebny wzorzec.

W Rozdziale 8 wracamy do rzeczy bardziej namacalnych: zamkow, kluczy i tego niedokonczonego Tajnego Przejscia z Rozdzialu 4.

## Rozdzial 8: zamki, sekrety i pulapki

### Wyrazenia kluczowe -- jak dziala blokowanie w MOO

Zanim zablokujemy pierwszy obiekt, warto zrozumiec mechanizm: kazdy obiekt moze byc "zablokowany" wzgledem pewnego **wyrazenia kluczowego** -- logicznego wyrazenia z obiektow polaczonych operatorami `&&` (i), `||` (lub) i `!` (nie). Wyrazenie jest sprawdzane wzgledem konkretnego gracza (a scislej: gracza i wszystkiego, co niesie) -- jesli wyjdzie prawdziwe, gracz moze uzyc obiektu. `help keys` ma pelny, formalny opis; tu wystarczy nam kilka przykladow:

- `klucz` -- prawda, jesli kandydat jest obiektem `klucz` **lub go niesie**.
- `me` -- prawda tylko dla ciebie samego.
- `klucz || straznik` -- prawda dla kogos, kto niesie `klucz`, **lub** dla samego `straznika`.
- `! trumna` -- prawda dla kazdego, kto NIE niesie `trumna`.

### Zamykamy skrzynie ze Skarbca

W Rozdziale 5 stworzylismy `stara okuta skrzynia` w Skarbcu, otwarta dla kazdego. Czas to naprawic. Najpierw potrzebujemy fizycznego klucza -- stworz go stojac w Skarbcu, obok skrzyni (`@move ja do <numer Skarbca>`, jesli nie jestes juz tam):

```
@create $thing named "zardzewialy zelazny klucz,klucz"
@describe klucz jako "Ciezki, mocno zardzewialy klucz. Ktos musial go tu zgubic dawno temu."
```

Nowy klucz jest teraz w twoim ekwipunku -- **zostaw go tam na razie** (nie upuszczaj jeszcze), bo `@lock_for_open` musi go znalezc, a wyrazenia kluczowe dopasowuja obiekty tak samo jak zwykle polecenia: musisz go niesc albo stac z nim w tym samym pokoju (zweryfikowane live: jesli klucz lezy w innym pokoju niz ten, w ktorym wydajesz polecenie, `@lock_for_open` zglosi "Nie mozna znalezc obiektu o nazwie 'klucz'").

Teraz blokujemy skrzynie -- dla kontenerow uzywamy **`@lock_for_open`**, nie zwyklego `@lock` (ten drugi kontroluje co innego -- czy kontener w ogole mozna wziac/przeniesc; `help @lock_for_open`, jesli chcesz sprawdzic roznice):

```
@lock_for_open skrzynia za pomoca klucz
```

(uwaga: tresc `help @lock_for_open` wciaz pokazuje w przykladzie skladni angielskie `with` -- to nieaktualny fragment pomocy, ktory umknal wczesniejszemu audytowi; faktycznie dzialajacy przyimek to `za pomoca` (albo `przy uzyciu`/`uzywajac`), zgodnie z zasada z Rozdzialu 2).

Skrzynia zostala otwarta jeszcze w Rozdziale 5 i tak juz zostala -- zamkniecie (`close`) to stan niezalezny od blokady, wiec zamknij ja teraz, zanim odejdziesz z kluczem (inaczej demonstracja ponizej nie zadziala -- skrzynia bedzie caly czas "juz otwarta"):

```
close skrzynia
```

Teraz przenies klucz na jego docelowe miejsce -- Komnate Straznika (Rozdzial 4) -- i tam go upusc: gracz musi minac straznika, zeby go znalezc, co samo w sobie jest juz malym wyzwaniem (a w Rozdziale 6 straznik dostal juz ostrzegawcza kwestie na ten temat):

```
@move ja do <numer Komnaty Straznika>
drop klucz
```

Wroc do Skarbca i sprobuj `open skrzynia` bez klucza w ekwipunku -- serwer odmowi. Wroc po klucz, wez go (`take klucz`), przynies z powrotem i sprobuj ponownie -- powinno zadzialac. Cofniecie blokady to `@unlock_for_open skrzynia`.

### Zlozone wyrazenie: zamykamy przejscie do Skarbca

Skarbiec (Rozdzial 4) laczy sie z Komnata Straznika wyjsciem "dol". Zablokujmy samo to wyjscie zlozonym wyrazeniem -- przepuszczamy kogos, kto niesie klucz, **lub** samego straznika (np. gdyby mial tam wracac patrolowac). Jesli w Rozdziale 6 zbudowales juz Straznika Kurhanu jako cwiczenie z "Reszty obsady", uzyj go -- jesli nie, przejdz do Komnaty Straznika (`@move ja do <numer z notatnika>`) i zbuduj minimalna wersje, wystarczajaca na potrzeby tego przykladu (ten sam wzorzec `$npc` co przy Kowalu, bez `.gadanie`/`:start()`, bo tu chodzi tylko o sam obiekt do wyrazenia kluczowego):

```
@create #1560 named "Straznik Kurhanu,straznik"
@describe straznik jako "Milczacy, opancerzony ksztalt, ktory nie spuszcza z ciebie wzroku."
drop straznik
```

Stojac w Komnacie Straznika:

```
@lock #<numer-wyjscia-na-dol> za pomoca klucz || straznik
```

Numer wyjscia znajdziesz poleceniem `@exits`, stojac w Komnacie Straznika -- wypisze ono wszystkie konwencjonalne wyjscia z biezacego pokoju wraz z ich numerami obiektow (`help @exits`).

### Ukryte przejscie miedzy Regionem 4 a Regionem 5

W Rozdziale 4 odlozylismy Tajne Przejscie -- polaczenie miedzy Krypta Druga a Podnozem Wzgorz. Teraz mamy juz oba pokoje wykopane, wiec mozemy uzyc **trzeciej formy** `@dig` -- laczacej dwa juz istniejace pokoje numerem obiektu (`help @dig`, forma z `to <numer>`):

Stojac w Krypcie Drugiej:

```
@dig zachod,w to <numer Podnoza Wzgorz>
```

To tworzy wyjscie z Krypty Drugiej do Podnoza Wzgorz (jednokierunkowe -- jesli chcesz przejscia w obie strony, powtorz operacje w drugim kierunku stojac w Podnozu Wzgorz, laczac `to <numer Krypty Drugiej>`).

Wyjscie juz dziala, ale wciaz jest widoczne dla zwyklego gracza, ktory sprobuje polecenia `@ways` (podpowiedz "jakie sa oczywiste wyjscia stad" -- zwykly `look` w tym forku w ogole nie pokazuje listy wyjsc, wiec to `@ways`, nie `look`, jest tu istotne). Zeby je ukryc, korzystamy z wlasciwosci `.obvious`, ktora sprawdza wbudowany mechanizm `$room:obvious_exits()` (dokladnie ten sam rodzaj mechanizmu, ktory nadpisalismy w Rozdziale 7 przy okazji `.na_zewnatrz` -- tym razem nie musimy nic nadpisywac, `.obvious` jest juz obslugiwane przez baze):

```
@exits
@set #<numer-nowego-wyjscia>.obvious do 0
```

(pierwsza komenda to zwykle `@exits`, zeby odczytac numer nowo utworzonego wyjscia -- **uwaga**: kazdy nowy exit juz ma wlasciwosc `.obvious` domyslnie ustawiona na prawde, wiec uzywamy `@set`, nie `@property` -- to drugie zwroci blad "juz istnieje", zweryfikowane live). Od teraz zwykly gracz nie zobaczy tego wyjscia przez `@ways`, ale kto wpisze `zachod` stojac w Krypcie Drugiej, wciaz zostanie przeniesiony -- dokladnie tak, jak powinno dzialac tajne przejscie. (Jako wlasciciel/wizard `@exits` i `@ways` wciaz pokazuja ci wszystko, wlacznie z ukrytymi wyjsciami -- to celowe udogodnienie dla budowniczych, nie blad; testujac ukrywanie, sprawdzaj z perspektywy zwyklego gracza albo bezposrednio przez `;pokoj:obvious_exits()`).

Zeby gracz mial jakakolwiek szanse je znalezc, dajmy podpowiedz przez prosty czasownik wyszukiwania w tym samym pokoju:

```
@verb #<Krypta Druga>:"szukaj search" none none none
```
```
@program #<Krypta Druga>:szukaj
player:tell("Przeszukujesz sciany... i czujesz przeciag z zachodniej strony, tam gdzie kamienie wygladaja na poluzowane.");
.
```

(Uwaga: opis w powyzszym `player:tell` nie zdradza wprost polecenia `zachod` -- to celowe, gracz wciaz musi sam skojarzyc "przeciag z zachodu" z proba wyjscia na zachod. Ile podpowiedziec, a ile zostawic do odkrycia, to decyzja projektowa, nie techniczna).

### Teleport: krag muchomorow na Polanie

Polana z Kregiem Grzybow (Region 2) dostaje teraz swoj "magiczny detal" zapowiedziany w Rozdziale 1 -- przejscie do malej, odosobnionej kieszeni swiata. Najpierw nowa lokacja (mamy na to zapas w budzecie z Rozdzialu 1 -- 38. lokacja, wciaz ponizej 50):

```
@dig "Druga Strona Kregu"
```

Teraz wlasna, plodna klasa teleportu -- ten sam wzorzec klasa+instancje co w Rozdzialach 5 i 6:

```
@create $thing named "Klasa: Teleport,teleport class"
@chmod #<klasa> +f
@property #<klasa>.cel #-1 rc
```

```
@verb #<klasa>:"wejdz enter" this none none
```
```
@program #<klasa>:wejdz
if (!valid(this.cel))
player:tell("Nic sie nie dzieje.");
return;
endif
player:tell("Swiat wiruje na moment...");
this.location:announce(player.name, " znika w powietrzu!");
move(player, this.cel);
player.location:announce(player.name, " pojawia sie znikad!");
.
```

Dwie instancje, kazda wskazujaca na druga -- dokladnie tak, jak dwa konce jednego wyjscia, tylko zaimplementowane jako przedmioty zamiast exitow:

```
@create #<klasa> named "krag muchomorow,krag"
@set #<krag1>.cel do <numer Drugiej Strony Kregu>
drop krag muchomorow
```

Przejdz do "Drugiej Strony Kregu" i powtorz w druga strone:

```
@create #<klasa> named "krag muchomorow,krag"
@set #<krag2>.cel do <numer Polany z Kregiem Grzybow>
drop krag muchomorow
```

Wpisz `wejdz krag` (albo `enter krag`) w Polanie -- powinienes trafic po drugiej stronie, i z powrotem tym samym poleceniem.

### Pulapka: Sala z Pulapka

Ostatni efekt w tym rozdziale wykorzystuje `:enterfunc()` -- czasownik, ktory `$room` (a scislej caly mechanizm wbudowanej funkcji `move()`) wywoluje automatycznie na kazdym pokoju, do ktorego cos wchodzi, z przybywajacym obiektem jako argumentem. Nadpisujac go (z `pass()`, zeby nie zgubic domyslnych komunikatow przyjscia), mozemy dodac efekt uboczny:

```
@verb #<Sala z Pulapka>:enterfunc this none this
```
```
@program #<Sala z Pulapka>:enterfunc
who = args[1];
pass(who);
if (is_player(who) && (random(2) == 1))
who:tell("Klik! Nadeptujesz na luzna plyte -- z sufitu spada siec kamiennych odwazikow i odpycha cie do tylu!");
this:announce(who.name, " wpada w pulapke i zostaje wypchniety z powrotem!");
move(who, <numer Korytarza Kurhanu>);
endif
.
```

Polowa szans na aktywacje (`random(2) == 1`) sprawia, ze pulapka nie jest deterministyczna -- gracz moze przejsc bez problemu za pierwszym razem i wpasc za drugim, co jest bardziej przekonujace niz sztywna, zawsze-taka-sama blokada. `is_player(who)` pilnuje, zeby pulapka nie odpalala sie na kazdym rzuconym przedmiocie czy NPC-u, ktory akurat tamtedy przejdzie.

### Co dalej

Mamy juz komplet mechanik "namacalnych": zamki, klucze, sekrety, teleporty, pulapki -- i przy okazji dokonczylismy mape z Rozdzialu 4 (Tajne Przejscie i Druga Strona Kregu). W Rozdziale 9 dodajemy ostatni duzy element brakujacy graczowi do pelnej rozgrywki: sposob, by cos kupic i sprzedac.

## Rozdzial 9: ekonomia

### Waluta: liczba, nie przedmiot

Najprostszy i najbardziej niezawodny sposob na walute w MOO to zwykla liczba we wlasciwosci gracza, a nie fizyczny przedmiot "moneta", ktory trzeba nosic, podnosic i pilnowac, zeby sie nie zdublowal. Dodajemy wlasciwosc do `$player` -- tak jak `.na_zewnatrz` na `$room` w Rozdziale 7, robimy to raz, na wspolnym rodzicu, i **kazdy** gracz w bazie (obecny i przyszly) dostaje ja automatycznie, z domyslna wartoscia 0:

```
@property $player.miedziaki 0 rc
```

Na potrzeby testowania daj sobie troche grosza:

```
@set ja.miedziaki do 20
```

### Wlasna klasa: sklepikarz

Sklepikarz to NPC ze specjalnymi czasownikami do handlu -- najprosciej zbudowac go jako **dziecko klasy `$npc`** z Rozdzialu 6, a nie zaczynac od zera. To pierwszy przypadek w tym poradniku, gdzie wlasna klasa dziedziczy po innej naszej wlasnej klasie, nie bezposrednio po standardowej -- lancuch wyglada tak: `$thing -> $npc -> $sklepikarz -> (konkretni sklepikarze)`.

```
@create $npc named "Klasa: Sklepikarz,sklepikarz class"
@chmod #<klasa> +f
@property #<klasa>.towar {} rc
```

`.towar` bedzie lista map, jedna mapa na kazdy towar: nazwa, aliasy, cena i opis. Dwa czasowniki do przegladania i kupowania:

```
@verb #<klasa>:"cennik pricelist" none z this
```
```
@program #<klasa>:cennik
player:tell(this.name, " ma na sprzedaz:");
for pozycja in (this.towar)
player:tell("  ", pozycja["nazwa"], " -- ", pozycja["cena"], " miedziakow");
endfor
.
```

```
@verb #<klasa>:"kup buy" any z this
```
```
@program #<klasa>:kup
tekst = dobjstr;
for pozycja in (this.towar)
if ((tekst == pozycja["nazwa"]) || (tekst in pozycja["aliasy"]))
if (player.miedziaki < pozycja["cena"])
player:tell("Nie stac cie na to -- potrzebujesz ", pozycja["cena"], " miedziakow, a masz ", player.miedziaki, ".");
else
player.miedziaki = player.miedziaki - pozycja["cena"];
nowy = create($thing, player);
nowy.name = pozycja["nazwa"];
nowy.aliases = pozycja["aliasy"];
nowy.description = pozycja["opis"];
player:tell("Kupujesz ", pozycja["nazwa"], " za ", pozycja["cena"], " miedziakow.");
this.location:announce(player.name, " kupuje ", pozycja["nazwa"], " u ", this.name, ".");
endif
return;
endif
endfor
player:tell("Nie mamy czegos takiego na sprzedaz. Sprobuj 'cennik'.");
.
```

Skladnia komendy: `kup mikstura z sklepikarz` -- `z` to standardowy, wbudowany przyimek tego forka (`help prepositions`; przypomnienie z Rozdzialu 2: silnik rozpoznaje tu polskie przyimki, nie angielskie).

I czasownik odwrotny, sprzedawanie -- gracz oddaje przedmiot, ktory faktycznie niesie, sklepikarz placi za niego stala kwote (chyba ze przedmiot ma wlasna wlasciwosc `.wartosc_sprzedazy`):

```
@verb #<klasa>:"sprzedaj sell" any do this
```
```
@program #<klasa>:sprzedaj
if ((dobj == $failed_match) || !valid(dobj) || (dobj.location != player))
player:tell("Nie masz czegos takiego przy sobie.");
return;
endif
if ($object_utils:has_property(dobj, "wartosc_sprzedazy"))
wartosc = dobj.wartosc_sprzedazy;
else
wartosc = 1;
endif
player.miedziaki = player.miedziaki + wartosc;
player:tell("Sprzedajesz ", dobj.name, " za ", wartosc, " miedziakow.");
recycle(dobj);
.
```

### Konkretny sklepikarz: Zielarka Jagna

Wracamy do Chatki Zielarki z Rozdzialu 1/4 (`@move ja do <numer Chatki z notatnika>`), gdzie od poczatku byla zapowiedziana jako zrodlo handlu:

```
@create #<klasa> named "Zielarka Jagna,jagna,zielarka"
@describe jagna jako "Starsza kobieta o zrecznych palcach, cala obwieszona pekami suszonych ziol."
@set jagna.towar do [["nazwa" -> "flaszeczka mikstury", "aliasy" -> {"flaszeczka", "mikstura"}, "cena" -> 3, "opis" -> "Metny, zielonkawy plyn o ostrym zapachu."], ["nazwa" -> "peczek suszonych ziol", "aliasy" -> {"peczek", "ziola"}, "cena" -> 1, "opis" -> "Kilka gatunkow ziol, zwiazanych razem sznurkiem."]]
drop jagna
```

Uruchom jej gadanie w tle, tak jak przy Kowalu w Rozdziale 6 (Jagna dziedziczy `:start`/`:stop`/`:heartbeat` po `$npc`, mimo ze jest jednoczesnie sklepikarzem) -- pamietaj o `;` i numerze obiektu (`#<numer Jagny>`), z tych samych powodow co przy Kowalu:

```
;#<numer Jagny>:start()
```

Sprobuj `cennik z jagna`, potem `kup mikstura z jagna` (majac przynajmniej 3 miedziaki), a na koniec `sprzedaj flaszeczka mikstury do jagna`, zeby zobaczyc pelny cykl handlu w obie strony.

### Co dalej

Mamy przedmioty, NPC-e, atmosfere, zamki i teraz ekonomie -- brakuje juz tylko jednego: powodu, dla ktorego gracz mialby to wszystko odwiedzic w konkretnej kolejnosci. W Rozdziale 10 spinamy kilka z tych mechanik w prosty, sledzony quest.

## Rozdzial 10: prosty system questow

### Stan questu: mapa na graczu

Tak jak waluta w Rozdziale 9, stan questow to wlasciwosc na `$player` -- wspolna dla kazdego gracza, dodana raz:

```
@property $player.questy [] rc
```

Pusta mapa domyslnie oznacza "gracz nie zaczal jeszcze zadnego questu". Klucz to nazwa questu (string), wartosc to jego status -- w naszym przykladzie beda to `"aktywny"` i `"ukonczony"`; brak klucza w mapie oznacza "nie zaczety". Ten sam wzorzec sprawdzania klucza co przy `.odpowiedzi` NPC-ow w Rozdziale 6:

```
if ("kurhan" in mapkeys(player.questy))
stan = player.questy["kurhan"];
else
stan = "nowy";
endif
```

### Quest: Sygnet z Kurhanu

Nasz quest laczy trzy mechaniki z poprzednich rozdzialow: dialog z NPC-em (Rozdzial 6), przedmiot ukryty za zamkiem w Skarbcu (Rozdzial 8) i nagrode w walucie (Rozdzial 9). Najpierw przedmiot questowy -- dopisz go obok `garsc starych srebrnych monet` w Skarbcu:

```
@create $thing named "stary zloty sygnet,sygnet"
@describe sygnet jako "Ciezki sygnet z wygrawerowanym herbem, ktorego nikt we wsi juz nie rozpoznaje."
drop stary zloty sygnet
```

Teraz dwa czasowniki na Staroscie Wlodzimierzu (Rozdzial 6) -- to czasowniki **na konkretnej instancji**, nie na calej klasie `$npc`, bo dotycza tylko jego, nie kazdego NPC-a w grze:

```
@verb starosta:"zadanie quest" this none this
```
```
@program starosta:zadanie
if ("kurhan" in mapkeys(player.questy))
stan = player.questy["kurhan"];
else
stan = "nowy";
endif
if (stan == "nowy")
player.questy["kurhan"] = "aktywny";
this:announce_line("W Kurhanie na poludniu spoczywa stary sygnet naszego rodu. Kaplani boja sie tam isc, ale ktos musi go odzyskac. Przynies mi go, a nie pozostaniesz bez nagrody.");
elseif (stan == "aktywny")
this:announce_line("Wciaz czekam na ten sygnet z Kurhanu.");
elseif (stan == "ukonczony")
this:announce_line("Jeszcze raz dziekuje za sygnet. Dobrze zrobiony.");
endif
.
```

(`this:announce_line` to ten sam pomocniczy czasownik z Rozdzialu 6, odziedziczony po `$npc` -- nie musimy go pisac od nowa).

```
@verb starosta:"oddaj zwroc" any do this
```
```
@program starosta:oddaj
if ("kurhan" in mapkeys(player.questy))
stan = player.questy["kurhan"];
else
stan = "nowy";
endif
if ((dobj == $failed_match) || !valid(dobj) || (dobj.location != player))
player:tell("Nie masz przy sobie czegos takiego.");
elseif (stan != "aktywny")
this:announce_line("Nie prosilem cie o nic takiego.");
elseif (!("sygnet" in dobj.aliases))
this:announce_line("To nie to, czego szukalem.");
else
recycle(dobj);
player.questy["kurhan"] = "ukonczony";
player.miedziaki = player.miedziaki + 15;
this:announce_line("Dziekuje ci, wreszcie mozemy odetchnac. Masz -- to dla ciebie 15 miedziakow.");
this.location:announce(player.name, " oddaje cos Staroscie Wlodzimierzowi.");
endif
.
```

Skladnia dla gracza: `zadanie starosta`, zeby przyjac (albo przypomniec sobie) quest, i `oddaj sygnet do starosta`, zeby go zakonczyc.

### Dlaczego stan questu, a nie tylko posiadanie przedmiotu

Moglibysmy sprawdzac tylko "czy gracz ma sygnet w ekwipunku", bez zadnej wlasciwosci `.questy` -- dla jednego questu to nawet by zadzialalo. Ale wlasciwosc stanu ma dwie przewagi, ktore widac dopiero przy wiekszej liczbie zadan: po pierwsze, quest moze byc "ukonczony" mimo ze przedmiot juz dawno zniknal (zostal zrecyklowany po oddaniu) -- bez osobnego stanu nie dalby sie odroznic "nigdy nie zaczety" od "juz ukonczony". Po drugie, `.questy` to jedna, wspolna mapa, do ktorej mozna z latwoscia dopisac kolejne questy (nowy klucz, nowy para czasownikow) bez zmiany istniejacego kodu -- to ten sam powod, dla ktorego `.towar` sklepikarza z Rozdzialu 9 jest lista, a nie osobna wlasciwoscia na kazdy przedmiot.

Jako cwiczenie, sprobuj dodac drugi quest wykorzystujacy mechaniki z wczesniejszych rozdzialow -- np. Kaplani ze Swiatyni Trzech Ksiezycow (Rozdzial 1) proszacy o pozbycie sie zbojcow z Obozowiska (Rozdzial 6) albo o zbadanie Polany z Kregiem Grzybow (Rozdzial 8).

### Co dalej

Caly mechaniczny szkielet swiata jest gotowy: mapa, przedmioty, NPC-e, atmosfera, zamki, ekonomia i quest, ktory je wszystkie spina. W Rozdziale 11 dopinamy ostatni, latwy do pominiecia element -- pomoc w grze, zeby gracz, ktory trafi do naszego swiata bez tego poradnika w reku, mial szanse sam sie w nim odnalezc.

## Rozdzial 11: pomoc w grze dla wlasnej zawartosci

### Jak dziala `help` w tym forku

Polecenie `help <temat>` przeszukuje kilka "baz pomocy" po kolei: samego gracza i jego przodkow (az do `$player`), a jesli gracz stoi w pokoju -- rowniez ten pokoj i jego przodkow (az do `$room`), a na koncu zawsze glowna baze `$help`. Kazdy z tych obiektow moze miec wlasciwosc `.help`, ktorej wartoscia jest obiekt-baza-pomocy (albo lista takich obiektow) -- w kazdej takiej bazie temat pomocy to po prostu wlasciwosc o nazwie tematu, a jej wartosc to tekst (string dla jednej linii, lista stringow dla wielu linii).

To znaczy: mozemy dodac pomoc **specyficzna dla naszego swiata**, ktora pojawi sie tylko wtedy, gdy gracz faktycznie w nim jest -- nie musimy niczego dopisywac do glownej, ogolnoswiatowej bazy pomocy.

### Wlasna baza pomocy

Nowa baza pomocy to zwykly obiekt dziedziczacy po Generic Help Database (`#30`):

```
@create #30 named "Baza Pomocy: Dolina Kruczych Wzgorz,baza pomocy doliny"
@corify baza pomocy doliny jako pomoc_doliny
```

Kazdy temat to jedna wlasciwosc -- nazwa wlasciwosci musi byc poprawnym identyfikatorem MOO (bez spacji), wiec gracz bedzie pisal np. `help kurhan`, nie `help stary kurhan`:

```
@property $pomoc_doliny.dolina {"Dolina Kruczych Wzgorz to niewielka kraina: wioska Kruczy Brod, otaczajacy ja Las Szepczacych Debow, Rzeka z Mostem Kruczym, stary Kurhan na poludniu i Wzgorza z opuszczona kopalnia na zachodzie."} rc
@property $pomoc_doliny.kurhan {"Stary kopiec grobowy na poludnie od rzeki. Straznik przy wejsciu do wnetrza ostrzega przybyszow -- podobno nie bez powodu. W srodku znajduje sie zamkniety Skarbiec."} rc
@property $pomoc_doliny.sklep {"Zielarka Jagna w swojej chatce sprzedaje towary. 'cennik z jagna' pokazuje oferte, 'kup <przedmiot> z jagna' kupuje, 'sprzedaj <przedmiot> do jagna' sprzedaje jej cos z twojego ekwipunku."} rc
@property $pomoc_doliny.zadania {"Zapytaj Starosty Wlodzimierza w Domu Starosty o 'zadanie', jesli szukasz czegos do zrobienia w tej okolicy."} rc
```

### Podpiecie pod system pomocy

Zeby te tematy byly widoczne przez `help`, dopisujemy nasza baze do wlasciwosci `.help` na `$room` -- podobnie jak `.na_zewnatrz` w Rozdziale 7 i `.miedziaki` w Rozdziale 9, robimy to raz, na wspolnym rodzicu, wiec dziala automatycznie w kazdym pokoju calego swiata (nie tylko naszych 38 lokacjach):

```
@property $room.help {} rc
```

(jesli serwer odpowie, ze `$room` juz ma wlasciwosc `.help`, pomin ten krok -- niektore baza moga ja juz definiowac; przechodzimy dalej niezaleznie od wyniku). Nastepnie dopisujemy nasza baze do listy, zamiast ja nadpisywac -- na wypadek, gdyby cos tam juz bylo:

```
@set $room.help do {@$room.help, $pomoc_doliny}
```

Stojac w dowolnej lokacji naszej mapy, wpisz `help kurhan` albo `help sklep` -- powinienes zobaczyc tresc odpowiedniej wlasciwosci. Poza naszym swiatem (w innej czesci bazy) te tematy nie beda widoczne -- dokladnie tak, jak powinno byc.

### Alternatywa: dopisanie do glownej bazy pomocy

Jesli wolisz, zeby twoje tematy byly dostepne wszedzie, a nie tylko w twoim swiecie, mozna je zamiast tego dopisac bezposrednio do glownej bazy `$help` (tej samej, ktora obsluguje `help @dig` czy `help movement`) -- to ten sam mechanizm wlasciwosci-per-temat, tylko na obiekcie `$help` zamiast na naszej wlasnej bazie. Dla tresci specyficznej dla jednego, wydzielonego swiata (tak jak nasz) osobna baza podpieta pod `$room` jest zwykle lepszym wyborem -- nie miesza sie z pomoca dotyczaca calego serwera.

### Co dalej

Caly swiat -- mapa, przedmioty, NPC-e, atmosfera, zamki, ekonomia, quest i teraz pomoc -- jest kompletny i gotowy do zwiedzania. W Rozdziale 12, ostatnim, przechodzimy przez checkliste testowa calosci i zbieramy wskazowki, dokad pojsc dalej.

## Rozdzial 12: testowanie i dalsze kierunki

### Checklist -- przejdz sie po calym swiecie

Zanim uznasz swiat za gotowy (nawet jesli to tylko twoj wlasny serwer testowy), warto przejsc systematycznie przez wszystko, co zbudowales -- latwo o literowke w numerze obiektu albo zapomniany krok, ktory wyjdzie dopiero przy faktycznym uzyciu, nie przy samym pisaniu kodu:

- **Mapa**: przejdz sie po wszystkich 38 lokacjach w obie strony kazdym wyjsciem -- brakujace wyjscie powrotne to najczestszy blad przy recznym `@dig`. `@dig` z Rozdzialu 4 tworzylo oba kierunki naraz, ale jesli cokolwiek poprawiales recznie, latwo zapomniec o drugiej stronie.
- **Opisy**: sprawdz, czy kazda lokacja wymieniona w Rozdzialach 5-10 (tam, gdzie stoi jakis przedmiot, NPC albo mechanika) ma opis inny niz domyslny pusty.
- **NPC-e**: dla kazdego, `zagadnij <npc> o <temat>` na przynajmniej jeden temat z jego `.odpowiedzi`, i sprawdz, czy `:start()` faktycznie zostalo wywolane (patrz nizej, jak to sprawdzic bez zgadywania).
- **Przedmioty**: `zjedz chleb` (czy cokolwiek zjadlego stworzyles), `open`/`close`/`take from` na skrzyni w Skarbcu (przed i po zdobyciu klucza).
- **Ekonomia**: pelny cykl `cennik z jagna` -> `kup ... z jagna` -> `sprzedaj ... do jagna`, sprawdzajac, czy `.miedziaki` faktycznie sie zmienia.
- **Quest**: `zadanie starosta` (nowy), `zadanie starosta` ponownie (aktywny -- inny tekst), zdobycie sygnetu, `oddaj sygnet do starosta` (nagroda), `zadanie starosta` ponownie (ukonczony -- trzeci wariant tekstu).
- **Zamki i sekrety**: probuj otworzyc skrzynie bez klucza (ma sie nie udac), z kluczem (ma sie udac); przejdz przez Tajne Przejscie mimo ze nie widac go na liscie wyjsc; wejdz w krag muchomorow i wroc.
- **Pulapka**: wejdz do Sali z Pulapka kilka razy pod rzad -- powinienes zobaczyc oba warianty (aktywacja i brak aktywacji), bo szansa jest losowa.
- **Pomoc**: `help dolina`, `help kurhan`, `help sklep`, `help zadania`, stojac gdziekolwiek w naszym swiecie.

### Sprzatanie po sobie: zadania w tle

Kazdy NPC i `$zegar_swiata` maja wlasne, samoplanujace sie zadania (Rozdzialy 6 i 7). Zeby sprawdzic, co aktualnie dziala w tle (przydatne, jesli podejrzewasz, ze cos zapetlilo sie bledne albo ze zapomniales czegos zatrzymac), wpisz:

```
queued_tasks()
```

Zwroci liste wszystkich zaplanowanych zadan -- wlacznie z tymi utworzonymi przez `fork` w naszych czasownikach `:heartbeat`/`:tick`. Jesli chcesz gruntownie posprzatac przed dluzsza przerwa (albo zanim zrecyklujesz jakiegos NPC-a -- **zawsze** `<npc>:stop()` przed `@recycle`, jak przypomnielismy w Rozdziale 6), mozesz zatrzymac konkretne zadanie przez `kill_task(<numer-zadania>)`.

### Typowe pulapki (tym razem nie te zaprogramowane)

- **Numery obiektow z tego poradnika sa przykladowe.** Kazdy `#1500`, `#1550`, `#1560`, `#1575` i tak dalej w tekscie to placeholder -- twoje beda inne. Jesli kopiujesz kod blok po bloku, upewnij sie za kazdym razem, ze podstawiles wlasciwy numer (albo, tam gdzie to mozliwe, uzywaj nazw obiektow, ktore akurat niesiesz lub w ktorych stoisz, tak jak w wielu przykladach powyzej).
- **`this none this` (`tnt`) to nie "polecenie bez argumentow".** To oznaczenie czasownika wywolywanego tylko z kodu, nigdy bezposrednio przez gracza -- prawdziwe polecenie bez zadnych dopelnien to `none none none` (Rozdzial 3 ma pelne wyjasnienie roznicy; poradnik mial ten blad we wczesniejszej wersji trzech czasownikow, wiec jesli porownujesz z jakas zapisana wczesniej kopia, sprawdz, czy jest juz poprawiona).
- **Zapomniane `:start()`.** Nowo stworzony NPC albo `$zegar_swiata` nie robi nic sam z siebie, dopoki nie wywolasz na nim `:start()` -- latwo o tym zapomniec, bo kod sie kompiluje i wyglada na gotowy.
- **`@create` nie umieszcza obiektu w pokoju.** Nowy obiekt laduje w twoim ekwipunku -- pamietaj o `drop`, jesli ma lezec w konkretnym miejscu (Rozdzial 5 zwraca na to uwage przy pierwszej notatce).
- **Limit quota.** Jesli w trakcie budowy serwer zaczyna odmawiac `@create`/`@dig`, wroc do Rozdzialu 2 -- prawdopodobnie przekroczyles `.size_quota`.

### Podsumowanie: co dokladnie zbudowalismy

- 38 lokacji w 5 regionach, w pelni polaczonych (wlacznie z jednym ukrytym i jednym teleportowym polaczeniem).
- Cztery wlasne, plodne klasy-rodzice: `$edible` (Rozdzial 5), `$npc` (Rozdzial 6), klasa teleportu (Rozdzial 8) i `$sklepikarz` dziedziczacy po `$npc` (Rozdzial 9).
- Szesc rozszerzen wspolnych klas bazowych (`$room`, `$player`) o nowe wlasciwosci i czasowniki, dzialajacych automatycznie w calej bazie: `.na_zewnatrz` + `:description()` (Rozdzial 7), `.miedziaki` (Rozdzial 9), `.questy` (Rozdzial 10), `.help` (Rozdzial 11).
- Jeden globalny obiekt stanu (`$zegar_swiata`) z samoplanujacym sie zadaniem w tle.
- Pelny cykl ekonomiczny i jeden quest laczacy dialog, zamek i nagrode.
- Wlasna baza pomocy widoczna tylko w obrebie naszego swiata.

Zaden pojedynczy element nie jest skomplikowany -- cala wartosc bierze sie z tego, jak sa ze soba polaczone.

### Dokad dalej

Kilka naturalnych kierunkow rozwoju, kazdy budujacy na czyms, co juz masz:

- **Wiecej questow** -- masz juz caly wzorzec z Rozdzialu 10, kolejne to glownie tresc, nie nowy kod.
- **System walki** -- ten poradnik celowo go pomija (to osobny, duzy temat), ale `random()`, wlasciwosci na graczu (jak `.miedziaki`/`.questy`) i `:enterfunc()`/czasowniki-akcje z Rozdzialu 8 to dokladnie te same narzedzia, ktorych by wymagal.
- **Gildie/frakcje** -- Rada Starszych i Zbojcy z Rozdzialu 1 sa gotowym punktem wyjscia; wlasciwosc-mapa podobna do `.questy`, tylko trzymajaca przynaleznosc gracza, poszlaby w te sama strone.
- **Wiecej NPC-ow z prawdziwa "sztuczna inteligencja"** -- `:heartbeat` z Rozdzialu 6 mozna rozbudowac o patrolowanie miedzy pokojami (`move(this, ...)` zamiast tylko `:announce()`), nie tylko losowe kwestie w miejscu.
- **Glebsza integracja z pomoca** -- Rozdzial 11 pokazuje minimum; Generic Help Database (`#30`, rodzic naszej `$pomoc_doliny`) obsluguje tez tematy w postaci `{"*forward*", ...}` i `{"*subst*", ...}`, przydatne przy wiekszej ilosci tresci.
- **WAIF-y zamiast wlasciwosci na obiektach** -- dla struktur danych bardziej zlozonych niz proste mapy/listy (np. rozbudowany ekwipunek questowy), [dokumentacja WAIF-ow](WAIF-PODRECZNIK-PROGRAMISTY.md) pokazuje lzejsza alternatywe dla pelnych obiektow MOO.
- **Zarzadzanie serwerem produkcyjnym** -- gdy uznasz, ze cos z tego poradnika nadaje sie do pokazania innym graczom, [Podstawy dla Czarodziei](PODSTAWY-DLA-CZARODZIEI.md) i [Przewodnik dla poczatkujacych](PRZEWODNIK-DLA-POCZATKUJACYCH.md) pokrywaja backupy, konta graczy i uruchamianie serwera na stale.

Dla pelnej, formalnej referencji jezyka i wszystkich funkcji wbudowanych, ktorych uzylismy po drodze (`fork`, `pass`, mapy, `random`, `move` i reszta), zajrzyj do [Podrecznika Programisty](PODRECZNIK-PROGRAMISTY.md) -- ten poradnik pokazywal je w dzialaniu, na konkretnym przykladzie, ale to on jest ostatecznym zrodlem prawdy o skladni i semantyce jezyka MOO.
