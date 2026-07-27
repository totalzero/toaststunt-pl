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

Rozdzialy:

1. Koncepcja swiata (ten rozdzial)
2. Przygotowanie warsztatu budowniczego
3. Pierwsza lokacja recznie
4. Budowa calej mapy
5. Przedmioty
6. NPC-e i dialogi
7. Efekty atmosferyczne
8. Zamki, sekrety i pulapki
9. Ekonomia
10. Proste zadania (questy)
11. Pomoc w grze dla wlasnej zawartosci
12. Testowanie i dalsze kierunki

*(Pelny spis tresci z odnosnikami do sekcji pojawi sie na koncu, gdy wszystkie rozdzialy beda gotowe -- na razie powyzsza lista to plan.)*

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
@programmer ja
```

(albo `@programmer <twoja-nazwa-gracza>`, jesli wolisz podac nazwe wprost). Jesli budujesz na cudzym serwerze, popros czarodzieja o to samo polecenie na twoim koncie -- zobacz [Podstawy dla Czarodziei](PODSTAWY-DLA-CZARODZIEI.md#jak-tworzyc-programistow) po ich stronie procesu.

### Limit obiektow (quota) -- sprawdz to, zanim zaczniesz

Kazdy nowy programista dostaje domyslny limit **7 obiektow** (wlasciwosc `size_quota`) -- to znaczy, ze bez podniesienia limitu nie zbudujesz nawet jednego regionu z naszej mapy, nie mowiac o calych ~37 lokacjach plus przedmiotach i NPC-ach. Wyjatkiem sa czarodzieje -- oni nie sa ograniczani limitem quota.

Sprawdz swoj aktualny limit:

```
@quota ja
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

Majac uprawnienia, limit i notatnik gotowe, mozemy wykopac pierwszy pokoj -- Rozdzial 3.

## Rozdzial 3: pierwsza lokacja recznie

Zaczynamy od centrum naszego swiata -- rynku w Kruczym Brodzie. To bedzie jedyny pokoj w calym poradniku, ktory budujemy krok po kroku z pelnym komentarzem do kazdego polecenia; od Rozdzialu 4 wiemy juz, co robimy, wiec tempo przyspiesza.

### Kopiemy pokoj

```
@dig "Rynek w Kruczym Brodzie"
```

Serwer odpowie czyms w rodzaju:

```
Rynek w Kruczym Brodzie stworzony jako #1500.
```

**Twoj numer bedzie inny** -- kazda baza ma inny stan licznika obiektow, wiec u ciebie moze to byc `#88`, `#3502`, cokolwiek. W dalszej czesci tego rozdzialu uzywam `#1500` jako przykladu -- wszedzie, gdzie go widzisz, podstaw swoj wlasny numer. (To zreszta dokladnie po to prowadzimy notatnik z Rozdzialu 2 -- zapisz go tam juz teraz.)

Ta forma `@dig` (bez `to`) tworzy pokoj **niepolaczony z niczym** -- wisi w probni, dokladnie tak jak mowi help @dig (`help @dig`, jesli chcesz przypomniec sobie skladnie). To celowe: polaczenia (exits) budujemy systematycznie dla calej mapy w Rozdziale 4, zeby nie robic tego kawalkami.

### Przenosimy sie tam

Nowy pokoj nie ma jeszcze zadnego wejscia, wiec zwykle chodzenie nic nie da -- teleportujemy sie poleceniem `@move`:

```
@move me do #1500
```

Powinienes zobaczyc nazwe pokoju i (na razie) pusty, domyslny opis.

### Opisujemy pokoj

Opis to najwazniejsza pojedyncza rzecz, jaka gracz widzi w kazdej lokacji -- wart czasu. Ustawiamy go przez `@describe`:

```
@describe here as "Nierowny bruk, wytarty tysiacami stop. Posrodku stoi kamienna studnia z zadaszeniem z poszarzalej dachowki. Wokol niej kilka drewnianych straganow, teraz pustych -- targ zaczyna sie dopiero rano. Z rynku widac gospode, kuznie i sciezki wiodace w strone lasu oraz wzgorz."
```

Uzylam `here`, bo po `@move` jestesmy juz w tym pokoju -- mozna tez podac numer wprost (`@describe #1500 as "..."`). Wpisz `look`, zeby zobaczyc efekt.

