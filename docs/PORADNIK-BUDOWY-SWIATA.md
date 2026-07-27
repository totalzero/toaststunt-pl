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
