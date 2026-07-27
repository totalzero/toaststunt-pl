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