Technicznie `@describe` po prostu ustawia wlasciwosc `.description` na obiekcie -- `@describe here as "..."` to skrot dla `@set here.description to "..."`. Warto to wiedziec, bo w Rozdziale 7 bedziemy ta wlasciwosc odczytywac i modyfikowac z poziomu kodu (np. zeby opis zmienial sie w zaleznosci od pory dnia).

Zauwaz cos waznego w tresci opisu: wspomina "sciezki wiodace w strone lasu oraz wzgorz", mimo ze tych wyjsc jeszcze fizycznie nie ma. To swiadomy zabieg -- opis pokoju to najlepsze miejsce, by *zapowiedziec* graczowi, dokad moze pojsc, zanim jeszcze sprawdzi liste wyjsc. Miej to na uwadze przy pisaniu opisow reszty mapy w Rozdziale 4.

### Pierwszy wlasny czasownik: `nasluchuj`

Zanim przejdziemy do budowy reszty mapy, zobaczmy pelny cykl pisania kodu na czyms malym -- czasownik, ktory dodaje odrobine klimatu, gdy gracz wpisze `nasluchuj` stojac na rynku.

Tworzymy nowy czasownik na naszym pokoju:

```
@verb #1500:"nasluchuj listen" tnt
```

`tnt` to skrot na `this none this` -- uzywamy go, bo to czasownik-polecenie bez dopelnien (patrz `help @verb`, jesli chcesz przypomniec sobie, co oznaczaja `dobj`/`prep`/`iobj`). Podajemy dwie nazwy na raz (`nasluchuj` i angielskie `listen`), zeby dzialalo niezaleznie od tego, w jakim jezyku gracz wpisuje polecenia -- tak jak reszta bazy ToastCore.

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

Ten fork rozpoznaje polskie nazwy kierunkow obok angielskich skrotow -- `polnoc`/`n`, `poludnie`/`s`, `wschod`/`e`, `zachod`/`w`, `polnocny-wschod`/`ne`, `poludniowy-wschod`/`se`, `poludniowy-zachod`/`sw`, `polnocny-zachod`/`nw`, `gore`/`u`, `na dol`/`d` (mozesz to zweryfikowac samemu -- to zaszyta w kodzie tabela w `$string_utils` uzywana m.in. do generowania wyjsc). W kazdym `@dig` z tego rozdzialu podaje oba warianty naraz, tak jak w przykladzie z `help @dig` (`west,w|east,e,out`) -- gracz bedzie mogl wpisac dowolny z nich.

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
| Korytarz Kurhanu | na dol od Wejscia do Kurhanu | |
| Krypta Pierwsza | wschod od Korytarza | |
| Krypta Druga | zachod od Korytarza | ukryte polaczenie z Regionem 5, Rozdzial 8 |
| Sala z Pulapka | poludnie od Korytarza | fizyczna pulapka, Rozdzial 8 |
| Komnata Straznika | poludnie od Sali z Pulapka | NPC-straznik/mini-boss, Rozdzial 6 |
| Skarbiec | na dol od Komnaty Straznika | zamkniete, Rozdzial 8 |
| Tajne Przejscie | (ukryty exit z Krypty Drugiej) | prowadzi do Regionu 5 |

**Region 5: Wzgorza i Opuszczona Kopalnia**

| Lokacja | Polaczenie | Uwaga |
|---|---|---|
| Podnoze Wzgorz | zachod od Tajnego Przejscia | |
| Szlak Gorski | polnoc od Podnoza Wzgorz | |
| Szczyt Wzgorza | polnoc od Szlaku Gorskiego | slepy zaulek, widok/atmosfera |
| Wejscie do Opuszczonej Kopalni | poludnie od Podnoza Wzgorz | |
| Kopalnia -- Poziom Pierwszy | na dol od Wejscia do Kopalni | |
| Grota Krysztalowa | wschod od Poziomu Pierwszego | skarb/ekonomia, Rozdzial 9 |
| Kopalnia -- Poziom Drugi (Obozowisko Zbojcow) | na dol od Poziomu Pierwszego | siedziba antagonistow, Rozdzial 6 i 8 |

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

Wroc do Rynku (`poludnie`, `poludnie`) i wykop wschodnia odnoge:

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

Wroc do Rynku (`polnoc`, `zachod`, `zachod` -- albo po prostu uzyj `@move me do #1500`, jesli wolisz nie liczyc krokow) i wykop pozostale dwie odnogi:

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

Wejdz do Bramy Polnocnej (z Kuzni: `polnoc`) i kop dalej w las:

```
@dig polnoc,n|poludnie,s to "Skraj Lasu"
```

Przejdz `polnoc`, i z Skraju Lasu wykop dwie odnogi:

```
@dig wschod,e|zachod,w to "Zrodlo Lesne"
```

Wroc (`zachod`) do Skraju Lasu i idz dalej w gab lasu:

```
@dig polnoc,n|poludnie,s to "Gesty Gaszcz"
```

Przejdz `polnoc` do Gestego Gaszczu i wykop chate pustelnika oraz dalsza sciezke:

```
@dig zachod,w|wschod,e to "Chata Pustelnika"
```

Wroc (`wschod`) do Gestego Gaszczu:

```
@dig polnoc,n|poludnie,s to "Polana z Kregiem Grzybow"
```

Przejdz `polnoc` na Polane i wykop ostatnie dwa pokoje regionu:

```
@dig polnoc,n|poludnie,s to "Jaskinia Niedzwiedzia"
```

Wroc (`poludnie`) na Polane:

```
@dig wschod,e|zachod,w to "Stary Dab Piorunem Rozlupany"
```

Region 2 gotowy -- 7 lokacji.

### Budujemy Region 3 (Rzeka i Most Kruczy)

Wroc do Rynku i wejdz przez Brame Poludniowa (`poludnie`, `poludnie`):

```
@dig poludnie,s|polnoc,n to "Brzeg Rzeki"
```

Przejdz `poludnie` na Brzeg Rzeki i wykop trzy odnogi:

```
@dig wschod,e|zachod,w to "Przystan Rybacka"
```

Wroc (`zachod`):

```
@dig zachod,w|wschod,e to "Wodny Mlyn"
```

Wroc (`wschod`):

```
@dig poludnie,s|polnoc,n to "Most Kruczy"
```

Przejdz `poludnie` na Most i wykop drugi brzeg:

```
@dig poludnie,s|polnoc,n to "Drugi Brzeg Rzeki"
```

Region 3 gotowy -- 5 lokacji.

### Budujemy Region 4 (Kurhan Kruczych Wzgorz)

Przejdz `poludnie` z Drugiego Brzegu Rzeki i wykop wejscie do kurhanu:

```
@dig poludnie,s|polnoc,n to "Wejscie do Kurhanu"
```

Przejdz `poludnie` i zejdz pod ziemie:

```
@dig gore,u|na dol,d to "Korytarz Kurhanu"
```

(zauwaz, ze tu wyjscie *w dol* prowadzi do nowego pokoju, wiec para wyjsc to `gore,u|na dol,d` -- z korytarza wraca sie `gore`, nie `polnoc`; kierunki nie musza trzymac sie geografii na powierzchni, gdy budujesz cos podziemnego).

Przejdz `na dol` do Korytarza i wykop trzy odnogi plus komnate straznika w linii prostej:

```
@dig wschod,e|zachod,w to "Krypta Pierwsza"
```

Wroc (`zachod`):

```
@dig zachod,w|wschod,e to "Krypta Druga"
```

Wroc (`wschod`):

```
@dig poludnie,s|polnoc,n to "Sala z Pulapka"
```

Przejdz `poludnie` i kop dalej w glab:

```
@dig poludnie,s|polnoc,n to "Komnata Straznika"
```

Przejdz `poludnie` i wykop skarbiec pod komnata:

```
@dig na dol,d|gore,u to "Skarbiec"
```

Ostatni pokoj tego regionu -- **Tajne Przejscie** -- celowo nie kopiemy teraz. To ukryte polaczenie miedzy Krypta Druga a Regionem 5, ktore wymaga mechanizmu ukrywania wyjscia (obiekt wyjscia istnieje, ale nie jest widoczny w zwyklym `look`) -- to dokladnie material Rozdzialu 8. Zanotuj sobie tylko w notatniku, ze Krypta Druga bedzie potrzebowac takiego polaczenia, i wroc do tego w Rozdziale 8.

Region 4 gotowy -- 7 z 8 zaplanowanych lokacji (ostatnia doczeka Rozdzialu 8).

### Budujemy Region 5 (Wzgorza i Opuszczona Kopalnia)

Ten region z zalozenia laczy sie z reszta mapy przez Tajne Przejscie z Regionu 4 -- skoro jeszcze go nie ma, na razie zbudujemy Region 5 jako osobna, chwilowo niepolaczona grupe pokoi (`@dig` bez `to`), a po Rozdziale 8 dostanie polaczenie. To dobra okazja, by przypomniec: pokoj bez wyjsc wejsciowych to nie blad -- to normalny, przejsciowy stan podczas budowy.

```
@dig "Podnoze Wzgorz"
```

Zapisz numer, ktory zwroci serwer, i przejdz tam recznie: `@move me do <numer>`.

```
@dig polnoc,n|poludnie,s to "Szlak Gorski"
```

Przejdz `polnoc`:

```
@dig polnoc,n|poludnie,s to "Szczyt Wzgorza"
```

Wroc na Podnoze Wzgorz (`poludnie`, `poludnie` -- albo `@move`):

```
@dig poludnie,s|polnoc,n to "Wejscie do Opuszczonej Kopalni"
```

Przejdz `poludnie` i zejdz do kopalni:

```
@dig na dol,d|gore,u to "Kopalnia -- Poziom Pierwszy"
```

Przejdz `na dol` i wykop dwie ostatnie lokacje:

```
@dig wschod,e|zachod,w to "Grota Krysztalowa"
```

Wroc (`zachod`):

```
@dig na dol,d|gore,u to "Kopalnia -- Poziom Drugi (Obozowisko Zbojcow)"
```

Region 5 gotowy -- 7 lokacji, na razie odizolowanych od reszty mapy (celowo, patrz wyzej).

### Opisy

Kazdy z powyzszych pokoi ma teraz nazwe i polaczenia, ale wciaz domyslny (pusty) opis. Wzorzec z Rozdzialu 3 (`@describe here as "..."`) jest identyczny dla kazdego z nich -- zamiast przepisywac 36 kolejnych przykladow, potraktuj to jako cwiczenie: przejdz sie po calej mapie i opisz przynajmniej te lokacje, ktore beda mialy znaczenie w kolejnych rozdzialach (Gospoda, Kuznia, Swiatynia, Chata Pustelnika, Polana z Kregiem Grzybow, Komnata Straznika, Obozowisko Zbojcow -- wszystkie pojawiaja sie ponownie przy przedmiotach, NPC-ach lub efektach). Reszte mozesz dopisac w dowolnym momencie -- pusty opis nie przeszkadza w dalszej pracy nad mechanika.

### Co dalej

Mamy szkielet calego swiata -- 36 zbudowanych lokacji plus jedna (Tajne Przejscie) odlozona do Rozdzialu 8, i caly Region 5 czekajacy na spiecie z reszta mapy. W Rozdziale 5 zaczynamy wypelniac te lokacje trescia: przedmiotami, ktore gracz moze podniesc, uzyc i (czasem) zjesc.

## Rozdzial 5: przedmioty

### Cztery standardowe klasy

`help @create` wymienia cztery gotowe "standardowe klasy", od ktorych mozesz od razu dziedziczyc: `$note`, `$letter`, `$thing` i `$container`. Kazda przydaje sie do czegos innego:

- `$thing` -- najbardziej ogolna klasa. Mozna ja podniesc, upuscic, przeniesc. Baza pod wszystko, co nie pasuje do pozostalych trzech.
- `$note` -- przedmiot z tekstem do przeczytania (wlasciwosc `.text`, lista linii). Idealny na liscik, zapiski, karteczki.
- `$letter` -- podobny do `$note`, ale pomyslany pod system pocztowy (adresat, mozliwosc wyslania) -- na potrzeby tego poradnika bedziemy uzywac gownie `$note`.
- `$container` -- przedmiot, do ktorego mozna wlozyc inne przedmioty (`put X in Y`) i z ktorego mozna je wyjac (`take X from Y`). Ma tez wbudowana obsluge opcjonalnego zamka (wlasciwosc `.key`) -- wykorzystamy to w Rozdziale 8.

### Pierwszy przedmiot: zapiski w Chacie Pustelnika

Przejdz do Chaty Pustelnika (Rozdzial 4, Region 2) i stworz tam notatke:

```
@create $note named "wyplowiale zapiski,zapiski,notatka"
```

Serwer zwroci numer nowego obiektu (przykladowo `#1540` -- podstaw swoj). Opisz go z zewnatrz i ustaw tresc do przeczytania:

```
@describe #1540 as "Kawalek pergaminu, pokryty niewprawnym pismem."
@set #1540.text to {"Jesli czytasz te slowa, pustelnik chyba pozwolil ci tu zostac.", "Trzy Ksiezyce widza wiecej, niz kaplani chca przyznac -- pytaj o Kurhan.", "-- P."}
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
@describe here as "Ciezka, debowa skrzynia okuta zelazem, pociemniala od wilgoci."
drop stara okuta skrzynia
```

Do srodka mozesz od razu wlozyc pierwszy "skarb" -- na razie zwykly `$thing`:

```
@create $thing named "garsc starych srebrnych monet,monety,srebro"
@describe here as "Garsc poczernialych ze staroscia monet z profilem wladcy, ktorego nikt juz nie pamieta."
put monety in skrzynia
```

Gracz, ktory dotrze do Skarbca, moze `open skrzynia`, `look in skrzynia` i `take monety from skrzynia` -- znowu, cala ta mechanika jest juz wbudowana w `$container`, nie napisalismy do niej ani linijki kodu.

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
player:notify_others(player.name + " zjada " + this.name + ".");
this:recycle();
endif
.
```

Kilka nowosci w tym kodzie, wyjasnione: `this` to zawsze obiekt, na ktorym uruchomiono czasownik (tu: konkretny posilek); `player` to gracz, ktory wydal polecenie; `this.location != player` sprawdza, czy przedmiot faktycznie jest w rekach gracza (a nie np. wciaz lezy w pokoju); `this.smak_opis || "..."` to wzorzec "wartosc domyslna, jesli wlasciwosc jest pusta/nieustawiona", ktory bedziemy uzywac wielokrotnie w kolejnych rozdzialach; `this:recycle()` niszczy przedmiot po zjedzeniu -- zjedzony bochenek chleba nie powinien zostac w ekwipunku.

Zauwaz, ze `zjedz` odwoluje sie do wlasciwosci `smak_opis`, ktorej klasa `$edible` jeszcze nie ma -- dodajmy ja, z sensowna domyslna wartoscia pustego stringu:

```
@property #1550.smak_opis "" rc
```

(`rc` to uprawnienia wlasciwosci -- readable i "chown-owned", czyli standardowe, patrz `help @property`).

Teraz tworzymy konkretny przedmiot dziedziczacy po tej klasie -- bochenek chleba w Gospodzie:

```
@create #1550 named "bochenek razowego chleba,chleb,bochenek"
@describe here as "Jeszcze cieply, razowy bochenek, pachnacy kminkiem."
@set here.smak_opis to "Chrupiaca skorka i cieply, gesty miekisz -- najlepszy chleb w calej dolinie."
```

(uzylam `here`, wiec upewnij sie, ze stoisz przy nowo stworzonym obiekcie -- `@create` zostawia go w twoim ekwipunku, wiec `here` w tym kontekscie nie zadziala tak jak w Rozdziale 3; podaj numer wprost, jesli wolisz: `@describe #1551 as "..."`).

Upusc chleb w Gospodzie, i sprobuj `zjedz chleb` (albo `eat chleb`) -- powinienes zobaczyc opis smaku i znikniecie przedmiotu z ekwipunku.

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
@verb #1560:"zagadnij ask" any about any
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

Skladnia polecenia gracza wyglada teraz tak: `zagadnij kowala about kurhan` albo `ask kowal about kurhan` (mieszanie jezykow w jednym poleceniu dziala, bo nazwa czasownika, `about` i nazwa dopelnienia to niezalezne od siebie slowa dla parsera -- parser MOO nie wymaga spojnosci jezykowej calego polecenia). `about` to jeden z przyimkow wbudowanych w silnik -- pelna liste rozpoznawanych przyimkow pokazuje `help prepositions`; jesli chcesz sprawdzic albo rozszerzyc polskie aliasy komend w calej bazie, zajrzyj do [Tworzenia tresci po polsku](TWORZENIE-TRESCI-PO-POLSKU.md).

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
@describe here as "Postawny mezczyzna o rekach jak balki, w skorzanym fartuchu poznaczonym iskrami. Pilnuje pieca, jakby to bylo najcenniejsze, co ma."
@set here.gadanie to {"Uwazaj na iskry, jesli podejdziesz blizej.", "Dobra stal wymaga cierpliwosci, tak samo jak dobre zycie."}
@set here.odpowiedzi to ["kurhan" -> "Nie chodz tam po zmroku, chlopcze. Kaplani cos wiedza, ale nie mowia.", "_domyslna" -> "Kowal mruczy cos pod nosem i wraca do pracy."]
```

Uruchom mu gadanie w tle (wpisujac to jako on -- czyli wywolujac czasownik na obiekcie, ktorego wlasnie stworzyles i ktory wciaz jest w twoim ekwipunku, wiec mozesz uzyc jego nazwy):

```
kowal:start()
```

Poczekaj minute w Kuzni i sprobuj `zapytaj kowala about kurhan`.

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

Od teraz `$zegar_swiata` dziala wszedzie, tak samo jak `$room` czy `$thing`. Uruchamiamy zegar:

```
$zegar_swiata:start()
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
@set #1500.na_zewnatrz to 1
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

W Rozdziale 5 stworzylismy `stara okuta skrzynia` w Skarbcu, otwarta dla kazdego. Czas to naprawic. Najpierw potrzebujemy fizycznego klucza:

```
@create $thing named "zardzewialy zelazny klucz,klucz"
@describe here as "Ciezki, mocno zardzewialy klucz. Ktos musial go tu zgubic dawno temu."
```

Zostaw go w Komnacie Straznika (Rozdzial 4) -- gracz musi minac straznika, zeby go znalezc, co samo w sobie jest juz malym wyzwaniem (a w Rozdziale 6 straznik dostal juz ostrzegawcza kwestie na ten temat).

Teraz blokujemy skrzynie -- dla kontenerow uzywamy **`@lock_for_open`**, nie zwyklego `@lock` (ten drugi kontroluje co innego -- czy kontener w ogole mozna wziac/przeniesc; `help @lock_for_open`, jesli chcesz sprawdzic roznice):

```
@lock_for_open skrzynia with klucz
```

Sprobuj teraz `open skrzynia` bez klucza w ekwipunku -- serwer odmowi. Podnies `zardzewialy zelazny klucz` i sprobuj ponownie -- powinno zadzialac. Cofniecie blokady to `@unlock_for_open skrzynia`.

### Zlozone wyrazenie: zamykamy przejscie do Skarbca

Skarbiec (Rozdzial 4) laczy sie z Komnata Straznika wyjsciem "na dol". Zablokujmy samo to wyjscie zlozonym wyrazeniem -- przepuszczamy kogos, kto niesie klucz, **lub** samego straznika (np. gdyby mial tam wracac patrolowac):

```
@lock #<numer-wyjscia-na-dol> with klucz || straznik
```

Numer wyjscia znajdziesz poleceniem `@exits`, stojac w Komnacie Straznika -- wypisze ono wszystkie konwencjonalne wyjscia z biezacego pokoju wraz z ich numerami obiektow (`help @exits`).

### Ukryte przejscie miedzy Regionem 4 a Regionem 5

W Rozdziale 4 odlozylismy Tajne Przejscie -- polaczenie miedzy Krypta Druga a Podnozem Wzgorz. Teraz mamy juz oba pokoje wykopane, wiec mozemy uzyc **trzeciej formy** `@dig` -- laczacej dwa juz istniejace pokoje numerem obiektu (`help @dig`, forma z `to <numer>`):

Stojac w Krypcie Drugiej:

```
@dig zachod,w to <numer Podnoza Wzgorz>
```

To tworzy wyjscie z Krypty Drugiej do Podnoza Wzgorz (jednokierunkowe -- jesli chcesz przejscia w obie strony, powtorz operacje w drugim kierunku stojac w Podnozu Wzgorz, laczac `to <numer Krypty Drugiej>`).

Wyjscie juz dziala, ale wciaz jest widoczne na liscie `look`/`@exits` jak kazde inne -- nic "tajnego". Zeby je ukryc, korzystamy z wlasciwosci `.obvious`, ktora sprawdza wbudowany mechanizm listowania wyjsc w `$room` (dokladnie ten sam kod, ktory nadpisalismy w Rozdziale 7 przy okazji `.na_zewnatrz` -- tym razem nie musimy nic nadpisywac, `.obvious` jest juz obslugiwane przez baze):

```
@exits
@property #<numer-nowego-wyjscia>.obvious 0 rc
```

(pierwsza komenda to zwykle `@exits`, zeby odczytac numer nowo utworzonego wyjscia). Od teraz wyjscie nie pojawia sie na liscie wyjsc pokoju, ale gracz, ktory wpisze `zachod` stojac w Krypcie Drugiej, wciaz zostanie przeniesiony -- dokladnie tak, jak powinno dzialac tajne przejscie.

Zeby gracz mial jakakolwiek szanse je znalezc, dajmy podpowiedz przez prosty czasownik wyszukiwania w tym samym pokoju:

```
@verb #<Krypta Druga>:"szukaj search" this none this
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
@set #<krag1>.cel to <numer Drugiej Strony Kregu>
drop krag muchomorow
```

Przejdz do "Drugiej Strony Kregu" i powtorz w druga strone:

```
@create #<klasa> named "krag muchomorow,krag"
@set #<krag2>.cel to <numer Polany z Kregiem Grzybow>
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
@set me.miedziaki to 20
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
@verb #<klasa>:"cennik pricelist" this none this
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
@verb #<klasa>:"kup buy" any from this
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

Skladnia komendy: `kup mikstura from sklepikarz` -- `from` to standardowy, wbudowany przyimek (`help prepositions`), wiec dziala od razu, nawet zanim dopiszesz do niego polski alias.

I czasownik odwrotny, sprzedawanie -- gracz oddaje przedmiot, ktory faktycznie niesie, sklepikarz placi za niego stala kwote (chyba ze przedmiot ma wlasna wlasciwosc `.wartosc_sprzedazy`):

```
@verb #<klasa>:"sprzedaj sell" any to this
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
dobj:recycle();
.
```

### Konkretny sklepikarz: Zielarka Jagna

Wracamy do Chatki Zielarki z Rozdzialu 1/4, gdzie od poczatku byla zapowiedziana jako zrodlo handlu:

```
@create #<klasa> named "Zielarka Jagna,jagna,zielarka"
@describe here as "Starsza kobieta o zrecznych palcach, cala obwieszona pekami suszonych ziol."
@set here.towar to [["nazwa" -> "flaszeczka mikstury", "aliasy" -> {"flaszeczka", "mikstura"}, "cena" -> 3, "opis" -> "Metny, zielonkawy plyn o ostrym zapachu."], ["nazwa" -> "peczek suszonych ziol", "aliasy" -> {"peczek", "ziola"}, "cena" -> 1, "opis" -> "Kilka gatunkow ziol, zwiazanych razem sznurkiem."]]
```

Uruchom jej gadanie w tle, tak jak przy Kowalu w Rozdziale 6 (Jagna dziedziczy `:start`/`:stop`/`:heartbeat` po `$npc`, mimo ze jest jednoczesnie sklepikarzem):

```
jagna:start()
```

Sprobuj `cennik from jagna`, potem `kup mikstura from jagna` (majac przynajmniej 3 miedziaki), a na koniec `sprzedaj flaszeczka mikstury to jagna`, zeby zobaczyc pelny cykl handlu w obie strony.

### Co dalej

Mamy przedmioty, NPC-e, atmosfere, zamki i teraz ekonomie -- brakuje juz tylko jednego: powodu, dla ktorego gracz mialby to wszystko odwiedzic w konkretnej kolejnosci. W Rozdziale 10 spinamy kilka z tych mechanik w prosty, sledzony quest.
