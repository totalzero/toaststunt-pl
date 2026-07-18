# Podrecznik Programisty ToastStunt, wersja 1.2.4

## Napisany dla ToastStunt w wersji 2.8+

*Polskie tlumaczenie oryginalu ("ToastStunt Programmer's Manual"), dostepnego pod adresem [https://github.com/lisdude/toaststunt-documentation/blob/master/manual/toaststunt-programmers-manual.md](https://github.com/lisdude/toaststunt-documentation/blob/master/manual/toaststunt-programmers-manual.md) (pobrane 2026-07-18). Autor oryginalu: Pavel Curtis i inni. Nazwy funkcji wbudowanych, zmiennych, typow, flag oraz przyklady kodu MOO pozostaja w oryginalnej, angielskiej formie -- sa to realne identyfikatory jezyka, tlumaczeniu podlega wylacznie tekst wyjasniajacy. Tlumaczenie jest tworzone etapami; pelny spis tresci z dzialajacymi odnosnikami zostanie dodany po ukonczeniu calosci (patrz plan etapow w pamieci projektu). Tresc bedzie takze zweryfikowana wzgledem faktycznego kodu silnika i bazy `toastcore.db` tego forka w koncowym etapie audytu.*

autorstwa Pavel Curtis i innych

Copyright (C) 1991, 1992, 1993, 1995, 1996 Pavel Curtis.

Copyright (C) 1996, 1997 Ken Fox

Copyright (C) 1997 Andy Bakun

Copyright (C) 1997 Erik Ostrom.

Copyright (C) 2004 Roger F. Crew.

Copyright (C) 2011, 2012, 2013, 2014 Todd Sundsted

Copyright (C) 2017-2026 [Brendan Butts](http://github.com/sevenecks).

Copyright (C) 2021-2025 [lisdude](http://github.com/lisdude)

Fragmenty zaadaptowane z [Podrecznika Programisty Stunt](https://lisdude.com/moo/ProgrammersManual.html) autorstwa Todda Sundsteda, Copyright (C) 2011, 2012, 2013, 2014 Todd Sundsted.

Fragmenty zaadaptowane z [dokumentacji WAIF](http://ben.com/MOO/waif.html) oraz [Podrecznika Programisty WAIF](http://ben.com/MOO/waif-progman.html) autorstwa Bena Jacksona.

([DZIENNIK ZMIAN](https://github.com/lisdude/toaststunt-documentation/blob/master/CHANGELOG.md)) -- w jezyku angielskim, nietlumaczony (konwencja tego projektu wobec wszystkich changelogow).

([WSPOLTWORCY](https://github.com/lisdude/toaststunt-documentation/blob/master/CONTRIBUTORS.md))

Zezwala sie na sporzadzanie i rozpowszechnianie doslownych kopii tego podrecznika, pod warunkiem zachowania na wszystkich kopiach informacji o prawach autorskich oraz niniejszej informacji o zezwoleniu.

Zezwala sie na kopiowanie i rozpowszechnianie zmodyfikowanych wersji tego podrecznika na warunkach kopiowania doslownego, pod warunkiem, ze cala powstala w ten sposob praca pochodna zostanie rozpowszechniona na warunkach informacji o zezwoleniu identycznej z niniejsza.

Zezwala sie na kopiowanie i rozpowszechnianie tlumaczen tego podrecznika na inny jezyk, na powyzszych warunkach dotyczacych wersji zmodyfikowanych, z tym wyjatkiem, ze niniejsza informacja o zezwoleniu moze zostac podana w tlumaczeniu zatwierdzonym przez autora. *(Niniejsze tlumaczenie na jezyk polski powstaje w ramach forka [totalzero/toaststunt-pl](https://github.com/totalzero/toaststunt-pl).)*

Starsze wersje tego dokumentu (lub wersje sprzed forka, dla LambdaMOO) mozna znalezc w sekcji zasobow.

## Przedmowa

08/01/2022

Czesc, jestem Brendan, znany tez jako Slither. Programuje w MOO na [Sindome](https://www.sindome.org/) od 2003 roku. Spedzilem wiele godzin przez lata, wertujac oryginalny podrecznik programisty LambdaMOO napisany przez Pavela Curtisa. W 2016 roku zabralem sie za aktualizacje oryginalnego podrecznika o niektore z moich wlasnych doswiadczen i dopiero w 2019 roku skonczylem te prace. Mniej wiecej w tym samym czasie uslyszalem o ToastStunt od [lisdude](https://github.com/lisdude). Chcialem sie zaangazowac, ale niestety moje umiejetnosci w C/C++ sa fatalne. Zdecydowalem wiec, ze moim wkladem bedzie aktualizacja podrecznika programisty o wszystkie zmiany dodane przez Toast, a takze o dalsze doswiadczenia i uwagi od lisdude, DistantOrigin i innych czlonkow serwera Discord ToastStunt.

Ten przewodnik to nie tylko dokument techniczny -- zawiera takze opinie (moje i innych) na temat tego, czego warto (waify), a czego nie warto (obiekty anonimowe, dziedziczenie wielokrotne) uzywac. Ostatecznie jednak decyzja nalezy do Ciebie. LambdaMOO, a teraz jego nastepca ToastStunt, sa swietne do tworzenia gier, projektow hobbystycznych oraz do majsterkowania i nauki programowania. Mam nadzieje, ze dobrze sie bawisz!

### Czym jest ToastStunt?

ToastStunt to fork [Stunt](https://github.com/toddsundsted/stunt), ktory z kolei jest forkiem [LambdaMOO](https://en.wikipedia.org/wiki/MOO). Jesli szukasz aktualnego, bogatego w funkcje LambdaMOO, ToastStunt jest dla Ciebie. Wlacza w siebie wiele latek wydanych dla klasycznego LambdaMOO i wiele wiecej, w tym TLS, lepsze FileIO, zaktualizowane i rozszerzone funkcje wbudowane, dziedziczenie wielokrotne, obsluge curl oraz watkowanie (threading).

## Zasoby ToastStunt i MOO

* [GitHub z zasobami programistycznymi LambdaMOO i ToastStunt](https://github.com/SevenEcks/lambda-moo-programming)
* [Przewodnik dla poczatkujacych po kompilacji ToastStunt](https://lisdude.com/moo/toaststunt_newbie.txt) -- patrz nasze [PRZEWODNIK-DLA-POCZATKUJACYCH.md](PRZEWODNIK-DLA-POCZATKUJACYCH.md), polskie tlumaczenie tego dokumentu
* [Zasoby MOO lisdude](http://www.lisdude.com/moo/)
* [Nieedytowany oryginalny Podrecznik Programisty MOO](http://www.hayseed.net/MOO/manuals/ProgrammersManual.html)
* [Starszy, nieedytowany Podrecznik Programisty MOO](http://www2.iath.virginia.edu/courses/moo/ProgrammersManual.texinfo_toc.html)
* [Zrodla ToastStunt (GitHub)](https://github.com/lisdude/toaststunt)
* [Repozytorium bazy danych ToastCore](https://github.com/lisdude/toastcore) [Plik bazy danych ToastCore](https://raw.githubusercontent.com/lisdude/toastcore/master/toastcore.db) -- patrz takze nasze [polskie tlumaczenie README ToastCore](README.ToastCore.md)
* [Lista mailingowa MOO Talk](https://groups.google.com/forum/#!forum/MOO-talk)
* [Klient MOO Dome (WebSocket)](https://github.com/JavaChilly/dome-client.js)
* [MOO FAQ](http://www.moo.mud.org/moo-faq/)
* [Arch Wizard FAQ](https://lisdude.com/moo/new-archwiz-faq.html)
* [Budowa pliku bazy danych LambdaMOO](https://lisdude.com/moo/lmdb.html)
* [Podstawy dla Czarodziei (Wizard Basics)](https://lisdude.com/moo/wizbasics.html)
* [Whitepaper o garbage collection](https://researcher.watson.ibm.com/researcher/files/us-bacon/Bacon01Concurrent.pdf) (dokument, do ktorego odwolywano sie przy tworzeniu garbage collectora, z ktorego opcjonalnie moze korzystac Toast)
* [Budowa bazy danych ToastStunt](https://lisdude.com/moo/toaststunt_anatomy/)

> Uwaga tlumacza: pozycje oznaczone powyzej jako polskie tlumaczenia zostaly lub zostana pobrane, przetlumaczone i zapisane jako osobne pliki w tym repozytorium w ramach tego samego przedsiewziecia tlumaczeniowego -- pozostale linki prowadza na razie do oryginalnych, angielskich zrodel zewnetrznych.

## Wstep

ToastStunt to dostepny przez siec, wieloosobowy, programowalny, interaktywny system, dobrze nadajacy sie do budowy gier tekstowych, systemow konferencyjnych i innego oprogramowania do wspolpracy. Najczesciej jednak uzywany jest jako wieloosobowa, niskoprzepustowa rzeczywistosc wirtualna i to z tym zastosowaniem na mysli opisujemy go tutaj.

Uczestnicy (zwykle nazywani _graczami_) laczy sie z ToastStunt uzywajac telnetu, SSH lub specjalizowanego [klienta MUD](https://en.wikipedia.org/wiki/MUD_client). Po polaczeniu zazwyczaj widza _wiadomosc powitalna_ wyjasniajaca, jak stworzyc nowa _postac_ lub polaczyc sie z juz istniejaca. Postacie sa wcieleniem graczy w rzeczywistosci wirtualnej, jaka jest ToastStunt.

> Uwaga: Nikt tak naprawde nie laczy sie dzis z MOO przy uzyciu samego klienta telnet. Klienty MUD sa niezwykle powszechne i moga laczyc sie zarowno przez port telnet, jak i SSH. Zobacz sekcje zasobow po wiecej informacji na ich temat. Istnieja nawet pewne klienty webowe ([dome-client](https://github.com/JavaChilly/dome-client.js)) korzystajace z WebSocketow, ktore lacza sie z MOO bezposrednio z przegladarki. ToastStunt mozna tez skonfigurowac tak, by oferowal bezpieczne polaczenia przez TLS.

Po polaczeniu sie z postacia gracze wydaja jednoliniowe polecenia, ktore sa parsowane i interpretowane przez ToastStunt w odpowiedni sposob. Takie polecenia moga powodowac zmiany w rzeczywistosci wirtualnej, np. w polozeniu postaci, lub po prostu raportowac aktualny stan tej rzeczywistosci, np. wyglad jakiegos obiektu.

Zadanie interpretowania tych polecen jest dzielone miedzy dwa glowne komponenty systemu ToastStunt: _serwer_ i _baze danych_. Serwer to program napisany w standardowym jezyku programowania, ktory zarzadza polaczeniami sieciowymi, utrzymuje kolejki polecen i innych zadan do wykonania, kontroluje caly dostep do bazy danych oraz wykonuje inne programy napisane w jezyku MOO. Baza danych zawiera reprezentacje wszystkich obiektow w rzeczywistosci wirtualnej, w tym programy MOO, ktore wykonuje serwer, by nadac tym obiektom ich specyficzne zachowania.

Niemal kazde polecenie jest parsowane przez serwer do postaci wywolania procedury MOO, czyli _czasownika (verb)_, ktory faktycznie wykonuje prace. Programowanie w jezyku MOO jest wiec centralnym elementem tworzenia nietrywialnych rozszerzen bazy danych, a tym samym rzeczywistosci wirtualnej.

W nastepnym rozdziale opisuje strukture i zawartosc bazy danych ToastStunt. Kolejny rozdzial daje pelny opis tego, jak serwer wykonuje swoje podstawowe zadanie: parsowanie polecen wpisywanych przez graczy. Nastepnie opisuje pelna skladnie i semantyke jezyka programowania MOO. Na koniec opisuje wszystkie konwencje bazodanowe zakladane przez serwer.

> Uwaga: W wiekszosci ten podrecznik opisuje wylacznie te aspekty ToastStunt, ktore sa calkowicie niezalezne od zawartosci bazy danych. Nie opisuje na przyklad polecen ani interfejsow programistycznych obecnych w bazie danych ToastCore. Sa od tego wyjatki, w sytuacjach, gdzie wydaje sie rozsadne zaglebic sie w te obszary.

## Baza danych ToastStunt

W tym rozdziale opisujemy szczegolowo rozne rodzaje danych, ktore moga wystapic w bazie danych ToastStunt i ktorymi moga manipulowac programy MOO. W kilku miejscach odwolujemy sie do bazy danych [ToastCore](https://github.com/lisdude/toastcore). Jest to jedna konkretna baza danych ToastStunt, aktywnie rozwijana przez spolecznosc ToastStunt.

### Typy wartosci MOO

Istnieje tylko kilka rodzajow wartosci, ktorymi moga manipulowac programy MOO:

* liczby calkowite (w okreslonym, duzym zakresie)
* liczby rzeczywiste (reprezentowane liczbami zmiennoprzecinkowymi)
* stringi (ciagi znakow)
* numery obiektow (obiektow trwalych w bazie danych)
* referencje do obiektow (do obiektow anonimowych w bazie danych)
* wartosci logiczne (bool)
* WAIFy
* bledy (powstajace podczas wykonywania programu)
* listy (wszystkich powyzszych, w tym takze list)
* mapy (wszystkich powyzszych, w tym list i map)

#### Typ calkowity (Integer)

ToastStunt obsluguje liczby calkowite 64-bitowe, ale mozna go tez skonfigurowac do obslugi 32-bitowych. W programach MOO liczby calkowite zapisuje sie dokladnie tak, jak je tu widzisz: opcjonalny znak minus, po ktorym nastepuje niepusty ciag cyfr dziesietnych. W szczegolnosci nie wolno wstawiac przecinkow, kropek ani spacji w srodku duzych liczb calkowitych, tak jak czasem robimy to w jezyku polskim czy angielskim (np. 2 147 483 647).

> Uwaga: wartosci $maxint i $minint definiuja w bazie danych maksymalna obslugiwana liczbe calkowita. W ToastCore sa one ustawiane automatycznie. Jesli migrujesz z LambdaMOO, warto mimo to sprawdzic, czy te liczby sa ustawione poprawnie.

#### Typ rzeczywisty (Real Number)

Liczby rzeczywiste w MOO sa reprezentowane tak, jak w niemal wszystkich innych jezykach programowania, przy uzyciu tzw. liczb _zmiennoprzecinkowych_. Maja one pewne (duze) ograniczenia rozmiaru i precyzji, dzieki czemu sa przydatne w szerokim zakresie zastosowan. Liczby zmiennoprzecinkowe zapisuje sie z opcjonalnym znakiem minus, po ktorym nastepuje niepusty ciag cyfr, w pewnym miejscu przedzielony kropka dziesietna '.' i/lub zakonczony oznaczeniem notacji naukowej (litera 'E' lub 'e', po ktorej nastepuje opcjonalny znak i jedna lub wiecej cyfr). Oto kilka przykladow liczb zmiennoprzecinkowych:

```
325.0   325.  3.25e2   0.325E3   325.E1   .0325e+4   32500e-2
```

Wszystkie te przyklady oznaczaja te sama liczbe. Trzeci z nich, jako przyklad notacji naukowej, nalezy odczytac jako "3,25 razy 10 do potegi 2".

Subtelny szczegol: MOO reprezentuje liczby zmiennoprzecinkowe uzywajac lokalnego znaczenia typu `double` z jezyka C, ktory niemal zawsze odpowiada podwojnej precyzji IEEE 754. Jesli tak, to najmniejsza dodatnia liczba zmiennoprzecinkowa nie jest wieksza niz `2.2250738585072014e-308`, a najwieksza liczba zmiennoprzecinkowa to `1.7976931348623157e+308`.

* Nieskonczonosci IEEE i wartosci NaN nie sa dozwolone w MOO.
* Blad `E_FLOAT` jest zglaszany, gdy w innym wypadku obliczona zostalaby nieskonczonosc.
* Blad `E_INVARG` jest zglaszany, gdy w innym wypadku powstalaby wartosc NaN.
* Przy niedomiarze (underflow) zawsze zwracana jest wartosc `0.0`.

#### Typ tekstowy (String)

_Stringi_ znakowe to dowolnie dlugie ciagi normalnych, drukowalnych znakow ASCII. Zapisywane jako wartosci w programie, stringi sa ujete w cudzyslowy, tak jak tutaj:

```
"To jest ciag znakow."
```

Aby zawrzec cudzyslow wewnatrz stringa, poprzedz go ukosnikiem wstecznym (`\`), tak jak tutaj:

```
"Nazywal sie \"Leroy\", ale nikt tak go nie nazywal."
```

Wreszcie, aby zawrzec ukosnik wsteczny w stringu, podwoj go:

```
"Niektorzy uzywaja ukosnika wstecznego ('\\') do oznaczenia roznicy zbiorow."
```

Stringi MOO nie moga zawierac specjalnych znakow ASCII, takich jak powrot karetki, wysuw linii, dzwonek itd. Jedynymi dozwolonymi znakami niedrukowalnymi sa spacje i tabulatory.

Subtelny szczegol: istnieje specjalny rodzaj stringa uzywany do reprezentowania dowolnych bajtow, stosowany ogolnie przy wejsciu i wyjsciu binarnym. W _stringu binarnym_ kazdy bajt, ktory nie jest drukowalnym znakiem ASCII ani spacja, jest reprezentowany jako trzyznakowy podciag "~XX", gdzie XX to szesnastkowa reprezentacja bajtu; znak wejsciowy '~' jest reprezentowany przez trzyznakowy podciag "~7E". Ta specjalna reprezentacja jest uzywana przez funkcje `encode_binary()` i `decode_binary()` oraz przez funkcje `notify()` i `read()` przy polaczeniach sieciowych bedacych w trybie binarnym. Zobacz opisy funkcji `set_connection_option()`, `encode_binary()` i `decode_binary()` po wiecej szczegolow.

Stringi MOO moga byc 'indeksowane' przy uzyciu nawiasow kwadratowych i indeksu calkowitego (w bardzo podobny sposob jak listy):

```
"to jest string"[4] -> "t"
```

Istnieje skladnia cukrowa (syntactic sugar), ktora pozwala napisac:
```
"Sli" in "Slither"
```
jako skrot dla wbudowanej funkcji index().

#### Typ obiektowy (Object)

_Obiekty_ sa szkieletem bazy danych MOO i jako takie zasluguja na obszerne omowienie; caly nastepny rozdzial jest im poswiecony. Na razie wystarczy powiedziec, ze kazdy obiekt ma numer, unikalny dla tego obiektu.

W programach zapisujemy referencje do konkretnego obiektu, stawiajac znak hash (`#`), po ktorym nastepuje numer, tak jak tutaj:

```
#495
```

> Uwaga: odwolywanie sie do numerow obiektow bezposrednio w kodzie jest odradzane. Obiekt istnieje tylko dopoki nie zostanie poddany recyklingowi (recycled). Technicznie mozliwe jest, ze numer obiektu ulegnie zmianie w pewnych okolicznosciach. Dlatego zamiast tego nalezy uzywac skorifikowanej referencji do obiektu ($my_special_object). Wiecej o referencjach skorifikowanych pozniej.

Numery obiektow sa zawsze liczbami calkowitymi.

Istnieja trzy specjalne numery obiektow uzywane do rozmaitych celow: `#-1`, `#-2` i `#-3`, w bazie ToastCore zwykle nazywane odpowiednio `$nothing`, `$ambiguous_match` i `$failed_match`.

#### Typ obiektu anonimowego (Anonymous Object)

Obiekty anonimowe sa referencjami i nie maja numeru obiektu. Sa tworzone przez przekazanie opcjonalnego trzeciego argumentu do `create()`. Obiekty anonimowe sa automatycznie poddawane garbage collection, gdy nie ma juz do nich zadnych referencji (w kodzie ani we wlasciwosciach).

Wiecej szczegolow na temat obiektow anonimowych znajdziesz w rozdziale [Praca z obiektami anonimowymi](#working-with-anonymous-objects).

#### Typ logiczny (Bool)

_Bool_ jest albo prawda (true), albo falszem (false). Np.: `my_bool = true; my_second_bool = false;`. W MOO `true` jest rowne `1`, a `false` jest rowne `0`. Na przyklad:

```
false == 0 daje prawde (true)
true  == 1 daje prawde (true)
false == 1 daje falsz (false)
true  == 0 daje falsz (false)
true  == 5 daje falsz (false)
false == -43 daje falsz (false)
```

#### Typ WAIF

_WAIFy_ to lekkie obiekty. WAIF to wartosc, ktora mozna przechowywac we wlasciwosci, zmiennej, wewnatrz LISTY lub innego WAIF-a. WAIF jest mniejszy rozmiarem (mierzonym w bajtach) niz zwykly obiekt i szybszy w tworzeniu oraz niszczeniu. Jest tez zliczany przez referencje (reference counted), co oznacza, ze jest niszczony automatycznie, gdy nie jest juz uzywany. Pusty WAIF zajmuje 72 bajty, pusta lista 64 bajty. WAIF zawsze bedzie o 8 bajtow wiekszy niz LISTA (na 64 bitach, 4 bajty na 32 bitach) zawierajaca te same wartosci.

> Uwaga: WAIFy nie sa naprawde obiektami i nie funkcjonuja tak naprawde jak obiekt. Nie da sie manipulowac WAIF-em bez zasadniczego odtworzenia normalnego obiektu (a wtedy jaki jest sens?). Moze lepiej myslec o WAIF-ie jako o kolejnym typie danych. Jest blizej listy niz obiektu. Ale to w koncu kwestia semantyki.

WAIFy sa mniejsze niz typowe obiekty i szybsze w tworzeniu. WAIF ma dwie wbudowane wlasciwosci typu OBJ: .class i .owner. WAIF bedzie zawsze co najwyzej o 4 bajty wiekszy niz LISTA z tymi samymi wartosciami.

OBJ-y rosna o value_bytes(value) - value_bytes(0) dla kazdej ustawionej wlasciwosci (czyli kazdej wlasciwosci, ktora przestaje byc "czysta" (clear) i przyjmuje wlasna wartosc, odrebna od rodzica). Zarowno LISTY, jak i WAIFy rosna o value_bytes(value) dla kazdego nowego elementu listy (w LISCIE) lub kazdej ustawionej wlasciwosci (w WAIF-ie). Tak wiec WAIF nigdy nie jest wiekszy niz o 4 bajty od LISTY przechowujacej te same wartosci, z tym ze WAIFy nadaja kazdej wartosci nazwe (nazwe wlasciwosci), a LISTY nadaja im tylko numery.

Zasadniczo mozesz traktowac WAIF jako cos, czego mozesz stworzyc tysiace w jednym czasowniku bez zastanowienia. Mozesz zrobic liste mailingowa z 1000 wiadomosciami, kazda jako WAIF (zamiast LISTY), ale najprawdopodobniej nie uzylbys 1000 obiektow.

OBJ-y tworzysz i niszczysz jawnie za pomoca wbudowanych funkcji create() i recycle() (albo przydzielasz je z puli, uzywajac czasownikow z rdzenia bazy). Pozostaja one, niezaleznie od tego co zrobisz, dopoki ich nie zniszczysz.

Wszystkie pozostale typy uzywane w MOO (wymagajace przydzielonej pamieci) sa zliczane przez referencje. Niezaleznie od tego, jak je stworzysz, pozostaja tak dlugo, jak dlugo trzymasz je we wlasciwosci lub zmiennej gdzies w kodzie, a gdy nie sa juz uzywane, po cichu znikaja i nie mozna ich odzyskac.

Wiecej szczegolow na temat WAIF-ow znajdziesz w rozdziale [Praca z WAIF-ami](#working-with-waifs).

#### Typ bledu (Error)

_Bledy_ sa zdecydowanie najrzadziej uzywanymi wartosciami w MOO. W normalnym przypadku, gdy program probuje wykonac operacje bledna z jakiegos powodu (na przyklad probuje dodac liczbe do ciagu znakow), serwer zatrzymuje wykonywanie programu i wypisuje komunikat o bledzie. Mozliwe jest jednak, by program zastrzegl, ze takie bledy nie powinny zatrzymywac wykonania; zamiast tego serwer powinien po prostu ustawic wartosc operacji na wartosc bledu. Program moze wtedy sprawdzic taki wynik i podjac odpowiednie dzialanie naprawcze. W programach wartosci bledow zapisuje sie jako slowa zaczynajace sie od `E_`. Pelna lista wartosci bledow, wraz z ich komunikatami, jest nastepujaca:

| Blad      | Opis                                    |
| --------- | ---------------------------------------- |
| E_NONE    | Brak bledu                               |
| E_TYPE    | Niezgodnosc typow                        |
| E_DIV     | Dzielenie przez zero                     |
| E_PERM    | Brak uprawnien                           |
| E_PROPNF  | Nie znaleziono wlasciwosci               |
| E_VERBNF  | Nie znaleziono czasownika                |
| E_VARNF   | Nie znaleziono zmiennej                  |
| E_INVIND  | Nieprawidlowa indyrekcja                 |
| E_RECMOVE | Rekurencyjne przeniesienie               |
| E_MAXREC  | Zbyt wiele wywolan czasownikow           |
| E_RANGE   | Blad zakresu                             |
| E_ARGS    | Nieprawidlowa liczba argumentow          |
| E_NACC    | Przeniesienie odrzucone przez cel        |
| E_INVARG  | Nieprawidlowy argument                   |
| E_QUOTA   | Przekroczony limit zasobow               |
| E_FLOAT   | Blad arytmetyki zmiennoprzecinkowej      |
| E_FILE    | Blad systemu plikow                      |
| E_EXEC    | Blad wykonania (exec)                    |
| E_INTRPT  | Przerwano                                |

#### Typ listy (List)

Kolejna wazna wartoscia w programach MOO sa _listy_. Lista to sekwencja dowolnych wartosci MOO, mogaca zawierac takze inne listy. W programach listy zapisuje sie w notacji zbliozonej do matematycznej notacji zbiorow, z kazdym elementem wypisanym po kolei, oddzielonym przecinkami, w calosci ujetym w nawiasy klamrowe (`{` i `}`). Na przyklad lista nazw dni tygodnia jest zapisana tak:

```
{"niedziela", "poniedzialek", "wtorek", "sroda",
 "czwartek", "piatek", "sobota"}
```

> Uwaga: nie ma znaczenia, ze wstawilismy zlamanie linii w srodku listy. Jest to prawda ogolnie w MOO: wszedzie, gdzie moze wystapic spacja, moze wystapic zlamanie linii, z tym samym znaczeniem. Jedynym wyjatkiem sa ciagi znakow, gdzie zlamania linii nie sa dozwolone.

#### Typ mapy (Map)

Ostatnim typem w MOO jest _mapa_. W innych jezykach programowania bywa nazywana hashmapa, tablica asocjacyjna lub slownik. Mapa jest zapisywana jako zbior par klucz -> wartosc, na przyklad: `["klucz" -> "wartosc", 0 -> {}, #15840 -> []]`. Klucze musza byc unikalne.

Kluczem mapy moze byc:

* string
* liczba calkowita
* obiekt
* blad
* liczba zmiennoprzecinkowa
* obiekt anonimowy (niezalecane)
* waif
* bool

Wartoscia mapy moze byc dowolny prawidlowy typ MOO, w tym inna mapa.

> Uwaga: znalezienie wartosci na liscie ma zlozonosc BigO(n), poniewaz uzywane jest przeszukiwanie liniowe. Mapy sa znacznie wydajniejsze i maja zlozonosc BigO(1) dla pobrania konkretnej wartosci po kluczu.

### Obiekty w bazie danych MOO

W ToastStunt istnieja obiekty anonimowe i obiekty trwale. W tym przewodniku, gdy mowimy o `obiektach`, mamy zazwyczaj na mysli `obiekty trwale`, a nie `obiekty anonimowe`. Gdy bedziemy omawiac obiekty anonimowe, wskazemy to wprost.

Obiekty hermetyzuja stan i zachowanie -- podobnie jak w innych jezykach programowania obiektowego. Obiekty trwale sluza tez do reprezentowania obiektow w rzeczywistosci wirtualnej, takich jak ludzie, pokoje, wyjscia i inne konkretne rzeczy. Z tego powodu MOO przywiazuje wieksza wage do tworzenia obiektow niz do innych rodzajow wartosci, takich jak liczby calkowite.

Liczby zawsze istnieja, w pewnym sensie; wystarczy je zapisac, by na nich operowac. Z obiektami trwalymi jest inaczej. Obiekt trwaly o numerze `#958` nie istnieje tylko dlatego, ze zapiszesz jego numer. Wymagana jest jawna operacja, funkcja `create()` opisana pozniej, by powolac obiekt trwaly do istnienia. Raz stworzone, obiekty trwale istnieja dopoki nie zostana jawnie zniszczone przez funkcje `recycle()` (rowniez opisana pozniej).

Obiekty anonimowe, ktore takze sa tworzone za pomoca `create()`, beda istniec dopoki nie zostanie wywolana funkcja `recycle()` lub dopoki nie bedzie do nich juz zadnych referencji.

Numer identyfikacyjny przypisany do obiektu trwalego jest unikalny dla tego obiektu. Zostal przydzielony w momencie tworzenia obiektu i nigdy nie zostanie ponownie uzyty, chyba ze wywolane zostanie `recreate()` lub `reset_max_object()`. Tak wiec, jesli stworzymy obiekt i zostanie mu przydzielony numer `#1076`, nastepny stworzony obiekt (uzywajac `create()`) otrzyma numer `#1077`, nawet jesli `#1076` zostanie w miedzyczasie zniszczony.

> Uwaga: powyzsze ograniczenie doprowadzilo do zaprojektowania systemow zarzadzania ponownym wykorzystaniem numerow obiektow. Jednym z przykladow takiego systemu jest `$recycler`. **Nie** jest on obecny w `minimal.db` dolaczonej do zrodel ToastStunt, natomiast jest obecny w najnowszym zrzucie [bazy danych ToastCore](https://github.com/lisdude/toastcore), ktora jest zalecanym punktem wyjscia dla nowych projektow.

Obiekty anonimowe i trwale skladaja sie z trzech rodzajow elementow, ktore razem definiuja ich zachowanie: _atrybutow_, _wlasciwosci_ (properties) i _czasownikow_ (verbs).

#### Podstawowe atrybuty obiektu

Kazdy obiekt ma trzy podstawowe _atrybuty_:

1. Flage reprezentujaca wbudowane wlasciwosci przypisane obiektowi.
2. Liste obiektow bedacych jego rodzicami.
3. Liste obiektow bedacych jego _dziecmi_, czyli tych obiektow, dla ktorych ten obiekt jest ich rodzicem.

Akt tworzenia postaci ustawia atrybut player na obiekcie i tylko czarodziej (uzywajac funkcji `set_player_flag()`) moze zmienic to ustawienie. Tylko postacie maja ustawiony bit player na 1. Tylko obiekty trwale moga byc graczami.

Hierarchia rodzic/dziecko sluzy do klasyfikowania obiektow w ogolne klasy, a nastepnie dzielenia zachowania miedzy wszystkimi czlonkami danej klasy. Na przyklad baza danych ToastCore zawiera obiekt reprezentujacy rodzaj "generycznego" pokoju. Wszystkie inne pokoje sa _potomkami_ (tj. dziecmi lub dziecmi dzieci, i tak dalej) tego jednego. Generyczny pokoj definiuje te elementy zachowania, ktore sa wspolne dla wszystkich pokoi; inne pokoje specjalizuja to zachowanie do wlasnych celow. Pojecie klas i specjalizacji jest sama istota tego, co rozumiemy przez programowanie _obiektowe_.

Tylko funkcje `create()`, `recycle()`, `chparent()`, `chparents()`, `renumber()` i `recreate()` moga zmieniac atrybuty rodzica i dzieci.

Ponizej znajduje sie tabela reprezentujaca `flage` dla wbudowanych wlasciwosci przypisanych obiektowi. Jest to po prostu reprezentacja bitow -- na przyklad flaga player to pojedynczy bit (0x01). Flaga jest wiec w rzeczywistosci liczba calkowita, ktora w zapisie binarnym reprezentuje wszystkie flagi ustawione na obiekcie.

```
Player:         0x01    set_player_flag()
Programmer:     0x02    .programmer
Wizard:         0x04    .wizard
Obsolete_1:     0x08    *csssssh*
Read:           0x10    .r
Write:          0x20    .w
Obsolete_2:     0x40    *csssssh*
Fertile:        0x80    .f
Anonymous:      0x100   .a
Invalid:        0x200   <zniszcz obiekt anonimowy>
Recycled:       0x400   <zniszcz obiekt anonimowy i wywolaj czasownik recycle>
```

#### Wlasciwosci obiektow (Properties)

_Wlasciwosc_ (property) to nazwany "slot" w obiekcie, ktory moze przechowywac dowolna wartosc MOO. Kazdy obiekt ma jedenascie wbudowanych wlasciwosci, ktorych wartosci sa ograniczone do okreslonych typow. Dodatkowo obiekt moze miec dowolna liczbe innych wlasciwosci, z ktorych zadna nie ma ograniczen typu. Wbudowane wlasciwosci sa nastepujace:

| Wlasciwosc | Opis                                                          |
| ---------- | -------------------------------------------------------------- |
| name       | string, zwykla nazwa tego obiektu                              |
| owner      | obiekt, gracz kontrolujacy dostep do niego                     |
| location   | obiekt, gdzie obiekt znajduje sie w rzeczywistosci wirtualnej   |
| contents   | lista obiektow, odwrotnosc location                            |
| last_move  | mapa ostatniej lokalizacji obiektu i czasu (time()) przeniesienia |
| programmer | bit, czy obiekt ma uprawnienia programisty?                    |
| wizard     | bit, czy obiekt ma uprawnienia czarodzieja?                     |
| r          | bit, czy obiekt jest publicznie czytelny?                       |
| w          | bit, czy obiekt jest publicznie zapisywalny?                    |
| f          | bit, czy obiekt jest plodny (fertile)?                          |
| a          | bit, czy ten obiekt moze byc rodzicem obiektow anonimowych?     |

Wlasciwosc `name` sluzy do identyfikowania obiektu w rozmaitych wypisywanych komunikatach. Moze byc ustawiona wylacznie przez czarodzieja lub wlasciciela obiektu. Dla obiektow-graczy wlasciwosc `name` moze byc ustawiona wylacznie przez czarodzieja; pozwala to na przyklad czarodziejom sprawdzic, czy dwoch graczy nie ma tej samej nazwy.

`owner` identyfikuje obiekt majacy prawa wlasciciela do tego obiektu, pozwalajace mu na przyklad zmieniac wlasciwosc `name`. Tylko czarodziej moze zmienic wartosc tej wlasciwosci.

Wlasciwosci `location` i `contents` opisuja hierarchie zawierania obiektow w rzeczywistosci wirtualnej. Wiekszosc obiektow znajduje sie "wewnatrz" jakiegos innego obiektu i ten inny obiekt jest wartoscia wlasciwosci `location`.

Wlasciwosc `contents` to lista tych obiektow, dla ktorych ten obiekt jest ich lokalizacja. Aby zachowac spojnosc tych wlasciwosci, tylko funkcja `move()` moze je zmieniac.

Wlasciwosc `last_move` to mapa postaci `["source" -> OBJ, "time" -> TIMESTAMP]`. Jest ustawiana przez serwer za kazdym razem, gdy obiekt zostaje przeniesiony.

Bity `wizard` i `programmer` maja zastosowanie wylacznie do postaci, czyli obiektow reprezentujacych graczy. Kontroluja uprawnienia do korzystania z pewnych mechanizmow serwera. Moga byc ustawione wylacznie przez czarodzieja.

Bit `r` kontroluje, czy gracze inni niz wlasciciel tego obiektu moga uzyskac liste wlasciwosci lub czasownikow w obiekcie.

Symetrycznie, bit `w` kontroluje, czy osoby inne niz wlasciciel moga dodawac lub usuwac wlasciwosci i/lub czasowniki na tym obiekcie. Bity `r` i `w` moga byc ustawione wylacznie przez czarodzieja lub wlasciciela obiektu.

Bit `f` okresla, czy ten obiekt jest _plodny_ (fertile), czyli czy gracze inni niz wlasciciel tego obiektu moga tworzyc nowe obiekty z tym jako rodzicem. Kontroluje tez, czy osoby inne niz wlasciciel moga uzyc wbudowanej funkcji `chparent()` lub `chparents()`, by uczynic ten obiekt rodzicem istniejacego obiektu. Bit `f` moze byc ustawiony wylacznie przez czarodzieja lub wlasciciela obiektu.

Bit `a` okresla, czy ten obiekt moze byc uzyty jako rodzic obiektu anonimowego tworzonego przez gracza innego niz wlasciciel tego obiektu. Dziala podobnie do bitu `f`, ale dotyczy wylacznie tworzenia obiektow anonimowych.

Wszystkie wbudowane wlasciwosci na kazdym obiekcie moga, domyslnie, byc odczytane przez kazdego gracza. Mozliwe jest jednak nadpisanie tego zachowania z poziomu bazy danych, czyniac ktorakolwiek z tych wlasciwosci czytelna wylacznie dla czarodziei. Zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly.

Jak wspomniano powyzej, obiekty moga miec, i jest to bardzo przydatne, inne wlasciwosci poza wbudowanymi. Moga one pochodzic z dwoch zrodel.

Po pierwsze, obiekt ma wlasciwosc odpowiadajaca kazdej wlasciwosci w jego obiekcie-rodzicu. Uzywajac zargonu programowania obiektowego, jest to rodzaj _dziedziczenia_. Jesli jakis obiekt ma wlasciwosc o nazwie `foo`, to beda ja miec takze wszystkie jego dzieci, a wiec i dzieci jego dzieci, i tak dalej.

Po drugie, obiekt moze miec nowa wlasciwosc zdefiniowana wylacznie na nim samym i jego potomkach. Na przyklad obiekt reprezentujacy kamien moglby miec wlasciwosci wskazujace jego wage, sklad chemiczny i/lub ostrosc, w zaleznosci od zastosowan, do jakich kamien mialby byc uzyty w rzeczywistosci wirtualnej.

Kazda zdefiniowana wlasciwosc (w odroznieniu od wbudowanych) ma wlasciciela i zestaw uprawnien dla osob niebedacych wlascicielem. Wlasciciel wlasciwosci moze odczytywac i ustawiac wartosc wlasciwosci oraz zmieniac uprawnienia dla pozostalych. Tylko czarodziej moze zmienic wlasciciela wlasciwosci.

Poczatkowym wlascicielem wlasciwosci jest gracz, ktory ja dodal; zwykle, choc nie zawsze, jest to gracz bedacy wlascicielem obiektu, do ktorego wlasciwosc zostala dodana. Dzieje sie tak, poniewaz wlasciwosci moga byc dodawane wylacznie przez wlasciciela obiektu lub czarodzieja, chyba ze obiekt jest publicznie zapisywalny (tj. jego wlasciwosc `w` wynosi 1), co jest rzadkie. Tak wiec wlasciciel obiektu niekoniecznie musi byc wlascicielem kazdej (a nawet ktorejkolwiek) wlasciwosci na tym obiekcie.

Uprawnienia do wlasciwosci pochodza z tego zbioru:

| Bit uprawnien | Opis                                                            |
| -------------- | ---------------------------------------------------------------- |
| `r`            | Uprawnienie do odczytu pozwala osobom niebedacym wlascicielem odczytac wartosc wlasciwosci |
| `w`            | Uprawnienie do zapisu pozwala osobom niebedacym wlascicielem ustawiac wartosc wlasciwosci |
| `c`            | Zmiana wlasciciela u potomkow                                    |

Bit `c` jest nieco bardziej skomplikowany. Przypomnijmy, ze kazdy obiekt ma wszystkie wlasciwosci, ktore ma jego rodzic, a byc moze i kilka wiecej. Zazwyczaj, gdy obiekt-dziecko dziedziczy wlasciwosc po rodzicu, wlasciciel dziecka staje sie wlascicielem tej wlasciwosci. Dzieje sie tak, poniewaz bit uprawnien `c` jest domyslnie "wlaczony". Jesli bit `c` nie jest wlaczony, odziedziczona wlasciwosc ma tego samego wlasciciela u dziecka, co u rodzica.

Jako przyklad, gdzie moze to byc przydatne: baza danych ToastCore zapewnia, ze kazdy gracz ma wlasciwosc `password` zawierajaca zaszyfrowana wersje hasla polaczenia gracza. Ze wzgledow bezpieczenstwa nie chcemy, by inni gracze mogli zobaczyc nawet zaszyfrowana wersje hasla, wiec wylaczamy bit uprawnien `r`. Aby zapewnic, ze haslo jest ustawiane wylacznie w spojny sposob (tj. na zaszyfrowana wersje hasla gracza), nie chcemy pozwolic nikomu poza czarodziejem na zmiane tej wlasciwosci. Dlatego w obiekcie-rodzicu dla wszystkich graczy uczynilismy czarodzieja wlascicielem wlasciwosci password i ustawilismy uprawnienia na pusty string, `""`. Oznacza to, ze osoby niebedace wlascicielem nie moga odczytac ani zapisac tej wlasciwosci, a poniewaz bit `c` nie jest ustawiony, czarodziej bedacy wlascicielem tej wlasciwosci na klasie-rodzicu jest tez jej wlascicielem u wszystkich potomkow tej klasy.

> Ostrzezenie: w klasycznym LambdaMOO haszowanych bylo tylko pierwszych 8 znakow hasla. W praktyce oznaczalo to, ze hasla `password` i `password12345` byly dokladnie takie same i kazdego z nich mozna bylo uzyc do zalogowania. Zostalo to naprawione w ToastStunt. Jesli aktualizujesz z LambdaMOO, musisz zalogowac sie uzywajac tylko pierwszych 8 znakow hasla (a nastepnie zresetowac haslo na cos bezpieczniejszego).

Inny, byc moze bardziej przyziemny przyklad pojawil sie, gdy postac imieniem Ford zaczela budowac obiekty, ktore nazwal "radiami", a inna postac, yduJ, chciala miec wlasne. Ford uprzejmie uczynil generyczny obiekt radia plodnym (fertile), pozwalajac yduJ stworzyc jego dziecko -- wlasne radio. Radia mialy wlasciwosc `channel` identyfikujaca cos w rodzaju czestotliwosci, na ktora radio bylo nastrojone. Ford napisal niezle programy na radiach (czasowniki, omowione ponizej) do przelaczania selektora kanalow z przodu radia, co powodowalo odpowiednia zmiane wartosci wlasciwosci `channel`. Jednak za kazdym razem, gdy ktos probowal przelaczyc selektor kanalow na radiu yduJ, otrzymywal blad uprawnien. Problem dotyczyl wlasciciela wlasciwosci `channel`.

Jak wyjasniono pozniej, programy dzialaja z uprawnieniami swojego autora. Tak wiec w tym przypadku niezly czasownik Forda do ustawiania kanalu dzialal z jego uprawnieniami. Ale poniewaz wlasciwosc `channel` w generycznym radiu miala ustawiony bit uprawnien `c`, wlasciwosc `channel` na radiu yduJ nalezala do niej. Ford nie mial uprawnien, by ja zmienic! Rozwiazanie bylo proste. Ford zmienil uprawnienia wlasciwosci `channel` generycznego radia na samo `r`, bez bitu `c`, a yduJ zrobila nowe radio. Tym razem, gdy radio yduJ odziedziczylo wlasciwosc `channel`, yduJ nie odziedziczyla jej wlasnosci -- Ford pozostal wlascicielem. Teraz radio dzialalo poprawnie, poniewaz czasownik Forda mial uprawnienia do zmiany kanalu.

#### Czasowniki na obiektach (Verbs)

Ostatnim rodzajem elementu skladajacego sie na obiekt sa _czasowniki_ (verbs). Czasownik to nazwany program MOO powiazany z konkretnym obiektem. Wiekszosc czasownikow implementuje polecenia, ktore moze wpisac gracz; na przyklad w bazie danych ToastCore istnieje czasownik na wszystkich obiektach reprezentujacych pojemniki, ktory implementuje polecenia postaci `put obiekt in pojemnik`.

Mozliwe jest tez, by programy MOO wywolywaly czasowniki zdefiniowane na obiektach. Niektore czasowniki sa w istocie zaprojektowane tak, by byly uzywane wylacznie wewnatrz kodu MOO; nie odpowiadaja zadnemu konkretnemu poleceniu gracza. Tak wiec czasowniki w MOO sa jak _procedury_ lub _metody_ znane z innych jezykow programowania.

> Uwaga: istnieje jeszcze wiecej sposobow odnoszenia sie do _czasownikow_ i ich odpowiednikow w innych jezykach programowania: _procedura_, _funkcja_, _podprogram_ i _metoda_ sa glownymi z nich. Jednak w _Programowaniu Obiektowym_, w skrocie _OOP_, mozesz je znac przede wszystkim jako metody.

Podobnie jak wlasciwosci, kazdy czasownik ma wlasciciela i zestaw bitow uprawnien. Wlasciciel czasownika moze zmieniac jego program, bity uprawnien oraz specyfikatory argumentow (omowione ponizej). Tylko czarodziej moze zmienic wlasciciela czasownika.

Wlasciciel czasownika okresla tez uprawnienia, z jakimi ten czasownik dziala; to znaczy, ze program w czasowniku moze wykonac wszystko, co moze wykonac wlasciciel tego czasownika, i nic wiecej. Tak wiec na przyklad czasownik nalezacy do czarodzieja musi byc napisany bardzo starannie, poniewaz czarodzieje moga zrobic niemal wszystko.

> Ostrzezenie: to powazna sprawa. MOO ma rozne zabezpieczenia uprawnien (na poziomie obiektu, czasownika i wlasciwosci), ktore sa niemal calkowicie ignorowane, gdy czasownik dziala z uprawnieniami czarodzieja. Mozesz rozwazyc stworzenie postaci niebedacej czarodziejem i nadanie jej bitu programisty, i pisac wiekszosc swojego kodu na niej, zostawiajac bit czarodzieja dla rzeczy faktycznie wymagajacych dostepu do wszystkiego, mimo uprawnien.

| Bit uprawnien | Opis                                              |
| -------------- | -------------------------------------------------- |
| r (read)       | Pozwala osobom niebedacym wlascicielem zobaczyc kod czasownika |
| w (write)      | Pozwala osobom niebedacym wlascicielem zapisac kod czasownika  |
| x (execute)    | Pozwala wywolac czasownik z wnetrza innego czasownika          |
| d (debug)      | Pozwala czasownikowi zglaszac bledy do przechwycenia            |

Bity uprawnien czasownikow pochodza z tego zbioru: `r` (read/odczyt), `w` (write/zapis), `x` (execute/wykonanie) i `d` (debug). Uprawnienie odczytu pozwala osobom niebedacym wlascicielem zobaczyc program czasownika, a symetrycznie uprawnienie zapisu pozwala im ten program zmienic. Dwa pozostale bity nie sa, scisle mowiac, bitami uprawnien w ogole; maja powszechny efekt, obejmujacy zarowno wlasciciela, jak i pozostale osoby.

Bit execute okresla, czy czasownik moze byc wywolany z wnetrza programu MOO (w odroznieniu od linii polecen, jak czasownik `put` na pojemnikach). Jesli bit `x` nie jest ustawiony, czasownik nie moze byc wywolany z wnetrza programu. Jest to najbardziej oczywiscie przydatne dla czasownikow `this none this`, ktore sa przeznaczone do wykonywania z wnetrza innych programow-czasownikow, jednak moze byc przydatne ustawienie bitu `x` na czasownikach przeznaczonych do wykonywania z linii polecen, poniewaz wtedy moga byc rowniez wykonywane z wnetrza innego czasownika.

Ustawienie bitu debug okresla, co dzieje sie, gdy program czasownika zrobi cos blednego, jak odejmowanie liczby od ciagu znakow. Jesli bit `d` jest ustawiony, serwer _zglasza_ (raises) wartosc bledu; takie zglaszane bledy moga byc _przechwycone_ (caught) przez pewne inne fragmenty kodu MOO. Jesli jednak blad nie zostanie przechwycony, serwer przerywa wykonanie polecenia i, domyslnie, wypisuje komunikat o bledzie na terminalu gracza, ktorego polecenie jest wykonywane. (Zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly obslugi nieprzechwyconych bledow.) Jesli bit `d` nie jest ustawiony, zaden blad nie jest zglaszany, zaden komunikat nie jest wypisywany i polecenie nie jest przerywane; zamiast tego wartosc bledu jest zwracana jako wynik blednej operacji.

> Uwaga: bit `d` istnieje wylacznie z powodow historycznych; kiedys byl jedynym sposobem, by kod MOO mogl przechwytywac i obslugiwac bledy. Wraz z wprowadzeniem instrukcji `try`-`except` oraz wyrazenia przechwytujacego bledy, bit `d` przestal byc przydatny. Wszystkie nowe czasowniki powinny miec ustawiony bit `d`, korzystajac w razie potrzeby z nowszych mechanizmow obslugi bledow. Z czasem stare czasowniki napisane w zalozeniu, ze bit `d` nie bedzie ustawiony, powinny zostac zmienione, by korzystac z nowych mechanizmow.

Oprocz wlasciciela i pewnych bitow uprawnien, kazdy czasownik ma trzy _specyfikatory argumentow_, po jednym dla `dopelnienia blizszego` (direct object), `przyimka` (preposition) i `dopelnienia dalszego` (indirect object). Specyfikatory dopelnienia blizszego i dalszego sa kazdy wybierane z tego zbioru: `this`, `any` lub `none`. Specyfikator przyimka to `none`, `any` lub jeden z elementow tej listy:

| Przyimek                  |
| ------------------------ |
| with/using               |
| at/to                    |
| in front of              |
| in/inside/into           |
| on top of/on/onto/upon   |
| out of/from inside/from  |
| over                     |
| through                  |
| under/underneath/beneath |
| behind                   |
| beside                   |
| for/about                |
| is                       |
| as                       |
| off/off of               |

> Uwaga tlumacza: przyimki powyzej pozostaja w oryginalnej, angielskiej formie, poniewaz sa to realne slowa kluczowe rozpoznawane przez parser polecen serwera przy dopasowywaniu wpisywanych przez graczy komend -- nie sa to elementy opisowe, tylko skladnia jezyka.

Specyfikatory argumentow sa uzywane w procesie parsowania polecen, opisanym w nastepnym rozdziale.

## Wbudowany parser polecen

Serwer MOO jest w stanie wykonac niewielka ilosc parsowania polecen wpisywanych przez gracza. W szczegolnosci potrafi rozbic polecenia majace jedna z nastepujacych form:

* czasownik
* czasownik dopelnienie-blizsze
* czasownik dopelnienie-blizsze przyimek dopelnienie-dalsze

Rzeczywiste przyklady tych form, sensowne w bazie danych ToastCore, sa nastepujace:

```
look
take yellow bird
put yellow bird in cuckoo clock
```

Zauwaz, ze angielskie przedimki (`the`, `a`, `an`) generalnie nie sa uzywane w poleceniach MOO; parser nie wie, ze nie sa one istotna czescia nazw obiektow.

Aby to wszystko mialo realny sens, wazne jest, by dokladnie zrozumiec, jak serwer decyduje, co zrobic, gdy gracz wpisze polecenie.

Ale najpierw wspomnijmy o trzech sytuacjach, w ktorych linia wpisana przez gracza nie jest traktowana jak zwykle polecenie:

1. Linia moze dokladnie odpowiadac zdefiniowanemu dla polaczenia poleceniu czyszczenia (flush), jesli takie istnieje (domyslnie `.flush`) -- w takim przypadku wszystkie oczekujace linie wejscia sa czyszczone i nic wiecej nie jest robione z samym poleceniem flush. Podobnie, kazda linia moze zostac wyczyszczona przez kolejne polecenie flush, zanim serwer zdazy ja przetworzyc w inny sposob. Wiecej na ten temat w sekcji o czyszczeniu nieprzetworzonego wejscia.
2. Linia moze zaczynac sie od prefiksu kwalifikujacego ja do przetwarzania poza pasmem (out-of-band) i byc moze, w rezultacie, do bycia poleceniem out-of-band. Wiecej na ten temat w sekcji o przetwarzaniu out-of-band.
3. Polaczenie moze byc obiektem wywolania `read()` (patrz sekcja o operacjach na polaczeniach sieciowych) lub moze byc w trakcie polecenie `.program` (patrz sekcja o poleceniu .program), z ktorych kazde odpowiednio skonsumuje te linie. Zauwaz tez, ze jesli ustawiono opcje polaczenia "hold-input", wszystkie linie wpisywane przez gracza "w pasmie" sa w tym momencie wstrzymywane do przyszlego odczytu, nawet jesli zadne zadanie odczytu nie jest aktualnie aktywne.

W przeciwnym razie mamy (wreszcie) prawdziwa linie polecenia, ktora moze przejsc normalny proces parsowania polecen, jak nastepuje:

Serwer sprawdza, czy pierwszy niepusty znak w poleceniu jest jednym z nastepujacych:

* `"`
* `:`
* `;`

Jesli tak, ten znak jest zastepowany odpowiednim ponizszym poleceniem, po ktorym nastepuje spacja:

* `say`
* `emote`
* `eval`

Na przyklad to polecenie:

```
"Hi, there.
```

zostanie potraktowane dokladnie tak, jakby brzmialo:

```
say Hi, there.
```

Nastepnie serwer rozbija polecenie na slowa. W najprostszym przypadku polecenie jest rozbijane na slowa przy kazdym ciagu znakow spacji; na przyklad polecenie `foo bar baz` zostanie rozbite na slowa `foo`, `bar` i `baz`. Aby zmusic serwer do wlaczenia spacji w "slowo", cale slowo lub jego czesc mozna ujac w cudzyslowy. Na przyklad polecenie:

```
foo "bar mumble" baz" "fr"otz" bl"o"rt
```

zostaje rozbite na slowa `foo`, `bar mumble`, `baz frotz` i `blort`.

Wreszcie, aby zawrzec w slowie cudzyslow lub ukosnik wsteczny, mozna je poprzedzic ukosnikiem wstecznym, tak jak w stringach MOO.

Rozbiwszy w ten sposob string na slowa, serwer nastepnie sprawdza, czy pierwsze slowo nazywa ktores z szesciu "wbudowanych" polecen:

* `.program`
* `PREFIX`
* `OUTPUTPREFIX`
* `SUFFIX`
* `OUTPUTSUFFIX`
* lub zdefiniowane dla polaczenia polecenie _flush_, jesli takie istnieje (domyslnie `.flush`).

Pierwsze z nich jest dostepne wylacznie dla programistow, kolejne cztery sa przeznaczone do uzytku przez programy-klienty, a ostatnie moze sie roznic w zaleznosci od bazy danych, a nawet polaczenia; wszystkie szesc jest opisanych w ostatnim rozdziale tego dokumentu, "Polecenia serwera i zalozenia bazy danych". Jesli pierwsze slowo nie jest zadnym z powyzszych, trafiamy do zwyklego przypadku: normalnego polecenia MOO.

Serwer nastepnie daje kodowi w bazie danych szanse na obsluzenie polecenia. Jesli istnieje czasownik `$do_command()`, jest on wywolywany ze slowami polecenia przekazanymi jako jego argumenty oraz `argstr` ustawionym na surowe polecenie wpisane przez uzytkownika. Jesli `$do_command()` nie istnieje, lub jesli to wywolanie czasownika zakonczy sie normalnie (tj. bez zawieszenia lub przerwania) i zwroci wartosc falszywa, wowczas wywolywany jest wbudowany parser polecen, aby obsluzyc polecenie w sposob opisany ponizej. W przeciwnym razie zaklada sie, ze kod bazy danych obsluzyl polecenie w calosci i serwer nie podejmuje dla tego polecenia zadnych dalszych dzialan.

> Uwaga: `$do_command` jest referencja skorifikowana. Odnosi sie do czasownika `do_command` na #0. Wiecej szczegolow o korifikowaniu wlasciwosci i czasownikow zostanie przedstawionych pozniej.

Jesli wywolany zostanie wbudowany parser polecen, serwer probuje sparsowac polecenie na czasownik, dopelnienie blizsze, przyimek i dopelnienie dalsze. Pierwsze slowo jest traktowane jako czasownik. Serwer nastepnie probuje znalezc jedna z fraz przyimkowych wymienionych na koncu poprzedniej sekcji, uzywajac dopasowania wystepujacego najwczesniej w poleceniu. Na przyklad w bardzo dziwnym poleceniu `foo as bar to baz` serwer przyjmie `as` jako przyimek, a nie `to`.

Jesli serwerowi uda sie znalezc przyimek, uznaje slowa miedzy czasownikiem a przyimkiem za dopelnienie blizsze, a te po przyimku za dopelnienie dalsze. W obu przypadkach sekwencja slow jest zamieniana na string przez wstawienie jednej spacji miedzy kazda para slow. Tak wiec w dziwnym poleceniu z poprzedniego akapitu nie ma zadnych slow w dopelnieniu blizszym (tj. jest ono uznawane za pusty string, `""`), a dopelnienie dalsze to `"bar to baz"`.

Jesli nie bylo przyimka, dopelnieniem blizszym sa wszystkie slowa po czasowniku, a dopelnienie dalsze jest pustym stringiem.

Kolejnym krokiem jest probe znalezienia obiektow MOO nazwanych przez stringi dopelnienia blizszego i dalszego.

Po pierwsze, jesli string obiektu jest pusty, odpowiadajacym mu obiektem jest specjalny obiekt `#-1` (czyli `$nothing` w ToastCore). Jesli string obiektu ma forme numeru obiektu (tj. znak hash (`#`), po ktorym nastepuja cyfry) i obiekt o tym numerze istnieje, to jest to nazwany obiekt. Jesli string obiektu to `"me"` lub `"here"`, uzywany jest odpowiednio sam obiekt gracza lub jego lokalizacja.

> Uwaga: $nothing jest uznawany za obiekt `skorifikowany` (corified). Oznacza to, ze na `#0` zostala utworzona _wlasciwosc_ o nazwie `nothing`, z wartoscia `#-1`. Na przyklad (po utworzeniu wlasciwosci): `;#0.nothing = #-1`. Pozwala to odwolywac sie do obiektu `#-1` poprzez jego skorifikowana referencje `$nothing`. W praktyce moze to byc bardzo przydatne, poniewaz mozesz (i powinienes!) uzywac skorifikowanych referencji w swoim kodzie zamiast numerow obiektow. Miedzy innymi korzysciami pozwala to napisac kod (odwolujacy sie do innych obiektow) raz, a nastepnie podmienic skorifikowana referencje, wskazujac na inny obiekt. Na przyklad, jesli masz nowy system logowania bledow i chcesz zastapic stara referencje $error_logger nowa, nie musisz szukac wszystkich odwolan do starego numeru obiektu error loggera w swoim kodzie. Wystarczy zmienic wlasciwosc na `#0`, by wskazywala na nowy obiekt.

W przeciwnym razie serwer rozwaza wszystkie obiekty, ktorych lokalizacja to albo gracz (tj. obiekty, ktore gracz "trzyma", by tak rzec), albo pokoj, w ktorym gracz sie znajduje (tj. obiekty w tym samym pokoju co gracz); bedzie probowal dopasowac string obiektu do roznych nazw tych obiektow.

Dopasowywanie wykonywane przez serwer korzysta z wlasciwosci `aliases` kazdego z rozwazanych obiektow. Wartoscia tej wlasciwosci powinna byc lista stringow, roznych alternatywnych nazw dla obiektu. Jesli nie jest to lista, lub obiekt nie ma wlasciwosci `aliases`, uzywana jest pusta lista. W kazdym przypadku wartosc wlasciwosci `name` jest dodawana do listy na potrzeby dopasowywania.

Serwer sprawdza, czy string obiektu w poleceniu jest albo dokladnie rowny, albo prefiksem ktoregos aliasu; jesli istnieja jakiekolwiek dokladne dopasowania, dopasowania prefiksowe sa ignorowane. Jesli dokladnie jeden z rozwazanych obiektow ma pasujacy alias, uzywany jest ten obiekt. Jesli wiecej niz jeden ma dopasowanie, uzywany jest specjalny obiekt `#-2` (czyli `$ambiguous_match` w ToastCore). Jesli nie ma zadnych dopasowan, uzywany jest specjalny obiekt `#-3` (czyli `$failed_match` w ToastCore).

Tak wiec serwer zidentyfikowal juz string czasownika, string przyimka oraz stringi i obiekty dopelnienia blizszego i dalszego. Nastepnie przeglada kazdy z czasownikow zdefiniowanych na kazdym z nastepujacych czterech obiektow, w kolejnosci:

1. gracz, ktory wpisal polecenie
2. pokoj, w ktorym znajduje sie gracz
3. dopelnienie blizsze, jesli istnieje
4. dopelnienie dalsze, jesli istnieje.

Dla kazdego z tych czasownikow po kolei sprawdza, czy wszystkie z nastepujacych sa prawdziwe:

* string czasownika w poleceniu pasuje do jednej z nazw czasownika
* wartosci dopelnienia blizszego i dalszego znalezione podczas dopasowywania sa dozwolone przez odpowiednie _specyfikatory argumentow_ czasownika
* string przyimka w poleceniu jest dopasowywany przez _specyfikator przyimka_ czasownika.

Wyjasnie po kolei kazde z tych kryteriow.

Kazdy czasownik ma jedna lub wiecej nazw; wszystkie nazwy sa przechowywane w jednym stringu, oddzielone spacjami. W najprostszym przypadku nazwa czasownika to po prostu slowo zlozone z dowolnych znakow innych niz spacje i gwiazdki (' ' i `*`). W tym przypadku nazwa czasownika pasuje tylko sama do siebie; to znaczy nazwa musi byc dopasowana dokladnie.

Jesli jednak nazwa zawiera pojedyncza gwiazdke, wowczas pasuje do dowolnego prefiksu samej siebie, ktory jest co najmniej tak dlugi jak czesc przed gwiazdka. Na przyklad nazwa czasownika `foo*bar` pasuje do dowolnego z ciagow `foo`, `foob`, `fooba` lub `foobar`; zauwaz, ze sama gwiazdka nie jest uznawana za czesc nazwy.

Jesli nazwa czasownika _konczy sie_ gwiazdka, pasuje do dowolnego stringa zaczynajacego sie od czesci przed gwiazdka. Na przyklad nazwa czasownika `foo*` pasuje do dowolnego z ciagow `foo`, `foobar`, `food` lub `foogleman`, miedzy wieloma innymi. Jako szczegolny przypadek, jesli nazwa czasownika to `*` (tj. sama pojedyncza gwiazdka), pasuje do wszystkiego.

Przypomnijmy, ze specyfikatory argumentow dla dopelnienia blizszego i dalszego pochodza ze zbioru `none`, `any` i `this`. Jesli specyfikator to `none`, odpowiadajaca wartosc obiektu musi byc `#-1` (czyli `$nothing` w ToastCore); to znaczy nie mogla zostac podana. Jesli specyfikator to `any`, odpowiadajaca wartosc obiektu moze byc dowolna. Wreszcie, jesli specyfikator to `this`, odpowiadajaca wartosc obiektu musi byc taka sama jak obiekt, na ktorym znalezlismy ten czasownik; na przyklad, jesli rozwazamy czasowniki na graczu, wartosc obiektu musi byc obiektem gracza.

Wreszcie, przypomnijmy, ze specyfikator argumentu dla przyimka to `none`, `any` lub jeden z kilku zbiorow fraz przyimkowych, podanych powyzej. Specyfikator `none` pasuje tylko wtedy, gdy w poleceniu nie znaleziono zadnego przyimka. Specyfikator `any` zawsze pasuje, niezaleznie od tego, jaki przyimek zostal znaleziony, jesli w ogole. Jesli specyfikator to zbior fraz przyimkowych, znaleziona fraza musi znajdowac sie w tym zbiorze, aby specyfikator pasowal.

Serwer rozwaza wiec kolejno kilka obiektow, sprawdzajac kolejno kazdy z ich czasownikow, szukajac pierwszego, ktory spelnia wszystkie wlasnie wyjasnione kryteria. Jesli go znajdzie, to jest to czasownik, ktorego program zostanie wykonany dla tego polecenia. Jesli nie, wtedy szuka czasownika o nazwie `huh` w pokoju, w ktorym znajduje sie gracz; jesli taki zostanie znaleziony, ten czasownik zostanie wywolany. Ta funkcja jest przydatna do implementowania parsowania polecen specyficznego dla pokoju lub odzyskiwania po bledzie. Jesli serwer nie moze znalezc nawet czasownika `huh` do uruchomienia, wypisuje komunikat o bledzie w rodzaju `I couldn't understand that.` i polecenie jest uznawane za zakonczone.

Nareszcie mamy program do uruchomienia w odpowiedzi na polecenie wpisane przez gracza. Gdy kod programu zaczyna sie wykonywac, nastepujace wbudowane zmienne beda mialy wskazane wartosci:

| Zmienna  | Wartosc                                                          |
| -------- | -------------------------------------------------------------------- |
| player   | obiekt, gracz, ktory wpisal polecenie                                |
| this     | obiekt, obiekt, na ktorym znaleziono ten czasownik                   |
| caller   | obiekt, taki sam jak <code>player</code>                             |
| verb     | string, pierwsze slowo polecenia                                     |
| argstr   | string, wszystko po pierwszym slowie polecenia                       |
| args     | lista stringow, slowa w <code>argstr</code>, lub lista mieszanych typow zawierajaca argumenty, z ktorymi wywolano czasownik |
| dobjstr  | string, string dopelnienia blizszego znaleziony podczas parsowania   |
| dobj     | obiekt, wartosc dopelnienia blizszego znaleziona podczas dopasowywania |
| prepstr  | string, fraza przyimkowa znaleziona podczas parsowania               |
| iobjstr  | string, string dopelnienia dalszego                                  |
| iobj     | obiekt, wartosc dopelnienia dalszego                                 |

Wartosc zwrocona przez program, jesli jakakolwiek, jest ignorowana przez serwer.

### Watkowanie (Threading)

ToastStunt jest jednowatkowy, ale wykorzystuje biblioteke watkowania (extension-background), by pozwolic pewnym funkcjom serwera dzialac w osobnym watku. Aby chronic baze danych, te funkcje w sposob niejawny zawieszaja kod MOO (podobnie jak dziala read()).

Mozliwe jest wylaczenie watkowania funkcji dla konkretnego czasownika, wywolujac `set_thread_mode(0)`.

> Uwaga: domyslnie ToastStunt ma watkowanie wlaczone.

Istnieja konfigurowalne opcje dla podsystemu tla (background), ktore mozna zdefiniowac w `options.h`.

* `TOTAL_BACKGROUND_THREADS` to calkowita liczba watkow pthread, ktore zostana utworzone przy starcie, aby przetwarzac zadania MOO w tle.
* `DEFAULT_THREAD_MODE` okresla domyslne zachowanie watkowanych funkcji MOO bez wywolania set_thread_mode. Gdy ustawione na prawde (true), domyslnym zachowaniem jest watkowanie tych funkcji, co wymaga wywolania set_thread_mode(0), by je wylaczyc. Gdy falsz (false), domyslnym zachowaniem jest brak watkowania i wymagane jest wywolanie set_thread_mode(1), by wlaczyc watkowanie dla funkcji w danym czasowniku.

Gdy wykonujesz watkowana funkcje wbudowana w swoim kodzie, twoj kod zostaje zawieszony. Z tego powodu nalezy zachowac ostroznosc co do tego, jak i kiedy uzywasz tych funkcji przy wlaczonym watkowaniu.

Funkcje obslugujace watkowanie oraz funkcje sluzace do wykorzystywania watkowania, takie jak `thread_pool`, sa omowione w sekcji o funkcjach wbudowanych.

## Jezyk programowania MOO

MOO oznacza "MUD, Object Oriented" (obiektowy MUD). MUD z kolei podobno oznacza wiele roznych rzeczy, ale ja sklaniam sie ku "Multi-User Dungeon" (wieloosobowy loch), w duchu tych starozytnych poprzednikow MUD-ow, Adventure i Zork.

MOO, jezyk programowania, jest wzglednie malym i prostym jezykiem obiektowym, zaprojektowanym tak, by byl latwy do nauczenia dla wiekszosci nieprogramistow; wiekszosc zlozonych systemow nadal jednak wymaga pewnych znaczacych umiejetnosci programistycznych.

Dawszy Ci wystarczajacy kontekst, by zrozumiec dokladnie, co robi kod MOO, wyjasnie teraz, jak wyglada kod MOO i co oznacza. Zaczne od skladni i semantyki wyrazen, czyli fragmentow kodu majacych wartosci. Potem omowie instrukcje, kolejny poziom struktury ponad wyrazeniami. Nastepnie omowie pojecie taska (zadania), czyli rodzaju uruchomionego procesu inicjowanego miedzy innymi przez wpisywanie polecen przez graczy. Na koniec wymienie wszystkie funkcje wbudowane dostepne dla kodu MOO i opisze, co robia.

Zanim jednak przejdziemy dalej, wspomne o komentarzach. Mozesz wlaczyc w swoim programie MOO fragmenty tekstu, ktore sa ignorowane przez serwer. Chodzi o to, by pozwolic Ci wstawiac notatki dla siebie i innych o tym, co robi kod. Aby to zrobic, zacznij tekst komentarza od dwoch znakow `/*` i zakoncz go dwoma znakami `*/`; jest to dokladnie tak jak komentarze w jezyku programowania C. Zauwaz, ze serwer calkowicie zignoruje ten tekst; _nie_ zostanie on zapisany w bazie danych. Tak wiec takie komentarze sa przydatne wylacznie w plikach kodu utrzymywanych poza baza danych.

Aby zawrzec w swoim kodzie bardziej trwaly komentarz, sprobuj uzyc literalu ciagu znakow jako instrukcji. Na przyklad zdanie o maslu orzechowym w ponizszym kodzie jest zasadniczo ignorowane podczas wykonania, ale zostanie zachowane w bazie danych:

```
for x in (players())
  "Grendel eats peanut butter!";
  player:tell(x.name, " (", x, ")");
endfor
```

> Uwaga: w praktyce jedynym stylem komentarzy, jakiego bedziesz uzywac, sa cytowane stringi tekstu. Przyzwyczaj sie do tego. Innym wartym uwagi faktem jest to, ze te stringi SA ewaluowane. Nic nie jest robione z wynikami tej ewaluacji, poniewaz wartosc nie jest nigdzie przechowywana -- moze byc jednak roztropne, by trzymac komentarze-stringi z dala od zagniezdzonych petli, dla nieco wiekszej szybkosci kodu.

### Wyrazenia jezyka MOO

Wyrazenia to te fragmenty kodu MOO, ktore generuja wartosci; na przyklad kod MOO

```
3 + 4
```

jest wyrazeniem, ktore generuje (lub "ma", lub "zwraca") wartosc 7. W MOO istnieje wiele rodzajow wyrazen, wszystkie omowione ponizej.

#### Bledy podczas ewaluacji wyrazen

Wiekszosc rodzajow wyrazen moze, w pewnych okolicznosciach, spowodowac wygenerowanie bledu. Na przyklad wyrazenie `x / y` wygeneruje blad `E_DIV`, jesli `y` jest rowne zero. Gdy wyrazenie generuje blad, zachowanie serwera jest kontrolowane przez ustawienie bitu `d` (debug) na czasowniku zawierajacym to wyrazenie. Jesli bit `d` nie jest ustawiony, blad jest natychmiast skutecznie "wyciszany" w momencie powstania; wartosc bledu jest po prostu zwracana jako wartosc wyrazenia, ktore go wygenerowalo.

> Uwaga: to zachowanie wyciszajace bledy jest bardzo podatne na bledy, poniewaz dotyczy _wszystkich_ bledow, w tym takich, ktorych programista mogl nie przewidziec. Bit `d` istnieje wylacznie z powodow historycznych; kiedys byl jedynym sposobem, by programisci MOO mogli przechwytywac i obslugiwac bledy. Wyrazenie przechwytujace bledy oraz instrukcja `try`-`except`, obie opisane ponizej, sa znacznie lepszymi sposobami osiagniecia tego samego celu.

Jesli bit `d` jest ustawiony, jak zwykle bywa, blad jest _zglaszany_ (raised) i moze zostac przechwycony i obsluzony albo przez kod otaczajacy dane wyrazenie, albo przez czasowniki wyzej w lancuchu wywolan prowadzacym do biezacego czasownika. Jesli blad nie zostanie przechwycony, serwer przerywa cale zadanie i, domyslnie, wypisuje komunikat biezacemu graczowi. Zobacz opisy wyrazenia przechwytujacego bledy oraz instrukcji `try`-`except` po szczegoly przechwytywania bledow, a takze rozdzial o zalozeniach serwera wobec bazy danych po szczegoly obslugi nieprzechwyconych bledow.

#### Zapisywanie wartosci bezposrednio w czasownikach

Najprostszym rodzajem wyrazenia jest literal wartosci MOO, dokladnie tak jak opisano w sekcji o wartosciach na poczatku tego dokumentu. Na przyklad wszystkie ponizsze sa wyrazeniami:

* 17
* #893
* "To jest ciag znakow."
* E_TYPE
* ["klucz" -> "wartosc"]
* {"To", "jest", "lista", "slow"}

W przypadku list, jak w ostatnim przykladzie powyzej, zauwaz, ze wyrazenie listy zawiera inne wyrazenia, w tym przypadku kilka ciagow znakow. Ogolnie te wyrazenia moga byc dowolnego rodzaju, niekoniecznie wartosciami literalnymi. Na przyklad

```
{3 + 4, 3 - 4, 3 * 4}
```

jest wyrazeniem, ktorego wartoscia jest lista `{7, -1, 12}`.

#### Nazywanie wartosci wewnatrz czasownika

Jak omowiono wczesniej, mozliwe jest przechowywanie wartosci we wlasciwosciach obiektow; wlasciwosci beda przechowywac te wartosci wiecznie, dopoki nie zostanie tam jawnie wstawiona inna wartosc. Dosc czesto jednak przydatne jest posiadanie miejsca, by odlozyc wartosc tylko na chwile. MOO udostepnia do tego celu zmienne lokalne.

Zmienne to nazwane miejsca do przechowywania wartosci; mozesz odczytywac i ustawiac wartosc w danej zmiennej tyle razy, ile chcesz. Zmienne sa jednak tymczasowe; trwaja tylko podczas dzialania danego czasownika; po jego zakonczeniu wszystkie zmienne, ktorym nadano tam wartosci, przestaja istniec, a wartosci zostaja zapomniane.

Zmienne sa tez "lokalne" dla konkretnego czasownika; kazdy czasownik ma wlasny ich zestaw. Tak wiec zmienne ustawione w jednym czasowniku nie sa widoczne dla kodu innych czasownikow.

Nazwa zmiennej sklada sie wylacznie z liter, cyfr i znaku podkreslenia (`_`) i nie zaczyna sie od cyfry. Nastepujace sa wszystkie prawidlowymi nazwami zmiennych:

* foo
* _foo
* this2that
* M68000
* two_words
* This_is_a_very_long_multiword_variable_name

Zauwaz, ze podobnie jak niemal wszystko inne w MOO, wielkosc liter w nazwach zmiennych nie ma znaczenia. Na przyklad wszystkie ponizsze sa nazwami tej samej zmiennej:

* fubar
* Fubar
* FUBAR
* fUbAr

Nazwa zmiennej sama w sobie jest wyrazeniem; jej wartoscia jest wartosc nazwanej zmiennej. Gdy czasownik zaczyna dzialac, niemal zadna zmienna nie ma jeszcze wartosci; jesli sprobujesz uzyc wartosci zmiennej, ktora jej nie ma, zglaszana jest wartosc bledu `E_VARNF`. (MOO rozni sie od wielu innych jezykow programowania, w ktorych trzeba _zadeklarowac_ kazda zmienna przed uzyciem; MOO nie ma takich deklaracji.) Nastepujace zmienne zawsze maja wartosci:

| Zmienna  |
| -------- |
| INT      |
| NUM      |
| FLOAT    |
| OBJ      |
| STR      |
| LIST     |
| ERR      |
| BOOL     |
| MAP      |
| WAIF     |
| ANON     |
| true     |
| false    |
| player   |
| this     |
| caller   |
| verb     |
| args     |
| argstr   |
| dobj     |
| dobjstr  |
| prepstr  |
| iobj     |
| iobjstr  |

> Uwaga: `num` jest przestarzala (deprecated) referencja do `int` i zostala tu wymieniona wylacznie dla kompletnosci.

Wartosci niektorych z tych zmiennych zawsze zaczynaja sie takie same:

| Zmienna             | Wartosc | Opis                                                     |
| ------------------- | ----- | ----------------------------------------------------- |
| <code>INT</code>    | 0     | liczba calkowita, kod typu dla liczb calkowitych        |
| <code>NUM</code>    | 0     | (przestarzale) liczba calkowita, kod typu dla liczb calkowitych |
| <code>OBJ</code>    | 1     | liczba calkowita, kod typu dla obiektow                 |
| <code>STR</code>    | 2     | liczba calkowita, kod typu dla stringow                 |
| <code>ERR</code>    | 3     | liczba calkowita, kod typu dla wartosci bledow          |
| <code>LIST</code>   | 4     | liczba calkowita, kod typu dla list                     |
| <code>FLOAT</code>  | 9     | liczba calkowita, kod typu dla liczb zmiennoprzecinkowych |
| <code>MAP</code>    | 10    | liczba calkowita, kod typu dla wartosci mapy            |
| <code>ANON</code>   | 12    | liczba calkowita, kod typu dla wartosci obiektow anonimowych |
| <code>WAIF</code>   | 13    | liczba calkowita, kod typu dla wartosci WAIF            |
| <code>BOOL</code>   | 14    | liczba calkowita, kod typu dla wartosci bool            |
| <code>true</code>   | true  | wartosc logiczna prawda                                 |
| <code>false</code>  | false | wartosc logiczna falsz                                  |

> Uwaga: warto tu wspomniec o funkcji `typeof`, opisanej w sekcji o funkcjach wbudowanych.

Dla innych, ogolne znaczenie wartosci jest spojne, choc sama wartosc rozni sie w zaleznosci od sytuacji:

| Zmienna              | Wartosc                                                                                                                                                                                                   |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <code>player</code> | obiekt, gracz, ktory wpisal polecenie inicjujace zadanie, w ramach ktorego wykonywany jest ten fragment kodu.                                                                                            |
| <code>this</code>   | obiekt, obiekt, na ktorym znaleziono aktualnie wykonywany czasownik.                                                                                                                                     |
| <code>caller</code> | obiekt, obiekt, na ktorym znaleziono czasownik, ktory wywolal aktualnie wykonywany czasownik. Dla pierwszego czasownika wywolanego dla danego polecenia, <code>caller</code> ma taka sama wartosc jak <code>player</code>. |
| <code>verb</code>   | string, nazwa, pod ktora zidentyfikowano aktualnie wykonywany czasownik.                                                                                                                                  |
| <code>args</code>   | lista, argumenty przekazane temu czasownikowi. Dla pierwszego czasownika wywolanego dla danego polecenia jest to lista stringow, slow z linii polecenia.                                                 |

Reszta tzw. "wbudowanych" zmiennych ma realne znaczenie tylko dla pierwszego czasownika wywolanego dla danego polecenia. Ich semantyka jest podana w omowieniu parsowania polecen, powyzej.

Aby zmienic wartosc przechowywana w zmiennej, uzyj wyrazenia _przypisania_ (assignment):

```
zmienna = wyrazenie
```

Na przyklad, by zmienic zmienna o nazwie `x` na wartosc 17, napisalbys `x = 17` jako wyrazenie. Wyrazenie przypisania robi dwie rzeczy:

* zmienia wartosc nazwanej zmiennej
* zwraca nowa wartosc tej zmiennej

Tak wiec wyrazenie

```
13 + (x = 17)
```

zmienia wartosc `x` na 17 i zwraca 30.

#### Operatory arytmetyczne

Wszystkie zwykle proste operacje na liczbach sa dostepne dla programow MOO:

```
+
-
*
/
%
```

Sa to, w kolejnosci: dodawanie, odejmowanie, mnozenie, dzielenie i reszta z dzielenia. W ponizszej tabeli wyrazenia po lewej maja odpowiadajace im wartosci po prawej:

```
5 + 2       =>   7
5 - 2       =>   3
5 * 2       =>   10
5 / 2       =>   2
5.0 / 2.0   =>   2.5
5 % 2       =>   1
5.0 % 2.0   =>   1.0
5 % -2      =>   1
-5 % 2      =>   -1
-5 % -2     =>   -1
-(5 + 2)    =>   -7
```

Zauwaz, ze dzielenie calkowite w MOO odrzuca reszte i ze wynik operatora reszty (`%`) ma taki sam znak jak lewy operand. Zauwaz tez, ze `-` moze byc uzyty bez lewego operandu, by zanegowac wyrazenie liczbowe.

Subtelny szczegol: liczby calkowite i zmiennoprzecinkowe nie moga byc mieszane w zadnym konkretnym uzyciu tych operatorow arytmetycznych; w odroznieniu od niektorych innych jezykow programowania, MOO nie konwertuje automatycznie liczb calkowitych na zmiennoprzecinkowe. Mozesz uzyc funkcji `tofloat()`, by wykonac jawna konwersje.

Operator `+` moze byc tez uzyty do laczenia dwoch stringow. Wyrazenie

`"foo" + "bar"`

ma wartosc `"foobar"`

Operator `+` moze byc tez uzyty do laczenia dwoch list. Wyrazenie

```
{1, 2, 3} + {4, 5, 6}
```

ma wartosc `{1, 2, 3, 4, 5, 6}`

Operator `+` moze byc tez uzyty, by dopisac cos do listy. Wyrazenie

```
{1, 2} + #123
```

ma wartosc `{1, 2, #123}`

Jesli oba operandy operatora arytmetycznego nie sa liczbami tego samego rodzaju (lub, dla `+`, oba stringami), zglaszana jest wartosc bledu `E_TYPE`. Jesli prawy operand dla operatora dzielenia lub reszty (`/` lub `%`) wynosi zero, zglaszana jest wartosc bledu `E_DIV`.

MOO obsluguje takze operacje potegowania, znana rowniez jako "podnoszenie do potegi", za pomoca operatora `^`:

```
3 ^ 4       =>   81
3 ^ 4.5     blad-->   E_TYPE
3.5 ^ 4     =>   150.0625
3.5 ^ 4.5   =>   280.741230801382
```

> Uwaga: jesli pierwszy operand jest liczba calkowita, wtedy drugi operand rowniez musi byc liczba calkowita. Jesli pierwszy operand jest liczba zmiennoprzecinkowa, drugi operand moze byc dowolnego rodzaju. Choc formalnie dozwolone jest podniesienie liczby calkowitej do potegi ujemnej, jest to malo prawdopodobnie przydatne.

#### Operatory bitowe

MOO obsluguje takze operacje bitowe na typach calkowitych:

| Operator | Znaczenie                              |
| -------- | ------------------------------------ |
| &.       | bitowe `and` (i)                     |
| \|.      | bitowe `or` (lub)                    |
| ^.       | bitowe `xor`                         |
| >>       | logiczne (nie arytmetyczne) przesuniecie w prawo |
| <<       | logiczne (nie arytmetyczne) przesuniecie w lewo  |
| ~        | dopelnienie (complement)             |

W ponizszej tabeli wyrazenia po lewej maja odpowiadajace im wartosci po prawej:

```
1 &. 2       =>  0
1 |. 2       =>  3
1 ^. 3       =>  1
8 << 1       =>  16
8 >> 1       =>  4
~0           =>  -1
```

Po wiecej informacji o operatorach bitowych zobacz strone [Wikipedii](https://en.wikipedia.org/wiki/Bitwise_operation) na ich temat.

#### Porownywanie wartosci

Dowolne dwie wartosci mozna porownac pod katem rownosci, uzywajac `==` i `!=`. Pierwszy z nich zwraca 1, jesli obie wartosci sa rowne, a 0 w przeciwnym razie; drugi dziala odwrotnie:

```
3 == 4                              =>  0
3 != 4                              =>  1
3 == 3.0                            =>  0
"foo" == "Foo"                      =>  1
#34 != #34                          =>  0
{1, #34, "foo"} == {1, #34, "FoO"}  =>  1
E_DIV == E_TYPE                     =>  0
3 != "foo"                          =>  1
[1 -> 2] == [1 -> 2]                =>  1
[1 -> 2] == [2 -> 1]                =>  0
true == true                        =>  1
false == true                       =>  0
```

Zauwaz, ze liczby calkowite i zmiennoprzecinkowe nigdy nie sa sobie rowne, nawet w _oczywistych_ przypadkach. Zauwaz tez, ze porownanie stringow (i wartosci list zawierajacych stringi) nie rozroznia wielkosci liter (case-insensitive); to znaczy nie odroznia wielkiej i malej litery. Aby przetestowac dwie wartosci pod katem rownosci z rozroznianiem wielkosci liter, uzyj funkcji `equal`, opisanej pozniej.

> Ostrzezenie: latwo (i bardzo irytujaco) pomylic operator testowania rownosci (`==`) z operatorem przypisania (`=`), co prowadzi do paskudnych, trudnych do znalezienia bledow. Nie rob tego.

> Ostrzezenie: porownywanie liczb zmiennoprzecinkowych pod katem rownosci moze byc trudne. Czasem dwie liczby zmiennoprzecinkowe wygladaja tak samo, ale sa zaokraglone w gore lub w dol na jakims znaczacym bicie, i przez to nie beda dokladnie rowne. Jest to szczegolnie prawdziwe przy porownywaniu liczby w pamieci (przypisanej do zmiennej) z liczba powstala z odczytu wartosci od gracza lub pobrana z wlasciwosci. Badz tego swiadomy, jesli kiedykolwiek sie z tym spotkasz, bo moze to byc meczace do debugowania.

Liczby calkowite, zmiennoprzecinkowe, numery obiektow, stringi i wartosci bledow moga byc tez porownywane pod katem uporzadkowania, uzywajac nastepujacych operatorow:

| Operator | Znaczenie                           |
| -------- | --------------------------------- |
| &lt;     | oznacza "mniejsze niz"     |
| &lt;=    | "mniejsze lub rowne"    |
| &gt;=    | "wieksze lub rowne" |
| &gt;     | "wieksze niz"          |

Podobnie jak operatory rownosci, zwracaja 1, gdy ich operandy sa w odpowiedniej relacji, a 0 w przeciwnym razie:

```
3 < 4           =>  1
3 < 4.0         =>  E_TYPE (blad)
#34 >= #32      =>  1
"foo" <= "Boo"  =>  0
E_DIV > E_TYPE  =>  1
```

Zauwaz, ze podobnie jak w przypadku operatorow rownosci, stringi sa porownywane bez rozroznienia wielkosci liter. Aby wykonac porownanie stringow z rozroznieniem wielkosci liter, uzyj funkcji `strcmp`, opisanej pozniej. Zauwaz tez, ze wartosci bledow sa uporzadkowane tak, jak podano w tabeli w sekcji o wartosciach. Jesli operandy tych czterech operatorow porownania sa roznych typow (nawet liczby calkowite i zmiennoprzecinkowe sa uznawane za rozne typy), lub sa listami, zglaszany jest `E_TYPE`.

#### Wartosci jako prawda i falsz

W MOO istnieje pojecie wartosci _prawdziwej_ (true) i _falszywej_ (false); kazda wartosc jest jedna lub druga. Wartosci prawdziwe sa nastepujace:

* wszystkie liczby calkowite inne niz zero (dodatnie lub ujemne)
* wszystkie liczby zmiennoprzecinkowe rozne od `0.0`
* wszystkie niepuste stringi (tj. inne niz `""`)
* wszystkie niepuste listy (tj. inne niz `{}`)
* wszystkie niepuste mapy (tj. inne niz `[]`)
* bool 'true'

Wszystkie pozostale wartosci sa falszywe:

* liczba calkowita zero
* liczby zmiennoprzecinkowe `0.0` i `-0.0`
* pusty string (`""`)
* pusta lista (`{}`)
* wszystkie numery obiektow i referencje do obiektow
* wszystkie wartosci bledow
* bool 'false'

> Uwaga: obiekty sa uznawane za falszywe. Jesli potrzebujesz ocenic, czy wartosc jest typu object, mozesz uzyc `typeof(potencjalny_obiekt) == OBJ`, jednak pamietaj, ze to nie oznacza, ze obiekt, do ktorego sie odwolujesz, faktycznie istnieje. Np.: #100000000 zwroci prawde, ale to nie znaczy, ze taki obiekt istnieje w Twoim MOO.

> Uwaga: nie mylmy wartosci ewaluujacych do prawdy lub falszu z wartosciami logicznymi `true` i `false`.

Istnieja cztery rodzaje wyrazen i dwa rodzaje instrukcji, ktore zaleza od tej klasyfikacji wartosci MOO. Opisujac je, czasami odwoluje sie do _wartosci logicznej_ (truth value) wartosci MOO; jest to po prostu _prawda_ lub _falsz_, kategoria, do ktorej ta wartosc MOO zostaje zaklasyfikowana.

Wyrazenie warunkowe w MOO ma nastepujaca forme:

```
wyrazenie-1 ? wyrazenie-2 | wyrazenie-3
```

> Uwaga: jest to powszechnie nazywane instrukcja trojargumentowa (ternary) w wiekszosci jezykow programowania. W MOO powszechnie uzywany znak ! jest zastapiony przez |.

Najpierw ewaluowane jest wyrazenie-1. Jesli zwraca wartosc prawdziwa, wtedy ewaluowane jest wyrazenie-2 i to, co zwraca, jest zwracane jako wartosc calego wyrazenia warunkowego. Jesli wyrazenie-1 zwraca wartosc falszywa, wtedy zamiast tego ewaluowane jest wyrazenie-3 i jego wartosc jest uzywana jako wartosc wyrazenia warunkowego.

```
1 ? 2 | 3           =>  2
0 ? 2 | 3           =>  3
"foo" ? 17 | {#34}  =>  17
```

Zauwaz, ze ewaluowane jest tylko jedno z wyrazen wyrazenie-2 i wyrazenie-3, nigdy oba.

Aby zanegowac wartosc logiczna wartosci MOO, uzyj operatora `!`:

```
! wyrazenie
```

Jesli wartosc wyrazenia jest prawdziwa, `!` zwraca 0; w przeciwnym razie zwraca 1:

```
! "foo"     =>  0
! (3 >= 4)  =>  1
```

> Uwaga: operator "negacji" lub "not" jest powszechnie nazywany "bang" we wspolczesnym zargonie.

Czesto przydatne jest sprawdzenie wiecej niz jednego warunku, by zobaczyc, czy niektore lub wszystkie z nich sa prawdziwe. MOO udostepnia do tego dwa operatory:

```
wyrazenie-1 && wyrazenie-2
wyrazenie-1 || wyrazenie-2
```

Te operatory sa zwykle czytane odpowiednio jako "i" (and) oraz "lub" (or).

Operator `&&` najpierw ewaluuje wyrazenie-1. Jesli zwraca wartosc prawdziwa, wtedy ewaluowane jest wyrazenie-2 i jego wartosc staje sie wartoscia calego wyrazenia `&&`; w przeciwnym razie jako wartosc wyrazenia `&&` uzywana jest wartosc wyrazenia-1.

> Uwaga: wyrazenie-2 jest ewaluowane tylko wtedy, gdy wyrazenie-1 zwraca wartosc prawdziwa.

Wyrazenie `&&` jest rownowazne wyrazeniu warunkowemu:

```
wyrazenie-1 ? wyrazenie-2 | wyrazenie-1
```

z tym ze wyrazenie-1 jest ewaluowane tylko raz.

Operator `||` dziala podobnie, z tym ze wyrazenie-2 jest ewaluowane tylko wtedy, gdy wyrazenie-1 zwraca wartosc falszywa. Jest rownowazny wyrazeniu warunkowemu:

```
wyrazenie-1 ? wyrazenie-1 | wyrazenie-2
```

z tym ze, podobnie jak w `&&`, wyrazenie-1 jest ewaluowane tylko raz.

Te dwa operatory zachowuja sie bardzo podobnie do "i" oraz "lub" w jezyku naturalnym:

```
1 && 1                  =>  1
0 && 1                  =>  0
0 && 0                  =>  0
1 || 1                  =>  1
0 || 1                  =>  1
0 || 0                  =>  0
17 <= 23  &&  23 <= 27  =>  1
```

#### Indeksowanie list, map i stringow

Stringi, listy i mapy mozna postrzegac jako uporzadkowane sekwencje wartosci MOO. W przypadku stringow, kazdy jest sekwencja jednoznakowych stringow; to znaczy string `"bar"` mozna widziec jako sekwencje stringow `"b"`, `"a"` i `"r"`. MOO pozwala odwolywac sie do elementow list, map i stringow po numerze, po _indeksie_ tego elementu na liscie lub w stringu. Pierwszy element ma indeks 1, drugi ma indeks 2, i tak dalej.

> Ostrzezenie: bardzo wazne jest, by zauwazyc, ze w odroznieniu od wielu jezykow programowania (ktore uzywaja 0 jako indeksu poczatkowego), MOO uzywa 1.

##### Wyciaganie elementu po indeksie

Wyrazenie indeksujace w MOO wyciaga wskazany element z listy, mapy lub stringa:

```
wyrazenie-1[wyrazenie-2]
```

Najpierw ewaluowane jest wyrazenie-1; musi zwrocic liste, mape lub string (_sekwencje_). Nastepnie ewaluowane jest wyrazenie-2 i musi zwrocic liczbe calkowita (_indeks_) lub _klucz_ w przypadku map. Jesli ktores z wyrazen zwroci inny typ wartosci, zwracany jest `E_TYPE`.

Dla list i stringow indeks musi zawierac sie miedzy 1 a dlugoscia sekwencji, wlacznie; jesli nie, zglaszany jest `E_RANGE`. Wartoscia wyrazenia indeksujacego jest element o danym indeksie w sekwencji. Dla map klucz musi byc obecny, jesli nie jest, zglaszany jest E_RANGE. Wewnatrz wyrazenia-2 mozesz uzyc symbolu ^ jako wyrazenia zwracajacego indeks lub klucz pierwszego elementu w sekwencji, a symbolu $ jako wyrazenia zwracajacego indeks lub klucz ostatniego elementu w wyrazeniu-1.

```
"fob"[2]                =>  "o"
[1 -> "A"][1]           =>  "A"
"fob"[1]                =>  "f"
{#12, #23, #34}[$ - 1]  =>  #23
```

Zauwaz, ze nie ma prawidlowych indeksow dla pustego stringa lub pustej listy, poniewaz nie ma liczb calkowitych miedzy 1 a 0 (dlugoscia pustego stringa lub listy).

Subtelny szczegol: wyrazenia ^ i $ zwracaja pierwszy/ostatni indeks/klucz wyrazenia znajdujacego sie bezposrednio przed najblizej otaczajacym je nawiasem indeksujacym lub zakresowym [...]. Na przyklad:

```
"frob"[{3, 2, 4}[^]]     =>  "o"
"frob"[{3, 2, 4}[$]]     =>  "b"
```

jest mozliwe, poniewaz $ w tym przypadku reprezentuje 3. indeks listy obok niego, co daje wartosc 4, ktora z kolei jest stosowana jako indeks do stringa, co daje "b".

##### Zastepowanie elementu listy, mapy lub stringa

Czesto zdarza sie, ze chcemy zmienic tylko jeden konkretny slot listy lub stringa, przechowywany w zmiennej lub wlasciwosci. Mozna to wygodnie zrobic uzywajac _przypisania indeksowanego_ (indexed assignment) majacego jedna z nastepujacych form:

```
zmienna[wyr-indeksu] = wyr-wyniku
wyr-obiektu.nazwa[wyr-indeksu] = wyr-wyniku
wyr-obiektu.(wyr-nazwy)[wyr-indeksu] = wyr-wyniku
$nazwa[wyr-indeksu] = wyr-wyniku
```

Pierwsza forma zapisuje do zmiennej, a trzy ostatnie zapisuja do wlasciwosci. Zwykle bledy (`E_TYPE`, `E_INVIND`, `E_PROPNF` i `E_PERM` przy braku uprawnien odczytu/zapisu do wlasciwosci) moga zostac zgloszone, dokladnie tak jak przy odczycie i zapisie dowolnej wlasciwosci obiektu; zobacz omowienie wyrazen wlasciwosci obiektu ponizej po szczegoly.

Odpowiednio, jesli zmienna nie ma jeszcze wartosci (tj. nigdy nie zostala jej przypisana), zglaszany bedzie `E_VARNF`.

Jesli wyr-indeksu nie jest liczba calkowita (dla list i stringow) lub jest wartoscia kolekcji (dla map), lub jesli wartosc `zmiennej` lub wlasciwosci nie jest lista, mapa ani stringiem, zglaszany jest `E_TYPE`. Jesli `wyr-wyniku` jest stringiem, ale nie dlugosci 1, zglaszany jest E_INVARG. Zalozmy, ze `wyr-indeksu` ewaluuje do wartosci `k`. Jesli `k` jest liczba calkowita i jest poza zakresem listy lub stringa (tj. mniejsza niz 1 lub wieksza niz dlugosc listy lub stringa), zglaszany jest `E_RANGE`. Jesli `k` nie jest prawidlowym kluczem mapy, zglaszany jest `E_RANGE`. W przeciwnym razie nastepuje faktyczne przypisanie.

Dla list zmiennej lub wlasciwosci przypisywana jest nowa lista, identyczna z oryginalna z wyjatkiem k-tej pozycji, gdzie nowa lista zawiera wynik wyr-wyniku zamiast poprzedniej wartosci. Podobnie dla map, zmiennej lub wlasciwosci przypisywana jest nowa mapa, identyczna z oryginalna z wyjatkiem klucza k, gdzie nowa mapa zawiera wynik wyr-wyniku zamiast poprzedniej wartosci. Dla stringow zmiennej lub wlasciwosci przypisywany jest nowy string, identyczny z oryginalnym, z wyjatkiem k-tego znaku, ktory jest zmieniany na wyr-wyniku.

Samo wyrazenie przypisania zwraca wartosc wyr-wyniku. W ponizszych przykladach zalozmy, ze `l` poczatkowo zawiera liste `{1, 2, 3}`, ze `m` poczatkowo zawiera mape `["one" -> 1, "two" -> 2]`, a `s` poczatkowo zawiera string "foobar":

```
l[5] = 3          =>   E_RANGE (blad)
l["first"] = 4    =>   E_TYPE  (blad)
s[3] = "baz"      =>   E_INVARG (blad)
l[2] = l[2] + 3   =>   5
l                 =>   {1, 5, 3}
l[2] = "foo"      =>   "foo"
l                 =>   {1, "foo", 3}
s[2] = "u"        =>   "u"
s                 =>   "fuobar"
s[$] = "z"        =>   "z"
s                 =>   "fuobaz"
m                 =>   ["foo" -> "bar"]
m[1] = "baz"      =>   ["foo" -> "baz"]
```

> Uwaga: (blad) sluzy w tych przykladach wylacznie do celow formatowania i identyfikacji, i nie jest obecne w rzeczywistym zglaszanym bledzie w MOO.

> Uwaga: wyrazenie `$` moze byc rowniez uzyte w przypisaniach indeksowanych z tym samym znaczeniem co wczesniej.

Subtelny szczegol: po przypisaniu indeksowanym zmienna lub wlasciwosc zawiera _nowa_ liste lub string, kopie oryginalnej listy we wszystkich miejscach poza n-tym, gdzie zawiera nowa wartosc. W zargonie programistycznym oryginalna lista nie jest mutowana i nie wystepuje aliasing. (Istotnie, zadna wartosc MOO nie jest mutowalna i aliasing nigdy nie wystepuje.)

W przypadku list i map przypisanie indeksowane moze byc zagniezdzone na wielu poziomach, by dzialac na zagniezdzonych listach i mapach. Zalozmy, ze `l` poczatkowo zawiera nastepujaca wartosc

```
{{1, 2, 3}, {4, 5, 6}, "foo", ["bar" -> "baz"]}
```

w nastepujacych przykladach:

```
l[7] = 4             =>   E_RANGE (blad)
l[1][8] = 35         =>   E_RANGE (blad)
l[3][2] = 7          =>   E_TYPE (blad)
l[1][1][1] = 3       =>   E_TYPE (blad)
l[2][2] = -l[2][2]   =>   -5
l                    =>   {{1, 2, 3}, {4, -5, 6}, "foo", ["bar" -> "baz"]}
l[2] = "bar"         =>   "bar"
l                    =>   {{1, 2, 3}, "bar", "foo", ["bar" -> "baz"]}
l[2][$] = "z"        =>   "z"
l                    =>   {{1, 2, 3}, "baz", "foo", ["bar" -> "baz"]}
l[$][^] = #3         =>   #3
l                    =>   {{1, 2, 3}, "baz", "foo", ["bar" -> #3]}
```

Pierwsze dwa przyklady zglaszaja E_RANGE, poniewaz 7 jest poza zakresem `l`, a 8 jest poza zakresem `l[1]`. Kolejne dwa przyklady zglaszaja `E_TYPE`, poniewaz `l[3]` i `l[1][1]` nie sa listami.

##### Wyciaganie podsekwencji listy, mapy lub stringa

Wyrazenie zakresowe wyciaga wskazana podsekwencje z listy, mapy lub stringa:

```
wyrazenie-1[wyrazenie-2..wyrazenie-3]
```

Trzy wyrazenia sa ewaluowane po kolei. Wyrazenie-1 musi zwrocic liste, mape lub string (_sekwencje_), a pozostale dwa wyrazenia musza zwrocic liczby calkowite (indeksy _dolny_ i _gorny_, odpowiednio) dla list i stringow, lub wartosci nie bedace kolekcja (klucze `begin` i `end` w uporzadkowanej mapie, odpowiednio) dla map; w przeciwnym razie zglaszany jest `E_TYPE`. Wyrazenia `^` i `$` moga byc uzyte w wyrazeniu-2 i/lub wyrazeniu-3, tak jak wczesniej.

Jesli dolny indeks jest wiekszy niz gorny, zwracany jest pusty string, lista lub mapa, w zaleznosci od tego, czy sekwencja jest stringiem, lista czy mapa. W przeciwnym razie oba indeksy musza zawierac sie miedzy 1 a dlugoscia sekwencji (dla list lub stringow) lub byc prawidlowymi kluczami (dla map); jesli nie, zglaszany jest `E_RANGE`. Zwracana jest nowa lista, mapa lub string, zawierajaca tylko elementy sekwencji o indeksach miedzy dolna/gorna granica.

```
"foobar"[2..$]                       =>  "oobar"
"foobar"[3..3]                       =>  "o"
"foobar"[17..12]                     =>  ""
{"one", "two", "three"}[$ - 1..$]    =>  {"two", "three"}
{"one", "two", "three"}[3..3]        =>  {"three"}
{"one", "two", "three"}[17..12]      =>  {}
[1 -> "one", 2 -> "two"][1..1]       =>  [1 -> "one"]
```

##### Zastepowanie podsekwencji listy, mapy lub stringa

Przypisanie zakresowe (subrange assignment) zastepuje wskazana podsekwencje listy, mapy lub stringa dostarczona podsekwencja. Dozwolone formy to:

```
zmienna[wyr-indeksu-poczatkowego..wyr-indeksu-koncowego] = wyr-wyniku
wyr-obiektu.nazwa[wyr-indeksu-poczatkowego..wyr-indeksu-koncowego] = wyr-wyniku
wyr-obiektu.(wyr-nazwy)[wyr-indeksu-poczatkowego..wyr-indeksu-koncowego] = wyr-wyniku
$nazwa[wyr-indeksu-poczatkowego..wyr-indeksu-koncowego] = wyr-wyniku
```

Podobnie jak w przypisaniach indeksowanych, pierwsza forma zapisuje do zmiennej, a trzy ostatnie zapisuja do wlasciwosci. Te same bledy (`E_TYPE`, `E_INVIND`, `E_PROPNF` i `E_PERM` przy braku uprawnien odczytu/zapisu do wlasciwosci) moga zostac zgloszone. Jesli zmienna nie ma jeszcze wartosci (tj. nigdy nie zostala jej przypisana), zglaszany bedzie `E_VARNF`. Podobnie jak wczesniej, wyrazenia `^` i `$` moga byc uzyte zarowno w wyr-indeksu-poczatkowego, jak i wyr-indeksu-koncowego.

Jesli wyr-indeksu-poczatkowego lub wyr-indeksu-koncowego nie jest liczba calkowita (dla list i stringow) ani wartoscia kolekcji (dla map), jesli wartosc zmiennej lub wlasciwosci nie jest lista, mapa ani stringiem, lub wyr-wyniku nie jest tego samego typu co zmienna lub wlasciwosc, zglaszany jest `E_TYPE`. Dla list i stringow zglaszany jest `E_RANGE`, jesli wyr-indeksu-koncowego jest mniejsze niz zero lub jesli wyr-indeksu-poczatkowego jest wieksze niz dlugosc listy lub stringa plus jeden. Uwaga: dlugosc wyr-wyniku nie musi byc taka sama jak dlugosc wskazanego zakresu. Dla map zglaszany jest `E_RANGE`, jesli `wyr-indeksu-poczatkowego` lub `wyr-indeksu-koncowego` nie sa kluczami w mapie.

W scislych terminach przypisanie zakresowe

```
v[start..end] = wartosc
```

jest rownowazne

```
v = {@v[1..start - 1], @wartosc, @v[end + 1..$]}
```

jesli v jest lista, oraz

```
v = v[1..start - 1] + wartosc + v[end + 1..$]
```

jesli v jest stringiem.

Nie ma literalnej reprezentacji tej operacji, jesli v jest mapa. W tym przypadku zakres wskazany przez wyr-indeksu-poczatkowego i wyr-indeksu-koncowego jest usuwany, a wartosci z wyr-wyniku sa dodawane.

Samo wyrazenie przypisania zwraca wartosc wyr-wyniku.

> Uwaga: uzycie symbolu @ poprzedzajacego liste zostanie omowione za chwile.

W ponizszych przykladach zalozmy, ze `l` poczatkowo zawiera liste `{1, 2, 3}`, ze `m` poczatkowo zawiera mape [1 -> "one", 2 -> "two", 3 -> "three"], a `s` poczatkowo zawiera string "foobar":

```
l[5..6] = {7, 8}       =>   E_RANGE (blad)
l[2..3] = 4            =>   E_TYPE (blad)
l[#2..3] = {7}         =>   E_TYPE (blad)
s[2..3] = {6}          =>   E_TYPE (blad)
l[2..3] = {6, 7, 8, 9} =>   {6, 7, 8, 9}
l                      =>   {1, 6, 7, 8, 9}
l[2..1] = {10, "foo"}  =>   {10, "foo"}
l                      =>   {1, 10, "foo", 6, 7, 8, 9}
l[3][2..$] = "u"       =>   "u"
l                      =>   {1, 10, "fu", 6, 7, 8, 9}
s[7..12] = "baz"       =>   "baz"
s                      =>   "foobarbaz"
s[1..3] = "fu"         =>   "fu"
s                      =>   "fubarbaz"
s[1..0] = "test"       =>   "test"
s                      =>   "testfubarbaz"
m[1..2] = ["abc" -> #1]=>   ["abc" -> #1]
m                      =>   [3 -> "three", "abc" -> #1]
```

#### Inne operacje na listach

Jak wspomniano wczesniej, listy mozna konstruowac, pisac sekwencje wyrazen oddzielonych przecinkami wewnatrz nawiasow klamrowych:

```
{wyrazenie-1, wyrazenie-2, ..., wyrazenie-N}
```

Wynikowa lista ma wartosc wyrazenia-1 jako pierwszy element, wartosc wyrazenia-2 jako drugi, itd.

```
{3 < 4, 3 <= 4, 3 >= 4, 3 > 4}  =>  {1, 1, 0, 0}
```

Operator dodawania dziala z listami. Przy dodawaniu dwoch list do siebie, obie zostana polaczone (concatenated):

```
{1, 2, 3} + {4, 5, 6} => {1, 2, 3, 4, 5, 6}
```

Przy dodaniu innego typu do listy, ta wartosc zostanie dopisana na koniec listy:

```
{1, 2} + #123 => {1, 2, #123}
```

Dodatkowo, dowolne z tych wyrazen mozna poprzedzic operatorem "rozpryskiwania" (splicing), `@`. Takie wyrazenie musi zwrocic liste; zamiast tego, by stara lista sama w sobie stala sie elementem nowej listy, wszystkie elementy starej listy zostaja wlaczone do nowej listy. To pojecie jest latwe do zrozumienia, ale trudne do wyjasnienia slowami, wiec oto kilka przykladow. Dla tych przykladow zalozmy, ze zmienna `a` ma wartosc `{2, 3, 4}`, a `b` ma wartosc `{"Foo", "Bar"}`:

```
{1, a, 5}   =>  {1, {2, 3, 4}, 5}
{1, @a, 5}  =>  {1, 2, 3, 4, 5}
{a, @a}     =>  {{2, 3, 4}, 2, 3, 4}
{@a, @b}    =>  {2, 3, 4, "Foo", "Bar"}
```

Jesli operator rozpryskiwania (`@`) poprzedza wyrazenie, ktorego wartosc nie jest lista, zglaszany jest `E_TYPE` jako wartosc calej konstrukcji listy.

Wyrazenie przynaleznosci do listy (list membership) sprawdza, czy dana wartosc MOO jest elementem danej listy, a jesli tak, to pod jakim indeksem:

```
wyrazenie-1 in wyrazenie-2
```

Wyrazenie-2 musi zwrocic liste; w przeciwnym razie zglaszany jest `E_TYPE`. Jesli wartosc wyrazenia-1 znajduje sie na tej liscie, zwracany jest indeks jej pierwszego wystapienia na liscie; w przeciwnym razie wyrazenie `in` zwraca 0.

```
2 in {5, 8, 2, 3}               =>  3
7 in {5, 8, 2, 3}               =>  0
"bar" in {"Foo", "Bar", "Baz"}  =>  2
```

Zauwaz, ze operator przynaleznosci do listy nie rozroznia wielkosci liter przy porownywaniu stringow, podobnie jak operatory porownania. Aby wykonac test przynaleznosci do listy z rozroznieniem wielkosci liter, uzyj funkcji `is_member`, opisanej pozniej. Zauwaz tez, ze poniewaz zwraca zero tylko wtedy, gdy danej wartosci nie ma na danej liscie, wyrazenia `in` mozna uzyc zarowno jako testu przynaleznosci, jak i lokalizatora elementu.

#### Rozpraszanie elementow listy miedzy zmienne

W programowaniu MOO czesto zdarza sie, ze chcesz uzyskac dostep do poszczegolnych elementow listy, kazdy przechowywany w osobnej zmiennej. Taka potrzeba pojawia sie na przyklad na poczatku niemal kazdego czasownika MOO, poniewaz argumenty wszystkich czasownikow sa dostarczane razem, zebrane w jedna liste. W takich okolicznosciach _mozna by_ napisac instrukcje takie jak te:

```
first = args[1];
second = args[2];
if (length(args) > 2)
  third = args[3];
else
  third = 0;
endif
```

Takie podejscie staje sie dosc meczace, zarowno do czytania, jak i pisania, i jest podatne na bledy, jesli pomylisz jeden z indeksow. Czesto tez chcesz sprawdzic, czy byly obecne jakiekolwiek _dodatkowe_ elementy listy, co dodaje uciazliwosci.

MOO udostepnia specjalny rodzaj wyrazenia przypisania, zwany _przypisaniem rozpraszajacym_ (scattering assignment), stworzony wlasnie na takie przypadki. Wyrazenie przypisania rozpraszajacego wyglada tak:

```
{cel, ...} = wyr
```

gdzie kazdy cel opisuje miejsce do przechowania elementow listy wynikajacej z ewaluacji wyr. Cel ma jedna z nastepujacych form:

| Cel                                    | Opis                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <code>zmienna</code>                 | To najprostszy cel, po prostu zwykla zmienna; element listy na odpowiadajacej pozycji jest przypisywany do zmiennej. Nazywany jest celem <em>wymaganym</em> (required), poniewaz przypisanie jest wymagane, by wlozyc jeden z elementow listy do zmiennej. |
| <code>?zmienna</code>                | Nazywany jest celem <em>opcjonalnym</em> (optional), poniewaz nie zawsze otrzymuje przypisany element. Jesli po uwzglednieniu wszystkich wymaganych celow (wraz ze wszystkimi innymi opcjonalnymi na lewo od tego) pozostana jakiekolwiek elementy listy, ta zmienna jest traktowana jak wymagana i element listy na odpowiadajacej pozycji jest jej przypisywany. Jesli nie ma wystarczajaco elementow, by przypisac jeden do tego celu, do tej zmiennej nie jest dokonywane zadne przypisanie, pozostawiajac ja z jakakolwiek poprzednia wartoscia. |
| <code>?zmienna = wyr-domyslne</code> | To rowniez cel opcjonalny, ale jesli nie ma wystarczajaco elementow listy, by przypisac jeden do tego celu, zamiast tego przypisywany jest wynik ewaluacji wyr-domyslne. Tak wiec wyr-domyslne dostarcza <em>wartosc domyslna</em> dla zmiennej. Wyrazenia wartosci domyslnych sa ewaluowane i przypisywane od lewej do prawej <em>po</em> wykonaniu wszystkich innych przypisan. |
| <code>@zmienna</code>                | Przez analogie do skladni <code>@</code> w konstrukcji listy, tej zmiennej przypisywana jest lista wszystkich 'pozostalych' elementow listy w tej czesci listy, po wypelnieniu wszystkich innych celow. Przypisywana jest pusta lista, jesli nie zostaly zadne elementy. Nazywany jest celem <em>reszty</em> (rest), poniewaz otrzymuje reszte elementow. W kazdym wyrazeniu przypisania rozpraszajacego moze byc co najwyzej jeden cel reszty. |

Jesli nie ma wystarczajaco elementow listy, by wypelnic wszystkie wymagane cele, lub jesli jest ich wiecej niz wystarczajaco, by wypelnic wszystkie wymagane i opcjonalne cele, ale nie ma celu reszty, ktory przyjalby pozostale, zglaszany jest `E_ARGS`.

Oto kilka przykladow tego, jak to dziala. Zalozmy najpierw, ze czasownik `me:foo()` zawiera nastepujacy kod:

```
b = c = e = 17;
{a, ?b, ?c = 8, @d, ?e = 9, f} = args;
return {a, b, c, d, e, f};
```

Wtedy nastepujace wywolania zwracaja podane wartosci:

```
me:foo(1)                        =>   E_ARGS (blad)
me:foo(1, 2)                     =>   {1, 17, 8, {}, 9, 2}
me:foo(1, 2, 3)                  =>   {1, 2, 8, {}, 9, 3}
me:foo(1, 2, 3, 4)               =>   {1, 2, 3, {}, 9, 4}
me:foo(1, 2, 3, 4, 5)            =>   {1, 2, 3, {}, 4, 5}
me:foo(1, 2, 3, 4, 5, 6)         =>   {1, 2, 3, {4}, 5, 6}
me:foo(1, 2, 3, 4, 5, 6, 7)      =>   {1, 2, 3, {4, 5}, 6, 7}
me:foo(1, 2, 3, 4, 5, 6, 7, 8)   =>   {1, 2, 3, {4, 5, 6}, 7, 8}
```

Uzywajac przypisania rozpraszajacego, przyklad z poczatku tej sekcji mozna przepisac prosciej, bardziej niezawodnie i czytelniej:

```
{first, second, ?third = 0} = args;
```

Subtelny szczegol: jesli znasz JavaScript, funkcjonalnosc 'rest' i 'spread' powinna wygladac znajomo. Dobrym stylem programowania w MOO jest uzywanie przypisania rozpraszajacego na poczatku niemal kazdego czasownika (przynajmniej tych typu 'this none this'), poniewaz jasno pokazuje, jakich argumentow czasownik oczekuje.

#### Operacje na BOOL-ach

ToastStunt oferuje typ `bool`. Ten typ moze byc albo `true`, uznawane za `1`, albo `false`, uznawane za `0`. Wartosci logiczne mozna ustawiac w swoim kodzie/wlasciwosciach w bardzo podobny sposob jak kazda inna wartosc moze byc przypisana do zmiennej lub wlasciwosci.

```
;true                   => true
;false                  => false
;true == true           => 1
;false == false         => 1
;true == false          => 0
;1 == true              => 1
;5 == true              => 0
;0 == false             => 1
;-1 == false            => 0
!true                   => 0
!false                  => 1
!false == true          => 1
!true == false          => 1
```

Zmienne true i false sa ustawiane przy starcie zadania (lub przez Twoj kod) i moga byc nadpisane w czasownikach w razie potrzeby. Nie przetrwa to jednak po zakonczeniu wykonywania czasownika.

> Subtelny szczegol: jak wspomniano wczesniej, istnieja stale, jak STR, ktore rozwiazuja sie do kodu calkowitego 2. OBJ rozwiazuje sie do kodu calkowitego 1. Tak wiec, gdybys wykonal kod taki jak `typeof(#15840) == TRUE`, otrzymalbys odpowiedz prawdziwa, poniewaz typeof() zwrociloby `1`, oznaczajace kod calkowity typu object. Jest to efekt uboczny tego, ze `true` zawsze rowna sie 1, z powodow zgodnosci wstecznej.

#### Odczytywanie i ustawianie wartosci wlasciwosci

Zazwyczaj mozna odczytac wartosc wlasciwosci na obiekcie prostym wyrazeniem:

```
wyrazenie.nazwa
```

Wyrazenie musi zwrocic numer obiektu; jesli nie, zglaszany jest `E_TYPE`. Jesli obiekt o tym numerze nie istnieje, zglaszany jest `E_INVIND`. W przeciwnym razie, jesli obiekt nie ma wlasciwosci o tej nazwie, zglaszany jest `E_PROPNF`. W przeciwnym razie, jesli nazwana wlasciwosc nie jest czytelna dla wlasciciela biezacego czasownika, zglaszany jest `E_PERM`. Wreszcie, zakladajac, ze nic z tych okropnych rzeczy sie nie wydarzylo, zwracana jest wartosc nazwanej wlasciwosci na danym obiekcie.

Napisalam "zazwyczaj" w powyzszym akapicie, poniewaz to proste wyrazenie dziala tylko wtedy, gdy nazwa wlasciwosci przestrzega tych samych zasad, co nazwy zmiennych (tj. sklada sie wylacznie z liter, cyfr i podkreslen i nie zaczyna sie od cyfry). Nazwy wlasciwosci nie sa jednak ograniczone do tego zbioru. Czasem tez przydatne jest ustalenie, ktora wlasciwosc odczytac, na podstawie jakiegos obliczenia. Do tych bardziej ogolnych zastosowan dozwolona jest tez nastepujaca skladnia:

```
wyrazenie-1.(wyrazenie-2)
```

Podobnie jak wczesniej, wyrazenie-1 musi zwrocic numer obiektu. Wyrazenie-2 musi zwrocic string, nazwe wlasciwosci do odczytania; w przeciwnym razie zglaszany jest `E_TYPE`. Uzywajac tej skladni, mozna odczytac dowolna wlasciwosc, niezaleznie od jej nazwy.

Zauwaz, ze podobnie jak niemal wszystko w MOO, wielkosc liter nie ma znaczenia w nazwach wlasciwosci. Tak wiec nastepujace wyrazenia sa rownowazne:

```
foo.bar
foo.Bar
foo.("bAr")
```

Baza danych ToastCore uzywa kilku wlasciwosci na `#0`, _obiekcie systemowym_, do rozmaitych specjalnych celow. Na przyklad wartoscia `#0.room` jest obiekt "generycznego pokoju", `#0.exit` to obiekt "generycznego wyjscia", itd. Pozwala to programom MOO odwolywac sie do tych przydatnych obiektow latwiej (i czytelniej) niz uzywajac bezposrednio ich numerow obiektow. Aby to uzycie bylo jeszcze latwiejsze i czytelniejsze, wyrazenie

```
$nazwa
```

(gdzie nazwa przestrzega zasad nazw zmiennych) jest skrotem dla

```
#0.nazwa
```

Tak wiec, na przyklad, wspomniana wczesniej wartosc `$nothing` to naprawde `#-1`, wartosc `#0.nothing`.

Podobnie jak w przypadku zmiennych, uzywa sie operatora przypisania (`=`), by zmienic wartosc wlasciwosci. Na przyklad wyrazenie

```
14 + (#27.foo = 17)
```

zmienia wartosc wlasciwosci `foo` obiektu o numerze 27 na 17, a nastepnie zwraca 31. Przypisania do wlasciwosci sprawdzaja, czy wlasciciel biezacego czasownika ma uprawnienia zapisu do danej wlasciwosci, zglaszajac w przeciwnym razie `E_PERM`. Uprawnienia odczytu nie sa wymagane.

#### Wywolywanie funkcji wbudowanych i innych czasownikow

MOO udostepnia duza liczbe przydatnych funkcji do wykonywania szerokiej gamy operacji; pelna lista, podajaca ich nazwy, argumenty i semantyke, pojawia sie w osobnej sekcji pozniej. Jako przyklad, by dac Ci wyobrazenie, istnieje funkcja o nazwie `length`, ktora zwraca dlugosc danego stringa, listy lub mapy.

Skladnia wywolania funkcji jest nastepujaca:

```
nazwa(wyr-1, wyr-2, ..., wyr-N)
```

gdzie nazwa to nazwa jednej z funkcji wbudowanych. Wyrazenia miedzy nawiasami, zwane _argumentami_, sa kazde ewaluowane po kolei, a nastepnie przekazywane nazwanej funkcji, by wykorzystala je w odpowiedni sposob. Wiekszosc funkcji wymaga podania okreslonej liczby argumentow; w przeciwnym razie zglaszany jest `E_ARGS`. Wiekszosc wymaga tez, by pewne argumenty mialy okreslone typy (np. funkcja `length()` wymaga jako argumentu stringa, listy lub mapy); zglaszany jest `E_TYPE`, jesli ktorykolwiek argument ma zly typ.

Podobnie jak w konstrukcji list, operator rozpryskiwania `@` moze poprzedzac dowolne wyrazenie argumentu. Wartosc takiego wyrazenia musi byc lista; w przeciwnym razie zglaszany jest `E_TYPE`. Elementy tej listy sa przekazywane jako pojedyncze argumenty, zamiast calej listy naraz.

Czasowniki moga tez wywolywac inne czasowniki, zwykle uzywajac tej skladni:

```
wyr-0:nazwa(wyr-1, wyr-2, ..., wyr-N)
```

Wyr-0 musi zwrocic numer obiektu; w przeciwnym razie zglaszany jest `E_TYPE`. Jesli obiekt o tym numerze nie istnieje, zglaszany jest `E_INVIND`. Jesli to zadanie jest zbyt gleboko zagniezdzone w czasownikach wywolujacych czasowniki wywolujace czasowniki, zglaszany jest `E_MAXREC`; domyslny limit to 50 poziomow, ale mozna to zmienic z poziomu bazy danych; zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly. Jesli ani obiekt, ani zaden z jego przodkow nie definiuje czasownika pasujacego do podanej nazwy, zglaszany jest `E_VERBNF`. W przeciwnym razie, jesli nic z tych przykrych rzeczy sie nie wydarzy, wywolywany jest nazwany czasownik na danym obiekcie; rozne wbudowane zmienne maja nastepujace wartosci poczatkowe w wywolywanym czasowniku:

| Zmienna              | Opis                                                                                                                                                                              |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <code>this</code>   | obiekt, wartosc wyr-0                                                                                                                                                              |
| <code>verb</code>   | string, nazwa uzyta przy wywolaniu tego czasownika                                                                                                                                 |
| <code>args</code>   | lista, wartosci wyr-1, wyr-2, itd.                                                                                                                                                 |
| <code>caller</code> | obiekt, wartosc <code>this</code> w wywolujacym czasowniku                                                                                                                         |
| <code>player</code> | obiekt, ta sama wartosc, jaka mial poczatkowo w wywolujacym czasowniku lub, jesli wywolujacy czasownik dziala z uprawnieniami czarodzieja, ta sama co biezaca wartosc w wywolujacym czasowniku. |

Wszystkie inne wbudowane zmienne (`argstr`, `dobj`, itd.) sa inicjalizowane tymi samymi wartosciami, jakie maja w wywolujacym czasowniku.

Podobnie jak w omowieniu referencji do wlasciwosci powyzej, napisalam "zwykle" na poczatku poprzedniego akapitu, poniewaz ta skladnia jest dozwolona tylko wtedy, gdy nazwa przestrzega zasad dozwolonych nazw zmiennych. Rowniez podobnie jak przy referencji do wlasciwosci, istnieje skladnia pozwalajaca obliczyc nazwe czasownika:

```
wyr-0:(wyr-00)(wyr-1, wyr-2, ..., wyr-N)
```

Wyrazenie wyr-00 musi zwrocic string; w przeciwnym razie zglaszany jest `E_TYPE`.

Operator rozpryskiwania (`@`) moze byc uzyty tez z argumentami wywolania czasownika, dokladnie tak jak z argumentami funkcji wbudowanych.

W wielu bazach danych szereg waznych czasownikow jest zdefiniowanych na `#0`, _obiekcie systemowym_. Podobnie jak notacja `$foo` dla wlasciwosci na `#0`, serwer definiuje specjalna skladnie do wywolywania czasownikow na `#0`:

```
$nazwa(wyr-1, wyr-2, ..., wyr-N)
```

(gdzie nazwa przestrzega zasad nazw zmiennych) jest skrotem dla

```
#0:nazwa(wyr-1, wyr-2, ..., wyr-N)
```

#### Wywolania czasownikow na typach prymitywnych

Serwer obsluguje wywolania czasownikow na typach prymitywnych (liczby, stringi, itd.), wiec wywolania takie jak `"foo bar":split()` moga byc zaimplementowane i dzialac zgodnie z oczekiwaniami (byly zawsze skladniowo poprawne w LambdaMOO, ale skutkowaly bledem E_TYPE). Czasowniki sa implementowane na obiektach-delegatach prototypow ($int_proto, $float_proto, $str_proto, itd.). Serwer w przezroczysty sposob wywoluje odpowiedni czasownik na wlasciwym prototypie -- wartosc prymitywna jest wartoscia `this`.

Obejmuje to takze mozliwosc wywolywania czasownikow na prototypie obiektu ($obj_proto). Wbrew intuicji, zadziala to wylacznie dla wartosci typu OBJ, ktore sa nieprawidlowe (invalid). Moze to byc przydatne dla niezalogowanych polaczen (tj. tworzenie zestawu wygodnych narzedzi do obslugi ujemnych polaczen wewnatrz MOO).

> Subtelny szczegol: korzystanie z czasownikow na prymitywach to kwestia stylu. Niektorym sie podoba, innym nie. Autor sugeruje, by trzymac obiekt narzedziowy (jak $string_utils) i po prostu przekazywac wywolania czasownikow z prymitywu do tego narzedzia, co zachowuje zgodnosc wsteczna ze sposobem, w jaki generalnie zbudowane sa ToastCore i LambdaCore. Domyslnie w ToastCore prymitywy po prostu opakowuja odpowiedniki `typ`_utils.

#### Przechwytywanie bledow w wyrazeniach

Czesto przydatne jest, by moc _przechwycic_ (catch) blad zglaszany przez wyrazenie, aby zapobiec przerwaniu calego zadania przez ten blad i kontynuowac dzialanie tak, jakby wyrazenie normalnie zwrocilo jakas inna wartosc. Nastepujace wyrazenie to umozliwia:

```
` wyr-1 ! kody => wyr-2 '
```

> Uwaga: otwierajacy i zamykajacy znak cudzyslowu w poprzedniej linii sa faktycznie czescia skladni; musisz je rzeczywiscie wpisac jako czesc swojego programu MOO dla tego rodzaju wyrazenia.

Czesc kody to albo slowo kluczowe `ANY`, albo lista wyrazen oddzielonych przecinkami, dokladnie jak lista argumentow. Podobnie jak w liscie argumentow, mozna tu uzyc operatora rozpryskiwania (`@`). Czesc `=> wyr-2` wyrazenia przechwytujacego bledy jest opcjonalna.

Najpierw ewaluowana jest czesc kody, dajac liste kodow bledow, ktore powinny zostac przechwycone, jesli zostana zgloszone; jesli kody to `ANY`, jest to rownowazne liscie wszystkich mozliwych wartosci MOO.

Nastepnie ewaluowane jest wyr-1. Jesli ewaluuje sie normalnie, bez zgloszenia bledu, jego wartosc staje sie wartoscia calego wyrazenia przechwytujacego bledy. Jesli ewaluacja wyr-1 skutkuje zgloszeniem bledu, nazwijmy ten blad E. Jesli E znajduje sie na liscie wynikajacej z ewaluacji kody, wtedy E jest uznawany za _przechwycony_ przez to wyrazenie przechwytujace bledy. W takim przypadku, jesli podano wyr-2, jest ono ewaluowane, by uzyskac wynik calego wyrazenia przechwytujacego bledy; jesli wyr-2 zostalo pominiete, wtedy E staje sie wartoscia calego wyrazenia. Jesli E _nie_ znajduje sie na liscie wynikajacej z kody, wtedy to wyrazenie w ogole nie przechwytuje bledu i jest on nadal zglaszany, mozliwe ze do przechwycenia przez jakis fragment kodu otaczajacy to wyrazenie lub wyzej na stosie wywolan czasownikow.

Oto kilka przykladow uzycia tego rodzaju wyrazenia:

```
`x + 1 ! E_TYPE => 0'
```

Zwraca `x + 1`, jesli `x` jest liczba calkowita, zwraca `0`, jesli `x` nie jest liczba calkowita, i zglasza `E_VARNF`, jesli `x` nie ma wartosci.

```
`x.y ! E_PROPNF, E_PERM => 17'
```

Zwraca `x.y`, jesli to nie powoduje bledu, `17`, jesli `x` nie ma wlasciwosci `y` lub ta wlasciwosc nie jest czytelna, i zglasza jakis inny rodzaj bledu (jak `E_INVIND`), jesli `x.y` go powoduje.

```
`1 / 0 ! ANY'
```

Zwraca `E_DIV`.

> Uwaga: warto wspomniec, jak potezna moze byc ta zwiezla skladnia do pisania kodu przechwytujacego bledy. Uzywana odpowiednio pozwala pisac bardzo zlozony i elegancki kod. Wyobraz sobie na przyklad, ze masz zestaw obiektow o roznych rodzicach, z ktorych niektore definiuja konkretny czasownik, a niektore nie. Jesli na przyklad Twoj kod chce wykonac jakas funkcje _jesli_ czasownik istnieje, mozesz napisac `obj:verbname() ! E_VERBNF'`, by pozwolic MOO probowac wykonac ten czasownik, a nastepnie, jesli sie to nie uda, przechwycic blad i kontynuowac normalne dzialanie.

#### Nawiasy i priorytet operatorow

Jak pokazano w kilku przykladach powyzej, MOO pozwala uzywac nawiasow, by jasno wskazac, jak zamierzasz pogrupowac zlozone wyrazenia. Na przyklad wyrazenie

```
3 * (4 + 5)
```

wykonuje dodawanie 4 i 5 przed pomnozeniem wyniku przez 3.

Jesli pominiesz nawiasy, MOO ustali, jak pogrupowac wyrazenie zgodnie z pewnymi regulami. Pierwsza z nich jest to, ze niektore operatory maja wyzszy _priorytet_ niz inne; operatory o wyzszym priorytecie beda mocniej wiazac sie ze swoimi operandami niz te o nizszym priorytecie. Na przyklad mnozenie ma wyzszy priorytet niz dodawanie; tak wiec, gdyby pominieto nawiasy w wyrazeniu z poprzedniego akapitu, MOO zgrupowaloby je nastepujaco:

```
(3 * 4) + 5
```

Ponizsza tabela podaje wzgledny priorytet wszystkich operatorow MOO; operatory na wyzszych liniach tabeli maja wyzszy priorytet, a te na tej samej linii maja identyczny priorytet:

```
!       - (bez lewego operandu)
^
*       /       %
+       -
==      !=      <       <=      >       >=      in
&&      ||
... ? ... | ... (wyrazenie warunkowe)
=
```

Tak wiec straszliwe wyrazenie

```
x = a < b && c > d + e * f ? w in y | - q - r
```

zostaloby zgrupowane nastepujaco:

```
x = (((a < b) && (c > (d + (e * f)))) ? (w in y) | ((- q) - r))
```

Najlepiej jest utrzymywac wyrazenia prostsze niz to i uzywac nawiasow hojnie, by wyjasnic swoje intencje innym ludziom.

### Instrukcje jezyka MOO

Instrukcje to konstrukcje MOO, ktore, w przeciwienstwie do wyrazen, wykonuja jakas uzyteczna operacje niegenerujaca wartosci. Na przyklad istnieje kilka rodzajow instrukcji, zwanych _konstrukcjami petli_, ktore wielokrotnie wykonuja jakis zestaw operacji. Na szczescie w MOO jest znacznie mniej rodzajow instrukcji niz rodzajow wyrazen.

#### Bledy podczas wykonywania instrukcji

Instrukcje nie zwracaja wartosci, ale niektore ich rodzaje moga, w pewnych opisanych nizej okolicznosciach, generowac bledy. Jesli taki blad zostanie wygenerowany w czasowniku, ktorego bit `d` (debug) nie jest ustawiony, blad jest ignorowany, a instrukcja, ktora go wygenerowala, jest po prostu pomijana; wykonanie przechodzi do nastepnej instrukcji.

> Uwaga: to zachowanie ignorujace bledy jest bardzo podatne na bledy, poniewaz dotyczy _wszystkich_ bledow, w tym takich, ktorych programista mogl nie przewidziec. Bit `d` istnieje wylacznie z powodow historycznych; kiedys byl jedynym sposobem, by programisci MOO mogli przechwytywac i obslugiwac bledy. Wyrazenie przechwytujace bledy oraz instrukcja `try`-`except` sa znacznie lepszymi sposobami osiagniecia tego samego celu.

Jesli bit `d` jest ustawiony, jak zwykle bywa, blad jest _zglaszany_ i moze zostac przechwycony i obsluzony albo przez kod otaczajacy dane wyrazenie, albo przez czasowniki wyzej w lancuchu wywolan prowadzacym do biezacego czasownika. Jesli blad nie zostanie przechwycony, serwer przerywa cale zadanie i, domyslnie, wypisuje komunikat biezacemu graczowi. Zobacz opisy wyrazenia przechwytujacego bledy oraz instrukcji `try`-`except` po szczegoly przechwytywania bledow, a takze rozdzial o zalozeniach serwera wobec bazy danych po szczegoly obslugi nieprzechwyconych bledow.

#### Proste instrukcje

Najprostszym rodzajem instrukcji jest instrukcja _pusta_, skladajaca sie z samego srednika:

```
;
```

Nie robi absolutnie nic, ale robi to bardzo szybko.

Nastepna najprostsza instrukcja jest jednoczesnie jedna z najczestszych: instrukcja wyrazenia, skladajaca sie z jakiegokolwiek wyrazenia zakonczonego srednikiem:

```
wyrazenie;
```

Podane wyrazenie jest ewaluowane, a wynikowa wartosc jest ignorowana. Powszechnie uzywane rodzaje wyrazen dla takich instrukcji to przypisania i wywolania czasownikow. Oczywiscie taka instrukcja nie ma sensu, jesli ewaluacja wyrazenia nie ma jakiegos efektu ubocznego, na przyklad zmiany wartosci jakiejs zmiennej lub wlasciwosci, wypisania jakiegos tekstu na ekranie kogos itd.

```
#42.weight = 40;
#42.weight;
2 + 5;
obj:verbname();
1 > 2;
2 < 1;
```

#### Instrukcje sprawdzania warunkow

Instrukcja `if` pozwala zdecydowac, czy wykonac jakies instrukcje na podstawie wartosci dowolnego wyrazenia:

```
if (wyrazenie)
  instrukcje
endif
```

Wyrazenie jest ewaluowane i, jesli zwraca wartosc prawdziwa, instrukcje sa wykonywane po kolei; w przeciwnym razie nic wiecej sie nie dzieje.

Czesto chce sie wykonac jeden zestaw instrukcji, jesli jakis warunek jest prawdziwy, a inny zestaw w przeciwnym przypadku. Opcjonalna fraza `else` w instrukcji `if` pozwala to zrobic:

```
if (wyrazenie)
  instrukcje-1
else
  instrukcje-2
endif
```

Ta instrukcja jest wykonywana tak jak poprzednia, z tym ze instrukcje-1 sa wykonywane, jesli wyrazenie zwraca wartosc prawdziwa, a instrukcje-2 sa wykonywane w przeciwnym razie.

Czasami trzeba sprawdzic kilka warunkow w rodzaju zagniezdzenia:

```
if (wyrazenie-1)
  instrukcje-1
else
  if (wyrazenie-2)
    instrukcje-2
  else
    if (wyrazenie-3)
      instrukcje-3
    else
      instrukcje-4
    endif
  endif
endif
```

Taki kod moze latwo stac sie meczacy do pisania i trudny do odczytania. MOO udostepnia troche prostsza notacje dla takich przypadkow:

```
if (wyrazenie-1)
  instrukcje-1
elseif (wyrazenie-2)
  instrukcje-2
elseif (wyrazenie-3)
  instrukcje-3
else
  instrukcje-4
endif
```

Zauwaz, ze `elseif` pisze sie jako jedno slowo, bez spacji. Ta prostsza wersja ma dokladnie takie samo znaczenie jak oryginalna: ewaluuj po kolei wyrazenie-i dla i rownego 1, 2 i 3, dopoki jedno z nich nie zwroci wartosci prawdziwej; nastepnie wykonaj instrukcje-i powiazane z tym wyrazeniem. Jesli zadne z wyrazenie-i nie zwroci wartosci prawdziwej, wykonaj instrukcje-4.

Moze wystapic dowolna liczba fraz `elseif`, kazda w tej postaci:

```
elseif (wyrazenie)
    instrukcje
```

Kompletna skladnia instrukcji `if` wyglada zatem tak:

```
if (wyrazenie)
  instrukcje
zero-lub-wiecej-fraz-elseif
opcjonalna-fraza-else
endif
```

#### Instrukcje petli

MOO udostepnia trzy rozne rodzaje instrukcji petli, pozwalajace wykonac zestaw instrukcji (1) raz dla kazdego elementu podanej sekwencji (listy, mapy lub ciagu znakow); (2) raz dla kazdej liczby calkowitej lub numeru obiektu w podanym zakresie; oraz (3) w kolko, dopoki podany warunek pozostaje prawdziwy.

Aby wykonac jakies instrukcje raz dla kazdego elementu podanej sekwencji, uzyj tej skladni:

```
for wartosc, klucz-lub-indeks in (wyrazenie)
  instrukcje
endfor
```

Wyrazenie jest ewaluowane i powinno zwracac liste, mape lub ciag znakow; jesli tego nie robi, zglaszany jest `E_TYPE`. Instrukcje sa nastepnie wykonywane raz dla kazdego elementu tej sekwencji po kolei; kazdorazowo podana wartosc otrzymuje wartosc danego elementu, a klucz-lub-indeks otrzymuje indeks wartosci na liscie lub w ciagu znakow, albo jej klucz, jesli sekwencja jest mapa. klucz-lub-indeks jest opcjonalny. Rozwaz na przyklad nastepujace instrukcje:

```
nieparzyste = {1, 3, 5, 7, 9};
parzyste = {};
for n in (nieparzyste)
  parzyste = {@parzyste, n + 1};
endfor
```

Wartoscia zmiennej `parzyste` po wykonaniu tych instrukcji jest lista

`{2, 4, 6, 8, 10}`

Jesli zmodyfikowac przyklad:

```
nieparzyste = {1, 3, 5, 7, 9};
pary = [];
for n, i in (nieparzyste)
  pary[i] = n + 1;
endfor
```

Wartoscia zmiennej `pary` po wykonaniu tych instrukcji jest mapa

`[1 -> 2, 2 -> 4, 3 -> 6, 4 -> 8, 5 -> 10]`

Aby wykonac zestaw instrukcji raz dla kazdej liczby calkowitej lub numeru obiektu w podanym zakresie, uzyj tej skladni:

```
for zmienna in [wyrazenie-1..wyrazenie-2]
  instrukcje
endfor
```

Oba wyrazenia sa ewaluowane po kolei i powinny zwracac albo obie liczby calkowite, albo obie numery obiektow; w przeciwnym razie zglaszany jest `E_TYPE`. Instrukcje sa nastepnie wykonywane raz dla kazdej liczby calkowitej (lub numeru obiektu, odpowiednio) wiekszej lub rownej wartosci wyrazenie-1 i mniejszej lub rownej wynikowi wyrazenie-2, w porzadku rosnacym. Kazdorazowo podana zmienna otrzymuje dana liczbe calkowita lub numer obiektu. Rozwaz na przyklad nastepujace instrukcje:

```
parzyste = {};
for n in [1..5]
  parzyste = {@parzyste, 2 * n};
endfor
```

Wartoscia zmiennej `parzyste` po wykonaniu tych instrukcji jest, tak jak w poprzednim przykladzie, lista

`{2, 4, 6, 8, 10}`

Nastepujaca petla po numerach obiektow wypisuje numer i nazwe kazdego prawidlowego obiektu w bazie danych:

```
for o in [#0..max_object()]
  if (valid(o))
    notify(player, tostr(o, ": ", o.name));
  endif
endfor
```

Ostatni rodzaj petli w MOO wykonuje zestaw instrukcji wielokrotnie, dopoki podany warunek pozostaje prawdziwy:

```
while (wyrazenie)
  instrukcje
endwhile
```

Wyrazenie jest ewaluowane i, jesli zwraca wartosc prawdziwa, instrukcje sa wykonywane; nastepnie wykonanie instrukcji `while` zaczyna sie od nowa od ewaluacji wyrazenia. To znaczy, ze wykonanie przechodzi na przemian miedzy ewaluowaniem wyrazenia i wykonywaniem instrukcji, dopoki wyrazenie nie zwroci wartosci falszywej. Nastepujacy przykladowy kod ma dokladnie ten sam efekt, co petla pokazana wyzej:

```
parzyste = {};
n = 1;
while (n <= 5)
  parzyste = {@parzyste, 2 * n};
  n = n + 1;
endwhile
```

Subtelnosc: mozna rowniez nadac _nazwe_ petli `while`.

```
while nazwa (wyrazenie)
  instrukcje
endwhile
```

co ma dokladnie taki sam efekt jak

```
while (nazwa = wyrazenie)
  instrukcje
endwhile
```

Ta mozliwosc nazywania jest naprawde uzyteczna tylko w polaczeniu z instrukcjami `break` i `continue`, opisanymi w nastepnej sekcji.

W przypadku kazdego rodzaju petli mozliwe jest, ze instrukcje w ciele petli nigdy sie nie wykonaja. Dla iteracji po listach zdarza sie to, gdy lista zwrocona przez wyrazenie jest pusta. Dla iteracji po liczbach calkowitych zdarza sie to, gdy wyrazenie-1 zwraca liczbe wieksza niz wyrazenie-2. Wreszcie dla petli `while` zdarza sie to, jesli wyrazenie zwroci wartosc falszywa juz przy pierwszej ewaluacji.

> Ostrzezenie: w przypadku petli `while` szczegolnie wazne jest, by nie stworzyc nieskonczonej petli. Czyli petli, ktora nigdy sie nie zakonczy, poniewaz jej wyrazenie nigdy nie stanie sie falszywe. Badz szczegolnie ostrozny, jesli wywolujesz suspend(), yin() lub $command_utils:suspend_if_needed() wewnatrz petli, poniewaz zadaniu moga nigdy nie skonczyc sie ticki.

#### Przerywanie jednej lub wszystkich iteracji petli

Czasami przydaje sie wyjscie z petli przed zakonczeniem wszystkich jej iteracji. Na przyklad, jesli petla sluzy do wyszukania konkretnego rodzaju elementu listy, moze miec sens przerwanie iterowania, jak tylko znaleziony zostanie wlasciwy rodzaj elementu, nawet jesli zostaly jeszcze elementy do sprawdzenia. Do tego celu sluzy instrukcja `break`; ma ona postac

```
break;
```

lub

```
break nazwa;
```

Kazda instrukcja `break` wskazuje na konkretna otaczajaca petle; jesli nazwa nie jest podana, instrukcja odnosi sie do najbardziej wewnetrznej petli. Jesli jest podana, nazwa musi byc nazwa wystepujaca zaraz po slowie kluczowym `for` lub `while` danej otaczajacej petli. Gdy instrukcja `break` jest wykonywana, wskazana petla jest natychmiast przerywana, a wykonanie kontynuuje sie tak, jakby petla normalnie zakonczyla swoje iteracje.

MOO pozwala rowniez przerwac tylko biezaca iteracje petli, powodujac natychmiastowe przejscie do nastepnej, jesli taka istnieje. Do tego sluzy instrukcja `continue`; ma ona dokladnie takie same postacie jak instrukcja `break`:

```
continue;
```

lub

```
continue nazwa;
```

Przyklad sumujacy liste liczb calkowitych, wykluczajac kazda liczbe calkowita rowna czterem:

```
moja_lista = {1, 2, 3, 4, 5, 6, 7};
suma = 0;
for element in (moja_lista)
    if (element == 4)
        continue;
    endif
    suma = suma + element;
endfor
```

Przyklad przerywajacy petle, gdy zostanie znaleziony konkretny obiekt na liscie:

```
moja_lista = {#13633, #98, #15840, #18657, #22664};
i = 0;
znaleziono = 0;
for obj in (moja_lista)
    i = i + 1;
    if (obj == #18657)
        znaleziono = 1;
        break;
    endif
endfor
if (znaleziono)
    notify(player, tostr("znaleziono #18657 na pozycji ", i));
else
    notify(player, "nie udalo sie znalezc #18657 na liscie!");
endif
```

#### Zwracanie wartosci z czasownika

Program MOO w czasowniku jest po prostu sekwencja instrukcji. Zwykle, gdy czasownik jest wywolywany, te instrukcje sa po prostu wykonywane po kolei, a nastepnie liczba calkowita 0 jest zwracana jako wartosc wywolania czasownika. Uzywajac instrukcji `return`, mozna zmienic to zachowanie. Instrukcja `return` ma jedna z dwoch postaci:

```
return;
```

lub

```
return wyrazenie;
```

Gdy jest wykonywana, wykonanie biezacego czasownika zostaje natychmiast zakonczone, po wczesniejszej ewaluacji podanego wyrazenia, jesli takie podano. Wywolanie czasownika, ktore zainicjowalo wykonanie tego czasownika, zwraca wtedy albo wartosc wyrazenia, albo liczbe calkowita 0, jesli nie podano zadnego wyrazenia.

Mozemy zmodyfikowac podany wczesniej przyklad. Wyobraz sobie czasownik zwany has_object, ktory przyjmuje jako pierwszy argument obiekt (ktorego chcemy znalezc), a jako drugi liste obiektow (do przeszukania):

```
{szukany_obj, lista_obiektow} = args;
for obj in (lista_obiektow)
    if (obj == szukany_obj)
        return 1;
    endif
endfor
```

Powyzszy czasownik moglby zostac wywolany jako `obj_z_czasownikiem:has_object(#18657, {#1, #3, #4, #3000})` i zwrocilby `falsz` (0), jesli obiekt nie zostalby znaleziony na liscie. Zwrocilby `prawde` (1), jesli obiekt zostalby znaleziony na liscie.

Oczywiscie moglibysmy napisac to znacznie prosciej (i uzyskac przy tym indeks obiektu na liscie):

```
{szukany_obj, lista_obiektow} = args;
return szukany_obj in lista_obiektow;
```

#### Obsluga bledow w instrukcjach

Traceback jest zglaszany, gdy podczas wykonania kodu wystapi blad (rozni sie to od bledu kompilacji, ktory moze wystapic podczas programowania czasownika).

Przyklady powodujace traceback:

```
;notify(5)

#-1:Input to EVAL (this == #-1), line 3:  Incorrect number of arguments (expected 2-4; got 1)
... called from built-in function eval()
... called from #58:eval_cmd_string, line 19
... called from #58:eval*-d, line 13
(End of traceback)
```

I kolejny przyklad:
```
;notify(me, 5)

#-1:Input to EVAL (this == #-1), line 3:  Type mismatch (args[1] of notify() expected object; got integer)
... called from built-in function eval()
... called from #58:eval_cmd_string, line 19
... called from #58:eval*-d, line 13
(End of traceback)
```

Jak widac w przykladach powyzej, ToastStunt poda numer linii bledu, a takze dodatkowe informacje o bledzie, w tym oczekiwana liczbe argumentow i typ. Bedzie to rowniez dzialac przy przechwytywaniu bledow w instrukcji try/except (opisanej nizej).

Dodatkowo pokazane zostanie {object, verb / property name}, jesli sprobujesz uzyskac dostep do czasownika lub wlasciwosci, ktorej nie znaleziono.

Zwykle, kiedy jakikolwiek fragment kodu MOO zglosi blad, cale zadanie jest przerywane, a uzytkownikowi wypisywany jest komunikat. Czesto takie bledy moga zostac przewidziane z wyprzedzeniem przez programiste, a kod moze zostac napisany tak, by radzil sobie z nimi w bardziej elegancki sposob. Instrukcja `try`-`except` pozwala to zrobic; jej skladnia jest nastepujaca:

```
try
  instrukcje-0
except zmienna-1 (kody-1)
  instrukcje-1
except zmienna-2 (kody-2)
  instrukcje-2
...
endtry
```

gdzie zmienne moga zostac pominiete, a kazda czesc kody jest albo slowem kluczowym `ANY`, albo lista wyrazen rozdzielonych przecinkami, tak jak w liscie argumentow. Podobnie jak w liscie argumentow, mozna tu uzyc operatora rozpraszania (`@`). Moze wystapic od 1 do 255 klauzul `except`.

Najpierw kazda czesc kody jest ewaluowana, dajac liste kodow bledow, ktore powinny zostac przechwycone, jesli zostana zgloszone; jesli kody to `ANY`, jest to rownowazne liscie wszystkich mozliwych wartosci MOO.

Nastepnie wykonywane sa instrukcje-0; jesli nie zglaszaja bledu, to jest wszystko, co sie dzieje w calej instrukcji `try`-`except`. W przeciwnym razie, niech E oznacza blad, ktory zostal zgloszony. Od gory do dolu, E jest wyszukiwany na listach wynikajacych z kolejnych czesci kody; jesli nie zostanie znaleziony na zadnej z nich, kontynuuje zglaszanie, mozliwe, ze zostanie przechwycony przez jakis fragment kodu otaczajacy te instrukcje `try`-`except` albo wyzej na stosie wywolan czasownikow.

Jesli E zostanie znalezione najpierw w kody-i, zmiennej-i (jesli podano) przypisywana jest wartosc zawierajaca informacje o zglaszanym bledzie, a instrukcje-i sa wykonywane. Wartosc przypisywana zmiennej-i jest lista czterech elementow:

```
{kod, komunikat, wartosc, traceback}
```

gdzie kod to E, zglaszany blad, komunikat i wartosc sa dostarczane przez kod, ktory zglosil blad, a traceback jest lista taka jak ta zwracana przez funkcje `callers()`, wraz z numerami linii. Lista traceback zawiera wpisy dla kazdego czasownika, od tego, ktory zglosil blad, do tego, ktory zawiera te instrukcje `try`-`except`.

Jesli nie wspomniano inaczej, wszystkie wbudowane bledy zglaszane przez wyrazenia, instrukcje i funkcje dostarczaja `tostr(kod)` jako komunikat i zero jako wartosc.

Przyklad uzycia tej instrukcji:

```
try
  wynik = object:(command)(@arguments);
  player:tell("=> ", toliteral(wynik));
except v (ANY)
  tb = v[4];
  if (length(tb) == 1)
    player:tell("** Nieprawidlowe polecenie: ", v[2]);
  else
    top = tb[1];
    tb[1..1] = {};
    player:tell(top[1], ":", top[2], ", linia ", top[6], ":", v[2]);
    for fr in (tb)
      player:tell("... wywolane z ", fr[1], ":", fr[2], ", linia ", fr[6]);
    endfor
    player:tell("(Koniec tracebacku)");
  endif
endtry
```

#### Czyszczenie po bledach

Kiedykolwiek zglaszany jest blad, zwykle zdarza sie, ze przynajmniej jakis kod MOO zostaje pominiety i nigdy wykonany. Czasami wazne jest, by pewny fragment kodu _zawsze_ zostal wykonany, niezaleznie od tego, czy zglaszany jest blad. Uzyj instrukcji `try`-`finally` w takich przypadkach; ma ona nastepujaca skladnie:

```
try
  instrukcje-1
finally
  instrukcje-2
endtry
```

Najpierw wykonywane sa instrukcje-1; jesli zakoncza sie bez zglaszania bledu, bez zwrocenia wartosci z czasownika i bez przerwania biezacej iteracji otaczajacej petli (nazywamy te mozliwosci _przekazywaniem kontroli_), wykonywane sa instrukcje-2 i to jest wszystko, co dzieje sie w calej instrukcji `try`-`finally`.

W przeciwnym razie proces przekazywania kontroli jest przerywany i wykonywane sa instrukcje-2. Jesli instrukcje-2 same nie przekazuja kontroli, przerwane przekazanie kontroli jest wznawiane wlasnie w miejscu, w ktorym zostalo przerwane. Jesli instrukcje-2 przekazuja kontrole, przerwane przekazanie jest po prostu zapominane na rzecz nowego.

Krotko mowiac, ta instrukcja zapewnia, ze instrukcje-2 zostana wykonane po tym, jak kontrola opusci instrukcje-1 z jakiegokolwiek powodu; moze byc wiec uzywana, by zapewnic, ze jakis fragment kodu czyszczacego zostanie wykonany, nawet jesli instrukcje-1 nie zakoncza sie po prostu normalnie.

Przyklad:

```
try
  start = time();
  object:(command)(@arguments);
finally
  koniec = time();
  this:charge_user_for_seconds(player, koniec - start);
endtry
```
> Ostrzezenie: jesli zadaniu skoncza sie ticki, mozliwe, ze twoj kod z finally nie zostanie wykonany.

#### Wykonywanie instrukcji w przyszlosci

Czasami przydatne jest, by jakas sekwencja instrukcji wykonala sie w przyszlosci, bez ludzkiej interwencji. Na przyklad mozna zaimplementowac obiekt, ktory, gdy zostanie wyrzucony w powietrze, w koncu spada z powrotem na ziemie; czasownik `throw` na tym obiekcie powinien zorganizowac wypisanie komunikatu o tym, ze obiekt ladowal na ziemi, ale komunikat nie powinien zostac wypisany, dopoki nie minie pewna liczba sekund.

Instrukcja `fork` jest przeznaczona wlasnie do takich sytuacji i ma nastepujaca skladnie:

```
fork (wyrazenie)
  instrukcje
endfork
```

Instrukcja `fork` najpierw wykonuje wyrazenie, ktore musi zwrocic liczbe calkowita lub zmiennoprzecinkowa; nazwijmy te wartosc n. Nastepnie tworzy nowe _zadanie_ MOO, ktore, po co najmniej n sekundach (lub czesciach sekundy w przypadku liczby zmiennoprzecinkowej, jak 0.1), wykona instrukcje. Gdy nowe zadanie zaczyna sie, wszystkie zmienne majcaja wartosci, jakie mialy w momencie wykonania instrukcji `fork`. Zadanie wykonujace instrukcje `fork` natychmiast kontynuuje wykonanie. Pojecie zadan jest szczegolowo omowione w nastepnej sekcji.

Domyslnie nie istnieje limit liczby zadan, jakie moze forkowac gracz, ale taki limit mozna wprowadzic z poziomu bazy danych. Zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly.

Czasami przydatna jest mozliwosc zabicia forkowanego zadania, zanim jeszcze sie zacznie; na przyklad jakis gracz mogl zlapac obiekt, ktory zostal wyrzucony w powietrze, wiec nie powinien zostac wypisany zaden komunikat o jego uderzeniu o ziemie. Jesli po slowie kluczowym `fork` podana jest nazwa zmiennej, w taki sposob:

```
fork nazwa (wyrazenie)
  instrukcje
endfork
```

to zmienna ta otrzymuje _identyfikator zadania_ nowo utworzonego zadania. Wartosc tej zmiennej jest widoczna zarowno dla zadania wykonujacego instrukcje fork, jak i dla instrukcji w nowo utworzonym zadaniu. Ten identyfikator moze zostac przekazany do funkcji `kill_task()`, by zapobiec wykonaniu zadania, i bedzie wartoscia `task_id()`, gdy zadanie zacznie sie wykonywac.

> Uwaga: ta funkcjonalnosc ma jeszcze inne zastosowania. MOO jest jednowatkowe (choc ToastStunt wspiera wykonywanie niektorych funkcji wbudowanych w innych watkach), co znaczy, ze zlozona logika (czasowniki wywolujace czasowniki wywolujace czasowniki...) moze powodowac, ze MOO zacznie _lagowac_. Na przyklad, powiedzmy, ze gdy gracz podrzuca swoja pilke, chcesz obliczyc zlozona trajektorie z udzialem pilki i innych obiektow w pokoju. Te obliczenia sa kosztowne i wykonywane w innym czasowniku, zajmuja czas. Chcesz jednak, by pewne akcje wykonaly sie zarowno przed obliczeniami (wszyscy w pokoju widza, ze pilka zostala wyrzucona w powietrze), jak i po tym, jak pilka opuscila rece gracza (gracz siega do kieszeni i wyciaga nowa pilke). Bez `fork()` obliczenia musialyby sie zakonczyc, zanim czasownik moglby kontynuowac wykonanie, co znaczy, ze gracz nie wyciagnie swiezej pilki, dopoki obliczenia sie nie zakoncza. `fork()` pozwala graczowi rzucic pilka, a MOO sforkowac zadanie, co pozwala wykonaniu czasownika kontynuowac natychmiast, a uzytkownikowi wyciagnac nowa pilke, bez doswiadczania zwlekania, ktore spowodowaloby zwrocenie wyniku obliczen (bez `fork()`).

Przyklad tego:

```
{pilka} = args;
player:tell("Rzucasz pilka!");
pilka:calculate_trajectory();
player:tell("Wyciagasz kolejna pilke!");
```

W powyzszym przykladzie `player:tell("Wyciagasz kolejna pilke!");` nie zostanie wykonane, dopoki `pilka:calculate_trajectory();` sie nie zakonczy.

```
{pilka} = args;
player:tell("Rzucasz pilka!");
fork (1)
    pilka:calculate_trajectory();
endfork
player:tell("Wyciagasz kolejna pilke!");
```

W tym sforkowanym przykladzie pilka zostanie rzucona, zadanie zostanie sforkowane na 1 sekunde pozniej, a ostatnia linia informujaca gracza, ze wyciagnal kolejna pilke, zostanie wykonana natychmiast, bez czekania na zakonczenie dzialania czasownika trajektorii.

Ten rodzaj forka nie moze zostac uzyty, jesli trajektoria jest wymagana przez kod wykonywany po nim. Na przyklad:

```
{pilka} = args;
player:tell("Rzucasz pilka!");
kierunek = pilka:calculate_trajectory();
player:tell("Wyciagasz kolejna pilke!");
player:tell("Twoja pilka lezy w kierunku " + kierunek);
```

Jesli powyzsze zadanie zostalo sforkowane w taki sposob, jak nizej:

```
{pilka} = args;
player:tell("Rzucasz pilka!");
fork (1)
    kierunek = pilka:calculate_trajectory();
endfork
player:tell("Wyciagasz kolejna pilke!");
player:tell("Twoja pilka lezy w kierunku " + kierunek);
```

Czasownik zglosilby `E_VARNF`, poniewaz kierunek nie jest zdefiniowany.

### Zadania MOO

_Zadanie_ (task) to wykonanie programu MOO. W ToastStunt istnieje piec rodzajow zadan:

* Kazdy raz, gdy gracz wpisuje polecenie, tworzone jest zadanie do jego wykonania; nazywamy je _zadaniami polecen_.
* Kiedy gracz laczy sie lub rozlacza z MOO, serwer uruchamia zadanie, by wykonac dowolne niezbedne przetwarzanie, na przyklad wypisanie `Munchkin polaczyl(a) sie` wszystkim graczom w tym samym pokoju; nazywamy je _zadaniami serwera_.
* Instrukcja `fork` w jezyku programowania tworzy zadanie, ktorego wykonanie jest odlozone o co najmniej podana liczbe sekund; nazywamy je _zadaniami forkowanymi_. Forkowanie na czesci sekundy jest mozliwe (np. 0.1)
* Funkcja `suspend()` zawiesza wykonanie biezacego zadania. Wykonywany jest zrzut calego stanu wykonania, a wykonanie zostanie wznowione pozniej. Nazywamy je _zadaniami zawieszonymi_. Zawieszanie na czesci sekundy jest mozliwe.
* Funkcja `read()` rowniez zawiesza wykonanie biezacego zadania, w tym przypadku czekajac, az gracz wpisze linie danych wejsciowych. Gdy linia zostanie odebrana, zadanie wznawia sie, a funkcja `read()` zwraca wprowadzona linie jako wynik. Nazywamy je _zadaniami odczytu_.

Trzy ostatnie rodzaje zadan powyzej sa zbiorczo znane jako _zadania w kolejce_ lub _zadania w tle_, poniewaz moga nie wykonac sie natychmiast.

Aby zapobiec zlosliwie lub niewlasciwie napisanemu programowi MOO dzialajacemu w nieskonczonosc i monopolizujacemu serwer, wprowadzane sa limity czasu dzialania kazdego zadania. Jednym z limitow jest to, ze zadne zadanie nie moze dzialac dluzej niz okreslona liczba sekund; zadania polecen i serwera otrzymuja po piec sekund, a inne zadania otrzymuja tylko trzy sekundy. Ten limit jest w praktyce rzadko osiagany. Powod jest taki, ze istnieje rowniez limit liczby operacji, jakie zadanie moze wykonac.

Serwer odlicza _ticki_ w miare wykonywania kazdego zadania. Mowiac w przyblizeniu, liczy jeden tick za kazda ewaluacje wyrazenia (poza zmiennymi i literalami), jeden za kazda instrukcje `if`, `fork` lub `return`, i jeden za kazda iteracje petli. Jesli licznik spadnie calkowicie do zera, zadanie jest natychmiast i bezceremonialnie przerywane. Domyslnie zadania polecen i serwera zaczynaja z zapasem 60 000 tickow; to wystarcza na prawie wszystkie normalne przypadki uzycia. Zadania forkowane, zawieszone i odczytu otrzymuja po 30 000 tickow.

Te limity sekund i tickow moga zostac zmienione z poziomu bazy danych, tak jak zachowanie serwera po przerwaniu zadania z powodu ich przekroczenia; zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly.

Poniewaz zadania w kolejce moga istniec przez dlugie okresy czasu przed rozpoczeciem wykonania, istnieja funkcje umozliwiajace wypisanie tych, ktore do Ciebie naleza, i zabicie ich przed wykonaniem. Te funkcje, wsrod innych, sa omowione w nastepnej sekcji.

Niektore funkcje serwera, gdy otrzymaja duze lub skomplikowane ilosci danych, moga potrzebowac znaczacej ilosci czasu, by zakonczyc swoja prace. Gdy to sie zdarza, MOO nie moze przetwarzac zadnych innych danych wejsciowych od graczy ani zadan w tle, a uzytkownicy doswiadczaja lagu. By pomoc w diagnozowaniu przyczyn lagu, ToastStunt udostepnia opcje `DEFAULT_LAG_THRESHOLD` w options.h (ktora moze zostac nadpisana z poziomu bazy danych. Zobacz sekcje o zalozeniach serwera wobec bazy danych). Gdy dzialajace zadanie przekroczy te liczbe sekund, serwer odnotuje to w logu serwera i wywola czasownik `#0:handle_lagging_task()` z argumentami: `{callers, czas wykonania}`. Callers bedzie lista w stylu `callers()` kazdego wywolania czasownika prowadzacego do lagujacego czasownika, a czas wykonania bedzie calkowitym czasem, jaki zajelo zakonczenie wykonania czasownika. Moze to pomoc dokladnie okreslic, ktory czasownik powoduje problem.

> Uwaga: w zaleznosci od konfiguracji Twojego systemu, FG_SECONDS i BG_SECONDS moga niekoniecznie odpowiadac rzeczywistym sekundom w czasie rzeczywistym. Czesto mierza czas CPU. To jest powod, dla ktorego Twoje czasowniki moga lagowac przez kilka sekund w rzeczywistosci i wciaz nie zglosic bledu "out of seconds".

### Praca z obiektami anonimowymi

Obiekty anonimowe sa zwykle tymczasowe i sa poddawane garbage collection, gdy nie sa juz potrzebne (to znaczy, gdy nic do nich sie nie odwoluje).

Referencja do obiektu anonimowego jest zwracana, gdy obiekt anonimowy zostaje utworzony za pomoca create(). Referencje moga byc udostepniane, ale nie moga zostac podrobione. To znaczy, nie istnieje literalowa reprezentacja referencji do obiektu anonimowego (to wlasnie dlatego sa "anonimowe").

Obiekty anonimowe tworzy sie za pomoca wbudowanej funkcji `create`, przekazujac opcjonalny trzeci argument jako `1`. Na przyklad:

```
anonimowy = create($thing, #2, 1);
```

Poniewaz nie istnieje literalowa reprezentacja obiektu anonimowego, jesli sprobowalbys go wypisac:

```
player:tell(toliteral(anonimowy));
```

Zobaczylbys: `\*anonymous\*`

Mozesz przechowac referencje do obiektu anonimowego w zmiennej, tak jak zrobilismy powyzej, albo mozesz przechowac ja we wlasciwosci.

```
player.test = create($thing, player, 1)
player:tell(player.test);
```

To rowniez wypisze: `\*anonymous\*`

Jesli przechowasz swoj obiekt anonimowy we wlasciwosci, ten obiekt anonimowy bedzie istniec, dopoki istnieje w tej wlasciwosci. Jesli obiekt posiadajacy te wlasciwosc zostalby poddany recyklingowi, albo wlasciwosc zostalaby usunieta lub nadpisana inna wartoscia, obiekt anonimowy zostalby poddany garbage collection.

Obiekty anonimowe moga byc przechowywane na listach:

```
moja_lista = {create($thing, player, 1)};
player.test = moja_lista;
```

Powyzszy kod skutkowalby:

```
{\*anonymous\*}
```

Obiekty anonimowe moga byc przechowywane w mapach, jako klucz lub jako wartosc:

```
[1 -> create($thing, player, 1)] => [1 -> \*anonymous\*]
[create($thing, player, 1) -> 1] => [\*anonymous\* -> 1]
```

> Ostrzezenie: \*anonymous\* nie jest faktycznym kluczem, nie istnieje literalowa reprezentacja referencji do obiektu anonimowego. To znaczy, ze choc obiekt bedzie istniec, dopoki jest kluczem mapy, jedynym sposobem odwolania sie do tego klucza bedzie referencja, ktora musialbys przechowac gdzies w zmiennej lub wlasciwosci. To NIE jest zalecana praktyka, poniewaz musialbys przechowywac referencje do klucza gdzies indziej, by miec do niego dostep (poza iterowaniem po wszystkich kluczach).

Obiekty anonimowe technicznie posiadaja flage gracza i listy dzieci, ale nie mozesz z nimi faktycznie nic zrobic. Podobnie z wiekszoscia wbudowanych wlasciwosci. Istnieja, ale sa bez znaczenia. Nie mozesz rowniez dodawac nowych wlasciwosci ani czasownikow bezposrednio do obiektu anonimowego. Ogolnie rzecz biorac, to sprawia, ze WAIF-y sa lepszym wyborem w wiekszosci sytuacji, poniewaz sa lzejsze.

Od wersji ToastStunt 2.8.0 obiekty anonimowe dziedziczace po rodzicu nie sa juz uniewazniane tylko dlatego, ze wlasciwosci tego rodzica sie zmienily.

> Ostrzezenie: podobnie jak z WAIF-ami, nalezy uwazac, jak tworzysz obiekty anonimowe, poniewaz gdy juz zostana utworzone, jesli nadal odwolujesz sie do nich we wlasciwosci, moze byc Ci trudno je pozniej znalezc, gdyz nie ma sposobu, by wyswietlic liste wszystkich obiektow anonimowych.

> Uwaga: sekcja [Dodatkowe szczegoly o WAIF-ach](#dodatkowe-szczegoly-o-waifach) zawiera przykladowe czasowniki, ktore mozna uzyc do wykrywania obiektow anonimowych, do ktorych odwoluje sie Twoj system.

**Funkcja: `anon`**

anon -- Zwraca informacje diagnostyczne o obiektach anonimowych.

lista `anon`([LISTA polecenie [, wartosc]])

Ta funkcja jest zarejestrowana wylacznie w kompilacjach bez `NDEBUG` i jest przeznaczona do rozwoju/diagnostyki. Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`. Wywolana bez argumentow, zwraca dostepne polecenia diagnostyczne dla obiektow anonimowych. Kod produkcyjny powinien tworzyc obiekty anonimowe za pomoca `create(rodzic, wlasciciel, 1)` lub `create(rodzice, wlasciciel, 1)`.

### Praca z WAIF-ami

Struktura obiektow MOO jest unikalna w tym, ze wszystkie klasy sa instancjami, a wszystkie instancje sa (potencjalnie) klasami. To znaczy, ze instancje niosa ze soba duzo bagazu, ktory jest przydatny wylacznie w sytuacji, gdyby stawaly sie klasami. Ponadto kazdy obiekt przychodzi z zestawem wbudowanych wlasciwosci i atrybutow, ktore sa przydatne przede wszystkim do budowania rzeczy VR. Moj pomysl na lekki obiekt to cos, co jest wylacznie instancja. Brakuje mu wielu rzeczy, ktore "prawdziwe obiekty MOO" maja dla swoich rol jako klasy i obiekty VR:

- nazwy
- informacje o lokalizacji/zawartosci
- dzieci
- flagi
- definicje czasownikow
- definicje wlasciwosci
- jawne niszczenie

Sprowadzony do samego jadra, WAIF ma nastepujace atrybuty:

- klase (jak rodzic)
- wlasciciela (dla informacji o uprawnieniach)
- wartosci wlasciwosci

Wlasciwosci i zachowanie WAIF-a sa hybryda kilku istniejacych typow MOO. Warto je porownac:

- WAIF-y sa wartosciami zliczanymi przez referencje, jak LISTY. Po utworzeniu istnieja, dopoki sa przechowywane gdzies w zmiennej lub wlasciwosci. Gdy ostatnia referencja przepada, WAIF zostaje zniszczony bez powiadomienia.
- Nie istnieje skladnia do tworzenia literalowego WAIF-a. Moga byc tworzone wylacznie za pomoca wbudowanej funkcji.
- Nie istnieje skladnia do odwolywania sie do istniejacego WAIF-a. Mozesz uzyc go wylacznie poprzez odczyt wlasciwosci lub zmiennej, w ktorej zostal przechowany.
- WAIF-y moga sie zmieniac, jak obiekty. Gdy zmieniasz WAIF-a, wszystkie referencje do tego WAIF-a widza te zmiane (jak OBJ, w przeciwienstwie do LISTY).
- Mozesz wywolywac czasowniki i odwolywac sie do wlasciwosci na WAIF-ach. Sa one dziedziczone z jego obiektu klasy (z mapowaniem opisanym nizej).
- WAIF-y sa tanie w tworzeniu, w przyblizeniu tak jak LISTY.
- WAIF-y sa male. WAIF z wszystkimi czystymi wlasciwosciami (jak zaraz po utworzeniu) jest tylko o kilka bajtow wiekszy niz LISTA wystarczajaco duza, by przechowac {klasa, wlasciciel}. Jesli przypiszesz wartosc do wlasciwosci, rosnie o tyle samo, o ile roslaby LISTA, gdybys dolaczyl do niej wartosc.
- Dostep do wlasciwosci WAIF-a jest kontrolowany tak samo, jak dostep do wlasciwosci OBJ. Posiadanie referencji do WAIF-a nie oznacza, ze widzisz, co jest w jego wnetrzu.
- WAIF-y nigdy nie moga definiowac nowych czasownikow ani wlasciwosci.
- WAIF-y nigdy nie moga miec zadnych dzieci.
- WAIF-y nie moga zmienic klasy ani wlasciciela.
- Jedynymi wbudowanymi wlasciwosciami WAIF-a sa .owner i .class.
- WAIF-y nie uczestnicza w hierarchii .location/.contents, manipulowanej przez move(). Klasa WAIF-a moze jednak zdefiniowac te wlasciwosci (jak opisano nizej).
- WAIF-y nie posiadaja flag OBJ, takich jak .r czy .wizard.
- WAIF-y moga byc przechowywane w MAPACH
- WAIF-y nie moga rekurencyjnie odwolywac sie do siebie nawzajem, ale jeden WAIF moze odwolywac sie do innego WAIF-a, jesli ten drugi nie odwoluje sie zwrotnie do niego.

> Uwaga: podczas wczytywania bazy danych LambdaMOO z waifami do ToastStunt po raz pierwszy, mozesz otrzymac bledy. Dzieje sie tak, poniewaz typ WAIF w LambdaMOO nie zgadza sie z typem WAIF w ToastStunt. By naprawic ten blad, musisz zrobic dwie proste rzeczy:
> 1. Uruchom swoja baze danych w LambdaMOO tak jak zawsze i zewaluuj to: `;typeof($waif:new())`
> 2. Uruchom swoja baze danych w ToastStunt z opcja linii komend `-w <wynik poprzedniej ewaluacji>`. Na przyklad, jesli `typeof($waif:new())` w LambdaMOO wynioslo 42, uruchomilbys swoje MOO czyms takim jak: `./moo -w 42 moja_baza.db moja_przekonwertowana_baza.db`
> Po tym gotowe! Twoja baza danych przekonwertuje wszystkie istniejace waify i zapisze je w nowym formacie ToastStunt. Musisz uzyc opcji `-w` tylko raz.

#### Przestrzen nazw czasownikow i wlasciwosci WAIF-a

W celu odseparowania czasownikow i wlasciwosci zdefiniowanych dla WAIF-ow danego obiektu, WAIF-y dziedzicza wylacznie czasowniki i wlasciwosci, ktorych nazwy zaczynaja sie od : (dwukropka). Innymi slowy, zastosowane jest nastepujace mapowanie:

`waif:czasownik(@argumenty)` staje sie `waif.class:(":"+czasownik)(@argumenty)`

Wewnatrz czasownika WAIF-a (nazywanego dalej _metoda_) lokalna zmienna `verb` nie ma dodatkowego dwukropka. Wartoscia `this` jest sam WAIF (moze okreslic, na jakim obiekcie jest, za pomoca `this.class`). Jesli metoda wywoluje inny czasownik na WAIF-ie lub OBJ-cie, `caller` bedzie WAIF-em.

`waif.wlasciwosc` jest zdefiniowana przez `waif.class.(":"+wlasciwosc)`

Definicja wlasciwosci zapewnia informacje o wlascicielu i flagach uprawnien dla tej wlasciwosci, a takze jej domyslna wartosc, tak jak dla kazdego OBJ-a. Oczywiscie faktyczna wartosc wlasciwosci jest czescia samego WAIF-a i moze byc zmieniana w trakcie zycia WAIF-a.

W przypadku wlasciwosci +c, wlasciciel WAIF-a jest uznawany za wlasciciela wlasciwosci.

W ToastCore znajdziesz skorifikowana referencje `$waif`, ktora jest wstepnie skonfigurowana, by pozwolic Ci zaczac tworzenie WAIF-ow albo Generycznych OBJ-ow, ktore mozesz nastepnie uzyc do tworzenia WAIF-ow. Tu jest wynik @display dla szkieletowego $waif:

```
Generic Waif (#118) [ ]
  Child of Root Class (#1).
  Size: 7,311 bytes at Sun Jan  2 10:37:09 2022 PST
```

Ten OBJ MOO `$waif` definiuje czasownik `new`, ktory jest zupelnie taki jak czasowniki, ktore juz znasz. W tym przypadku tworzy nowy WAIF:

```
set_task_perms(caller_perms());
w = new_waif();
w:initialize(@args);
return w;
```

Gdy WAIF zostal juz utworzony, mozesz wywolywac na nim czasowniki. Zauwaz, jak WAIF dziedziczy `$waif::initialize`. Zauwaz, ze nie moze dziedziczyc `$waif:new`, poniewaz nazwa tego czasownika nie zaczyna sie od dwukropka.

Generyczny waif jest plodny (`$waif.f == 1`), tak by nowe klasy waifow moglyby byc z niego wyprowadzone. Plodnosc OBJ-a jest nieistotna przy tworzeniu WAIF-a. Mozliwosc jej wykonania jest ograniczona do samego obiektu (poniewaz `new_waif()` zawsze zwraca WAIF-a klasy=caller).

Nie istnieje format tekstowy dla WAIF-a. `tostr()` po prostu zwraca {waif}. `toliteral()` obecnie zwraca troche wiecej informacji, ale to wylacznie do celow diagnostycznych. Nie istnieje towaif(). Jesli chcesz odwolac sie do WAIF-a, musisz odczytac go bezposrednio ze zmiennej lub wlasciwosci gdzies. Jesli nie mozesz odczytac go z wlasciwosci (lub wywolac czasownika, ktory go zwraca), nie masz do niego dostepu. Nie ma sposobu, by skonstruowac referencje do WAIF-a z innego typu.

**Dostep do WAIF-a w stylu mapy**

;me.waif["cheese"]
To wywola czasownik :_index na klasie waifa z {"cheese"} jako argumentami.

;me.waif["cheese"] = 17
To wywola czasownik :_set_index na klasie waifa z {"cheese", 17} jako argumentami.

Pierwotnie ulatwialo to zaimplementowanie map w LambdaMOO, poniewaz moglbys po prostu miec swojego "waifa-mape" przechowujacego liste kluczy i wartosci oraz czasowniki index ustawiajace i odczytujace dane w odpowiedni sposob. Nastepnie mozesz uzywac ich zupelnie jak natywnego typu mapa, ktory ToastCore ma dzisiaj.

Istnieja jednak inne zastosowania, ktore wciaz czynia to przydatnym dzisiaj. Na przyklad WAIF abstrakcji pliku. Jedna z rzeczy, ktore mozesz zrobic to:

```
file = $file:open("thing.txt");
return file[5..19];
```

To uzywa :_index, by sparsowac '5..19' i ostatecznie przekazac to do file_readlines(), by zwrocic te linie. Bardzo wygodne.

#### Dodatkowe szczegoly o WAIF-ach

* Gdy WAIF zostaje zniszczony, MOO wywola czasownik `recycle` na tym WAIF-ie, jesli istnieje.
* WAIF ma swoj wlasny typ, tak wiec mozesz zrobic: `typeof(jakis_waif) == WAIF)``
* Wbudowana funkcja waif_stats() pokaze, ile instancji kazdej klasy WAIF istnieje, ile WAIF-ow oczekuje na recykling i ile WAIF-ow istnieje w sumie
* Mozesz uzyskac dostep do wlasciwosci WAIF-a za pomoca `mywaif.:nazwa_wlasciwosci_waifa`

> Ostrzezenie: podobnie jak z obiektami anonimowymi, nalezy uwazac, jak tworzysz WAIF-y, poniewaz moze byc trudno znalezc WAIF-y, ktore istnieja w Twoim systemie, i gdzie sa uzyte.

Nastepujacy kod moze zostac uzyty, by znalezc WAIF-y i obiekty anonimowe istniejace w Twojej bazie danych.

```
@verb $waif_utils:"find_waif_types find_anon_types" this none this
@program $waif_utils:find_waif_types
if (!caller_perms().wizard)
  return E_PERM;
endif
{data, ?class = 0} = args;
ret = {};
TYPE = verb == "find_anon_types" ? ANON | WAIF;
if (typeof(data) in {LIST, MAP})
  "Rather than wasting time iterating through the entire list, we can find if it contains any waifs with a relatively quicker index().";
  if (index(toliteral(data), "[[class = #") != 0)
    for x in (data)
      yin(0, 1000);
      ret = {@ret, @this:(verb)(x, class)};
    endfor
  endif
elseif (typeof(data) == TYPE)
  if (class == 0 || (class != 0 && (TYPE == WAIF && data.class == class || (TYPE == ANON && `parent(data) ! E_INVARG' == class))))
    ret = {@ret, data};
  endif
endif
return ret;
.


@verb me:"@find-waifs @find-anons" any any any
@program me:@find-waifs
"Provide a summary of all properties and running verb programs that contain instantiated waifs.";
"Usage: @find-waifs [<class>] [on <object>]";
"       @find-anons [<parent>] [on <object>]";
"  e.g. @find-waifs $some_waif on #123 => Find waifs of class $some_waif on #123 only.";
"       @find-waifs on #123            => Find all waifs on #123.";
"       @find-waifs $some_waif         => Find all waifs of class $some_waif.";
"The above examples also apply to @find-anons.";
if (!player.wizard)
  return E_PERM;
endif
total = class = tasks = 0;
exclude = {$spell};
find_anon = index(verb, "anon");
search_verb = tostr("find_", find_anon ? "anon" | "waif", "_types");
{min, max} = {#0, max_object()};
if (args)
  if ((match = $string_utils:match_string(argstr, "* on *")) != 0)
    class = player:my_match_object(match[1]);
    min = max = player:my_match_object(match[2]);
  elseif ((match = $string_utils:match_string(argstr, "on *")) != 0)
    min = max = player:my_match_object(match[1]);
  else
    class = player:my_match_object(argstr);
  endif
  if (!valid(max))
    return player:tell("That object doesn't exist.");
  endif
  if (class != 0 && (class == $failed_match || !valid(class) || (!find_anon && !isa(class, $waif))))
    return player:tell("That's not a valid ", find_anon ? "object parent." | "waif class.");
  endif
endif
" -- Constants (avoid #0 property lookups on each iteration of loops) -- ";
WAIF_UTILS = $waif_utils;
STRING_UTILS = $string_utils;
OBJECT_UTILS = $object_utils;
LIST_UTILS = $list_utils;
" -- ";
player:tell("Searching for ", find_anon ? "ANON" | "WAIF", " instances. This may take some time...");
start = ftime(1);
for x in [min..max]
  yin(0, 1000);
  if (!valid(x))
    continue;
  endif
  if (toint(x) % 100 == 0 && player:is_listening() == 0)
    "No point in carrying on if the player isn't even listening.";
    return;
  elseif (x in exclude)
    continue;
  endif
  for y in (OBJECT_UTILS:all_properties(x))
    yin(0, 1000);
    if (is_clear_property(x, y))
      continue y;
    endif
    match = WAIF_UTILS:(search_verb)(x.(y), class);
    if (match != {})
      total = total + 1;
      player:tell(STRING_UTILS:nn(x), "[bold][yellow].[normal](", y, ")");
      for z in (match)
        yin(0, 1000);
        player:tell("    ", `STRING_UTILS:nn(find_anon ? parent(z) | z.class) ! E_INVARG => "*INVALID*"');
      endfor
    endif
  endfor
endfor
"Search for running verb programs containing waifs / anons. But only do this when a specific object wasn't specified.";
if (min == #0 && max == max_object())
  for x in (queued_tasks(1))
    if (length(x) < 11 || x[11] == {})
      continue;
    endif
    match = WAIF_UTILS:(search_verb)(x[11], class);
    if (match != {})
      tasks = tasks + 1;
      player:tell(x[6], ":", x[7], " (task ID ", x[1], ")");
      for z in (match)
        yin(0, 1000);
        player:tell("    ", find_anon ? parent(z) | STRING_UTILS:nn(z.class));
      endfor
    endif
  endfor
endif
player:tell();
player:tell("Total: ", total, " ", total == 1 ? "property" | "properties", tasks > 0 ? tostr(" and ", tasks, " ", tasks == 1 ? "task" | "tasks") | "", " in ", ftime(1) - start, " seconds.");
.
```

### Funkcje wbudowane

Istnieje duza liczba funkcji wbudowanych dostepnych do uzycia przez programistow MOO. Kazda z nich jest szczegolowo opisana w tej sekcji. Prezentacja jest podzielona na podsekcje, grupujace funkcje o podobnym lub powiazanym zastosowaniu.

Dla wiekszosci funkcji podane sa oczekiwane typy argumentow; jesli rzeczywiste argumenty nie sa tych typow, zglaszany jest `E_TYPE`. Niektore argumenty moga byc jakiegokolwiek typu; w takich przypadkach nie podaje sie specyfikacji typu dla argumentu. Rowniez dla wiekszosci funkcji podany jest typ wyniku funkcji. Niektore funkcje nie zwracaja uzytecznego wyniku; w takich przypadkach uzywana jest specyfikacja `none`. Kilka funkcji moze potencjalnie zwrocic jakikolwiek typ wartosci; w takich przypadkach uzywana jest specyfikacja `value`.

Wiekszosc funkcji przyjmuje pewna okreslona liczbe wymaganych argumentow, a w niektorych przypadkach jeden lub dwa opcjonalne argumenty. Jesli funkcja jest wywolana z za duza lub za mala liczba argumentow, zglaszany jest `E_ARGS`.

Funkcje sa zawsze wywolywane przez program pewnego czasownika; ten program dziala z uprawnieniami pewnego gracza, zwykle wlasciciela danego czasownika (choc nie zawsze jest to wlasciciel; czarodzieje moga uzyc `set_task_perms()`, by zmienic uprawnienia _na biezaco_). W opisach funkcji nizej odnosimy sie do gracza, czyich uprawnien sie uzywa, jako do _programisty_.

Wiele funkcji wbudowanych opisanych nizej zglasza `E_PERM`, jesli programista nie spelnia pewnych okreslonych kryteriow. Mozliwe jest jednak ograniczenie uzycia dowolnej funkcji tak, by mogli jej uzywac wylacznie czarodzieje; zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly.

#### Programowanie obiektowe

Jedna z najwazniejszych mozliwosci jezyka programowania obiektowego jest zdolnosc obiektu-dziecka do skorzystania z implementacji rodzica dla pewnej operacji, nawet gdy dziecko dostarcza wlasna definicje tej operacji. Funkcja `pass()` udostepnia te mozliwosc w MOO.

**Funkcja: `pass`**

pass -- wywoluje czasownik o tej samej nazwie co biezacy czasownik, ale zdefiniowany na rodzicu obiektu definiujacego biezacy czasownik.

value `pass` (arg, ...)

Czesto przydatne jest, by obiekt-dziecko zdefiniowal czasownik, ktory _rozszerza_ zachowanie czasownika na jego obiekcie-rodzicu. Na przyklad w bazie danych ToastCore obiekt root (bedacy przodkiem kazdego innego obiektu) definiuje czasownik `description`, ktory po prostu zwraca wartosc `this.description`; ten czasownik jest uzywany przez implementacje polecenia `look`. W wielu przypadkach programista chcialby, by opis pewnego obiektu zawieral pewna niestala czesc; na przyklad zdanie o tym, czy obiekt jest "przebudzony" czy "spi". To zdanie powinno zostac dodane na koniec normalnego opisu. Programista chcialby miec sposob wywolania normalnego czasownika `description`, a nastepnie dolaczenia tego zdania na koniec tego opisu. Funkcja `pass()` jest przeznaczona wlasnie do takich sytuacji.

`pass` wywoluje czasownik o tej samej nazwie co biezacy czasownik, ale zdefiniowany na rodzicu obiektu definiujacego biezacy czasownik. Argumenty podane do `pass` sa tymi podanymi do wywolanego czasownika, a zwrocona wartosc wywolanego czasownika jest zwracana z wywolania `pass`. Poczatkowa wartosc `this` w wywolanym czasowniku jest taka sama, jak w wywolujacym czasowniku.

Tak wiec w przykladzie powyzej czasownik `description` obiektu-dziecka moglby miec nastepujaca implementacje:

```
return pass() + "  It is " + (this.awake ? "awake." | "sleeping.");
```

To znaczy, wywoluje czasownik `description` swojego rodzica, a nastepnie dolacza do wyniku zdanie, ktorego zawartosc jest obliczana na podstawie wartosci wlasciwosci obiektu.

W prawie wszystkich przypadkach bedziesz chcial wywolac `pass()` z tymi samymi argumentami, jakie podano do biezacego czasownika. Latwo to napisac w MOO; wystarczy wywolac `pass(@args)`.

#### Operacje na wartosciach MOO

Istnieje kilka funkcji do wykonywania podstawowych operacji na wartosciach MOO i moga one zostac czysto podzielone na dwa rodzaje: te, ktore wykonuja rozne bardzo ogolne operacje, stosowane do wszystkich typow wartosci, oraz te, ktore sa specyficzne dla jednego konkretnego typu. Istnieje tak wiele operacji dotyczacych obiektow, ze nie wymieniamy ich w tej sekcji, lecz dajemy im wlasna sekcje, nastepujaca po tej.

##### Ogolne operacje stosowane do wszystkich wartosci

**Funkcja: `typeof`**

typeof -- Bierze jakakolwiek wartosc MOO i zwraca liczbe calkowita reprezentujaca typ tej wartosci.

int `typeof` (value)

Wynik jest taki sam jak poczatkowa wartosc jednej z tych wbudowanych zmiennych: `INT`, `FLOAT`, `STR`, `LIST`, `OBJ`, lub `ERR`, `BOOL`, `MAP`, `WAIF`, `ANON`. Zwykle pisze sie wiec kod taki jak ten:

```
if (typeof(x) == LIST) ...
```

a nie taki:

```
if (typeof(x) == 3) ...
```

poniewaz pierwszy jest znacznie bardziej czytelny niz drugi.

**Funkcja: `tostr`**

tostr -- Konwertuje wszystkie podane wartosci MOO na stringi i zwraca konkatenacje wynikow.

str `tostr` (value, ...)

```
tostr(17)                  =>   "17"
tostr(1.0/3.0)             =>   "0.333333333333333"
tostr(#17)                 =>   "#17"
tostr("foo")               =>   "foo"
tostr({1, 2})              =>   "{list}"
tostr([1 -> 2])            =>   "[map]"
tostr(E_PERM)              =>   "Permission denied"
tostr("3 + 4 = ", 3 + 4)   =>   "3 + 4 = 7"
```

Ostrzezenie: `tostr()` nie radzi sobie dobrze z konwertowaniem list i map na stringi; wszystkie listy, wliczajac liste pusta, sa konwertowane na string `"{list}"`, a wszystkie mapy sa konwertowane na string `"[map]"`. Funkcja `toliteral()`, opisana nizej, jest lepsza do tego celu.

**Funkcja: `toliteral`**

Zwraca string zawierajacy literal wyrazenia MOO, ktory, gdy zewaluowany, bylby rowny value.

str `toliteral` (value)

```
toliteral(17)         =>   "17"
toliteral(1.0/3.0)    =>   "0.333333333333333"
toliteral(#17)        =>   "#17"
toliteral("foo")      =>   "\"foo\""
toliteral({1, 2})     =>   "{1, 2}"
toliteral([1 -> 2])   =>   "[1 -> 2]"
toliteral(E_PERM)     =>   "E_PERM"
```

**Funkcja: `toint`**

toint -- Konwertuje podana wartosc MOO na liczbe calkowita i zwraca te liczbe calkowita.

int `toint` (value)

Liczby zmiennoprzecinkowe sa zaokraglane w strone zera, obcinajac ich czesc dziesietna. Numery obiektow sa konwertowane na rownowazne liczby calkowite. Stringi sa parsowane jako dziesietny zapis liczby rzeczywistej, ktora jest nastepnie konwertowana na liczbe calkowita. Bledy sa konwertowane na liczby calkowite, zachowujac ten sam porzadek (wzgledem `<=`) jak same bledy. `toint()` zglasza `E_TYPE`, jesli value jest lista. Jesli value jest stringiem, ale ten string nie zawiera skladniowo poprawnej liczby, `toint()` zwraca 0.

```
toint(34.7)        =>   34
toint(-34.7)       =>   -34
toint(#34)         =>   34
toint("34")        =>   34
toint("34.7")      =>   34
toint(" - 34  ")   =>   -34
toint(E_TYPE)      =>   1
```

**Funkcja: `toobj`**

toobj -- Konwertuje podana wartosc MOO na numer obiektu i zwraca ten numer obiektu.

obj `toobj` (value)

Konwersje sa bardzo podobne do tych dla `toint()`, z tym ze dla stringow liczba _moze_ byc poprzedzona `#`.

```
toobj("34")       =>   #34
toobj("#34")      =>   #34
toobj("foo")      =>   #0
toobj({1, 2})     =>   E_TYPE (error)
```

**Funkcja: `tofloat`**

tofloat -- Konwertuje podana wartosc MOO na liczbe zmiennoprzecinkowa i zwraca te liczbe.

float `tofloat` (value)

Liczby calkowite i numery obiektow sa konwertowane na odpowiadajace im calkowite liczby zmiennoprzecinkowe. Stringi sa parsowane jako dziesietny zapis liczby rzeczywistej, ktora jest nastepnie reprezentowana jak najbardziej precyzyjnie jako liczba zmiennoprzecinkowa. Bledy sa najpierw konwertowane na liczby calkowite jak w `toint()`, a nastepnie konwertowane jak liczby calkowite. `tofloat()` zglasza `E_TYPE`, jesli value jest lista. Jesli value jest stringiem, ale ten string nie zawiera skladniowo poprawnej liczby, `tofloat()` zwraca 0.

```
tofloat(34)          =>   34.0
tofloat(#34)         =>   34.0
tofloat("34")        =>   34.0
tofloat("34.7")      =>   34.7
tofloat(E_TYPE)      =>   1.0
```

**Funkcja: `equal`**

equal -- Zwraca prawde, jesli value1 jest calkowicie nieodroznialna od value2.

int `equal` (value, value2)

To w duzej mierze ta sama operacja co `value1 == value2`, z tym ze, w przeciwienstwie do `==`, funkcja `equal()` nie traktuje wielkich i malych liter w stringach jako rownych i tak wiec rozroznia wielkosc liter.

```
"Foo" == "foo"         =>   1
equal("Foo", "foo")    =>   0
equal("Foo", "Foo")    =>   1
```

**Funkcja: `value_bytes`**

value_bytes -- Zwraca liczbe bajtow pamieci serwera wymaganych do przechowania podanej wartosci.

int `value_bytes` (value)

**Funkcja: `value_hash`**

value_hash -- Zwraca ten sam string co `string_hash(toliteral(value))`.

str `value_hash` (value, [, str algo] [, binary])

Zobacz opis `string_hash()` po szczegoly.

**Funkcja: `value_hmac`**

value_hmac -- Zwraca ten sam string co string_hmac(toliteral(value), key)

str `value_hmac` (value, STR key [, STR algo [, binary]])

Zobacz opis string_hmac() po szczegoly.

**Funkcja: `generate_json`**

generate_json -- Zwraca reprezentacje JSON wartosci MOO.

str generate_json (value [, str mode [, any disable_binary_escapes]])

Zwraca reprezentacje JSON wartosci MOO.

MOO wspiera bogatszy zestaw wartosci, niz pozwala na to JSON. Opcjonalny mode okresla, jak ta funkcja obsluguje konwersje wartosci MOO na ich reprezentacje JSON.

Tryb wspolnego podzbioru (common subset), okreslony przez literalowy string mode "common-subset", jest domyslnym trybem konwersji. W tym trybie stringi, liczby i wartosci logiczne sa tlumaczone z pelna wiernoscia miedzy typami MOO i typami JSON. Wszystkie inne typy sa traktowane jako alternatywne reprezentacje typu string. Ten tryb jest przydatny do integracji z aplikacjami nie-MOO.

Tryb wbudowanych typow (embedded types), okreslony przez literalowy string mode "embedded-types", dodaje informacje o typie. Konkretnie, wartosci inne niz stringi, liczby i wartosci logiczne, ktore niosa ze soba niejawna informacje o typie, sa konwertowane na stringi z dolaczona informacja o typie. Skonwertowany string sklada sie z reprezentacji tekstowej wartosci (jak gdyby zastosowano tostr()), po ktorej nastepuje znak potoku (|) i typ. Ten tryb jest przydatny do serializacji/deserializacji obiektow i kolekcji wartosci MOO.

Opcjonalny argument disable_binary_escapes kontroluje, czy binarne sekwencje stringow MOO (takie jak ~08 czy ~1F) sa konwertowane na sekwencje ucieczki JSON. Domyslnie te sekwencje sa konwertowane (np. ~08 staje sie \b). Jesli disable_binary_escapes jest prawda, te sekwencje przechodza bez zmian. To jest przydatne przy pracy z literalowymi stringami, ktore zawieraja ~0 lub ~1 nastepowane cyframi szesnastkowymi.

```
generate_json([])                                           =>  "{}"
generate_json(["foo" -> "bar"])                             =>  "{\"foo\":\"bar\"}"
generate_json(["foo" -> "bar"], "common-subset")            =>  "{\"foo\":\"bar\"}"
generate_json(["foo" -> "bar"], "embedded-types")           =>  "{\"foo\":\"bar\"}"
generate_json(["foo" -> 1.1])                               =>  "{\"foo\":1.1}"
generate_json(["foo" -> 1.1], "common-subset")              =>  "{\"foo\":1.1}"
generate_json(["foo" -> 1.1], "embedded-types")             =>  "{\"foo\":1.1}"
generate_json(["foo" -> true, "bar" -> false])              =>  "{\"bar\":false,\"foo\":true}"
generate_json(["foo" -> #1])                                =>  "{\"foo\":\"#1\"}"
generate_json(["foo" -> #1], "common-subset")               =>  "{\"foo\":\"#1\"}"
generate_json(["foo" -> #1], "embedded-types")              =>  "{\"foo\":\"#1|obj\"}"
generate_json(["foo" -> E_PERM])                            =>  "{\"foo\":\"E_PERM\"}"
generate_json(["foo" -> E_PERM], "common-subset")           =>  "{\"foo\":\"E_PERM\"}"
generate_json(["foo" -> E_PERM], "embedded-types")          =>  "{\"foo\":\"E_PERM|err\"}"
```

Klucze JSON musza byc stringami, wiec niezaleznie od trybu, klucz zostanie skonwertowany na wartosc string.

```
generate_json([1 -> 2])                                     =>  "{\"1\":2}"
generate_json([1 -> 2], "common-subset")                    =>  "{\"1\":2}"
generate_json([1 -> 2], "embedded-types")                   =>  "{\"1|int\":2}"
generate_json([#1 -> 2], "embedded-types")                  =>  "{\"#1|obj\":2}"
```

Przyklady przetwarzania sekwencji ucieczki binarnych:

```
generate_json(["foo" -> "bar~08baz"])                       =>  "{\"foo\":\"bar\\bbaz\"}"
generate_json(["foo" -> "bar~08baz"], "common-subset", 0)   =>  "{\"foo\":\"bar\\bbaz\"}"
generate_json(["foo" -> "bar~08baz"], "common-subset", 1)   =>  "{\"foo\":\"bar~08baz\"}"
generate_json(["foo" -> "Hoodie (~1.5k)"])                  =>  "{\"foo\":\"Hoodie (~1.5k)\"}"
```

> Ostrzezenie: generate_json nie wspiera typow WAIF ani ANON.

**Funkcja: `parse_json`**

parse_json -- Zwraca reprezentacje wartosci MOO stringa JSON.

value parse_json (str json [, str mode])

Jesli podany string nie jest poprawnym JSON-em, zglaszany jest E_INVARG.

Opcjonalny mode okresla, jak ta funkcja obsluguje konwersje wartosci MOO na ich reprezentacje JSON. Opcje sa takie same jak dla generate_json().

```
parse_json("{}")                                            =>  []
parse_json("{\"foo\":\"bar\"}")                             =>  ["foo" -> "bar"]
parse_json("{\"foo\":\"bar\"}", "common-subset")            =>  ["foo" -> "bar"]
parse_json("{\"foo\":\"bar\"}", "embedded-types")           =>  ["foo" -> "bar"]
parse_json("{\"foo\":1.1}")                                 =>  ["foo" -> 1.1]
parse_json("{\"foo\":1.1}", "common-subset")                =>  ["foo" -> 1.1]
parse_json("{\"foo\":1.1}", "embedded-types")               =>  ["foo" -> 1.1]
parse_json("{\"foo\":true,\"bar\":false,\"baz\":null}")      =>  ["bar" -> false, "baz" -> E_NONE, "foo" -> true]
parse_json("{\"foo\":\"#1\"}")                              =>  ["foo" -> "#1"]
parse_json("{\"foo\":\"#1\"}", "common-subset")             =>  ["foo" -> "#1"]
parse_json("{\"foo\":\"#1|obj\"}", "embedded-types")        =>  ["foo" -> #1]
parse_json("{\"foo\":\"E_PERM\"}")                          =>  ["foo" -> "E_PERM"]
parse_json("{\"foo\":\"E_PERM\"}", "common-subset")         =>  ["foo" -> "E_PERM"]
parse_json("{\"foo\":\"E_PERM|err\"}", "embedded-types")    =>  ["foo" -> E_PERM]
```

W trybie wbudowanych typow, wartosci kluczy moga zostac skonwertowane na typy MOO poprzez dolaczenie informacji o typie. Pelny zestaw wspieranych typow to obj, str, err, float i int.

```
parse_json("{\"1\":2}")                                     =>   ["1" -> 2]
parse_json("{\"1\":2}", "common-subset")                    =>   ["1" -> 2]
parse_json("{\"1|int\":2}", "embedded-types")               =>   [1 -> 2]
parse_json("{\"#1|obj\":2}", "embedded-types")              =>   [#1 -> 2]
```

Wartosci logiczne JSON sa konwertowane na wartosci BOOL MOO. Wartosci `null` JSON sa konwertowane na `E_NONE`.

```
parse_json("{\"foo\":null}")                                =>   ["foo" -> E_NONE]
```

> Ostrzezenie: typy WAIF i ANON nie sa wspierane.

##### Operacje na liczbach

**Funkcja: `random`**

random -- Zwraca losowa liczbe calkowita.

int `random` ([int mod, [int range]])

mod musi byc liczba calkowita dodatnia; w przeciwnym razie zglaszany jest `E_INVARG`. Jesli mod nie jest podany, domyslnie przyjmuje wartosc najwiekszej liczby calkowitej MOO, ktora zalezy od tego, czy uruchamiasz wersje 32- czy 64-bitowa.

Jesli podano range, zwracana jest liczba calkowita z zakresu od mod do range (wlacznie).

```
random(10)                  => integer between 1-10
random()                    => integer between 1 and maximum integer supported
random(1, 5000)             => integer between 1 and 5000
```

**Funkcja: `frandom`**

float `frandom` (FLOAT mod1 [, FLOAT mod2])

Jesli podano tylko jeden argument, liczba zmiennoprzecinkowa jest wybierana losowo z zakresu `[1.0..mod1]` i zwracana. Jesli podano dwa argumenty, liczba zmiennoprzecinkowa jest wybierana losowo z zakresu `[mod1..mod2]`.

**Funkcja: `random_bytes`**

str `random_bytes` (int count)

Zwraca binarny string skladajacy sie z od jednego do 10000 losowych bajtow. count okresla liczbe bajtow i musi byc liczba calkowita dodatnia; w przeciwnym razie zglaszany jest E_INVARG.

**Funkcja: `reseed_random`**

reseed_random -- Podaje nowe ziarno (seed) generatorowi pseudolosowych liczb.

void `reseed_random`()

**Funkcja: `min`**

min -- Zwraca najmniejszy ze swoich argumentow.

int|float `min` (int|float x, ...)

Wszystkie argumenty musza byc liczbami tego samego rodzaju (tzn. albo liczbami calkowitymi, albo zmiennoprzecinkowymi); w przeciwnym razie zglaszany jest `E_TYPE`.

**Funkcja: `max`**

max -- Zwraca najwiekszy ze swoich argumentow.

int|float `max` (int|float x, ...)

Wszystkie argumenty musza byc liczbami tego samego rodzaju (tzn. albo liczbami calkowitymi, albo zmiennoprzecinkowymi); w przeciwnym razie zglaszany jest `E_TYPE`.

**Funkcja: `abs`**

abs -- Zwraca wartosc absolutna x.

int|float `abs` (int|float x)

Jesli x jest ujemne, wynikiem jest `-x`; w przeciwnym razie wynikiem jest x. Liczba x moze byc liczba calkowita lub zmiennoprzecinkowa; wynik jest tego samego rodzaju.

**Funkcja: `floatstr`**

floatstr -- Konwertuje x na string z wieksza kontrola, niz zapewniaja `tostr()` czy `toliteral()`.

str `floatstr` (float x, int precision [, scientific])

Precision to liczba cyfr, jakie maja pojawic sie po prawej stronie przecinka dziesietnego, ograniczona do maksymalnie 4 wiecej niz maksymalna dostepna precyzja, w sumie 19 na wiekszosci maszyn; to umozliwia unikniecie bledow zaokraglenia, jesli wynikowy string zostanie pozniej odczytany jako wartosc zmiennoprzecinkowa. Jesli scientific jest falszem lub nie podano go, wynikiem jest string w formie `"MMMMMMM.DDDDDD"`, poprzedzony znakiem minus wtedy i tylko wtedy, gdy x jest ujemne. Jesli scientific jest podane i jest prawda, wynikiem jest string w formie `"M.DDDDDDe+EEE"`, ponownie poprzedzony znakiem minus wtedy i tylko wtedy, gdy x jest ujemne.

**Funkcja: `sqrt`**

sqrt -- Zwraca pierwiastek kwadratowy z x.

float `sqrt` (float x)

Zglasza `E_INVARG`, jesli x jest ujemne.

**Funkcja: `sin`**

sin -- Zwraca sinus x.

float `sin` (float x)

**Funkcja: `cos`**

cos -- Zwraca kosinus x.

float `cos` (float x)

**Funkcja: `tan`**

tan -- Zwraca tangens x.

float `tan` (float x)

**Funkcja: `asin`**

asin -- Zwraca arcus sinus (odwrotny sinus) x, w zakresie `[-pi/2..pi/2]`

float `asin` (float x)

Zglasza `E_INVARG`, jesli x jest poza zakresem `[-1.0..1.0]`.

**Funkcja: `acos`**

acos -- Zwraca arcus kosinus (odwrotny kosinus) x, w zakresie `[0..pi]`

float `acos` (float x)

Zglasza `E_INVARG`, jesli x jest poza zakresem `[-1.0..1.0]`.

**Funkcja: `atan`**

atan -- Zwraca arcus tangens (odwrotny tangens) y, w zakresie `[-pi/2..pi/2]`.

float `atan` (float y [, float x])

jesli x nie jest podane, lub `y/x` w zakresie `[-pi..pi]`, jesli x jest podane.

**Funkcja: `atan2`**

atan2 -- Zwraca arcus tangens y/x w zakresie `[-pi..pi]`.

float `atan2` (float y, float x)

**Funkcja: `sinh`**

sinh -- Zwraca sinus hiperboliczny x.

float `sinh` (float x)

**Funkcja: `cosh`**

cosh -- Zwraca kosinus hiperboliczny x.

float `cosh` (float x)

**Funkcja: `tanh`**

tanh -- Zwraca tangens hiperboliczny x.

float `tanh` (float x)

**Funkcja: `asinh`**

asinh -- Zwraca odwrotny sinus hiperboliczny x.

float `asinh` (float x)

**Funkcja: `acosh`**

acosh -- Zwraca odwrotny kosinus hiperboliczny x.

float `acosh` (float x)

Zglasza `E_INVARG`, jesli x jest mniejsze niz 1.0.

**Funkcja: `atanh`**

atanh -- Zwraca odwrotny tangens hiperboliczny x.

float `atanh` (float x)

Zglasza `E_INVARG`, jesli x jest poza zakresem `[-1.0..1.0]`.

**Funkcja: `exp`**

exp -- Zwraca e podniesione do potegi x.

float `exp` (float x)

**Funkcja: `log`**

log -- Zwraca logarytm naturalny x.

float `log` (float x)

Zglasza `E_INVARG`, jesli x nie jest dodatnie.

**Funkcja: `log10`**

log10 -- Zwraca logarytm dziesietny (o podstawie 10) x.

float `log10` (float x)

Zglasza `E_INVARG`, jesli x nie jest dodatnie.

**Funkcja: `ceil`**

ceil -- Zwraca najmniejsza liczbe calkowita nie mniejsza niz x, jako liczbe zmiennoprzecinkowa.

float `ceil` (float x)

**Funkcja: `floor`**

floor -- Zwraca najwieksza liczbe calkowita nie wieksza niz x, jako liczbe zmiennoprzecinkowa.

float `floor` (float x)

**Funkcja: `round`**

round -- Zwraca x zaokraglone do najblizszej wartosci calkowitej, jako liczbe zmiennoprzecinkowa.

float `round` (float x)

**Funkcja: `trunc`**

trunc -- Zwraca liczbe calkowita uzyskana przez obciecie x przy przecinku dziesietnym, jako liczbe zmiennoprzecinkowa.

float `trunc` (float x)

Dla ujemnego x jest to rownowazne `ceil()`; w przeciwnym razie jest to rownowazne `floor()`.

**Funkcja: `cbrt`**

cbrt -- Zwraca pierwiastek trzeciego stopnia (szescienny) z x.

float `cbrt` (float x)

**Funkcja: `distance`**

distance -- Zwraca odleglosc euklidesowa miedzy dwiema listami wspolrzednych.

float `distance` (LIST from, LIST to)

Obliczenie paruje wpisy wedlug indeksu, wiec wywolujacy powinni podawac listy wspolrzednych tej samej dlugosci. Kazdy element uzyty w obliczeniu musi byc liczba calkowita lub zmiennoprzecinkowa. Jesli ktoras z list zawiera element nienumeryczny, zglaszany jest `E_TYPE`.

**Funkcja: `relative_heading`**

relative_heading -- Zwraca kierunek horyzontalny i wertykalny od jednego trojwymiarowego punktu do drugiego.

list `relative_heading` (LIST from, LIST to)

Obie listy musza zawierac trzy liczby zmiennoprzecinkowe. Zwrocona lista zawiera dwie liczby calkowite: kierunek horyzontalny w stopniach i kierunek wertykalny w stopniach. Jesli ktoras z list zawiera elementy niebedace liczbami zmiennoprzecinkowymi, zglaszany jest `E_TYPE`.

**Funkcja: `simplex_noise`**

simplex_noise -- Zwraca szum simplex dla jednego do czterech wymiarow.

float `simplex_noise` (LIST coordinates)

Lista wspolrzednych musi zawierac jedna, dwie, trzy lub cztery liczby zmiennoprzecinkowe. Jesli jakakolwiek wspolrzedna nie jest liczba zmiennoprzecinkowa, zglaszany jest `E_TYPE`. Niewspierana liczba wymiarow zwraca `E_TYPE`.

##### Operacje na stringach

**Funkcja: `length`**

length -- Zwraca liczbe znakow w string.

int `length` (str string)

Mozliwe jest rowniez przekazanie listy lub mapy do `length()`; zobacz opis w nastepnej sekcji.

```
length("foo")   =>   3
length("")      =>   0
```

**Funkcja: `strsub`**

strsub -- Zastepuje wszystkie wystapienia what w subject przez with, wykonujac substytucje stringow.

str `strsub` (str subject, str what, str with [, int case-matters])

Wystapienia sa znajdowane od lewej do prawej, a wszystkie substytucje zachodza jednoczesnie. Domyslnie wystapienia what sa wyszukiwane, ignorujac rozroznienie wielkich i malych liter. Jesli case-matters jest podane i jest prawda, wielkosc liter jest traktowana jako istotna we wszystkich porownaniach.

```
strsub("%n is a fink.", "%n", "Fred")   =>   "Fred is a fink."
strsub("foobar", "OB", "b")             =>   "fobar"
strsub("foobar", "OB", "b", 1)          =>   "foobar"
```

**Funkcja: `index`**

**Funkcja: `rindex`**

index -- Zwraca indeks pierwszego znaku pierwszego wystapienia str2 w str1.

rindex -- Zwraca indeks pierwszego znaku ostatniego wystapienia str2 w str1.

int `index` (str str1, str str2 [, int case-matters [, int skip]])
int `rindex` (str str1, str str2 [, int case-matters [, int skip]])

Te funkcje zwroca zero, jesli str2 wogole nie wystepuje w str1.

Domyslnie wyszukiwanie wystapienia str2 odbywa sie, ignorujac rozroznienie wielkich i malych liter. Jesli case-matters jest podane i jest prawda, wielkosc liter jest traktowana jako istotna we wszystkich porownaniach.

Domyslnie wyszukiwanie zaczyna sie od poczatku (konca) str1. Jesli podano skip, wyszukiwanie pomija pierwsze (ostatnie) skip znakow i zaczyna sie od przesuniecia wzgledem poczatku (konca) str1. skip musi byc liczba calkowita dodatnia dla index() i liczba calkowita ujemna dla rindex(). Domyslna wartoscia skip jest 0 (nie pomijaj zadnych znakow).

```
index("foobar", "o")            =>   2
index("foobar", "o", 0, 0)      =>   2
index("foobar", "o", 0, 2)      =>   1
rindex("foobar", "o")           =>   3
rindex("foobar", "o", 0, 0)     =>   3
rindex("foobar", "o", 0, -4)    =>   2
index("foobar", "x")            =>   0
index("foobar", "oba")          =>   3
index("Foobar", "foo", 1)       =>   0
```

**Funkcja: `strtr`**

strtr -- Przeksztalca string source, zastepujac znaki podane w str1 odpowiadajacymi znakami podanymi w str2.

str `strtr` (str source, str str1, str str2 [, case-matters])

Wszystkie inne znaki nie sa przeksztalcane. Jesli str2 ma mniej znakow niz str1, niesparowane znaki sa po prostu usuwane z source. Domyslnie przeksztalcenie jest wykonywane na znakach wielkich i malych, niezaleznie od wielkosci liter. Jesli case-matters jest podane i jest prawda, wielkosc liter jest traktowana jako istotna.

```
strtr("foobar", "o", "i")           =>    "fiibar"
strtr("foobar", "ob", "bo")         =>    "fbboar"
strtr("foobar", "", "")             =>    "foobar"
strtr("foobar", "foba", "")         =>    "r"
strtr("5xX", "135x", "0aBB", 0)     =>    "BbB"
strtr("5xX", "135x", "0aBB", 1)     =>    "BBX"
strtr("xXxX", "xXxX", "1234", 0)    =>    "4444"
strtr("xXxX", "xXxX", "1234", 1)    =>    "3434"
```

**Funkcja: `strcmp`**

strcmp -- Wykonuje rozroznajace wielkosc liter porownanie dwoch stringow-argumentow.

int `strcmp` (str str1, str str2)

Jesli str1 jest [leksykograficznie](https://en.wikipedia.org/wiki/Lexicographical_order) mniejsze niz str2, `strcmp()` zwraca liczbe calkowita ujemna. Jesli oba stringi sa identyczne, `strcmp()` zwraca zero. W przeciwnym razie `strcmp()` zwraca liczbe calkowita dodatnia. Do porownania uzywane jest uporzadkowanie znakow ASCII.

**Funkcja: `explode`**

explode -- Zwraca liste podstringow subject, rozdzielonych przez break. break domyslnie przyjmuje wartosc spacji.

list  `explode`(STR subject [, STR break [, INT include-sequential-occurrences]])

Tylko pierwszy znak `break` jest brany pod uwage:

```
explode("slither%is%wiz", "%")      => {"slither", "is", "wiz"}
explode("slither%is%%wiz", "%%")    => {"slither", "is", "wiz"}
```

Mozesz uzyc include-sequential-occurrences, by otrzymac z powrotem pusty string jako czesc swojej listy, jesli `break` wystepuje wielokrotnie z niczym pomiedzy, albo jesli w Twoim stringu jest wiodacy/koncowy `break`:

```
explode("slither%is%%wiz", "%%", 1)  => {"slither", "is", "", "wiz"}
explode("slither%is%%wiz%", "%", 1)  => {"slither", "is", "", "wiz", ""}
explode("%slither%is%%wiz%", "%", 1) => {"", "slither", "is", "", "wiz", ""}
```

> Uwaga: to moze zostac uzyte jako zamiennik dla `$string_utils:explode`.

**Funkcja: `parse_ansi`**

parse_ansi -- Zastepuje tagi ANSI ToastStunt w string sekwencjami ucieczki ANSI.

str `parse_ansi` (STR string)

Rozpoznawane tagi obejmuja kolory pierwszego planu, takie jak `[red]`, `[green]`, `[yellow]`, `[blue]`, `[purple]`, `[cyan]`, `[white]`, `[gray]`, `[grey]` i `[black]`; kolory tla, takie jak `[b:red]`; tagi stylu, takie jak `[bold]`, `[underline]`, `[inverse]`, `[blink]`, `[normal]`, `[unbold]`, `[unblink]` i `[unbright]`; oraz tagi uzytkowe, takie jak `[beep]`, `[random]` i `[null]`.

**Funkcja: `remove_ansi`**

remove_ansi -- Usuwa tagi ANSI ToastStunt ze string.

str `remove_ansi` (STR string)

To usuwa te same tagi w nawiasach kwadratowych, rozpoznawane przez `parse_ansi()`, bez zastepowania ich sekwencjami ucieczki ANSI.

**Funkcja: `decode_binary`**

decode_binary -- Zwraca liste stringow i/lub liczb calkowitych reprezentujacych bajty w binarnym stringu bin_string, w porzadku.

list `decode_binary` (str bin-string [, int fully])

Jesli fully jest falszem lub pominiete, lista zawiera liczbe calkowita wylacznie dla kazdego niewypisywalnego, nie-spacjowego bajtu; wszystkie inne znaki sa grupowane w najdluzsze mozliwe ciagle podstringi. Jesli fully jest podane i jest prawda, lista zawiera wylacznie liczby calkowite, jedna dla kazdego bajtu reprezentowanego w bin_string. Zglasza `E_INVARG`, jesli bin_string nie jest poprawnie sformowanym stringiem binarnym. (Zobacz wczesniejsza sekcje o typach wartosci MOO po pelny opis stringow binarnych.)

```
decode_binary("foo")               =>   {"foo"}
decode_binary("~~foo")             =>   {"~foo"}
decode_binary("foo~0D~0A")         =>   {"foo", 13, 10}
decode_binary("foo~0Abar~0Abaz")   =>   {"foo", 10, "bar", 10, "baz"}
decode_binary("foo~0D~0A", 1)      =>   {102, 111, 111, 13, 10}
```

**Funkcja: `encode_binary`**

encode_binary -- Tlumaczy kazda liczbe calkowita i string po kolei na jej binarny odpowiednik string, zwracajac konkatenacje wszystkich tych podstringow w jeden binarny string.

str `encode_binary` (arg, ...)

Kazdy argument musi byc liczba calkowita od 0 do 255, stringiem lub lista zawierajaca wylacznie legalne argumenty dla tej funkcji. (Zobacz wczesniejsza sekcje o typach wartosci MOO po pelny opis stringow binarnych.)

```
encode_binary("~foo")                     =>   "~7Efoo"
encode_binary({"foo", 10}, {"bar", 13})   =>   "foo~0Abar~0D"
encode_binary("foo", 10, "bar", 13)       =>   "foo~0Abar~0D"
```

**Funkcja: `decode_base64`**

decode_base64 -- Zwraca binarna reprezentacje stringa podanego zakodowanego argumentu string Base64.

str `decode_base64` (str base64 [, int safe])

Zglasza E_INVARG, jesli base64 nie jest poprawnie sformowanym stringiem Base64. Jesli safe jest podane i jest prawda, uzywana jest wersja Base64 bezpieczna dla URL (zobacz RFC4648).

```
decode_base64("AAEC")      =>    "~00~01~02"
decode_base64("AAE", 1)    =>    "~00~01"
```

**Funkcja: `encode_base64`**

encode_base64 -- Zwraca zakodowana w Base64 reprezentacje stringa podanego binarnego argumentu string.

str `encode_base64` (str binary [, int safe])

Zglasza E_INVARG, jesli binary nie jest poprawnie sformowanym stringiem binarnym. Jesli safe jest podane i jest prawda, uzywana jest wersja Base64 bezpieczna dla URL (zobacz [RFC4648](https://datatracker.ietf.org/doc/html/rfc4648)).

```
encode_base64("~00~01~02")    =>    "AAEC"
encode_base64("~00~01", 1)    =>    "AAE"
```

**Funkcja: `spellcheck`**

spellcheck -- Ta funkcja sprawdza angielska ortografie word.

int | list `spellcheck`(STR word)

Jesli pisownia jest poprawna, funkcja zwroci 1. Jesli pisownia jest niepoprawna, zamiast tego zwrocona zostanie LISTA sugestii poprawnej pisowni. Jesli pisownia jest niepoprawna i nie mozna znalezc sugestii, zwracana jest pusta LISTA.

**Funkcja: `chr`**

chr -- Ta funkcja tlumaczy wartosci bajtowe na znaki ASCII. Argumentami moga byc liczby calkowite, stringi lub listy wartosci, ktore moga byc zakodowane jako bajty.

str `chr`(INT|STR|LIST arg, ...)

Dla programistow-czarodziejow calkowite wartosci bajtowe moga byc od 0 do 255. Jesli programista nie jest czarodziejem, calkowite wartosci bajtowe musza byc od 32 do 254; w przeciwnym razie zglaszany jest `E_INVARG`. To zapobiega zapisywaniu znakow kontrolnych, znakow nowej linii i niewlasciwych wartosci bajtowych do pliku bazy danych przez niezaufane osoby.

**Funkcja: `match`**

match -- Wyszukuje pierwsze wystapienie wyrazenia regularnego pattern w stringu subject

list `match` (str subject, str pattern [, int case-matters])

Jesli pattern jest skladniowo niepoprawny, zglaszany jest `E_INVARG`. Proces dopasowywania moze w niektorych przypadkach zajac duzo pamieci serwera; jesli to zuzycie pamieci stanie sie nadmierne, proces dopasowywania jest przerywany i zglaszany jest `E_QUOTA`.

Jesli nie znaleziono dopasowania, zwracana jest pusta lista; w przeciwnym razie te funkcje zwracaja liste zawierajaca informacje o dopasowaniu (zobacz nizej). Domyslnie wyszukiwanie ignoruje rozroznienie wielkich i malych liter. Jesli case-matters jest podane i jest prawda, wielkosc liter jest traktowana jako istotna we wszystkich porownaniach.

Lista, ktora zwraca `match()`, zawiera szczegoly o wykonanym dopasowaniu. Lista ma postac:

```
{start, end, replacements, subject}
```

gdzie start to indeks w subject poczatku dopasowania, end to indeks konca dopasowania, replacements to lista opisana nizej, a subject to ten sam string, ktory podano jako pierwszy argument do `match()`.

Lista replacements ma zawsze dziewiec elementow, kazdy element sam jest lista dwoch liczb calkowitych, indeksow poczatku i konca w string dopasowanego przez pewien wzorzec-podwyrazenie w nawiasach z pattern. Pierwszy element w replacements niesie indeksy dla pierwszego podwyrazenia w nawiasach, drugi element niesie te dla drugiego podwyrazenia, i tak dalej. Jesli w pattern jest mniej niz dziewiec podwyrazen w nawiasach, albo jesli jakies podwyrazenie nie zostalo uzyte w dopasowaniu, odpowiadajacy element w replacements to lista {0, -1}. Zobacz dyskusje o `%)` nizej, po wiecej informacji o podwyrazeniach w nawiasach.

```
match("foo", "^f*o$")        =>  {}
match("foo", "^fo*$")        =>  {1, 3, {{0, -1}, ...}, "foo"}
match("foobar", "o*b")       =>  {2, 4, {{0, -1}, ...}, "foobar"}
match("foobar", "f%(o*%)b")
        =>  {1, 4, {{2, 3}, {0, -1}, ...}, "foobar"}
```

**Funkcja: `rmatch`**

rmatch -- Wyszukuje ostatnie wystapienie wyrazenia regularnego pattern w stringu subject

list `rmatch` (str subject, str pattern [, int case-matters])

Jesli pattern jest skladniowo niepoprawny, zglaszany jest `E_INVARG`. Proces dopasowywania moze w niektorych przypadkach zajac duzo pamieci serwera; jesli to zuzycie pamieci stanie sie nadmierne, proces dopasowywania jest przerywany i zglaszany jest `E_QUOTA`.

Jesli nie znaleziono dopasowania, zwracana jest pusta lista; w przeciwnym razie te funkcje zwracaja liste zawierajaca informacje o dopasowaniu (zobacz nizej). Domyslnie wyszukiwanie ignoruje rozroznienie wielkich i malych liter. Jesli case-matters jest podane i jest prawda, wielkosc liter jest traktowana jako istotna we wszystkich porownaniach.

Lista, ktora zwraca `match()`, zawiera szczegoly o wykonanym dopasowaniu. Lista ma postac:

```
{start, end, replacements, subject}
```

gdzie start to indeks w subject poczatku dopasowania, end to indeks konca dopasowania, replacements to lista opisana nizej, a subject to ten sam string, ktory podano jako pierwszy argument do `match()`.

Lista replacements ma zawsze dziewiec elementow, kazdy element sam jest lista dwoch liczb calkowitych, indeksow poczatku i konca w string dopasowanego przez pewien wzorzec-podwyrazenie w nawiasach z pattern. Pierwszy element w replacements niesie indeksy dla pierwszego podwyrazenia w nawiasach, drugi element niesie te dla drugiego podwyrazenia, i tak dalej. Jesli w pattern jest mniej niz dziewiec podwyrazen w nawiasach, albo jesli jakies podwyrazenie nie zostalo uzyte w dopasowaniu, odpowiadajacy element w replacements to lista {0, -1}. Zobacz dyskusje o `%)` nizej, po wiecej informacji o podwyrazeniach w nawiasach.

```
rmatch("foobar", "o*b")      =>  {4, 4, {{0, -1}, ...}, "foobar"}
```

##### Wyrazenia regularne kompatybilne z Perlem (PCRE)

ToastStunt ma dwie metody operowania na wyrazeniach regularnych. Klasyczny styl (przestarzaly, trudniejszy w uzyciu, opisany w nastepnej sekcji) oraz preferowana biblioteka wyrazen regularnych kompatybilnych z Perlem. Nauczenie wyrazen regularnych wykracza poza zakres tego dokumentu, ale wyszukiwanie w internecie powinno dostarczyc wszystkich informacji potrzebnych do rozpoczecia tego, co z pewnoscia stanie sie podroza na cale zycie, pelna albo milosci, albo frustracji.

ToastCore udostepnia dwie podstawowe metody interakcji z wyrazeniami regularnymi.

**Funkcja: `pcre_match`**

pcre_match -- Funkcja `pcre_match()` wyszukuje `pattern` w `subject`, uzywajac biblioteki wyrazen regularnych kompatybilnych z Perlem. ToastStunt uzywa PCRE2 do tej funkcjonalnosci.

LIST `pcre_match`(STR subject, STR pattern [, ?case matters=0] [, ?repeat until no matches=1])

Wartoscia zwracana jest lista map zawierajacych kazde dopasowanie. Kazda zwrocona mapa bedzie miala klucz odpowiadajacy albo nazwanej grupie przechwytujacej, albo numerowi dopasowywanej grupy przechwytujacej. Pelne dopasowanie zawsze znajduje sie pod kluczem "0". Wartoscia kazdego klucza bedzie kolejna mapa zawierajaca klucze 'match' i 'position'. Match odpowiada tekstowi, ktory zostal dopasowany, a position zwroci indeksy podstringu w `subject`.

Jesli `repeat until no matches` wynosi 1, wyrazenie bedzie nadal ewaluowane, dopoki nie mozna znalezc kolejnych dopasowan albo dopoki nie wyczerpie limitu iteracji. Domyslnie wynosi 1.

Puste wzorce (pattern) zglaszaja `E_INVARG`. Puste subject sa poprawne, ale obecna implementacja zwraca pusta liste bez podejmowania proby dopasowania o dlugosci zero.

Dodatkowo czarodzieje moga kontrolowac, ile iteracji petli jest mozliwych, dodajac wlasciwosc do $server_options. $server_options.pcre_match_max_iterations to maksymalna liczba petli dozwolonych, przed poddaniem sie i pozwoleniem innym zadaniom na dzialanie. UWAGA: zaleca sie utrzymywanie tej wartosci na dosc niskim poziomie. Domyslna wartoscia jest 1000. Minimalna wartosc to 100.

Przyklady:

Wyodrebnienie dat ze stringa:

```
pcre_match("09/12/1999 other random text 01/21/1952", "([0-9]{2})/([0-9]{2})/([0-9]{4})")

=> {["0" -> ["match" -> "09/12/1999", "position" -> {1, 10}], "1" -> ["match" -> "09", "position" -> {1, 2}], "2" -> ["match" -> "12", "position" -> {4, 5}], "3" -> ["match" -> "1999", "position" -> {7, 10}]], ["0" -> ["match" -> "01/21/1952", "position" -> {30, 39}], "1" -> ["match" -> "01", "position" -> {30, 31}], "2" -> ["match" -> "21", "position" -> {33, 34}], "3" -> ["match" -> "1952", "position" -> {36, 39}]]}
```

Podzielenie stringa (choc to naciagany przyklad):

```
;;ret = {}; for x in (pcre_match("This is a string of words, with punctuation, that should be exploded. By space. --zippy--", "[a-zA-Z]+", 0, 1)) ret = {@ret, x["0"]["match"]}; endfor return ret;

=> {"This", "is", "a", "string", "of", "words", "with", "punctuation", "that", "should", "be", "exploded", "By", "space", "zippy"}
```

**Funkcja: `pcre_replace`**

pcre_replace -- Funkcja `pcre_replace()` zamienia `subject` na zamienniki znalezione w `pattern`, uzywajac biblioteki wyrazen regularnych kompatybilnych z Perlem. ToastStunt uzywa PCRE2 do tej funkcjonalnosci.

STR `pcre_replace` (STR `subject`, STR `pattern`)

String pattern ma okreslony format, ktorego trzeba sie trzymac, co powinno byc znajome, jesli uzywales czegos takiego jak Vim, Perl czy sed. String sklada sie z czterech elementow, kazdy rozdzielony delimiterem (typowo ukosnikiem (/) lub wykrzyknikiem (!)), ktore mowia silnikowi wyrazen regularnych, jak parsowac Twoj zamiennik. Rozlozymy string na czesci i wspomnimy o odpowiednich opcjach nizej:

1. Typ wyszukiwania do wykonania. W MOO poprawne jest wylacznie 's'. Ten parametr jest zachowany dla zachowania spojnosci.

2. Wzorzec wyrazenia regularnego do dopasowania.

3. Tekst zamiennika do podstawienia dla kazdego dopasowania.

4. Opcjonalne modyfikatory:
    * Global. To zastapi wszystkie wystapienia w Twoim stringu, zamiast zatrzymywac sie na pierwszym.
    * Case-insensitive (nierozroznianie wielkosci liter). Wielkie, male litery, to nie ma znaczenia. Wszystkie zostana zastapione.

Przyklady:

Zastapienie jednego slowa innym:

```
pcre_replace("I like banana pie. Do you like banana pie?", "s/banana/apple/g")

=> "I like apple pie. Do you like apple pie?"
```

Jesli chcesz zastapic string zawierajacy ukosniki, moze byc przydatne zmienic swoj delimiter na wykrzyknik:

```
pcre_replace("Unix, wow! /bin/bash is a thing.", "s!/bin/bash!/bin/fish!g")

=> "Unix, wow! /bin/fish is a thing."
```

**Funkcja: `pcre_cache_stats`**

pcre_cache_stats -- Zwraca statystyki cache wzorcow PCRE.

list `pcre_cache_stats` ()

Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`. Zwrocona lista zawiera wpisy w formie `{pattern, cache-hits}`.

##### Starsze wyrazenia regularne MOO (Legacy)

Dopasowywanie _wyrazen regularnych_ pozwala sprawdzic, czy string wpisuje sie w okreslony ksztalt skladniowy. Mozesz rowniez wyszukac w stringu podstring, ktory wpisuje sie we wzorzec.

Wyrazenie regularne opisuje zbior stringow. Najprostszy przypadek to takie, ktore opisuje konkretny string; na przyklad string `foo`, traktowany jako wyrazenie regularne, dopasowuje `foo` i nic wiecej. Nietrywialne wyrazenia regularne uzywaja pewnych specjalnych konstrukcji, by moc dopasowac wiecej niz jeden string. Na przyklad wyrazenie regularne `foo%|bar` dopasowuje albo string `foo`, albo string `bar`; wyrazenie regularne `c[ad]*r` dopasowuje ktorykolwiek ze stringow `cr`, `car`, `cdr`, `caar`, `cadddar` i wszystkie inne takie stringi z jakakolwiek liczba `a` i `d`.

Wyrazenia regularne maja skladnie, w ktorej kilka znakow to specjalne konstrukcje, a reszta to znaki _zwykle_. Znak zwykly to proste wyrazenie regularne, ktore dopasowuje ten znak i nic wiecej. Znakami specjalnymi sa `$`, `^`, `.`, `*`, `+`, `?`, `[`, `]` i `%`. Jakikolwiek inny znak wystepujacy w wyrazeniu regularnym jest zwykly, o ile nie jest poprzedzony przez `%`.

Na przyklad `f` nie jest znakiem specjalnym, jest wiec zwykly, a zatem `f` jest wyrazeniem regularnym, ktore dopasowuje string `f` i zaden inny string. (Nie dopasowuje, na przyklad, stringa `ff`.) Podobnie `o` jest wyrazeniem regularnym, ktore dopasowuje wylacznie `o`.

Jakiekolwiek dwa wyrazenia regularne a i b moga zostac skonkatenowane. Wynikiem jest wyrazenie regularne, ktore dopasowuje string, jesli a dopasowuje jakas czesc poczatku tego stringa, a b dopasowuje reszte stringa.

Jako prosty przyklad, mozemy skonkatenowac wyrazenia regularne `f` i `o`, by otrzymac wyrazenie regularne `fo`, ktore dopasowuje wylacznie string `fo`. Wciaz trywialne.

Nastepujace sa znaki i sekwencje znakow, ktore maja specjalne znaczenie w wyrazeniach regularnych. Jakikolwiek znak niewspomniany tutaj nie jest specjalny; reprezentuje dokladnie samego siebie dla celow wyszukiwania i dopasowywania.

| Sekwencje znakow      | Specjalne znaczenie                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |                                                                                                                 |                                                                                     |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| <code>.</code>        | jest znakiem specjalnym, ktory dopasowuje jakikolwiek pojedynczy znak. Uzywajac konkatenacji, mozemy stworzyc wyrazenia regularne takie jak <code>a.b</code>, ktore dopasowuje jakikolwiek trzyznakowy string zaczynajacy sie od <code>a</code> i konczacy sie na <code>b</code>.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                                                                 |                                                                                     |
| <code>*</code>        | nie jest samodzielna konstrukcja; jest sufiksem, ktory oznacza, ze poprzedzajace wyrazenie regularne ma zostac powtorzone tyle razy, ile mozliwe. W <code>fo*</code>, <code>*</code> odnosi sie do <code>o</code>, wiec <code>fo*</code> dopasowuje <code>f</code> nastepowane przez jakakolwiek liczbe <code>o</code>. Przypadek zera <code>o</code> jest dozwolony: <code>fo*</code> dopasowuje rowniez <code>f</code>.  <code>*</code> zawsze odnosi sie do <em>najmniejszego</em> mozliwego poprzedzajacego wyrazenia.  Tak wiec <code>fo*</code> ma powtarzajace sie <code>o</code>, nie powtarzajace sie <code>fo</code>.  Dopasowujacy przetwarza konstrukcje <code>*</code>, dopasowujac natychmiast tyle powtorzen, ile mozna znalezc. Nastepnie kontynuuje z reszta wzorca.  Jesli to sie nie powiedzie, wycofuje sie (backtracking), odrzucajac niektore z dopasowan konstrukcji z <code>*</code>, na wypadek gdyby to umozliwilo dopasowanie reszty wzorca. Na przyklad, dopasowujac <code>c[ad]*ar</code> do stringa <code>caddaar</code>, <code>[ad]*</code> najpierw dopasowuje <code>addaa</code>, ale to nie pozwala nastepnemu <code>a</code> we wzorcu zostac dopasowanym. Wiec ostatnie z dopasowan <code>[ad]</code> jest wycofywane, a nastepujace <code>a</code> jest probowane ponownie. Teraz to sie udaje.                                                                                                     |                                                                                                                 |                                                                                     |
| <code>+</code>        | <code>+</code> jest jak <code>*</code>, z tym ze wymagane jest co najmniej jedno dopasowanie poprzedzajacego wzorca dla <code>+</code>. Tak wiec <code>c[ad]+r</code> nie dopasowuje <code>cr</code>, ale dopasowuje wszystko inne, co dopasowalby <code>c[ad]*r</code>.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                 |                                                                                     |
| <code>?</code>        | <code>?</code> jest jak <code>*</code>, z tym ze pozwala na zero lub jedno dopasowanie poprzedzajacego wzorca. Tak wiec <code>c[ad]?r</code> dopasowuje <code>cr</code>, <code>car</code> lub <code>cdr</code>, i nic wiecej.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |                                                                                                                 |                                                                                     |
| <code>[ ... ]</code>  | <code>[</code> zaczyna <em>zestaw znakow</em>, ktory jest zakonczony przez <code>]</code>. W najprostszym przypadku znaki miedzy dwoma nawiasami kwadratowymi tworza ten zestaw. Tak wiec <code>[ad]</code> dopasowuje albo <code>a</code>, albo <code>d</code>, a <code>[ad]*</code> dopasowuje jakikolwiek string z <code>a</code> i <code>d</code> (wliczajac string pusty), z czego wynika, ze <code>c[ad]*r</code> dopasowuje <code>car</code> itd.<br>Zakresy znakow moga rowniez zostac wliczone do zestawu znakow, poprzez napisanie dwoch znakow z <code>-</code> pomiedzy nimi. Tak wiec <code>[a-z]</code> dopasowuje jakakolwiek mala litere. Zakresy moga byc swobodnie przemieszane z pojedynczymi znakami, jak w <code>[a-z$%.]</code>, ktory dopasowuje jakakolwiek mala litere lub <code>$</code>, <code>%</code> lub kropke.<br> Zauwaz, ze zwykle znaki specjalne nie sa juz specjalne wewnatrz zestawu znakow. Zupelnie inny zestaw znakow specjalnych istnieje wewnatrz zestawow znakow: <code>]</code>, <code>-</code> i <code>^</code>.<br> By wliczyc <code>]</code> do zestawu znakow, musisz uczynic go pierwszym znakiem.  Na przyklad <code>[]a]</code> dopasowuje <code>]</code> lub <code>a</code>. By wliczyc <code>-</code>, musisz go uzyc w kontekscie, w ktorym nie moze on wskazywac zakresu: to znaczy, jako pierwszy znak, lub bezposrednio po zakresie. |                                                                                                                 |                                                                                     |
| <code>[^ ... ]</code> | <code>[^</code> zaczyna <em>dopelniajacy zestaw znakow</em>, ktory dopasowuje jakikolwiek znak, oprocz tych podanych. Tak wiec <code>[^a-z0-9A-Z]</code> dopasowuje wszystkie znaki <em>oprocz</em> liter i cyfr.<br><code>^</code> nie jest specjalny w zestawie znakow, chyba ze jest pierwszym znakiem.  Znak nastepujacy po <code>^</code> jest traktowany, jakby byl pierwszy (moze to byc <code>-</code> lub <code>]</code>).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                                                                 |                                                                                     |
| <code>^</code>        | jest znakiem specjalnym, ktory dopasowuje string pusty -- ale tylko jesli jest na poczatku dopasowywanego stringa. W przeciwnym razie nie udaje mu sie dopasowac niczego.  Tak wiec <code>^foo</code> dopasowuje <code>foo</code>, ktore wystepuje na poczatku stringa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                 |                                                                                     |
| <code>$</code>        | jest podobny do <code>^</code>, ale dopasowuje wylacznie <em>koniec</em> stringa. Tak wiec <code>xx*$</code> dopasowuje string jednego lub wiecej <code>x</code> na koncu stringa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                                                                 |                                                                                     |
| <code>%</code>        | ma dwie funkcje: cytuje powyzsze znaki specjalne (wliczajac <code>%</code>) oraz wprowadza dodatkowe specjalne konstrukcje.<br> Poniewaz <code>%</code> cytuje znaki specjalne, <code>%$</code> jest wyrazeniem regularnym, ktore dopasowuje wylacznie <code>$</code>, a <code>%[</code> jest wyrazeniem regularnym, ktore dopasowuje wylacznie <code>[</code>, i tak dalej.<br> W wiekszosci przypadkow <code>%</code> nastepowane jakimkolwiek znakiem dopasowuje wylacznie ten znak. Jednak istnieje kilka wyjatkow: znaki, ktore, gdy poprzedzone <code>%</code>, sa specjalnymi konstrukcjami. Takie znaki sa zawsze zwykle, gdy napotkane samodzielnie.<br>  Zadne nowe znaki specjalne nigdy nie zostana zdefiniowane. Wszystkie rozszerzenia skladni wyrazen regularnych sa tworzone poprzez definiowanie nowych dwuznakowych konstrukcji, ktore zaczynaja sie od <code>%</code>.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                 |                                                                                     |
| <code>%\|</code>      | okresla alternatywe. Dwa wyrazenia regularne a i b z <code>%                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | </code> pomiedzy tworza wyrazenie, ktore dopasowuje wszystko, co dopasuje albo a, albo b.<br> Tak wiec <code>foo% | bar</code> dopasowuje albo <code>foo</code>, albo <code>bar</code>, ale zaden inny string. |
<code>%|</code> odnosi sie do najwiekszego mozliwego otaczajacego wyrazenia. Tylko otaczajace grupowanie <code>%( ... %)</code> moze ograniczyc sile grupowania <code>%|</code>.<br> Istnieje pelna mozliwosc wycofywania (backtracking) na wypadek uzycia wielu <code>%|</code>. |
| <code>%( ... %)</code> | jest konstrukcja grupujaca, ktora sluzy trzem celom:<br> * By zamknac zestaw alternatyw <code>%\|</code> dla innych operacji. Tak wiec <code>%(foo%\|bar%)x</code> dopasowuje albo <code>foox</code>, albo <code>barx</code>.<br> * By zamknac skomplikowane wyrazenie, na ktorym ma operowac nastepujace <code>*</code>, <code>+</code> lub <code>?</code>. Tak wiec <code>ba%(na%)*</code> dopasowuje <code>bananana</code> itd., z jakakolwiek liczba <code>na</code>, wliczajac brak.<br> * By oznaczyc dopasowany podstring do przyszlego uzycia.<br> Ta ostatnia funkcja nie jest konsekwencja idei grupowania w nawiasach; jest to odrebna funkcjonalnosc, ktora akurat zostala przypisana jako drugie znaczenie tej samej konstrukcji <code>%( ... %)</code>, poniewaz w praktyce nie ma konfliktu miedzy tymi dwoma znaczeniami. Tutaj jest wyjasnienie tej funkcjonalnosci: |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <code>%digit</code>    | Po zakonczeniu konstrukcji <code>%( ... %)</code>, dopasowujacy pamieta poczatek i koniec tekstu dopasowanego przez te konstrukcje. Nastepnie, dalej w wyrazeniu regularnym, mozesz uzyc <code>%</code> nastepowanego cyfra, by oznaczyc &quot;dopasuj ten sam tekst dopasowany przez digit-ta konstrukcje <code>%( ... %)</code> we wzorcu.&quot;  Konstrukcje <code>%( ... %)</code> sa numerowane w porzadku, w jakim ich <code>%(</code> wystepuja we wzorcu.<br> Stringi dopasowujace pierwszych dziewiec konstrukcji <code>%( ... %)</code> wystepujacych w wyrazeniu regularnym otrzymuja numery od 1 do 9 w porzadku swoich poczatkow. <code>%1</code> do <code>%9</code> moga byc uzyte, by odniesc sie do tekstu dopasowanego przez odpowiadajaca konstrukcje <code>%( ... %)</code>.<br> Na przyklad <code>%(.*%)%1</code> dopasowuje jakikolwiek string, ktory sklada sie z dwoch identycznych polowek. <code>%(.*%)</code> dopasowuje pierwsza polowe, ktora moze byc czymkolwiek, ale nastepujace <code>%1</code> musi dopasowac ten sam, dokladny tekst. |                                                                                                                 |
| <code>%b</code>        | dopasowuje string pusty, ale tylko jesli jest na poczatku lub koncu slowa. Tak wiec <code>%bfoo%b</code> dopasowuje jakiekolwiek wystapienie <code>foo</code> jako odrebne slowo. <code>%bball%(s%                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | %)%b</code> dopasowuje <code>ball</code> lub <code>balls</code> jako odrebne slowo.<br> Dla celow tej konstrukcji i pieciu nastepujacych, slowo jest zdefiniowane jako sekwencja liter i/lub cyfr. |
| <code>%B</code>        | dopasowuje string pusty, o ile <em>nie</em> jest na poczatku lub koncu slowa.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                 |
| <code>%&lt;</code>     | dopasowuje string pusty, ale tylko jesli jest na poczatku slowa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                 |
| <code>%&gt;</code>     | dopasowuje string pusty, ale tylko jesli jest na koncu slowa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                                                                 |
| <code>%w</code>        | dopasowuje jakikolwiek znak skladajacy sie na slowo (tzn. jakakolwiek litere lub cyfre).                                                                                                                                                                                                                                                                                                                                                                                                                                          |                                                                                                                 |
| <code>%W</code>        | dopasowuje jakikolwiek znak, ktory nie jest czescia slowa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                                                                                 |

**Funkcja: `substitute`**

substitute -- Wykonuje standardowy zestaw substytucji na stringu template, uzywajac informacji zawartych w subs, zwracajac wynikowy, przeksztalcony template.

str `substitute` (str template, list subs)

Subs powinien byc lista taka, jak te zwracane przez `match()` lub `rmatch()`, gdy dopasowanie sie powiedzie; w przeciwnym razie zglaszany jest `E_INVARG`.

W template stringi `%1` do `%9` zostana zastapione tekstem dopasowanym przez pierwszy do dziewiatego podwzorzec w nawiasach, gdy wywolano `match()` lub `rmatch()`. String `%0` w template zostanie zastapiony tekstem dopasowanym przez caly wzorzec, gdy wywolano `match()` lub `rmatch()`. String `%%` zostanie zastapiony pojedynczym znakiem `%`. Jesli `%` wystepuje w template, nastepowany jakimkolwiek innym znakiem, zglaszany jest `E_INVARG`.

```
subs = match("*** Welcome to ToastStunt!!!", "%(%w*%) to %(%w*%)");
substitute("I thank you for your %1 here in %2.", subs)
        =>   "I thank you for your Welcome here in ToastStunt."
```

**Funkcja: `salt`**

salt -- Generuje string salt kompatybilny z crypt() dla podanego formatu salt, uzywajac podanego binarnego losowego wejscia.

str `salt` (str format, str input)

Konkretny zestaw wspieranych formatow zalezy od bibliotek uzytych do zbudowania serwera, ale zawsze bedzie zawieral standardowy format salt, wskazywany przez string formatu "" (string pusty), oraz format salt BCrypt, wskazywany przez string formatu "$2a$NN$" (gdzie "NN" to wspolczynnik pracy). Inne mozliwe formaty obejmuja MD5 ("$1$"), SHA256 ("$5$") i SHA512 ("$6$"). Oba formaty, SHA256 i SHA512, wspieraja opcjonalne rundy.

```
salt("", ".M")                                           =>    "iB"
salt("$1$", "~183~1E~C6/~D1")                            =>    "$1$MAX54zGo"
salt("$5$", "x~F2~1Fv~ADj~92Y~9E~D4l~C3")                =>    "$5$s7z5qpeOGaZb"
salt("$5$rounds=2000$", "G~7E~A7~F5Q5~B7~0Aa~80T")       =>    "$5$rounds=2000$5trdp5JBreEM"
salt("$6$", "U7~EC!~E8~85~AB~CD~B5+~E1?")                =>    "$6$JR1vVUSVfqQhf2yD"
salt("$6$rounds=5000$", "~ED'~B0~BD~B9~DB^,\\~BD~E7")    =>    "$6$rounds=5000$hT0gxavqSl0L"
salt("$2a$08$", "|~99~86~DEq~94_~F3-~1A~D2#~8C~B5sx")    =>    "$2a$08$dHkE1lESV9KrErGhhJTxc."
```

> Uwaga: by zapewnic wlasciwe bezpieczenstwo, losowe wejscie musi pochodzic z wystarczajaco losowego zrodla.

**Funkcja: `crypt`**

crypt -- Szyfruje podany text, uzywajac standardowej metody szyfrowania UNIX.

str `crypt` (str text [, str salt])

Szyfruje (hashuje) podany text, uzywajac standardowej metody szyfrowania UNIX. Jesli podano, salt powinien byc stringiem o dlugosci co najmniej dwoch znakow i moze dyktowac konkretny algorytm do uzycia. Domyslnie crypt uzywa oryginalnego, obecnie niebezpiecznego algorytmu DES. ToastStunt konkretnie zawiera algorytm BCrypt (identyfikowany przez salt zaczynajace sie od "$2a$") i moze zawierac algorytmy MD5, SHA256 i SHA512, w zaleznosci od bibliotek uzytych do zbudowania serwera. Uzyty salt jest zwracany jako pierwsza czesc wynikowego zaszyfrowanego stringa.

Poza mozliwie losowym wejsciem w salt, algorytmy szyfrujace sa calkowicie deterministyczne. W szczegolnosci mozesz sprawdzic, czy podany string jest taki sam jak ten uzyty do wytworzenia danego fragmentu zaszyfrowanego tekstu; po prostu wyodrebnij salt z przodu zaszyfrowanego tekstu i podaj kandydujacy string oraz salt do crypt(). Jesli wynik jest identyczny z podanym zaszyfrowanym tekstem, masz dopasowanie.

```
crypt("foobar", "iB")                               =>    "iBhNpg2tYbVjw"
crypt("foobar", "$1$MAX54zGo")                      =>    "$1$MAX54zGo$UKU7XRUEEiKlB.qScC1SX0"
crypt("foobar", "$5$s7z5qpeOGaZb")                  =>    "$5$s7z5qpeOGaZb$xkxjnDdRGlPaP7Z ... .pgk/pXcdLpeVCYh0uL9"
crypt("foobar", "$5$rounds=2000$5trdp5JBreEM")      =>    "$5$rounds=2000$5trdp5JBreEM$Imi ... ckZPoh7APC0Mo6nPeCZ3"
crypt("foobar", "$6$JR1vVUSVfqQhf2yD")              =>    "$6$JR1vVUSVfqQhf2yD$/4vyLFcuPTz ... qI0w8m8az076yMTdl0h."
crypt("foobar", "$6$rounds=5000$hT0gxavqSl0L")      =>    "$6$rounds=5000$hT0gxavqSl0L$9/Y ... zpCATppeiBaDxqIbAN7/"
crypt("foobar", "$2a$08$dHkE1lESV9KrErGhhJTxc.")    =>    "$2a$08$dHkE1lESV9KrErGhhJTxc.QnrW/bHp8mmBl5vxGVUcsbjo3gcKlf6"
```

> Uwaga: konkretny zestaw wspieranych algorytmow zalezy od bibliotek uzytych do zbudowania serwera. Gwarantowana jest wylacznie dostepnosc algorytmu BCrypt, ktory jest dystrybuowany z kodem zrodlowym serwera. BCrypt jest obecnie dojrzaly i dobrze przetestowany i jest zalecany dla nowych projektow, gdy biblioteka Argon2 jest niedostepna. (Zobacz nastepna sekcje).

> Ostrzezenie: caly salt (jakiejkolwiek dlugosci) jest przekazywany do niskopoziomowej funkcji crypt systemu operacyjnego. Jest jednak malo prawdopodobne, ze wszystkie systemy operacyjne zwroca ten sam string, gdy otrzymaja dluzszy salt. W zwiazku z tym identyczne wywolania crypt() moga generowac rozne wyniki na roznych platformach, a Twoje systemy weryfikacji hasel zawiodlyby. Uzywanie salt dluzszego niz dwa znaki jest na wlasne ryzyko.

**Funkcja: `argon2`**

argon2 -- Hashuje haslo, uzywajac algorytmu hashowania hasel Argon2id.

Funkcja `argon2()` hashuje haslo, uzywajac algorytmu hashowania hasel Argon2id. Jest parametryzowana trzema opcjonalnymi argumentami:

str `argon2` (STR password, STR salt [, iterations = 3] [, memory usage in KB = 4096] [, CPU threads = 1])

 * Time (czas): to liczba razy, jaka hash zostanie wykonany. To okresla ilosc wymaganych obliczen i, w efekcie, jak dlugo funkcja bedzie potrzebowala, by sie zakonczyc.
 * Memory (pamiec): to, jak duzo RAM jest zarezerwowane do hashowania.
 * Parallelism (rownoleglosc): to liczba watkow CPU, ktore beda dzialac rownolegle.

Salt do hasla powinien miec co najmniej 16 bajtow do hashowania hasel. Zaleca sie uzycie funkcji random_bytes().

Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`.

```
salt = random_bytes(20);
return argon2(password, salt, 3, 4096, 1);
```

> Ostrzezenie: MOO jest w wiekszosci przypadkow jednowatkowe, a ta funkcja moze zajac znaczaco duzo czasu, w zaleznosci od tego, jak ja wywolasz. Podczas gdy dziala, nic innego nie bedzie sie dzialo na Twoim MOO. Mozliwe jest zbudowanie serwera z opcja `THREAD_ARGON2`, ktora zminimalizuje lag. To ma jednak istotne zastrzezenia, zobacz sekcje nizej o `argon2_verify` po wiecej informacji.

**Funkcja: `argon2_verify`**

argon2_verify -- Porownuje password do wczesniej zahashowanego hash.

int argon2_verify (STR hash, STR password)

Zwraca 1, jesli te dwa sie zgadzaja, lub 0, jesli nie.

Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`.

To bezpieczniejszy sposob hashowania hasel niz wbudowana funkcja `crypt()`.

> Uwaga: ToastCore definiuje pewne rozsadne wartosci domyslne dla sposobu uzycia `argon2` i `argon2_verify`. Mozesz uzyc `@grep argon2` w ToastCore, by je znalezc.

> Ostrzezenie: mozliwe jest zbudowanie serwera z opcja `THREAD_ARGON2`. To umozliwi tej funkcji wbudowanej dzialanie w watku w tle i zminimalizuje lag, jaki te funkcje moga powodowac. Jednak to niesie ze soba pewne istotne zastrzezenia. `do_login_command` (gdzie typowo bedziesz weryfikowac hasla) nie moze zostac zawieszony. Poniewaz watkowanie niejawnie zawiesza zadanie MOO, nie bedziesz mogl uzyc Argon2 bezposrednio w do_login_command. Zamiast tego bedziesz musial opracowac nowe rozwiazanie dla logowania, ktore nie wymaga bezposredniego wywolania Argon2 w do_login_command.

> Uwaga: wiecej informacji o Argon2 mozna znalezc na [Argon2 Github](https://github.com/P-H-C/phc-winner-argon2).

**Funkcja: `string_hash`**

**Funkcja: `binary_hash`**

string_hash -- Zwraca string kodujacy wynik zastosowania kryptograficznie bezpiecznej funkcji hashujacej SHA256 do zawartosci stringa text lub binarnego stringa bin-string.

binary_hash -- Zwraca string kodujacy wynik zastosowania kryptograficznie bezpiecznej funkcji hashujacej SHA256 do zawartosci stringa text lub binarnego stringa bin-string.

str `string_hash` (str string [, str algo [, any binary]])

str `binary_hash` (str bin-string [, str algo [, any binary]])

Jesli podano algo, okresla ono algorytm hashowania do uzycia. Wspierane sa "MD5", "SHA1", "SHA224", "SHA256", "SHA384", "SHA512" i "RIPEMD160". Jesli binary jest podane i jest prawda, wynik jest w formacie binarnego stringa MOO; domyslnie wynik jest stringiem szesnastkowym.

Zauwaz, ze algorytm hashujacy MD5 jest zlamany z kryptograficznego punktu widzenia, podobnie jak SHA1. Oba sa wliczone dla interoperacyjnosci z istniejacymi aplikacjami (oba sa wciaz popularne).

Wszystkie wspierane funkcje hashujace maja te wlasciwosc, ze jesli

`string_hash(x) == string_hash(y)`

to, prawie na pewno,

`equal(x, y)`

To moze byc przydatne, na przyklad, w pewnych aplikacjach sieciowych: po wyslaniu duzego fragmentu tekstu przez polaczenie, wyslij rowniez wynik zastosowania string_hash() do tego tekstu; jesli strona docelowa rowniez zastosuje string_hash() do tekstu i otrzyma ten sam wynik, mozesz byc calkiem przekonany, ze duzy tekst dotarl bez zmian.

**Funkcja: `string_hmac`**

**Funkcja: `binary_hmac`**

str `string_hmac` (str text, str key [, str algo [, binary]])

str binary_hmac (str bin-string, str key [, str algo [, binary]])

Zwraca string kodujacy wynik zastosowania kryptograficznie bezpiecznej funkcji HMAC-SHA256 do zawartosci stringa text lub binarnego stringa bin-string z podanym tajnym kluczem. Jesli podano algo, okresla ono algorytm hashowania do uzycia. Obecnie wspierane sa wylacznie "SHA1" i "SHA256". Jesli binary jest podane i jest prawda, wynik jest w formacie binarnego stringa MOO; domyslnie wynik jest stringiem szesnastkowym.

Wszystkie kryptograficznie bezpieczne HMAC-i maja te wlasciwosc, ze jesli

`string_hmac(x, a) == string_hmac(y, b)`

to, prawie na pewno,

`equal(x, y)`

a ponadto,

`equal(a, b)`

To moze byc przydatne, na przyklad, w aplikacjach, ktore musza zweryfikowac zarowno integralnosc wiadomosci (tekstu), jak i autentycznosc nadawcy (wykazywana przez posiadanie tajnego klucza).

##### Operacje na listach

**Funkcja: `length`**

length -- Zwraca liczbe elementow w list lub map.

int `length` (list|map value)

Mozliwe jest rowniez przekazanie stringa do `length()`; zobacz opis w poprzedniej sekcji.

```
length({1, 2, 3})   =>   3
length({})          =>   0
length(["a" -> 1])  =>   1
```

**Funkcja: `is_member`**

is_member -- Zwraca prawde, jesli istnieje element list, ktory jest calkowicie nieodroznialny od value.

int `is_member` (ANY value, LIST list [, INT case-sensitive])

To w duzej mierze ta sama operacja co " `value in list`", z tym ze, w przeciwienstwie do `in`, funkcja `is_member()` nie traktuje wielkich i malych liter w stringach jako rownych. Ten sposob traktowania stringow moze byc kontrolowany za pomoca argumentu `case-sensitive`; ustawienie `case-sensitive` na falsz efektywnie wylacza to zachowanie.

Zglasza E_ARGS, jesli podano dwie wartosci lub jesli podano wiecej niz trzy argumenty. Zglasza E_TYPE, jesli drugi argument nie jest lista. W przeciwnym razie zwraca indeks `value` w `list`, lub 0, jesli go tam nie ma.

```
is_member(3, {3, 10, 11})                  => 1
is_member("a", {"A", "B", "C"})            => 0
is_member("XyZ", {"XYZ", "xyz", "XyZ"})    => 3
is_member("def", {"ABC", "DEF", "GHI"}, 0) => 2 
```

**Funkcja: `all_members`**

all_members -- Zwraca indeksy kazdego wystapienia `value` w `alist`.

LIST `all_members`(ANY `value`, LIST `alist`)

Przyklad:

```
all_members("a", {"a", "b", "a", "c", "a", "d"}) => {1, 3, 5}
```

**Funkcja: `listinsert`**

**Funkcja: `listappend`**

listinsert -- Ta funkcja zwraca kopie list z value dodanym jako nowy element.

listappend -- Ta funkcja zwraca kopie list z value dodanym jako nowy element.

list `listinsert` (list list, value [, int index])

list `listappend` (list list, value [, int index])

`listinsert()` i `listappend()` dodaja value przed i po (odpowiednio) istniejacym elemencie o podanym index, jesli podano.

Nastepujace trzy wyrazenia zawsze maja te sama wartosc:

```
listinsert(list, element, index)
listappend(list, element, index - 1)
{@list[1..index - 1], element, @list[index..length(list)]}
```

Jesli index nie jest podany, `listappend()` dodaje value na koniec listy, a `listinsert()` dodaje go na poczatek; to uzycie jest jednak odradzane, poniewaz ta sama intencja moze zostac wyrazona jasniej za pomoca wyrazenia konstrukcji listy, jak pokazano w przykladach nizej.

```
x = {1, 2, 3};
listappend(x, 4, 2)   =>   {1, 2, 4, 3}
listinsert(x, 4, 2)   =>   {1, 4, 2, 3}
listappend(x, 4)      =>   {1, 2, 3, 4}
listinsert(x, 4)      =>   {4, 1, 2, 3}
{@x, 4}               =>   {1, 2, 3, 4}
{4, @x}               =>   {4, 1, 2, 3}
```

**Funkcja: `listdelete`**

listdelete -- Zwraca kopie list z usunietym elementem o pozycji index.

list `listdelete` (list list, int index)

Jesli index nie jest w zakresie `[1..length(list)]`, zglaszany jest `E_RANGE`.

```
x = {"foo", "bar", "baz"};
listdelete(x, 2)   =>   {"foo", "baz"}
```

**Funkcja: `listset`**

listset -- Zwraca kopie list z elementem o pozycji index zastapionym przez value.

list `listset` (list list, value, int index)

Jesli index nie jest w zakresie `[1..length(list)]`, zglaszany jest `E_RANGE`.

```
x = {"foo", "bar", "baz"};
listset(x, "mumble", 2)   =>   {"foo", "mumble", "baz"}
```

Ta funkcja istnieje przede wszystkim z powodow historycznych; byla intensywnie uzywana, zanim serwer zaczal wspierac przypisania indeksowane takie jak `x[i] = v`. Nowy kod powinien zawsze uzywac przypisania indeksowanego zamiast `listset()`, gdziekolwiek to mozliwe.

**Funkcja: `setadd`**

**Funkcja: `setremove`**

setadd -- Zwraca kopie list z dodana podana value.

setremove -- Zwraca kopie list z usunieta podana value.

list `setadd` (list list, value)

list `setremove` (list list, value)

`setadd()` dodaje value tylko jesli nie jest ono juz elementem list; list jest wiec traktowana jako zbior matematyczny. value jest dodawane na koniec wynikowej listy, jesli w ogole. Podobnie `setremove()` zwraca liste identyczna z list, jesli value nie jest jej elementem. Jesli value wystepuje w list wiecej niz raz, w zwroconej kopii usuwane jest tylko pierwsze wystapienie.

```
setadd({1, 2, 3}, 3)         =>   {1, 2, 3}
setadd({1, 2, 3}, 4)         =>   {1, 2, 3, 4}
setremove({1, 2, 3}, 3)      =>   {1, 2}
setremove({1, 2, 3}, 4)      =>   {1, 2, 3}
setremove({1, 2, 3, 2}, 2)   =>   {1, 3, 2}
```

**Funkcja: `reverse`**

reverse -- Zwraca odwrocona liste lub string.

str | list `reverse`(LIST|STR value)

Jesli value nie jest ani lista, ani stringiem, zglaszany jest `E_INVARG`.

Przyklady:

```
reverse({1,2,3,4}) => {4,3,2,1}
reverse("asdf") => "fdsa"
```

**Funkcja: `slice`**

list `slice`(LIST alist [, INT | LIST | STR index, ANY default map value])

Zwraca elementy alist o pozycji index. Domyslnie index bedzie wynosic 1. Jesli index jest lista liczb calkowitych, zwrocona lista bedzie miala te elementy z alist. To wbudowany rownowaznik czasownika $list_utils:slice z LambdaCore.

Jesli alist jest lista map, index moze byc stringiem wskazujacym klucz do zwrocenia z kazdej mapy w alist.

Jesli podano default map value, kazda mapa nieposiadajaca klucza index bedzie miala zwrocone default map value w jej miejsce. To przydatne w sytuacjach, gdy musisz zachowac zgodnosc z indeksem listy i nie mozesz miec dziur w swojej zwracanej liscie.

Przyklady:

```
slice({{"z", 1}, {"y", 2}, {"x",5}}, 2)                                 => {1, 2, 5}
slice({{"z", 1, 3}, {"y", 2, 4}}, {2, 1})                               => {{1, "z"}, {2, "y"}}
slice({["a" -> 1, "b" -> 2], ["a" -> 5, "b" -> 6]}, "a")                => {1, 5}
slice({["a" -> 1, "b" -> 2], ["a" -> 5, "b" -> 6], ["b" -> 8]}, "a", 0) => {1, 5, 0}
```
**Funkcja: `sort`**

sort -- Sortuje list albo wedlug keys, albo uzywajac samej listy.

list `sort`(LIST list [, LIST keys, INT natural sort order?, INT reverse])

Podczas sortowania list wedlug samej siebie, mozesz uzyc pustej listy ({}) dla keys, by podac dodatkowe opcjonalne argumenty.

Podczas sortowania wedlug niepustej listy keys, lista keys musi miec taka sama dlugosc jak list, w przeciwnym razie zglaszany jest `E_INVARG`. Wartosci uzyte do sortowania musza byc jednorodnymi wartosciami skalarnymi. Listy, mapy, obiekty anonimowe i WAIF-y nie moga zostac zsortowane i zglaszaja `E_TYPE`.

Jesli natural sort order jest prawda, stringi zawierajace wieloznakowe liczby beda traktowac te liczby jako pojedynczy znak. Tak wiec, na przyklad, to znaczy, ze 'x2' bedzie wystepowac przed 'x11' przy naturalnym sortowaniu, poniewaz 2 jest mniejsze niz 11. Ten argument domyslnie wynosi 0.

Jesli reverse jest prawda, porzadek sortowania jest odwrocony. Ten argument domyslnie wynosi 0.

Przyklady:

Sortowanie listy wedlug samej siebie:

```
sort({"a57", "a5", "a7", "a1", "a2", "a11"}) => {"a1", "a11", "a2", "a5", "a57", "a7"}
```

Sortowanie listy wedlug samej siebie z naturalnym porzadkiem sortowania:

```
sort({"a57", "a5", "a7", "a1", "a2", "a11"}, {}, 1) => {"a1", "a2", "a5", "a7", "a11", "a57"}
```

Sortowanie listy stringow wedlug listy numerycznych kluczy:

```
sort({"foo", "bar", "baz"}, {123, 5, 8000}) => {"bar", "foo", "baz"}
```

> Uwaga: to funkcja watkowana.

##### Operacje na mapach

Mapy sa porzadkowane wedlug swoich kluczy, nie wedlug porzadku, w jakim wpisy zostaly wstawione. Funkcje, ktore przechodza przez cala mape, takie jak `mapkeys()` i `mapvalues()`, zwracaja wpisy w tym porzadku kluczy. Klucze tego samego typu sa porzadkowane wedlug ich naturalnego porownania: liczby numerycznie, numery obiektow wedlug id obiektu, bledy wedlug wartosci bledu, a stringi leksykalnie. Klucze-stringi sa zwykle porownywane bez rozroznienia wielkosci liter, wiec klucze rozniace sie wylacznie wielkoscia liter sa traktowane jako ten sam klucz przy zwyklym dostepie do mapy. Klucze roznych typow sa grupowane wedlug wewnetrznego porzadku typow serwera; jest to deterministyczne, ale zwykle nie powinno byc uzywane jako znaczacy porzadek na poziomie aplikacji.

Na przyklad:

```
x = [3 -> "three", 1 -> "one", "foo" -> 4, "bar" -> 5];
mapkeys(x)   => {1, 3, "bar", "foo"}
mapvalues(x) => {"one", "three", 5, 4}
```

Jesli potrzebujesz porzadku wstawiania, porzadku wyswietlania lub jakiegos innego wlasnego porzadkowania, przechowuj ten porzadek w osobnej liscie lub sortuj klucze explicite.

**Funkcja: `mapkeys`**

mapkeys -- zwraca klucze elementow mapy.

list `mapkeys` (map map)

```
x = ["foo" -> 1, "bar" -> 2, "baz" -> 3];
mapkeys(x)   =>  {"bar", "baz", "foo"}
```

**Funkcja: `mapvalues`**

mapvalues -- zwraca wartosci elementow mapy.

list `mapvalues` (MAP `map` [, ... ANY `key`])

Jesli chcesz wylacznie wartosci konkretnych kluczy w mapie, mozesz je podac jako opcjonalne argumenty. Zobacz przyklady nizej.

Jesli jakikolwiek zadany klucz nie jest obecny w mapie, zglaszany jest `E_RANGE`.

Przyklady:

```
x = ["foo" -> 1, "bar" -> 2, "baz" -> 3];
mapvalues(x)               =>  {2, 3, 1}
mapvalues(x, "foo", "baz") => {1, 3}
```

**Funkcja: `mapdelete`**

mapdelete -- Zwraca kopie map z wartoscia odpowiadajaca key(s) usunieta.

map `mapdelete` (MAP map, key|LIST keys)

Jesli key jest wartoscia kolekcji, taka jak lista lub mapa, zglaszany jest `E_TYPE`. Jesli key jest poprawny, ale nie jest obecny w mapie, zglaszany jest `E_RANGE`.

```
x = ["foo" -> 1, "bar" -> 2, "baz" -> 3];
mapdelete(x, "bar")   =>   ["baz" -> 3, "foo" -> 1]
```

Gdy jako drugi argument podana zostanie lista, mapdelete() usunie teraz wiele kluczy z mapy w jednej operacji. Jesli jakikolwiek klucz z listy nie zostanie znaleziony, zglaszany jest `E_RANGE` z opisowa wartoscia wskazujaca, ktory klucz byl brakujacy.

**Funkcja: `maphaskey`**

maphaskey -- Zwraca 1, jesli key istnieje w map. Gdy nie mamy do czynienia z setkami kluczy, ta funkcja jest szybsza (i latwiejsza do odczytania) niz cos w rodzaju: !(x in mapkeys(map))

int `maphaskey` (MAP map, ANY key [, INT case-matters])

Jesli `case-matters` jest prawda, porownanie klucza-stringa rozroznia wielkosc liter. Wartosci kolekcji nie moga byc uzyte jako klucze do tego wyszukiwania; jesli key jest lista, mapa lub inna wartoscia kolekcji, zglaszany jest `E_TYPE`.

#### Manipulowanie obiektami

Obiekty sa, oczywiscie, glownym punktem zainteresowania wiekszosci programowania MOO i, w duzej mierze z tego powodu, istnieje wiele funkcji wbudowanych do ich manipulowania.

##### Podstawowe operacje na obiektach

**Funkcja: `create`**

create -- Tworzy i zwraca nowy obiekt, ktorego rodzicem (lub rodzicami) jest parent (lub parents) i ktorego wlasciciel jest jak opisano nizej.

obj `create` (obj parent [, obj owner] [, int anon-flag] [, list init-args])

obj `create` (list parents [, obj owner] [, int anon-flag] [, list init-args])

Tworzy i zwraca nowy obiekt, ktorego rodzicami sa parents (lub ktorego rodzicem jest parent) i ktorego wlasciciel jest jak opisano nizej. Jesli ktorykolwiek z podanych parents nie jest poprawny, lub jesli podany parent nie jest ani poprawny, ani #-1, zglaszany jest E_INVARG. Podane obiekty parents musza byc poprawne i musza byc uzywalne jako rodzic (tzn. ich bit `a` lub `f` musi byc prawda), albo programista musi byc wlascicielem parents lub czarodziejem; w przeciwnym razie zglaszany jest E_PERM. Ponadto, jesli anon-flag jest prawda, `a` musi byc prawda; a jesli anon-flag jest falszem lub nie podano go, `f` musi byc prawda. W przeciwnym razie zglaszany jest E_PERM, o ile programista nie jest wlascicielem parents lub czarodziejem. E_PERM jest rowniez zglaszany, jesli owner jest podany i nie jest taki sam jak programista, o ile programista nie jest czarodziejem.

Po utworzeniu nowego obiektu wywolywany jest jego czasownik initialize, jesli istnieje. Jesli podano init-args, sa one przekazywane jako args do initialize. Nowemu obiektowi przypisywany jest najmniejszy nieujemny numer obiektu, ktory nie zostal jeszcze uzyty dla utworzonego obiektu. Zauwaz, ze zaden numer obiektu nigdy nie jest uzyty ponownie, nawet jesli obiekt o tym numerze zostanie poddany recyklingowi.

> Uwaga: to nie jest do konca prawda, zwlaszcza jesli uzywasz ToastCore i `$recycler`, co jest swietnym pomyslem. Jesli nie, skonczysz z bardzo wysokimi numerami obiektow. Jednak jesli planujesz ponowne uzywanie numerow obiektow, musisz to uwazne rozwazyc w swoim kodzie. Nie chcesz umieszczac numerow obiektow w swoim kodzie w takim przypadku, poniewaz numery obiektow mogly sie zmienic. Uzywaj zamiast tego skorifikowanych referencji. Na przyklad mozesz uzyc `@corify #numerobiektu as $moj_obiekt`, a nastepnie odwolywac sie do $moj_obiekt w swoim kodzie. Alternatywnie mozesz zrobic ` @prop $sysobj.moj_obiekt #numerobiektu`. Jesli numer obiektu kiedykolwiek sie zmieni, mozesz zmienic referencje bez aktualizowania calego swojego kodu.)

> Uwaga: $sysobj to typowo #0. Choc technicznie moze zostac zmienione na cos innego, autor nie zna zadnego powodu, by odejsc tutaj od konwencji.

Jesli anon-flag jest falszem lub nie podano go, nowy obiekt jest obiektem permanentnym i otrzymuje najmniejszy nieujemny numer obiektu, ktory nie zostal jeszcze uzyty dla utworzonego obiektu. Zauwaz, ze zaden numer obiektu nigdy nie jest uzyty ponownie, nawet jesli obiekt o tym numerze zostanie poddany recyklingowi.

Jesli anon-flag jest prawda, nowy obiekt jest obiektem anonimowym i nie otrzymuje numeru obiektu. Obiekty anonimowe sa automatycznie poddawane recyklingowi, gdy nie sa juz uzywane.

Wlascicielem nowego obiektu jest albo programista (jesli owner nie zostal podany), sam nowy obiekt (jesli owner zostal podany i jest niepoprawny), albo owner (w przeciwnym razie).

Inne wbudowane wlasciwosci nowego obiektu sa inicjowane w nastepujacy sposob:

```
name         ""
location     #-1
contents     {}
programmer   0
wizard       0
r            0
w            0
f            0
```

Funkcja `is_player()` zwraca falsz dla nowo utworzonych obiektow.

Dodatkowo nowy obiekt dziedziczy wszystkie inne wlasciwosci swoich rodzicow. Te wlasciwosci maja te same bity uprawnien, co na rodzicach. Jesli bit uprawnien `c` jest ustawiony, wlascicielem wlasciwosci na nowym obiekcie jest ten sam, co wlasciciel samego nowego obiektu; w przeciwnym razie wlascicielem wlasciwosci na nowym obiekcie jest ten sam, co na rodzicu. Poczatkowa wartosc kazdej dziedziczonej wlasciwosci jest czysta (clear); zobacz opis funkcji wbudowanej clear_property() po szczegoly.

Jesli zamierzony wlasciciel nowego obiektu ma wlasciwosc o nazwie `ownership_quota`, a wartosc tej wlasciwosci jest liczba calkowita, `create()` traktuje te wartosc jako quota (limit). Jesli quota jest mniejsza lub rowna zeru, quota jest uznawana za wyczerpana i `create()` zglasza E_QUOTA zamiast tworzyc obiekt. W przeciwnym razie quota jest zmniejszana i zapisywana z powrotem do wlasciwosci `ownership_quota` jako czesc tworzenia nowego obiektu.

> Uwaga: w ToastStunt to jest domyslnie wylaczone za pomoca opcji "OWNERSHIP_QUOTA" w options.h

**Funkcja: `owned_objects`**

owned_objects -- Zwraca liste wszystkich obiektow w bazie danych, ktorych wlascicielem jest `owner`. Wlasnosc jest okreslana przez wartosc .owner na obiekcie.

list `owned_objects`(OBJ owner)

Zglasza `E_INVIND`, jesli owner nie jest poprawnym obiektem.

**Funkcja: `chparent`**

**Funkcja: `chparents`**

chparent -- Zmienia rodzica object na new-parent.

chparents -- Zmienia rodzica object na new-parents.

none `chparent` (obj object, obj new-parent)

none `chparents` (obj object, list new-parents)

Jesli object jest niepoprawny, lub jesli new-parent nie jest ani poprawny, ani rowny `#-1`, zglaszany jest `E_INVARG`. Jesli programista nie jest ani czarodziejem, ani wlascicielem object, lub jesli new-parent nie jest plodny (tzn. jego bit `f` nie jest ustawiony) i programista nie jest ani wlascicielem new-parent, ani czarodziejem, zglaszany jest `E_PERM`. Jesli new-parent jest rowny `object` lub jednemu z jego biezacych przodkow, zglaszany jest `E_RECMOVE`. Jesli object lub jeden z jego potomkow definiuje wlasciwosc o tej samej nazwie, co ta zdefiniowana albo na new-parent, albo na jednym z jego przodkow, zglaszany jest `E_INVARG`.

Zmiana rodzica obiektu moze miec efekt usuniecia pewnych wlasciwosci z i dodania innych wlasciwosci do tego obiektu i wszystkich jego potomkow (tzn. jego dzieci i dzieci jego dzieci itd.). Niech common bedzie najblizszym przodkiem, ktorego object i new-parent maja wspolnego, przed zmiana rodzica object. Wtedy wszystkie wlasciwosci zdefiniowane przez przodkow object ponizej common (to znaczy, tych przodkow object, ktorzy z kolei sa potomkami common) sa usuwane z object i wszystkich jego potomkow. Wszystkie wlasciwosci zdefiniowane przez new-parent lub jego przodkow ponizej common sa dodawane do object i wszystkich jego potomkow. Podobnie jak w `create()`, nowo dodanym wlasciwosciom przypisywane sa te same bity uprawnien, jakie maja na new-parent, wlascicielem kazdej dodanej wlasciwosci jest albo wlasciciel obiektu, do ktorego jest dodawana (jesli bit uprawnien `c` jest ustawiony), albo wlasciciel tej wlasciwosci na new-parent, a wartosc kazdej dodanej wlasciwosci jest _czysta_ (clear); zobacz opis funkcji wbudowanej `clear_property()` po szczegoly. Wszystkie wlasciwosci, ktore nie sa usuwane ani dodawane w procesie zmiany rodzica, pozostaja calkowicie niezmienione.

Jesli new-parent jest rowny `#-1`, object nie otrzymuje zadnego rodzica; staje sie nowym korzeniem hierarchii rodzic/dziecko. W tym przypadku wszystkie wczesniej dziedziczone wlasciwosci na object sa po prostu usuwane.

Jesli new-parents jest rowny {}, object nie otrzymuje zadnego rodzica; staje sie nowym korzeniem hierarchii rodzic/dziecko. W tym przypadku wszystkie wczesniej dziedziczone wlasciwosci na object sa po prostu usuwane.

> Ostrzezenie: w temacie dziedziczenia wielokrotnego, autor (Slither) uwaza, ze powinienes calkowicie go unikac. Preferuj [kompozycje nad dziedziczeniem](https://en.wikipedia.org/wiki/Composition_over_inheritance).

**Funkcja: `valid`**

valid -- Zwraca niezerowa liczbe calkowita, jesli object jest poprawny i nie zostal jeszcze poddany recyklingowi.

int `valid` (obj object)

Zwraca niezerowa liczbe calkowita (tzn. wartosc prawdziwa), jesli object jest poprawnym obiektem (takim, ktory zostal utworzony i nie jest jeszcze poddany recyklingowi), a zero (tzn. wartosc falszywa) w przeciwnym razie.

```
valid(#0)    =>   1
valid(#-1)   =>   0
```

**Funkcja: `parent`**

**Funkcja: `parents`**

parent -- zwraca rodzica object

parents -- zwraca rodzicow object

obj `parent` (obj object)

list `parents` (obj object)

**Funkcja: `children`**

children -- zwraca liste dzieci object.

list `children` (obj object)

**Funkcja: `isa`**

int isa(OBJ object, OBJ parent)

obj isa(OBJ object, LIST parent list [, INT return_parent])

Zwraca prawde, jesli object jest potomkiem parent, w przeciwnym razie falsz.

Jesli podano trzeci argument i jest on prawda, wartoscia zwracana bedzie pierwszy rodzic, od ktorego object1 pochodzi w `parent list`.

```
isa(#2, $wiz)                           => 1
isa(#2, {$thing, $wiz, $container})     => 1
isa(#2, {$thing, $wiz, $container}, 1)  => #57 (generic wizard)
isa(#2, {$thing, $room, $container}, 1) => #-1 
```

**Funkcja: `locate_by_name`**

locate_by_name -- Ta funkcja wyszukuje w kazdym obiekcie bazy danych te zawierajace `object name` w swojej wlasciwosci .name.

list `locate_by_name` (STR object name [, INT case-matters])

Jesli `case-matters` jest prawda, dopasowywanie stringow rozroznia wielkosc liter. Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`.

Od ToastStunt 2.8.0 to nie jest funkcja watkowana.

**Funkcja: `locations`**

list `locations`(OBJ object [, OBJ stop [, INT is-parent]])

Rekurencyjnie budowana jest lista lokalizacji obiektu, lokalizacji jego lokalizacji i tak dalej, az wreszcie trafi na $nothing.

Zglasza `E_INVIND`, jesli object jest niepoprawny.

Przyklad:

```
locations(me) => {#20381, #443, #104735}

$string_utils:title_list(locations(me)) => "\"Butterknife Ballet\" Control Room FelElk, the one-person celestial birther \"Butterknife Ballet\", and Uncharted Space: Empty Space"
```

Jesli `stop` jest w znalezionych lokalizacjach, zatrzyma sie przed nia i zwroci liste (bez obiektu stop).

Jesli trzeci argument jest prawda, zaklada sie, ze `stop` jest RODZICEM. I jesli ktorakolwiek z Twoich lokalizacji jest dzieckiem tego rodzica, zatrzymuje sie tam.

**Funkcja: `occupants`**

list `occupants`(LIST objects [, OBJ | LIST parent, INT player flag set, INT inverse-match])

Iteruje przez liste objects i zwraca te dopasowujace okreslony zestaw kryteriow:

1. Jesli podano wylacznie objects, funkcja occupants zwroci liste obiektow z ustawiona flaga player.

2. Jesli podano argument parent, zwrocona zostanie lista obiektow pochodzacych od parent. Jesli parent jest lista, obiekt musi pochodzic od co najmniej jednego obiektu z tej listy.

3. Jesli podano oba, parent i flage player, occupants sprawdzi zarowno, czy obiekt pochodzi od parent, jak i to, czy ma ustawiona flage player.

4. Jesli inverse-match wynosi 0 (domyslne zachowanie). Jesli wynosi 1, odwraca dopasowanie na 'elementy z listy, ktore NIE dopasowuja parent(s)'

Od ToastStunt 2.8.0 to nie jest funkcja watkowana.

Zglasza `E_TYPE`, jesli podano parent i nie jest on obiektem lub lista obiektow. Zglasza `E_INVARG`, jesli objects nie jest poprawna lista obiektow.

**Funkcja: `recycle`**

recycle -- niszczy obiekt lub obiekt anonimowy nieodwolalnie.

none `recycle` (OBJ|ANON object)

Podany obiekt jest niszczony, nieodwolalnie. Programista musi albo byc wlascicielem object, albo byc czarodziejem; w przeciwnym razie zglaszany jest `E_PERM`. Jesli object nie jest ani poprawnym obiektem permanentnym, ani obiektem anonimowym, zglaszany jest `E_INVARG`. Dla obiektow permanentnych dzieci object otrzymuja jako nowego rodzica rodzica object. Przed poddaniem object recyklingowi, kazdy obiekt w jego zawartosci jest przenoszony do `#-1` (co implikuje wywolanie czasownika `exitfunc` obiektu, jesli istnieje), a nastepnie wywolywany jest czasownik `recycle` object, jesli istnieje, bez argumentow.

Obiekty anonimowe moga rowniez zostac poddane recyklingowi explicite. Sa oznaczane jako niepoprawne i czyszczone, gdy nie zostaje zadna aktywna referencja.

Po poddaniu obiektu permanentnego recyklingowi, jesli wlasciciel bylego obiektu ma wlasciwosc o nazwie `ownership_quota`, a wartosc tej wlasciwosci jest liczba calkowita, `recycle()` traktuje te wartosc jako _quota_ i zwieksza ja o jeden, zapisujac wynik z powrotem do wlasciwosci `ownership_quota`.

**Funkcja: `recreate`**

recreate -- Odtwarza niepoprawny obiekt old (taki, ktory zostal wczesniej poddany recycle()) jako parent, opcjonalnie z wlascicielem owner.

obj `recreate`(OBJ old, OBJ parent [, OBJ owner])

To ma efekt wypelniania dziur stworzonych przez recycle(), co normalnie wymagaloby przenumerowania i zresetowania maksymalnego obiektu.

Normalne reguly stosuja sie do parent i owner. Musisz albo byc wlascicielem parent, parent musi byc plodny, albo musisz byc czarodziejem. Podobnie, by zmienic owner, powinienes byc czarodziejem. W przeciwnym razie jest to zbedne.

**Funkcja: `next_recycled_object`**

next_recycled_object -- Zwraca najnizszy niepoprawny obiekt. Jesli podano start, zaden obiekt nizszy niz start nie zostanie wziety pod uwage. Jesli nie ma niepoprawnych obiektow, ta funkcja zwroci 0.

obj | int `next_recycled_object`([OBJ start])

Zglasza `E_INVARG`, jesli start jest ujemny lub wiekszy niz ostatni kiedykolwiek uzyty numer obiektu.

**Funkcja: `recycled_objects`**

recycled_objects -- Zwraca liste wszystkich niepoprawnych obiektow w bazie danych. Niepoprawny obiekt to taki, ktory zostal zniszczony za pomoca funkcji recycle().

list `recycled_objects`()

**Funkcja: `ancestors`**

ancestors -- Zwraca liste wszystkich przodkow `object` w porzadku wznoszacym sie w hierarchii dziedziczenia. Jesli `full` jest prawda, `object` zostanie wliczony do listy.

list `ancestors`(OBJ object [, INT full])

**Funkcja: `descendants`**

list `descendants`(OBJ object [, INT full])

Zwraca liste wszystkich zagniezdzonych dzieci object. Jesli full jest prawda, object zostanie wliczony do listy.

**Funkcja: `object_bytes`**

object_bytes -- Zwraca liczbe bajtow pamieci serwera wymaganych do przechowania podanego obiektu.

int `object_bytes` (obj object)

Obliczenie miejsca wlicza miejsce uzywane przez wartosci wszystkich nieczystych wlasciwosci obiektu oraz przez czasowniki i wlasciwosci zdefiniowane bezposrednio na obiekcie.

Zglasza `E_TYPE`, jesli object nie jest obiektem, `E_INVIND`, jesli object jest niepoprawny, i `E_PERM`, jesli programista nie jest czarodziejem.

**Funkcja: `respond_to`**

int | list respond_to(OBJ object, STR verb)

Zwraca prawde, jesli verb jest wywolywalny na object, biorac pod uwage dziedziczenie, wieloznaczniki (czasowniki z gwiazdka) itd. W przeciwnym razie zwraca falsz. Jesli wywolujacy ma uprawnienia do odczytu obiektu (poniewaz flaga `r` obiektu jest prawda, lub wywolujacy jest wlascicielem albo czarodziejem), wartoscia prawdziwa jest lista zawierajaca numer obiektu definiujacego dany czasownik oraz pelna nazwe (nazwy) czasownika. W przeciwnym razie zwracana jest wartosc numeryczna `1`.

**Funkcja: `max_object`**

max_object -- Zwraca najwiekszy numer obiektu, jaki zostal kiedykolwiek przypisany utworzonemu obiektowi.

obj `max_object`()

Zauwaz, ze obiekt o tym numerze moze juz nie istniec; moze zostac poddany recyklingowi. Nastepny obiekt utworzony przez wbudowana funkcje `create()` normalnie otrzyma numer obiektu o jeden wiekszy niz wartosc `max_object()`, o ile numery obiektow nie sa ponownie uzywane przez `recreate()`, lub `reset_max_object()` nie zmniejszyl maksymalnego numeru obiektu serwera. To nie dotyczy narzedzi recyklingu na poziomie bazy danych, takich jak `$recycler`, ktore moga explicite wybrac ponowne uzycie numerow obiektow.

##### Przemieszczanie obiektow

**Funkcja: `move`**

move -- Zmienia lokalizacje what na where.

none `move` (obj what, obj where [, INT position])

To skomplikowany proces, poniewaz musi zostac wykonana pewna liczba sprawdzen uprawnien i powiadomien. Faktyczne przemieszczenie zachodzi jak opisano w nastepujacych paragrafach.

what powinien byc poprawnym obiektem, a where powinno byc albo poprawnym obiektem, albo `#-1` (oznaczajacym lokalizacje 'nigdzie'); w przeciwnym razie zglaszany jest `E_INVARG`. Programista musi byc albo wlascicielem what, albo czarodziejem; w przeciwnym razie zglaszany jest `E_PERM`.

Jesli where jest poprawnym obiektem, wywolywany jest czasownik

```
where:accept(what)
```

jest wykonywany, przed jakimkolwiek przemieszczeniem. Jesli czasownik zwroci wartosc falszywa i programista nie jest czarodziejem, where jest uznawane za odmawiajace wejscia what; `move()` zglasza `E_NACC`. Jesli where nie definiuje czasownika `accept`, jest traktowane, jakby zdefiniowalo taki, ktory zawsze zwraca falsz.

Jesli przeniesienie what do where stworzyloby petle w hierarchii zawierania (tzn. what zawieraloby samo siebie, nawet niebezposrednio), zamiast tego zglaszany jest `E_RECMOVE`.

Wlasciwosc `location` what jest zmieniana na where, a wlasciwosci `contents` starej i nowej lokalizacji sa odpowiednio modyfikowane. Niech old-where bedzie lokalizacja what przed przeniesieniem. Jesli old-where jest poprawnym obiektem, wywolywany jest czasownik

```
old-where:exitfunc(what)
```

jest wykonywany, a jego wynik jest ignorowany; to nie jest blad, jesli old-where nie definiuje czasownika o nazwie `exitfunc`. Wreszcie, jesli where i what sa wciaz poprawnymi obiektami, a where jest wciaz lokalizacja what, wywolywany jest czasownik

```
where:enterfunc(what)
```

jest wykonywany, a jego wynik jest ignorowany; ponownie, to nie jest blad, jesli where nie definiuje czasownika o nazwie `enterfunc`.

Przekazanie `position` do move efektywnie wykona listinsert() obiektu na tej pozycji na liscie .contents.

##### Operacje na wlasciwosciach

**Funkcja: `properties`**

properties -- Zwraca liste nazw wlasciwosci zdefiniowanych bezposrednio na podanym obiekcie, nie dziedziczonych z jego rodzica.

list `properties` (obj object)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli programista nie ma uprawnien do odczytu object, zglaszany jest `E_PERM`.

**Funkcja: `property_info`**

property_info -- Pobiera wlasciciela i bity uprawnien dla wlasciwosci o nazwie prop-name na podanym obiekcie.

list `property_info` (obj object, str prop-name)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli object nie ma niewbudowanej wlasciwosci o nazwie prop-name, zglaszany jest `E_PROPNF`. Jesli programista nie ma uprawnien do odczytu (zapisu) danej wlasciwosci, `property_info()` zglasza `E_PERM`.

**Funkcja: `set_property_info`**

set_property_info -- Ustawia wlasciciela i bity uprawnien dla wlasciwosci o nazwie prop-name na podanym obiekcie.

none `set_property_info` (obj object, str prop-name, list info)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli object nie ma niewbudowanej wlasciwosci o nazwie prop-name, zglaszany jest `E_PROPNF`. Jesli programista nie ma uprawnien do odczytu (zapisu) danej wlasciwosci, `set_property_info()` zglasza `E_PERM`. Property info ma nastepujaca postac:

```
{owner, perms [, new-name]}
```

gdzie owner jest obiektem, perms jest stringiem zawierajacym wylacznie znaki ze zbioru `r`, `w` i `c`, a new-name jest stringiem; new-name nigdy nie jest czescia wartosci zwracanej przez `property_info()`, ale moze opcjonalnie zostac podane jako czesc wartosci przekazywanej do `set_property_info()`. Ta lista jest rodzajem wartosci zwracanej przez property_info() i oczekiwanej jako trzeci argument do `set_property_info()`; ta druga funkcja zglasza `E_INVARG`, jesli owner jest niepoprawny, jesli perms zawiera jakiekolwiek niedozwolone znaki, lub, gdy podano new-name, jesli prop-name nie jest zdefiniowany bezposrednio na object, albo new-name nazywa istniejaca wlasciwosc zdefiniowana na object lub jakimkolwiek z jego przodkow lub potomkow.

**Funkcja: `add_property`**

add_property -- Definiuje nowa wlasciwosc na podanym obiekcie.

none `add_property` (obj object, str prop-name, value, list info)

Wlasciwosc jest dziedziczona przez wszystkich jego potomkow; wlasciwosc nazywa sie prop-name, jej poczatkowa wartosc to value, a jej wlasciciel i poczatkowe bity uprawnien sa podane przez info w tym samym formacie, jaki jest zwracany przez `property_info()`, opisany wyzej. Argument object musi byc obiektem permanentnym; obiekty anonimowe nie moga miec nowych wlasciwosci dodawanych do nich bezposrednio.

Jesli object nie jest obiektem permanentnym, zglaszany jest `E_TYPE`. Jesli object jest niepoprawny, lub info nie okresla poprawnego wlasciciela i dobrze sformowanych bitow uprawnien, lub object albo jego przodkowie lub potomkowie juz definiuja wlasciwosc o nazwie prop-name, zglaszany jest `E_INVARG`. Jesli programista nie ma uprawnien do zapisu object, lub jesli wlasciciel okreslony przez info nie jest programista i programista nie jest czarodziejem, zglaszany jest `E_PERM`.

**Funkcja: `delete_property`**

delete_property -- Usuwa wlasciwosc o nazwie prop-name z podanego obiektu i wszystkich jego potomkow.

none `delete_property` (obj object, str prop-name)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli programista nie ma uprawnien do zapisu object, zglaszany jest `E_PERM`. Jesli object nie definiuje bezposrednio wlasciwosci o nazwie prop-name (w przeciwienstwie do dziedziczenia jej z rodzica), zglaszany jest `E_PROPNF`.

**Funkcja: `is_clear_property`**

is_clear_property -- Sprawdza, czy podana wlasciwosc jest czysta.

int `is_clear_property` (obj object, str prop-name)

**Funkcja: `clear_property`**

clear_property -- Ustawia podana wlasciwosc jako czysta.

none `clear_property` (obj object, str prop-name)

Te dwie funkcje sprawdzaja odpowiednio, czy wlasciwosc o nazwie prop-name na podanym obiekcie jest czysta, oraz ustawiaja ja jako czysta. Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli object nie ma niewbudowanej wlasciwosci o nazwie prop-name, zglaszany jest `E_PROPNF`. Jesli programista nie ma uprawnien do odczytu (zapisu) danej wlasciwosci, `is_clear_property()` (`clear_property()`) zglasza `E_PERM`.

Jesli wlasciwosc jest czysta, to gdy wartosc tej wlasciwosci jest odpytywana, zwracana jest wartosc wlasciwosci rodzica o tej samej nazwie. Jesli wlasciwosc rodzica jest czysta, sprawdzana jest wartosc rodzica rodzica, i tak dalej. Jesli object jest definiujacym wlasciwosc prop-name, w przeciwienstwie do dziedziczacego te wlasciwosc, `clear_property()` zglasza `E_INVARG`.

##### Operacje na czasownikach

**Funkcja: `verbs`**

verbs -- Zwraca liste nazw czasownikow zdefiniowanych bezposrednio na podanym obiekcie, nie dziedziczonych z jego rodzica.

list verbs (obj object)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli programista nie ma uprawnien do odczytu object, zglaszany jest `E_PERM`.

Wiekszosc pozostalych operacji na czasownikach przyjmuje string zawierajacy nazwe czasownika, by zidentyfikowac dany czasownik. Poniewaz czasowniki moga miec wiele nazw i poniewaz obiekt moze miec wiele czasownikow o tej samej nazwie, ta praktyka moze prowadzic do trudnosci. By najbardziej jednoznacznie odniesc sie do konkretnego czasownika, mozna zamiast tego uzyc liczby calkowitej dodatniej, indeksu czasownika na liscie zwracanej przez `verbs()`, opisanej wyzej.

Na przyklad, zalozmy, ze `verbs(#34)` zwraca te liste:

```
{"foo", "bar", "baz", "foo"}
```

Obiekt `#34` ma zdefiniowane na nim dwa czasowniki o nazwie `foo` (to moze nie byc bledem, jesli te dwa czasowniki maja rozna skladnie polecen). By jednoznacznie odniesc sie do pierwszego z listy, uzywa sie liczby calkowitej 1; by odniesc sie do drugiego, uzywa sie 4.

W opisach funkcji nizej argument o nazwie verb-desc jest albo stringiem zawierajacym nazwe czasownika, albo liczba calkowita dodatnia podajaca indeks tego czasownika na liscie `verbs()` obiektu go definiujacego.
Z powodow historycznych istnieje rowniez drugi, gorszy mechanizm odnoszenia sie do czasownikow za pomoca liczb, ale jego uzycie jest silnie odradzane. Jesli wlasciwosc `$server_options.support_numeric_verbname_strings` istnieje z wartoscia prawdziwa, funkcje na czasownikach beda rowniez akceptowac numeryczny string (np. `"4"`) jako deskryptor czasownika. Liczba dziesietna w stringu dziala mniej wiecej tak jak liczby calkowite dodatnie opisane wyzej, ale z dwoma istotnymi roznicami:

Numeryczny string jest indeksem _liczonym od zera_ w `verbs()`; to znaczy, w przypadku stringa uzylbys liczby o jeden mniejszej niz ta, ktorej uzylbys w przypadku liczby calkowitej dodatniej.

Gdy istnieje czasownik, ktorego faktyczna nazwa wyglada jak liczba dziesietna, ta notacja numeryczno-stringowa jest niejednoznaczna; serwer we wszystkich przypadkach zalozy, ze odniesienie dotyczy pierwszego czasownika na liscie, dla ktorego podany string mogl byc nazwa, albo w zwyklym sensie, albo jako indeks numeryczny.

Ewidentnie, ten starszy mechanizm jest trudniejszy i bardziej ryzykowny w uzyciu; nowy kod powinien byc pisany wylacznie z uzyciem obecnego mechanizmu, a stary kod uzywajacy numerycznych stringow powinien zostac zmodyfikowany, by tego nie robic.

**Funkcja: `verb_info`**

verb_info -- Pobiera wlasciciela, bity uprawnien i nazwe (nazwy) czasownika okreslonego przez verb-desc na podanym obiekcie.

list `verb_info` (obj object, str|int verb-desc) 

**Funkcja: `set_verb_info`**

set_verb_info -- Ustawia wlasciciela, bity uprawnien i nazwe (nazwy) czasownika okreslonego przez verb-desc na podanym obiekcie.

none `set_verb_info` (obj object, str|int verb-desc, list info)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli object nie definiuje czasownika okreslonego przez verb-desc, zglaszany jest `E_VERBNF`. Jesli programista nie ma uprawnien do odczytu (zapisu) danego czasownika, `verb_info()` (`set_verb_info()`) zglasza `E_PERM`.

Verb info ma nastepujaca postac:

```
{owner, perms, names}
```

gdzie owner jest obiektem, perms jest stringiem zawierajacym wylacznie znaki ze zbioru `r`, `w`, `x` i `d`, a names jest stringiem. To rodzaj wartosci zwracanej przez `verb_info()` i oczekiwanej jako trzeci argument do `set_verb_info()`. `set_verb_info()` zglasza `E_INVARG`, jesli owner jest niepoprawny, jesli perms zawiera jakiekolwiek niedozwolone znaki, lub jesli names jest pustym stringiem albo sklada sie wylacznie ze spacji; zglasza `E_PERM`, jesli owner nie jest programista i programista nie jest czarodziejem.

**Funkcja: `verb_args`**

verb_args -- pobiera specyfikacje dopelnienia blizszego, przyimka i dopelnienia dalszego dla czasownika okreslonego przez verb-desc na podanym obiekcie.

list `verb_args` (obj object, str|int verb-desc) 

**Funkcja: `set_verb_args`**

verb_args -- ustawia specyfikacje dopelnienia blizszego, przyimka i dopelnienia dalszego dla czasownika okreslonego przez verb-desc na podanym obiekcie.

none `set_verb_args` (obj object, str|int verb-desc, list args)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli object nie definiuje czasownika okreslonego przez verb-desc, zglaszany jest `E_VERBNF`. Jesli programista nie ma uprawnien do odczytu (zapisu) danego czasownika, funkcja zglasza `E_PERM`.

Specyfikacje verb args maja nastepujaca postac:

```
{dobj, prep, iobj}
```

gdzie dobj i iobj sa stringami ze zbioru `"this"`, `"none"` i `"any"`, a prep jest stringiem, ktory jest albo `"none"`, `"any"`, albo jedna z fraz przyimkowych wymienionych dawno wczesniej w opisie czasownikow w pierwszym rozdziale. To rodzaj wartosci zwracanej przez `verb_args()` i oczekiwanej jako trzeci argument do `set_verb_args()`. Zauwaz, ze dla `set_verb_args()`, prep musi byc tylko jedna z fraz przyimkowych, nie (jak pokazano w tamtej tabeli) zbiorem takich fraz rozdzielonych znakami `/`. `set_verb_args` zglasza `E_INVARG`, jesli jakikolwiek ze stringow dobj, prep lub iobj jest niedozwolony.

```
verb_args($container, "take")
                    =>   {"any", "out of/from inside/from", "this"}
set_verb_args($container, "take", {"any", "from", "this"})
```

**Funkcja: `add_verb`**

add_verb -- definiuje nowy czasownik na podanym obiekcie.

int `add_verb` (obj object, list info, list args)

Wlasciciel, bity uprawnien i nazwa (nazwy) nowego czasownika sa podane przez info w tym samym formacie, jaki jest zwracany przez `verb_info()`, opisany wyzej. Specyfikacje dopelnienia blizszego, przyimka i dopelnienia dalszego nowego czasownika sa podane przez args w tym samym formacie, jaki jest zwracany przez `verb_args`, opisany wyzej. Nowy czasownik ma poczatkowo skojarzony z nim pusty program; ten program nic nie robi, tylko zwraca nieokreslona wartosc. Argument object musi byc obiektem permanentnym; obiekty anonimowe nie moga miec nowych czasownikow dodawanych do nich bezposrednio. Przy powodzeniu zwrocona liczba calkowita to numer nowego czasownika na object, liczony od jednego.

Jesli object nie jest obiektem permanentnym, zglaszany jest `E_TYPE`. Jesli object jest niepoprawny, lub info nie okresla poprawnego wlasciciela i dobrze sformowanych bitow uprawnien i nazw czasownika, lub args nie jest prawomocna specyfikacja skladni, zglaszany jest `E_INVARG`. Jesli programista nie ma uprawnien do zapisu object, lub jesli wlasciciel okreslony przez info nie jest programista i programista nie jest czarodziejem, zglaszany jest `E_PERM`.

**Funkcja: `delete_verb`**

delete_verb -- usuwa czasownik okreslony przez verb-desc z podanego obiektu.

none `delete_verb` (obj object, str|int verb-desc)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli programista nie ma uprawnien do zapisu object, zglaszany jest `E_PERM`. Jesli object nie definiuje czasownika okreslonego przez verb-desc, zglaszany jest `E_VERBNF`.

**Funkcja: `verb_code`**

verb_code -- pobiera program w kodzie MOO skojarzony z czasownikiem okreslonym przez verb-desc na object.

list `verb_code` (obj object, str|int verb-desc [, fully-paren [, indent]]) 

**Funkcja: `set_verb_code`**

set_verb_code -- ustawia program w kodzie MOO skojarzony z czasownikiem okreslonym przez verb-desc na object.

list `set_verb_code` (obj object, str|int verb-desc, list code)

Program jest reprezentowany jako lista stringow, jeden dla kazdej linii programu; to rodzaj wartosci zwracanej przez `verb_code()` i oczekiwanej jako trzeci argument do `set_verb_code()`. Dla `verb_code()`, wyrazenia w zwroconym kodzie sa zwykle pisane z minimalnie niezbedna liczba nawiasow; jesli full-paren jest prawda, wszystkie wyrazenia sa w pelni ujete w nawiasy.

Rowniez dla `verb_code()`, linie w zwroconym kodzie sa zwykle wcale nie wciete; jesli indent jest prawda, kazda linia jest wcieta, by lepiej pokazac zagniezdzenie instrukcji.

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli object nie definiuje czasownika okreslonego przez verb-desc, zglaszany jest `E_VERBNF`. Jesli programista nie ma uprawnien do odczytu (zapisu) danego czasownika, `verb_code()` (`set_verb_code()`) zglasza `E_PERM`. Jesli programista w rzeczywistosci nie jest programista, zglaszany jest `E_PERM`.

Dla `set_verb_code()`, wynikiem jest lista stringow, komunikaty bledow wygenerowane przez kompilator kodu MOO podczas przetwarzania code. Jesli lista nie jest pusta, `set_verb_code()` nie zainstalowal code; program skojarzony z danym czasownikiem pozostaje niezmieniony.

**Funkcja: `disassemble`**

disassemble -- zwraca (dosc dluga) liste stringow podajacych wykaz wewnetrznej, "skompilowanej" formy serwera dla czasownika okreslonego przez verb-desc na object.

list `disassemble` (obj object, str|int verb-desc)

Ten format nie jest udokumentowany i moze wrecz zmieniac sie z wydania na wydanie, ale niektorzy programisci moga wciaz uznac wynik `disassemble()` za interesujacy do przegladania, jako sposob na zdobycie glebszego zrozumienia, jak dziala serwer.

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli object nie definiuje czasownika okreslonego przez verb-desc, zglaszany jest `E_VERBNF`. Jesli programista nie ma uprawnien do odczytu danego czasownika, `disassemble()` zglasza `E_PERM`.

##### Operacje na WAIF-ach

**Funkcja: `new_waif`**

new_waif -- Wbudowana funkcja `new_waif()` tworzy nowy WAIF, ktorego klasa jest wywolujacy obiekt, a wlascicielem sa uprawnienia wywolujacego czasownika.

waif `new_waif`()

Klasa jest obiektem, ktory wywolal biezacy czasownik, a wlascicielem jest programista, z ktorego uprawnieniami dziala zadanie. Nie istnieje alternatywna forma wywolania wylacznie dla czarodziejow.

**Funkcja: `waif_stats`**

waif_stats -- Zwraca MAPE statystyk o zainstancjonowanych waifach.

map `waif_stats`()

Kazda klasa waif bedzie kluczem w MAPIE, a jej wartoscia bedzie liczba waifow tej klasy obecnie zainstancjonowanych. Dodatkowo istnieje klucz `total`, ktory zwroci calkowita liczbe zainstancjonowanych waifow, oraz klucz `pending_recycle`, ktory zwroci liczbe waifow, ktore zostaly zniszczone i oczekuja na wywolanie ich czasownika :recycle.

##### Operacje na obiektach gracza

**Funkcja: `players`**

players -- zwraca liste numerow obiektow wszystkich obiektow-graczy w bazie danych.

list `players` ()

**Funkcja: `is_player`**

is_player -- zwraca wartosc prawdziwa, jesli podany obiekt jest obiektem-graczem, a falszywa w przeciwnym razie.

int `is_player` (obj object)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`.

**Funkcja: `set_player_flag`**

set_player_flag -- przyznaje lub usuwa status "obiektu-gracza" podanego obiektu, w zaleznosci od wartosci logicznej value.

none `set_player_flag` (obj object, value)

Jesli object jest niepoprawny, zglaszany jest `E_INVARG`. Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`.

Jesli value jest prawda, object otrzymuje (lub zachowuje) status "obiektu-gracza": bedzie elementem listy zwracanej przez `players()`, wyrazenie `is_player(object)` zwroci prawde, a serwer bedzie traktowac wywolanie `$do_login_command()`, ktore zwraca object, jako logowanie biezacego polaczenia.

Jesli value jest falszem, obiekt traci (lub dalej nie ma) status "obiektu-gracza": nie bedzie elementem listy zwracanej przez `players()`, wyrazenie `is_player(object)` zwroci falsz, a uzytkownicy nie beda mogli polaczyc sie z object po nazwie podczas logowania do serwera. Dodatkowo, jesli uzytkownik jest polaczony z object w momencie, gdy ten traci status "obiektu-gracza", to polaczenie jest natychmiast zrywane, tak jakby wywolano `boot_player(object)` (zobacz opis `boot_player()` nizej).

#### Operacje na plikach

Istnieje kilka funkcji wbudowanych, dostepnych wylacznie dla administratorow, do manipulowania plikami z wewnatrz MOO. Bezpieczenstwo jest zapewniane przez umozliwienie wykonywania tych funkcji wbudowanych wylacznie z uprawnieniami czarodzieja, a takze przez zezwalanie na dostep wylacznie do katalogu pod biezacym katalogiem (tym, w ktorym dziala serwer). Nowe funkcje wbudowane sa skonstruowane podobnie do biblioteki stdio jezyka C. To pozwala kodowi MOO wykonywac zorientowane na strumienie operacje we/wy na plikach.

Danie kodowi MOO bezposredniego dostepu do plikow otwiera dziure w skad inad dosc dobrym murze, ktory serwer ToastStunt wznosi miedzy systemem operacyjnym a baza danych. Bezpieczenstwo jest dosc dobrze ograniczane przez restrykcje co do miejsc, w ktorych mozna otwierac pliki, oraz przez zezwalanie na wywolywanie funkcji wbudowanych wylacznie z uprawnieniami czarodzieja. Wciaz mozliwe jest wykonanie roznych form atakow typu odmowa uslugi (denial of service), ale serwer MOO umozliwia rowniez ten rodzaj ataku.

> Ostrzezenie: w zaleznosci od uzywanego Core (ToastCore, LambdaMOO itd.) moze byc dostepne narzedzie sluzace jako wrapper na kod FileIO. To preferowana metoda obslugi plikow, a bezposrednie uzywanie funkcji wbudowanych jest odradzane. W ToastCore moze byc dostepny WAIF $file, ktorego mozesz uzyc do tego celu.

> Ostrzezenie: FileIO uzywa skonfigurowanego katalogu plikow, domyslnie `files/` pod katalogiem roboczym serwera, o ile nie zostanie to nadpisane przez `-i` lub `--file-dir`. Ten katalog musi istniec, by funkcje wbudowane FileIO dzialaly.

> Uwaga: bardziej szczegolowe informacje o kodzie FileIO mozna znalezc w pliku docs/FileioDocs.txt repozytorium ToastStunt.

System FileIO zostal zaktualizowany w ToastCore i zawiera wiele usprawnien wzgledem wczesniejszych wersji LambdaMOO i Stunt.
* Szybsze odczytywanie
* Otwieraj tyle plikow, ile chcesz, konfigurowalne za pomoca FILE_IO_MAX_FILES lub $server_options.file_io_max_files

**Obsluga bledow FileIO**

Bledy sa zawsze obslugiwane poprzez zglaszanie jakiegos rodzaju wyjatku. Zdefiniowane sa nastepujace wyjatki:

`E_FILE`

Jest zglaszany, gdy wywolanie stdio zwrocilo wartosc bledu. CODE jest ustawiane na E_FILE, MSG jest ustawiane na wynik strerror() (ktory moze rozniec sie miedzy systemami), a VALUE zalezy od tego, ktora funkcja zglosila blad. Gdy funkcja zawodzi, poniewaz funkcja stdio zwrocila EOF, MSG i VALUE sa ustawiane na "End of file".

`E_INVARG`

Jest zglaszany z wielu przyczyn. Powszednymi przyczynami sa przekazanie do funkcji niepoprawnego FHANDLE oraz niepoprawna specyfikacja pathname. W kazdym z tych przypadkow MSG zostanie ustawione na przyczyne, a VALUE bedzie problematyczna wartoscia.

`E_PERM`

Jest zglaszany, gdy jakakolwiek z tych funkcji zostaje wywolana z uprawnieniami innymi niz czarodziejskie.

**Otwieranie i zamykanie plikow oraz funkcje powiazane**

Strumienie plikow sa skojarzone z FHANDLE. FHANDLE sa podobne do FILE\* uzywanego w stdio. FHANDLE otrzymujesz z file_open. Nie powinienes zalezec od faktycznego typu FHANDLE (obecnie TYPE_INT). FHANDLE nie przetrwaja restartow serwera. To znaczy, pliki otwarte, gdy serwer jest wylaczany, sa zamykane, gdy wraca, a zadna informacja o otwartych plikach nie jest zapisywana w bazie danych.

**Funkcja: `file_open`**

file_open -- Otwiera plik.

FHANDLE `file_open`(STR pathname, STR mode)

Zglasza: E_INVARG, jesli mode nie jest poprawnym mode, E_QUOTA, jesli otwartych jest za wiele plikow.

To otwiera plik okreslony przez pathname i zwraca dla niego FHANDLE. Zapewnia, ze pathname jest dozwolony. Mode jest stringiem znakow wskazujacym, w jakim mode plik jest otwierany. String mode ma cztery znaki.

Pierwszy znak musi byc (r)ead (odczyt), (w)rite (zapis) lub (a)ppend (dopisywanie). Drugi musi byc '+' lub '-'. To modyfikuje poprzedni argument.

* r- otwiera plik do odczytu i zawodzi, jesli plik nie istnieje.
* r+ otwiera plik do odczytu i zapisu i zawodzi, jesli plik nie istnieje.
* w- otwiera plik do zapisu, obcinajac go, jesli istnieje, i tworzac, jesli nie.
* w+ otwiera plik do odczytu i zapisu, obcinajac go, jesli istnieje, i tworzac, jesli nie.
* a- otwiera plik do zapisu, tworzy go, jesli nie istnieje, i ustawia strumien na koniec pliku.
* a+ otwiera plik do odczytu i zapisu, tworzy go, jesli nie istnieje, i ustawia strumien na koniec pliku.

Trzeci znak to albo (t)ext (tekst), albo (b)inary (binarny). W trybie tekstowym dane sa zapisywane tak, jak sa z MOO, a dane odczytywane przez MOO sa oczyszczane z niewypisywalnych znakow. W trybie binarnym dane sa zapisywane filtrowane przez konwersje binarny-string->surowe-bajty, a dane sa odczytywane filtrowane przez konwersje surowe-bajty->binarny-string. Na przyklad w trybie tekstowym zapisanie " 1B" znaczy, ze zapisywane sa trzy bajty: ' ' Podobnie, w trybie tekstowym odczytanie " 1B" znaczy, ze w pliku byly obecne znaki ' ' '1' 'B'. W trybie binarnym odczytanie " 1B" znaczy, ze w pliku byl ASCII ESC. W trybie tekstowym odczytanie ESC z pliku powoduje usuniecie ESC.

Nie zaleca sie odczytywania w trybie tekstowym plikow zawierajacych niewypisywalne dane ASCII, z oczywistych powodow.

Ostatni znak to albo 'n', albo 'f'. Jesli ten znak to 'f', kiedy dane sa zapisywane do pliku, MOO wymusi zakonczenie zapisu na fizyczny dysk przed powrotem. Jesli to 'n', to sie nie stanie.

To zaimplementowane za pomoca fopen().

**Funkcja: `file_close`**

file_close -- Zamyka plik.

void `file_close`(FHANDLE fh)

Zamyka plik skojarzony z fh.

To zaimplementowane za pomoca fclose().

**Funkcja: `file_name`**

file_name -- Zwraca pathname oryginalnie skojarzony z fh przez file_open(). To niekoniecznie jest biezaca nazwa pliku, jesli zostal przemianowany lub odlinkowany po otwarciu fh.

STR `file_name`(FHANDLE fh)

**Funkcja: `file_openmode`**

file_openmode -- Zwraca znormalizowany mode pliku skojarzonego z fh.

str `file_openmode`(FHANDLE fh)

To odzwierciedla biezace flagi odczytu/zapisu, tekst/binarny i flush uchwytu pliku. Nie jest gwarantowane, ze bedzie to dokladnie ten sam string mode, jaki oryginalnie przekazano do `file_open()`, poniewaz mode dopisywania sa przechowywane jako mode zapisu.

**Funkcja: `file_handles`**

file_handles -- Zwraca liste otwartych plikow.

LIST `file_handles` ()

**Operacje wejscia i wyjscia**

**Funkcja: `file_readline`**

file_readline -- Odczytuje nastepna linie w pliku i zwraca ja (bez znaku nowej linii).

str `file_readline`(FHANDLE fh)

Nie zalecane do uzycia na plikach w trybie binarnym.

To zaimplementowane za pomoca fgetc().

**Funkcja: `file_readlines`**

file_readlines -- Przewija plik, a nastepnie odczytuje podane linie z pliku, zwracajac je jako liste stringow. Po tej operacji strumien jest ustawiony na poczatku pierwszej zwroconej linii.

list `file_readlines`(FHANDLE fh, INT start, INT end)

Nie zalecane do uzycia na plikach w trybie binarnym.

To zaimplementowane za pomoca fgetc().

**Funkcja: `file_writeline`**

file_writeline -- Zapisuje podana linie do pliku (dodajac znak nowej linii).

void `file_writeline`(FHANDLE fh, STR line)

Nie zalecane do uzycia na plikach w trybie binarnym.

To zaimplementowane za pomoca fputs()

**Funkcja: `file_read`**

file_read -- Odczytuje do podanej liczby bajtow z pliku i zwraca je.

str `file_read`(FHANDLE fh, INT bytes)

Nie zalecane do uzycia na plikach w trybie tekstowym.

To zaimplementowane za pomoca fread().

**Funkcja: `file_write`**

file_write -- Zapisuje podane data do pliku. Zwraca liczbe zapisanych bajtow.

int `file_write`(FHANDLE fh, STR data)

Nie zalecane do uzycia na plikach w trybie tekstowym.

To zaimplementowane za pomoca fwrite().

**Funkcja: `file_flush`**

file_flush -- Zrzuca (flush) zbuforowane zapisy dla pliku.

void `file_flush`(FHANDLE fh)

To zaimplementowane za pomoca fflush().

**Funkcja: `file_count_lines`**

file_count_lines -- liczy linie w pliku.

INT `file_count_lines` (FHANDLE fh)

To przewija plik i czyta do EOF, liczac przy tym, pozostawiajac strumien ustawiony na EOF.

**Funkcja: `file_grep`**

file_grep -- wyszukuje string w pliku.

LIST `file_grep`(FHANDLE fh, STR search [,?match_all = 0])

Zalozmy, ze mamy plik `test.txt` z zawartoscia:

```
asdf asdf 11
11
112
```

I mamy otwarty uchwyt pliku z wywolania:

```
;file_open("test.txt", "r-tn")
```

Jesli wykonalibysmy file grep:

```
;file_grep(1, "11")
```

Otrzymalibysmy pierwszy wynik:

```
{{"asdf asdf 11", 1}}
```

Wynikowa LISTA jest w formie {{STR match, INT line-number}}

Jesli podasz opcjonalny trzeci argument

```
;file_grep(1, "11", 1)
```

otrzymamy wszystkie dopasowane wyniki:

```
{{"asdf asdf 11", 1}, {"11", 2}, {"112", 3}}
```

**Pobieranie i ustawianie pozycji strumienia**

**Funkcja: `file_tell`**

file_tell -- Zwraca pozycje w pliku.

INT `file_tell`(FHANDLE fh)

To zaimplementowane za pomoca ftell().

**Funkcja: `file_seek`**

file_seek -- Przeszukuje do konkretnej lokalizacji w pliku.

void `file_seek`(FHANDLE fh, INT loc, STR whence)

whence jest jednym ze stringow:

* "SEEK_SET" - przejdz do lokalizacji wzgledem poczatku
* "SEEK_CUR" - przejdz do lokalizacji wzgledem biezacej pozycji
* "SEEK_END" - przejdz do lokalizacji wzgledem konca

To zaimplementowane za pomoca fseek().

**Funkcja: `file_eof`**

file_eof -- Zwraca prawde wtedy i tylko wtedy, gdy strumien fh jest ustawiony na EOF.

int `file_eof`(FHANDLE fh)

To zaimplementowane za pomoca feof().

**Operacje porzadkowe**

**Funkcja: `file_size`**

**Funkcja: `file_last_access`**

**Funkcja: `file_last_modify`**

**Funkcja: `file_last_change`**

int `file_size`(STR pathname)

int `file_last_access`(STR pathname)

int `file_last_modify`(STR pathname)

int `file_last_change`(STR pathname)

int `file_size`(FHANDLE filehandle)

int `file_last_access`(FHANDLE filehandle)

int `file_last_modify`(FHANDLE filehandle)

int `file_last_change`(FHANDLE filehandle)

Te funkcje zwracaja rozmiar, czas ostatniego dostepu, czas ostatniej modyfikacji lub czas ostatniej zmiany statusu podanego pliku. Wszystkie z nich przyjmuja rowniez argumenty FHANDLE i wtedy operuja na otwartym pliku. Sa zaimplementowane za pomoca `stat()` lub `fstat()`.

**Funkcja: `file_mode`**

str `file_mode`(STR filename)

str `file_mode`(FHANDLE fh)

Zwraca oktalny mode pliku (np. "644").

To zaimplementowane za pomoca stat() lub fstat().

**Funkcja: `file_stat`**

list `file_stat`(STR pathname)

list `file_stat`(FHANDLE fh)

Zwraca wynik stat() (lub fstat()) na podanym pliku.

Konkretnie liste w nastepujacej postaci:

`{rozmiar pliku w bajtach, typ pliku, mode dostepu do pliku, wlasciciel, grupa, ostatni dostep, ostatnia modyfikacja i ostatnia zmiana}`

owner i group sa zawsze pustym stringiem.

Zaleca sie uzywanie zamiast tego konkretnych funkcji informacyjnych file_size, file_type, file_mode, file_last_access, file_last_modify i file_last_change. W wiekszosci przypadkow pozadany jest tylko jeden z tych elementow i w takich przypadkach nie ma powodu tworzyc i zwalniac listy.

**Funkcja: `file_rename`**

file_rename -- Probuje przemianowac oldpath na newpath.

void `file_rename`(STR oldpath, STR newpath)

To zaimplementowane za pomoca rename().

**Funkcja: `file_remove`**

file_remove -- Probuje usunac podany plik.

void `file_remove`(STR pathname)

To zaimplementowane za pomoca remove().

**Funkcja: `file_mkdir`**

file_mkdir -- Probuje utworzyc podany katalog.

void `file_mkdir`(STR pathname)

To zaimplementowane za pomoca mkdir().

**Funkcja: `file_rmdir`**

file_rmdir -- Probuje usunac podany katalog.

void `file_rmdir`(STR pathname)

To zaimplementowane za pomoca rmdir().

**Funkcja: `file_list`**

file_list -- Probuje wypisac zawartosc podanego katalogu.

LIST `file_list`(STR pathname, [ANY detailed])

Zwraca liste plikow w katalogu. Jesli podano argument detailed i jest on prawda, lista zawiera szczegolowe wpisy, w przeciwnym razie zawiera prosta liste nazw.

szczegolowy wpis:

`{STR nazwa pliku, STR typ pliku, STR mode pliku, INT rozmiar pliku}`

normalny wpis:

STR nazwa pliku

To zaimplementowane za pomoca `opendir()` i `readdir()`; porzadek wyniku nie jest gwarantowany.

**Funkcja: `file_type`**

file_type -- Zwraca typ podanego pathname lub uchwytu, jeden z "reg", "dir", "fifo", "block", "socket" lub "unknown".

STR `file_type`(STR pathname)

STR `file_type`(FHANDLE fh)

To zaimplementowane za pomoca stat() lub fstat().

**Funkcja: `file_chmod`**

file_chmod -- Probuje ustawic mode pliku, uzywajac mode jako oktalnego stringa o dokladnie trzech znakach.

void `file_chmod`(STR filename, STR mode)

To zaimplementowane za pomoca chmod().

##### Operacje na SQLite

SQLite pozwala przechowywac informacje w lokalnie hostowanych bazach danych SQLite. Te funkcje wbudowane sa dostepne wylacznie, gdy ToastStunt jest zbudowany ze wsparciem SQLite.

Wszystkie funkcje wbudowane SQLite wymagaja uprawnien czarodzieja. Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`.

**Funkcja: `sqlite_open`**

sqlite_open -- Funkcja `sqlite_open` bedzie probowac otworzyc baze danych w path do uzycia z SQLite.

int `sqlite_open`(STR path to database, [INT options])

Drugi argument to bitmaska opcji. Opcje to:

SQLITE_PARSE_OBJECTS [4]: okresla, czy stringi zaczynajace sie od symbolu hasha (#) sa interpretowane jako numery obiektow MOO, czy nie. Domyslnie jest to prawda, co znaczy, ze wszystkie zapytania, ktore zwrocilyby string (taki jak "#123"), zostana zwrocone jako obiekty.

SQLITE_PARSE_TYPES [2]: jesli nieustawione, nie zachodzi zadne parsowanie wierszy i zwracane sa wylacznie stringi.

SQLITE_SANITIZE_STRINGS [8]: jesli ustawione, znaki nowej linii (\n) sa konwertowane na taby (\t), by uniknac uszkodzenia bazy danych MOO. Domyslnie nieustawione.

> Uwaga: dla opcji SQLITE_PARSE_TYPES, typami, ktore beda parsowane przez te opcje, sa INT i FLOAT. LISTY/MAPY/WAIF-y/ANON-y trafia do bazy danych jako "NULL"

> Uwaga: jesli MOO nie wspiera bitmaskowania, wciaz mozesz okreslac opcje. Bedziesz musial jedynie samodzielnie zmanipulowac liczbe calkowita. Np. jesli chcesz parsowac obiekty i typy, arg[2] bedzie 6. Jesli chcesz parsowac wylacznie typy, arg[2] bedzie 2.

Jesli sie powiedzie, funkcja zwroci numeryczny uchwyt otwartej bazy danych.

Jesli za wiele uchwytow baz danych jest juz otwartych, zglaszany jest `E_QUOTA`. Jesli path jest niepoprawny, zglaszany jest `E_INVARG`. Jesli baza danych jest juz otwarta, zglaszany jest `E_INVARG` z istniejacym uchwytem bazy danych jako wartoscia bledu. Jesli SQLite nie moze otworzyc bazy danych, zglaszany jest `E_NONE` z komunikatem bledu SQLite.

**Funkcja: `sqlite_close`**

sqlite_close -- Ta funkcja zamknie otwarta baze danych.

none `sqlite_close`(INT database handle)

Jesli database handle jest niepoprawny, zglaszany jest `E_INVARG`. Jesli uchwyt jest wciaz uzywany przez watki robocze, zglaszany jest `E_PERM`.

**Funkcja: `sqlite_execute`**

sqlite_execute -- Ta funkcja bedzie probowac utworzyc i wykonac przygotowane zapytanie (prepared statement) podane w query, na bazie danych, do ktorej odnosi sie handle, z wartosciami values.

list | str `sqlite_execute`(INT database handle, STR SQL prepared statement query, LIST values)

Przy powodzeniu ta funkcja zwroci liste identyfikujaca zwrocone wiersze. Jesli zapytanie nie zwrocilo wierszy, ale bylo pomyslne, zwracana jest pusta lista.

Jesli zapytanie zawiedzie, zwrocony zostanie string identyfikujacy komunikat bledu SQLite.

Jesli database handle jest niepoprawny, zwracany jest `E_INVARG`.

`sqlite_execute` uzywa przygotowanych zapytan (prepared statements), wiec jest to preferowana funkcja do uzycia z powodow bezpieczenstwa i wydajnosci.

Przyklad:

```
sqlite_execute(0, "INSERT INTO users VALUES (?, ?, ?);", {#7, "lisdude", "Albori Sninvel"})
```

Gdy ToastStunt jest zbudowany ze wsparciem PCRE2, zapytania SQLite wspieraja operator dopasowywania wzorcow REGEXP:

```
sqlite_execute(4, "SELECT rowid FROM notes WHERE body REGEXP ?;", {"albori (sninvel)?"})
```

> Uwaga: to funkcja watkowana.

**Funkcja: `sqlite_query`**

sqlite_query -- Ta funkcja bedzie probowac wykonac zapytanie podane w query na bazie danych, do ktorej odnosi sie handle.

list | str `sqlite_query`(INT database handle, STR database query[, INT show columns])

Przy powodzeniu ta funkcja zwroci liste identyfikujaca zwrocone wiersze. Jesli zapytanie nie zwrocilo wierszy, ale bylo pomyslne, zwracana jest pusta lista.

Jesli zapytanie zawiedzie, zwrocony zostanie string identyfikujacy komunikat bledu SQLite.

Jesli database handle jest niepoprawny, zwracany jest `E_INVARG`.

Jesli show columns jest prawda, lista wynikowa bedzie wliczac nazwe kolumny przed jej wynikami.

> Ostrzezenie: sqlite_query NIE uzywa przygotowanych zapytan (prepared statements) i NIE powinien byc uzywany do zapytan zawierajacych dane wprowadzone przez uzytkownika.

> Uwaga: to funkcja watkowana.

**Funkcja: `sqlite_limit`**

sqlite_limit -- Ta funkcja pozwala okreslic rozne limity konstrukcji, osobno dla kazdej bazy danych.

int `sqlite_limit`(INT database handle, STR|INT category, INT new value)

Jesli new value jest liczba ujemna, limit jest niezmieniony. Kazda kategoria limitu ma zakodowana na stale gorna granice. Proby zwiekszenia limitu powyzej jego twardej gornej granicy sa po cichu obcinane do tej twardej gornej granicy.

Niezaleznie od tego, czy limit zostal zmieniony, funkcja sqlite_limit() zwraca poprzednia wartosc limitu. Tak wiec, by znalezc biezaca wartosc limitu bez jej zmieniania, po prostu wywolaj ten interfejs z trzecim parametrem ustawionym na -1.

Category moze byc albo jedna z nazw limitow-stringow nizej, albo odpowiadajaca liczba calkowita kategorii limitu SQLite. Jesli database handle jest niepoprawny lub category nie jest rozpoznana, zglaszany jest `E_INVARG`.

W momencie pisania tego istnieja nastepujace limity:

| Limit                     | Opis                                                                                                                                                                                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| LIMIT_LENGTH              | Maksymalny rozmiar jakiegokolwiek stringa, BLOB-a lub wiersza tabeli, w bajtach.                                                                                                                                                                                                           |
| LIMIT_SQL_LENGTH          | Maksymalna dlugosc instrukcji SQL, w bajtach.                                                                                                                                                                                                                        |
| LIMIT_COLUMN              | Maksymalna liczba kolumn w definicji tabeli lub w zbiorze wynikow SELECT, albo maksymalna liczba kolumn w indeksie lub w klauzuli ORDER BY lub GROUP BY.                                                                                                  |
| LIMIT_EXPR_DEPTH          | Maksymalna glebokosc drzewa parsowania dla jakiegokolwiek wyrazenia.                                                                                                                                                                                                                   |
| LIMIT_COMPOUND_SELECT     | Maksymalna liczba terminow w zlozonej instrukcji SELECT.                                                                                                                                                                                                              |
| LIMIT_VDBE_OP             | Maksymalna liczba instrukcji w programie maszyny wirtualnej uzywanym do zaimplementowania instrukcji SQL. Jesli sqlite3_prepare_v2() lub odpowiednik probuje przydzielic miejsce na wiecej niz te liczbe opkodow w jednym przygotowanym zapytaniu, zwracany jest blad SQLITE_NOMEM. |
| LIMIT_FUNCTION_ARG        | Maksymalna liczba argumentow funkcji.                                                                                                                                                                                                                           |
| LIMIT_ATTACHED            | Maksymalna liczba przylaczonych baz danych.                                                                                                                                                                                                                                |
| LIMIT_LIKE_PATTERN_LENGTH | Maksymalna dlugosc argumentu wzorca dla operatorow LIKE lub GLOB.                                                                                                                                                                                                |
| LIMIT_VARIABLE_NUMBER     | Maksymalny numer indeksu jakiegokolwiek parametru w instrukcji SQL.                                                                                                                                                                                                           |
| LIMIT_TRIGGER_DEPTH       | Maksymalna glebokosc rekursji dla triggerow.                                                                                                                                                                                                                             |
| LIMIT_WORKER_THREADS | Maksymalna liczba pomocniczych watkow roboczych, ktore jedno przygotowane zapytanie moze uruchomic. |

Po aktualna liste limitow, zobacz [dokumentacje SQLite](https://www.sqlite.org/c3ref/c_limit_attached.html).

**Funkcja: `sqlite_last_insert_row_id`**

sqlite_last_insert_row_id -- Ta funkcja identyfikuje ID wiersza ostatniej komendy insert wykonanej na bazie danych.

int `sqlite_last_insert_row_id`(INT database handle)

Jesli database handle jest niepoprawny, zglaszany jest `E_INVARG`.

**Funkcja: `sqlite_interrupt`**

sqlite_interrupt -- Ta funkcja powoduje przerwanie jakiejkolwiek oczekujacej operacji na bazie danych przy najblizszej mozliwej okazji.

none `sqlite_interrupt`(INT database handle)

Jesli operacja jest juz prawie zakonczona, gdy wywolywane jest sqlite_interrupt, moze nie miec okazji zostac przerwana i moze kontynuowac do zakonczenia.

To moze byc przydatne, gdy wykonujesz dlugo trwajace zapytanie i chcesz je przerwac.

Jesli database handle jest niepoprawny, zglaszany jest `E_INVARG`.

> UWAGA: w momencie pisania tego (wersja serwera 2.7.0) polecenie @kill NIE przerwie operacji zachodzacych w watku pomocniczym. Jesli chcesz przerwac zapytanie SQLite, musisz uzyc sqlite_interrupt, a NIE polecenia @kill.

**Funkcja: `sqlite_info`**

sqlite_info -- Ta funkcja zwraca mape informacji o bazie danych przy handle.

map `sqlite_info`(INT database handle)

Zwrocona mapa zawiera te klucze:

| Klucz | Wartosc |
| --- | --- |
| path | Sciezka bazy danych |
| parse_types | Prawda, jesli wartosci wynikowe sa parsowane na wartosci MOO |
| parse_objects | Prawda, jesli stringi takie jak "#123" sa parsowane jako referencje do obiektow |
| sanitize_strings | Prawda, jesli znaki nowej linii w stringach sa konwertowane na taby |
| locks | Liczba aktywnych operacji watkow roboczych uzywajacych tego uchwytu |

Jesli database handle jest niepoprawny, zglaszany jest `E_INVARG`.

**Funkcja: `sqlite_handles`**

sqlite_handles -- Zwraca liste otwartych uchwytow baz danych SQLite.

list `sqlite_handles()`

##### Operacje na srodowisku serwera

**Funkcja: `exec`**

Zobacz sekcje operacji administracyjnych po pelna dokumentacje `exec()`, wliczajac wsparcie dla zmiennych srodowiskowych.

**Funkcja: `getenv`**

getenv -- Zwraca wartosc podanej nazwanej zmiennej srodowiskowej.

str `getenv` (str name)

Jesli taka zmienna srodowiskowa nie istnieje, zwracane jest 0. Jesli programista nie jest czarodziejem, zglaszany jest E_PERM.

```
getenv("HOME")                                          =>   "/home/foobar"
getenv("XYZZY")                                         =>   0
```

##### Operacje na polaczeniach sieciowych

**Funkcja: `connected_players`**

connected_players -- zwraca liste numerow obiektow tych obiektow-graczy, ktore maja aktualnie aktywne polaczenia

list `connected_players` ([include-all])

Jesli podano include-all i jest ono prawdziwe, lista zawiera numery obiektow zwiazane ze _wszystkimi_ biezacymi polaczeniami, wliczajac te wychodzace i/lub jeszcze niezalogowane.

**Funkcja: `connected_seconds`**

connected_seconds -- zwraca liczbe sekund, przez jaka istnieje biezace aktywne polaczenie z graczem player

int `connected_seconds` (obj player)

**Funkcja: `idle_seconds`**

idle_seconds -- zwraca liczbe sekund, przez jaka biezace aktywne polaczenie z graczem player pozostaje bezczynne

int `idle_seconds` (obj player)

Jesli player nie jest numerem obiektu gracza z biezacym aktywnym polaczeniem, zglaszany jest `E_INVARG`.

**Funkcja: `notify`**

notify -- kolejkuje string do wypisania (w osobnej linii) na polaczeniu conn

int `notify` (obj conn, str string [, INT no-flush [, INT suppress-newline]])

Jesli programista nie jest conn ani czarodziejem, zglaszany jest `E_PERM`. Jesli conn nie jest biezacym aktywnym polaczeniem, ta funkcja nic nie robi. Wyjscie jest normalnie zapisywane na polaczenia wylacznie pomiedzy zadaniami, nie w trakcie wykonania.

Serwer nie bedzie kolejkowal dowolnej ilosci wyjscia dla polaczenia; opcja kompilacji `MAX_QUEUED_OUTPUT` (w `options.h`) kontroluje ten limit (`MAX_QUEUED_OUTPUT` mozna nadpisac z poziomu bazy danych, dodajac wlasciwosc `$server_options.max_queued_output` i wywolujac `load_server_options()`). Gdy nastapi proba zakolejkowania wyjscia, ktore przekroczyloby ten limit serwera, serwer najpierw probuje zapisac jak najwiecej wyjscia na polaczenie bez koniecznosci czekania na drugi koniec. Jesli to nie pozwoli nowemu wyjsciu zmiescic sie w kolejce, serwer zaczyna odrzucac najstarsze linie w kolejce, az nowe wyjscie sie zmiesci. Serwer pamieta, ile linii wyjscia w ten sposob "wyczyscil" (flushed) i, gdy nastepnym razem uda mu sie cokolwiek zapisac na polaczenie, najpierw wypisuje linie w rodzaju `>> Network buffer overflow: X lines of output to you have been lost <<`, gdzie X to liczba wyczyszczonych linii.

Jesli podano no-flush i jest ono prawdziwe, `notify()` nigdy nie czysci zadnego wyjscia z kolejki; zamiast tego natychmiast zwraca falsz. W przeciwnym razie `notify()` zawsze zwraca prawde.

Jesli podano suppress-newline i jest ono prawdziwe, `notify()` nie dodaje znaku nowej linii na koncu stringa.

**Funkcja: `buffered_output_length`**

buffered_output_length -- zwraca liczbe bajtow aktualnie zbuforowanych do wyjscia na polaczenie conn

int `buffered_output_length` ([obj conn])

Jesli nie podano conn, zwraca maksymalna liczbe bajtow, jaka bedzie buforowana do wyjscia na dowolnym polaczeniu.

Jesli podano conn, ale nie jest ono biezacym aktywnym polaczeniem, zglaszany jest `E_INVARG`. Jesli programista nie jest conn ani czarodziejem, zglaszany jest `E_PERM`.

**Funkcja: `read`**

read -- odczytuje i zwraca linie wejscia z polaczenia conn (lub, jesli nie podano, od gracza, ktory wpisal polecenie inicjujace biezace zadanie)

str `read` ([obj conn [, non-blocking]])

Jesli non-blocking jest falszywe lub nie podano go, ta funkcja zawiesza biezace zadanie, wznawiajac je, gdy dostepne jest wejscie do odczytu. Jesli podano non-blocking i jest ono prawdziwe, ta funkcja nigdy nie zawiesza wywolujacego zadania; jesli aktualnie nie ma dostepnego wejscia, `read()` po prostu natychmiast zwraca 0.

Jesli podano player, programista musi byc albo czarodziejem, albo wlascicielem `player`; jesli nie podano `player`, `read()` moze byc wywolana wylacznie przez czarodzieja i wylacznie w zadaniu, ktore zostalo ostatnio zapoczatkowane poleceniem z danego polaczenia. W przeciwnym razie zglaszany jest `E_PERM`.

Jesli podany `player` nie jest aktualnie polaczony i nie ma oczekujacych linii wejscia, lub jesli polaczenie zostanie zamkniete, gdy zadanie czeka na wejscie, ale zanim odebrano jakiekolwiek linie wejscia, `read()` zglasza `E_INVARG`.

Ograniczenie uzycia `read()` bez argumentow zachowuje nastepujacy prosty niezmiennik: jesli wejscie jest odczytywane od gracza, to jest ono przeznaczone dla zadania zapoczatkowanego ostatnim poleceniem wpisanym przez tego gracza. Ten niezmiennik naklada jednak dodatkowa odpowiedzialnosc na programiste. Jesli Twoj program wywoluje inny czasownik przed wykonaniem `read()`, to albo ten czasownik nie moze sie zawiesic, albo musisz zadbac, by w miedzyczasie zadne polecenia nie byly odczytywane z polaczenia. Najprostszym sposobem, by to zrobic, jest wywolanie

```
set_connection_option(player, "hold-input", 1)
```

zanim moglaby nastapic jakakolwiek zawieszka zadania, nastepnie wykonanie wszystkich wywolan `read()` i innego kodu, ktory moze sie zawiesic, a na koniec wywolanie

```
set_connection_option(player, "hold-input", 0)
```

by ponownie pozwolic na normalne odczytywanie i interpretowanie polecen.

**Funkcja: `force_input`**

force_input -- wstawia string line jako zadanie wejsciowe do kolejki dla polaczenia conn, dokladnie tak, jakby przybyl jako wejscie przez siec

none `force_input` (obj conn, str line [, at-front])

Jesli podano at_front i jest ono prawdziwe, nowa linia wejscia jest umieszczana na poczatku kolejki conn, tak by byla nastepna przetwarzana linia wejscia, nawet jesli w tej kolejce jest juz jakies inne wejscie. Zglasza `E_INVARG`, jesli conn nie okresla biezacego polaczenia, oraz `E_PERM`, jesli programista nie jest ani conn, ani czarodziejem.

**Funkcja: `flush_input`**

flush_input -- wykonuje te same akcje, jak gdyby zdefiniowane dla polaczenia conn polecenie flush zostalo odebrane na tym polaczeniu

none `flush_input` (obj conn [show-messages])

Czyli usuwa wszystkie oczekujace linie wejscia z kolejki conn i, jesli podano show-messages i jest ono prawdziwe, wypisuje na conn komunikat wymieniajacy wyczyszczone linie, jesli takie byly. Zobacz rozdzial o zalozeniach serwera wobec bazy danych po wiecej informacji o zdefiniowanym dla polaczenia poleceniu flush.

**Funkcja: `output_delimiters`**

output_delimiters -- zwraca liste dwoch stringow: biezacy _prefiks wyjscia_ i _sufiks wyjscia_ dla gracza player.

list `output_delimiters` (obj player)

Jesli player nie ma aktywnego polaczenia sieciowego, zglaszany jest `E_INVARG`. Jesli ktorys ze stringow jest aktualnie niezdefiniowany, uzywana jest w jego miejsce wartosc `""`. Zobacz omowienie polecen `PREFIX` i `SUFFIX` w nastepnym rozdziale po wiecej informacji o prefiksie i sufiksie wyjscia.

**Funkcja: `boot_player`**

boot_player -- oznacza do rozlaczenia dowolne biezace aktywne polaczenie z podanym graczem

none `boot_player` (obj player)

Polaczenie nie zostanie faktycznie zamkniete, dopoki biezaco wykonywane zadanie nie zwroci wyniku lub sie nie zawiesi, ale wszystkie funkcje MOO (takie jak `notify()`, `connected_players()` i podobne) natychmiast zaczynaja zachowywac sie tak, jakby polaczenie juz nie istnialo. Jesli programista nie jest ani czarodziejem, ani tym samym co player, zglaszany jest `E_PERM`. Jesli nie ma biezacego aktywnego polaczenia z graczem player, ta funkcja nic nie robi.

Jesli istnialo biezace aktywne polaczenie, to gdy polaczenie zostanie faktycznie zamkniete, wykonywane jest nastepujace wywolanie czasownika:

```
$user_disconnected(player)
```

To nie jest bledem, jesli ten czasownik nie istnieje; wywolanie jest po prostu pomijane.

**Funkcja: `connection_info`**

connection_info -- Zwraca MAPE informacji o polaczeniu sieciowym dla `connection`. W chwili pisania tego tekstu zwracane sa nastepujace informacje:

map `connection_info` (OBJ `connection`)

| Klucz | Wartosc |
| --- | --- |
| destination_address | Nazwa hosta polaczenia. Dla polaczen przychodzacych jest to nazwa hosta polaczonego uzytkownika. Dla polaczen wychodzacych jest to nazwa hosta celu polaczenia wychodzacego. |
| destination_ip | Nierozwiazany numeryczny adres IP polaczenia. |
| destination_port | Dla polaczen przychodzacych jest to lokalny port uzyty do nawiazania polaczenia. Dla polaczen wychodzacych jest to port, do ktorego nawiazano polaczenie. |
| source_address | Nazwa hosta interfejsu, na ktorym nawiazano polaczenie przychodzace. Dla polaczen wychodzacych ta wartosc nie ma znaczenia. |
| source_ip | Nierozwiazany numeryczny adres IP interfejsu, na ktorym nawiazano polaczenie. Dla polaczen wychodzacych ta wartosc nie ma znaczenia. |
| source_port | Lokalny port, z ktorym polaczono. Dla polaczen wychodzacych ta wartosc nie ma znaczenia. |
| protocol | Opisuje protokol uzyty do nawiazania polaczenia. W chwili pisania tego tekstu moze to byc IPv4 lub IPv6. |
| outbound | Wskazuje, czy polaczenie jest wychodzace, czy nie |
| tls | Informacje o polaczeniu TLS. Ten klucz jest obecny wylacznie, gdy ToastStunt zbudowano ze wsparciem `USE_TLS`. |

Jesli connection nie jest prawidlowe lub jest w trakcie rozlaczania, zglaszany jest `E_INVARG`. Jesli programista nie jest czarodziejem i nie jest connection, zglaszany jest `E_PERM`.

**Funkcja: `connection_name`**

connection_name -- zwraca string specyficzny dla sieci, identyfikujacy polaczenie uzywane przez danego gracza

str `connection_name` (obj player, [INT method])

Podana tylko z obiektem gracza, ta funkcja zwraca jedynie nazwe hosta obj (np. `1-2-3-6.someplace.com`). Opcjonalny argument pozwala okreslic 1, jesli chcesz numeryczny adres IP, lub 2, jesli chcesz zwrocic string connection_name w starym (legacy) formacie.

> Ostrzezenie: jesli uzywasz rdzenia LambdaMOO, jest to zmiana czesciowo lamiaca kompatybilnosc. Bedziesz chcial zaktualizowac kod na swoim serwerze wywolujacy `connection_name`, by przekazywal argument zwracajacy string connection_name w starym formacie, jesli chcesz, by wszystko dzialalo dokladnie tak samo.

Jesli programista nie jest czarodziejem i nie jest graczem player, zglaszany jest `E_PERM`. Jesli player nie jest aktualnie polaczony, zglaszany jest `E_INVARG`.

Informacje o stringu polaczenia w starym formacie (Legacy Connection String):

Dla konfiguracji sieciowych TCP/IP, dla polaczen przychodzacych, string ma postac:

```
"port lport from host, port port"
```

gdzie lport to dziesietny port nasluchujacy TCP, na ktory przybylo polaczenie, host to nazwa lub dziesietny adres TCP hosta, z ktorego polaczony jest gracz, a port to dziesietny port TCP polaczenia na tym hoscie.

Dla wychodzacych polaczen TCP/IP, string ma postac

```
"port lport to host, port port"
```

gdzie lport to dziesietny numer lokalnego portu TCP, z ktorego wywodzi sie polaczenie, host to nazwa lub dziesietny adres TCP hosta, do ktorego otwarto polaczenie, a port to dziesietny port TCP polaczenia na tym hoscie.

Dla konfiguracji sieciowej System V 'local', string to nazwa logowania UNIX laczacego sie uzytkownika lub, jesli takiej nazwy nie mozna znalezc, cos w postaci:

```
"User #number"
```

gdzie number to numeryczny identyfikator uzytkownika UNIX.

Dla innych konfiguracji sieciowych string jest taki sam dla wszystkich polaczen, a wiec bezuzyteczny.

**Funkcja: `connection_name_lookup`**

connection_name_lookup -- Ta funkcja wykonuje wyszukiwanie nazwy DNS dla adresu IP connection.

str `connection_name_lookup` (OBJ connection [, INT record_result])

Jesli nazwa hosta nie moze zostac rozwiazana, funkcja po prostu zwraca numeryczny adres IP. W przeciwnym razie zwroci rozwiazana nazwe hosta.

Jesli record_result jest prawdziwe, rozwiazana nazwa hosta zostanie zapisana wraz z polaczeniem i nadpisze jego istniejacy wynik 'connection_name()'. Oznacza to, ze mozesz wywolac 'connection_name_lookup()' jednorazowo w momencie tworzenia polaczenia, a potem nadal uzywac 'connection_name()' tak jak zawsze wczesniej.

Ta funkcja jest przeznaczona przede wszystkim do uzytku, gdy ustawiona jest opcja serwera 'NO_NAME_LOOKUP'. Poza tymczasowymi awariami Twojego serwera nazw, niewiele zyskasz, wywolujac ja, gdy serwer sam wykonuje dla Ciebie wyszukiwania DNS.

> Uwaga: ta funkcja dziala w osobnym watku. Choc jest to dobre dla wydajnosci (dlugie wyszukiwania nie zablokuja Twojego MOO tak, jak tradycyjne wyszukiwania nazw sprzed wersji 2.6.0), oznacza to tez, ze stworzenie w pelni wewnatrzbazodanowego rozwiazania wyszukiwania DNS wymaga nieco wiecej pracy. Poniewaz ta funkcja jawnie sie zawiesza, nie bedziesz mogl jej uzyc w 'do_login_command()' bez uzycia rowniez funkcji 'switch_player()'. Przyklad, jak to moze dzialac, znajdziesz w '#0:do_login_command()' w ToastCore.

**Funkcja: `switch_player`**

switch_player -- Cicho przelacza gracza powiazanego z tym polaczeniem z object1 na object2.

none `switch_player`(OBJ object1, OBJ object2 [, INT silent])

object1 musi byc polaczony, a object2 musi byc graczem. Mozna tego uzyc w czasownikach do_login_command(), ktore odczytuja lub sie zawieszaja (co uniemozliwia dzialanie normalnego mechanizmu wyboru gracza).

Jesli silent jest prawdziwe, nie zostana wypisane zadne komunikaty polaczenia.

Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`. `E_INVARG` jest zglaszany, jesli object1 i object2 sa tym samym obiektem, jesli object1 nie jest polaczony, jesli object2 nie jest graczem, lub jesli object1 nie ma kolejki zadan do przekazania.

> Uwaga: to wywoluje czasowniki user_disconnected i user_connected obiektu nasluchujacego, gdy jest to stosowne.

**Funkcja: `set_connection_option`**

set_connection_option -- kontroluje szereg opcjonalnych zachowan zwiazanych z polaczeniem conn

none `set_connection_option` (obj conn, str option, value)

Zglasza E_INVARG, jesli conn nie okresla biezacego polaczenia, i E_PERM, jesli programista nie jest ani conn, ani czarodziejem. O ile nie zaznaczono inaczej ponizej, opcje moga byc wylacznie wlaczone (value jest prawdziwe) lub wylaczone (w przeciwnym razie). Aktualnie wspierane sa nastepujace wartosci dla option:

`"binary"`
Gdy ustawione, polaczenie jest w trybie binarnym, w ktorym zarowno wejscie z conn, jak i wyjscie do conn moze zawierac dowolne bajty. Wejscie z polaczenia w trybie binarnym w ogole nie jest dzielone na linie; jest dostarczane albo do funkcji read(), albo do normalnego parsowania polecen jako stringi binarne, w takich fragmentach, w jakich przychodza z systemu operacyjnego. (Zobacz subtelny szczegol o stringach binarnych po opis reprezentacji stringa binarnego.) Dla wyjscia na polaczenie w trybie binarnym, drugi argument `notify()` musi byc stringiem binarnym; jesli jest zle sformowany, zglaszany jest E_INVARG.

> Subtelny szczegol: jesli tryb polaczenia zostanie zmieniony w momencie, gdy na polaczeniu jest oczekujace wejscie, to wejscie zostanie dostarczone zgodnie z poprzednim trybem (tj. przy przelaczaniu z trybu binarnego moga byc oczekujace "linie" zawierajace sekwencje escape z tylda dla wbudowanych znakow konca linii, tabulatorow, tyld i innych znakow; przy przelaczaniu na tryb binarny moga byc oczekujace linie zawierajace surowe tabulatory, z ktorych znaki niedrukowalne zostaly po cichu usuniete zgodnie z trybem normalnym). Wylacznie w trakcie poczatkowego wywolania $do_login_command() na polaczeniu przychodzacym lub bezposrednio po wywolaniu open_network_connection() tworzacym polaczenie wychodzace masz pewnosc, ze nie ma oczekujacego wejscia. W innych momentach prawdopodobnie zechcesz wyczyscic wszelkie oczekujace wejscie bezposrednio po zmianie trybu polaczenia.

`"hold-input"`

Gdy ustawione, zadne wejscie odebrane na conn nie bedzie traktowane jako polecenie; zamiast tego wszystkie wejscie pozostaje w kolejce, dopoki nie zostanie pobrane wywolaniami read() lub dopoki ta opcja polaczenia nie zostanie wylaczona, w ktorym to momencie przetwarzanie polecen zostaje wznowione. Ta opcja nie wplywa na przetwarzanie linii wejscia poza pasmem (out-of-band).

`"disable-oob"`

Gdy ustawione, wylacza wszelkie przetwarzanie poza pasmem (zobacz sekcje o przetwarzaniu poza pasmem). Wszystkie kolejne linie wejscia, az do nastepnego polecenia wylaczajacego te opcje, beda dostepne dla zadan odczytu lub normalnego parsowania polecen dokladnie tak, jakby prefiks poza pasmem i prefiks cytowania poza pasmem nie byly zdefiniowane dla tego serwera.

`"client-echo"`
Ustawienie tej opcji nie ma znaczenia dla serwera. Jednak wywolanie set_connection_option() dla tej opcji wysyla komende protokolu Telnet `WONT ECHO` lub `WILL ECHO`, odpowiednio do tego, czy value jest prawdziwe czy falszywe. Dla klientow wspierajacych protokol Telnet powinno to przelaczac, czy klient lokalnie echouje znaki wpisywane przez uzytkownika. Zauwaz, ze sam serwer nigdy w zadnych okolicznosciach nie echouje znakow wejscia. (Ta opcja jest dostepna wylacznie w konfiguracjach sieciowych TCP/IP.)

`"flush-command"`
Ta opcja przyjmuje wartosc typu string. Jesli string jest niepusty, jest to polecenie flush dla tego polaczenia, ktorym gracz moze wyczyscic wszystkie zakolejkowane wejscie jeszcze nie przetworzone przez serwer. Jesli string jest pusty, conn w ogole nie ma polecenia flush. set_connection_option pozwala tez podac wartosc niebedaca stringiem, co jest rownowazne podaniu pustego stringa. Domyslna wartosc tej opcji mozna ustawic przez wlasciwosc `$server_options.default_flush_command`; zobacz sekcje o czyszczeniu nieprzetworzonego wejscia po szczegoly.

`"intrinsic-commands"`

Wartoscia tej opcji jest lista stringow, z ktorych kazdy jest nazwa jednego z dostepnych wewnetrznych (intrinsic) polecen serwera (zobacz sekcje o liniach polecen otrzymujacych specjalne traktowanie). Polecenia spoza tej listy sa wylaczone, tj. traktowane jak zwykle polecenia MOO obslugiwane przez $do_command i/lub wbudowany parser polecen

set_connection_option pozwala tez podac wartosc calkowitoliczbowa, ktora, jesli wynosi zero, jest rownowazna podaniu pustej listy, a w przeciwnym razie jest traktowana jako lista wszystkich dostepnych polecen wewnetrznych (ustawienie domyslne).

Tak wiec jednym ze sposobow udostepnienia nazwy czasownika `PREFIX` jako zwyklego polecenia jest:

```
set_connection_option(
  player, "intrinsic-commands",
  setremove(connection_options(player, "intrinsic-commands"),
            "PREFIX"));
```

Zauwaz, ze connection_options() bez drugiego argumentu zwroci liste, natomiast podanie drugiego argumentu zwroci wartosc zadanego klucza.

```
save = connection_options(player,"intrinsic-commands");
set_connection_option(player, "intrinsic-commands", 1);
full_list = connection_options(player,"intrinsic-commands");
set_connection_option(player,"intrinsic-commands", save);
return full_list;
```

to sposob na uzyskanie pelnej listy polecen wewnetrznych dostepnych w serwerze bez wplywu na biezace polaczenie.

Od wersji 2.7.1 kazde polaczenie ma teraz opcje wlaczenia TCP keep-alive. Mozna je skonfigurowac przez set_connection_option, podajac albo 1 (by wlaczyc i uzyc wartosci domyslnych), albo mape opcji. Klucze opcji to: idle, interval i count. Wiecej informacji o tym, co robia, oraz wartosci domyslne, znajdziesz w options.h.

Nic nie zepsuto w kwestii kompatybilnosci. Stary sposob ustawiania opcji nadal istnieje. Keep-alive jest opcja:
```
set_connection_option(player, "keep-alive", 1);
```

Lub:

```
set_connection_option(player, "keep-alive", ["idle" -> 90, "interval" -> 60]);
```

Uwaga: jesli nie podasz jednej z 3 opcji w mapie, przyjmie ona wartosc domyslna zgodnie z options.h.

**Funkcja: `connection_options`**

connection_options -- zwraca liste par `{name, value}` opisujacych biezace ustawienia wszystkich dozwolonych opcji dla polaczenia conn, albo wartosc, jesli podano `name`

ANY `connection_options` (obj conn [, STR name])

Zglasza `E_INVARG`, jesli conn nie okresla biezacego polaczenia, i `E_PERM`, jesli programista nie jest ani conn, ani czarodziejem.

Wywolanie connection_options bez nazwy zwroci LISTE. Podanie name zwroci wylacznie wartosc zadanej opcji `name`.

**Funkcja: `open_network_connection`**

open_network_connection -- nawiazuje polaczenie sieciowe z miejscem okreslonym przez argumenty i mniej wiecej udaje, ze zostalo stamtad nawiazane nowe, normalne polaczenie gracza

obj `open_network_connection` (STR host, INT port [, MAP options])

Nawiazuje polaczenie sieciowe z miejscem okreslonym przez argumenty i mniej wiecej udaje, ze zostalo stamtad nawiazane nowe, normalne polaczenie gracza. Nowe polaczenie, jak zwykle, nie bedzie poczatkowo zalogowane i bedzie mialo powiazany z nim ujemny numer obiektu do uzytku z `read()`, `notify()` i `boot_player()`. Ten numer obiektu jest wartoscia zwracana przez te funkcje.

Jesli programista nie jest czarodziejem lub jesli opcja kompilacji `OUTBOUND_NETWORK` nie byla uzyta przy budowaniu serwera, zglaszany jest `E_PERM`. Jesli wsparcie dla sieci wychodzacej jest obecne, ale wylaczone w czasie dzialania, `E_PERM` jest zglaszany z wartoscia wskazujaca, ze polaczenia sieciowe wychodzace sa wylaczone.

`host` odnosi sie do stringa nazywajacego host (mozliwe, ze numeryczny adres IP), a `port` to liczba calkowita odnoszaca sie do numeru portu TCP. Jesli polaczenia nie mozna nawiazac, poniewaz host nie istnieje, port nie istnieje, host jest nieosiagalny lub odrzucil polaczenie, zglaszany jest `E_INVARG`. Jesli polaczenia nie mozna nawiazac z innych powodow, wliczajac ograniczenia zasobow, zglaszany jest `E_QUOTA`. Gdy te bledy zostana przechwycone, wartosc bledu moze zawierac bardziej szczegolowe informacje diagnostyczne, takie jak szczegoly niepowodzenia wyszukiwania adresu, gniazda, polaczenia lub TLS.

Opcjonalnie mozesz podac mape z dowolnymi lub wszystkimi z nastepujacych opcji:

  listener: Obiekt, ktorego czasowniki nasluchujace beda wywolywane w odpowiednich momentach. (Zobacz HELP LISTEN() po wiecej szczegolow.)

  tls: Jesli prawdziwe, nawiazuje bezpieczne polaczenie TLS.

  ipv6: Jesli prawdziwe, wykorzystuje protokol IPv6 zamiast IPv4.

  tls_verify: Jesli prawdziwe, weryfikuje zdalnego partnera TLS. Ta opcja jest dostepna wylacznie, gdy ToastStunt zbudowano ze wsparciem TLS.

Przy otwieraniu wychodzacego polaczenia TLS, ToastStunt wysyla Server Name Indication (SNI), uzywajac podanej nazwy hosta.

Proces nawiazywania polaczenia wychodzacego obejmuje pewne kroki, ktore moga zajac dosc duzo czasu, w trakcie ktorych serwer nie robi nic innego, wliczajac odpowiadanie na polecenia uzytkownikow i wykonywanie zadan MOO. Zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly tego, jak serwer ogranicza czas oczekiwania na pomyslne zakonczenie tych krokow.

Warto wspomniec o jednym trudnym aspekcie zwiazanym z uzyciem tej funkcji. Poniewaz serwer traktuje nowe polaczenie niemal tak samo jak kazde normalne polaczenie gracza, w naturalny sposob bedzie probowal parsowac dowolne wejscie z tego polaczenia jako polecenia w zwykly sposob. By temu zapobiec, powinienes uzyc `set_connection_option()`, by ustawic opcje `hold-input` na prawde dla tego polaczenia.

Przyklad:

```
open_network_connection("2607:5300:60:4be0::", 1234, ["ipv6" -> 1, "listener" -> #6, "tls" -> 1])
```

Otworz nowe polaczenie z adresem IPv6 2607:5300:60:4be0:: na porcie 1234, uzywajac TLS. Odpowiednie czasowniki zostana wywolane na #6.

**Funkcja: `curl`**

str `curl` (STR url [, INT include_headers [, INT timeout]])

Wbudowana funkcja curl pobierze strone internetowa i zwroci ja jako string. Jesli include_headers jest prawdziwe, naglowki HTTP zostana wlaczone do zwracanego stringa.

Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`. Jesli sieciowe polaczenia wychodzace sa wylaczone w czasie dzialania, `curl()` zglasza `E_PERM` z wartoscia wskazujaca, ze polaczenia sieciowe wychodzace sa wylaczone.

Warto zauwazyc, ze otrzymane dane beda zakodowane binarnie. W szczegolnosci zauwazysz, ze znaki nowej linii pojawiaja sie jako ~0A. Mozesz latwo przeksztalcic strone w liste, przekazujac zwrocony string do funkcji decode_binary().

CURL_TIMEOUT jest zdefiniowany w options.h i okresla maksymalny czas, jaki moze zajac zadanie CURL, zanim zawiedzie. Dla szczegolnych przypadkow mozesz okreslic dluzszy lub krotszy limit czasu za pomoca trzeciego argumentu curl().

Od wersji ToastStunt 2.7.3 curl wspiera protokol Dictionary Server (DICT).

**Funkcja: `url_encode`**

url_encode -- koduje string w formacie URL.

str `url_encode` (STR string)

Zwraca string ze znakami zakodowanymi (escaped) do uzytku w URL. Jesli sieciowe polaczenia wychodzace sa wylaczone w czasie dzialania, zglaszany jest `E_PERM`. Jesli ToastStunt zbudowano bez wsparcia dla curl, ta funkcja jest niedostepna.

**Funkcja: `url_decode`**

url_decode -- dekoduje string zakodowany w formacie URL.

str `url_decode` (STR string)

Zwraca zdekodowana kopie string. Jesli sieciowe polaczenia wychodzace sa wylaczone w czasie dzialania, zglaszany jest `E_PERM`. Jesli ToastStunt zbudowano bez wsparcia dla curl, ta funkcja jest niedostepna.

**Funkcja: `read_http`**

map `read_http` (request-or-response [, OBJ conn])

Odczytuje linie z polaczenia conn (lub, jesli nie podano, od gracza, ktory wpisal polecenie inicjujace biezace zadanie) i probuje sparsowac te linie tak, jakby byly zadaniem (request) lub odpowiedzia (response) HTTP. request-or-response musi byc albo stringiem "request", albo "response". Okresla to rodzaj parsowania, jakie zostanie wykonane.

Jesli parsowanie zawiedzie, poniewaz zadanie lub odpowiedz sa skladniowo niepoprawne, `read_http()` zwraca mape z pojedynczym kluczem `"error"` i lista wartosci opisujacych powod bledu. Jesli zakolejkowanego wejscia nie mozna zdekodowac jako prawidlowego stringa binarnego MOO, `read_http()` zwraca 0.

Podobnie jak read(), jesli podano conn, programista musi byc albo czarodziejem, albo wlascicielem conn; jesli conn nie podano, read_http() moze byc wywolana wylacznie przez czarodzieja i wylacznie w zadaniu, ktore zostalo ostatnio zapoczatkowane poleceniem z danego polaczenia. W przeciwnym razie zglaszany jest E_PERM. Podobnie, jesli conn nie jest aktualnie polaczony i nie ma oczekujacych linii wejscia, lub jesli polaczenie zostanie zamkniete, gdy zadanie czeka na wejscie, ale zanim odebrano jakiekolwiek linie wejscia, read_http() zglasza E_INVARG.

Jesli parsowanie zawiedzie, poniewaz zadanie lub odpowiedz sa skladniowo niepoprawne, read_http() zwroci mape z pojedynczym kluczem "error" i lista wartosci opisujacych powod bledu. Jesli parsowanie sie powiedzie, read_http() zwroci mape z odpowiednim podzbiorem nastepujacych kluczy, z wartosciami sparsowanymi z zadania lub odpowiedzi HTTP: "method", "uri", "headers", "body", "status" i "upgrade".

> Subtelny szczegol: read_http() zaklada, ze stringi wejsciowe sa stringami binarnymi. Gdy wywolywana interaktywnie, jak w przykladzie ponizej, programista musi wstawic doslowne terminatory linii, w przeciwnym razie parsowanie zawiedzie.

Nastepujacy przyklad interaktywnie odczytuje zadanie HTTP z polaczenia gracza.

```
read_http("request", player)
GET /path HTTP/1.1~0D~0A
Host: example.com~0D~0A
~0D~0A
```

W tym przykladzie string ~0D~0A konczy zadanie. Wywolanie zwraca nastepujace (zadanie nie ma ciala):

```
["headers" -> ["Host" -> "example.com"], "method" -> "GET", "uri" -> "/path"]
```

Nastepujacy przyklad interaktywnie odczytuje odpowiedz HTTP z polaczenia gracza.

```
read_http("response", player)
HTTP/1.1 200 Ok~0D~0A
Content-Length: 10~0D~0A
~0D~0A
1234567890
```

Wywolanie zwraca nastepujace:

```
["body" -> "1234567890", "headers" -> ["Content-Length" -> "10"], "status" -> 200]
```

**Funkcja: `listen`**

listen -- tworzy nowy punkt, w ktorym serwer bedzie nasluchiwal polaczen sieciowych, dokladnie tak jak robi to normalnie

value `listen` (obj object, port [, MAP options])

Tworzy nowy punkt, w ktorym serwer bedzie nasluchiwal polaczen sieciowych, dokladnie tak jak robi to normalnie. `Object` to obiekt, ktorego czasowniki `do_login_command`, `do_command`, `do_out_of_band_command`, `user_connected`, `user_created`, `user_reconnected`, `user_disconnected` i `user_client_disconnected` beda wywolywane w odpowiednich momentach, tak jak te czasowniki sa wywolywane na #0 dla normalnych polaczen. (Zobacz rozdzial w Podreczniku Programisty LambdaMOO o zalozeniach serwera wobec bazy danych po pelna historie, kiedy te funkcje sa wywolywane.) `Port` to numer portu TCP, na ktorym nalezy nasluchiwac. Funkcja listen() zwroci `port`, chyba ze `port` wynosi zero, w takim przypadku wartoscia zwracana jest numer portu przydzielony przez system operacyjny.

Opcjonalny trzeci argument pozwala ustawic rozne dodatkowe opcje dla punktu nasluchu. Sa to:

  print-messages: Jesli prawdziwe, rozne konfigurowalne z poziomu bazy danych komunikaty (rowniez opisane w rozdziale o zalozeniach serwera) beda wypisywane na polaczeniach odebranych na nowym punkcie nasluchu.

  ipv6: Uzyj protokolu IPv6 zamiast IPv4.

  tls: Akceptuj wylacznie prawidlowe, bezpieczne polaczenia TLS.

  certificate: Pelna sciezka do certyfikatu TLS. UWAGA: wymaga, by opcja TLS byla rowniez podana i prawdziwa. Ta opcja jest potrzebna wylacznie, gdy certyfikat rozni sie od tego okreslonego w options.h.

  key: Pelna sciezka do klucza prywatnego TLS. UWAGA: wymaga, by opcja TLS byla rowniez podana i prawdziwa. Ta opcja jest potrzebna wylacznie, gdy klucz rozni sie od tego okreslonego w options.h.

  interface: Pozwala okreslic interfejs, na ktorym nalezy nasluchiwac. (Podobnie do argumentow linii polecen --ipv4 lub --ipv6.)

listen() zglasza E_PERM, jesli programista nie jest czarodziejem, E_INVARG, jesli `object` jest niepoprawne lub juz istnieje punkt nasluchu opisany przez `point`, oraz E_QUOTA, jesli wystapil jakis blad specyficzny dla konfiguracji sieciowej.

Przyklad:

```
listen(#0, 1234, ["ipv6" -> 1, "tls" -> 1, "certificate" -> "/etc/certs/something.pem", "key" -> "/etc/certs/privkey.pem", "print-messages" -> 1])
```

Nasluchuj polaczen IPv6 na porcie 1234 i wypisuj komunikaty w stosownych przypadkach. Te polaczenia musza byc TLS i beda uzywac klucza prywatnego i certyfikatu znalezionych w /etc/certs.

**Funkcja: `unlisten`**

unlisten -- przestaje nasluchiwac polaczen na punkcie opisanym przez canon, ktory powinien odpowiadac wartosci `port` z elementu listy zwracanej przez `listeners()`

none `unlisten` (canon [, INT ipv6])

Zglasza `E_PERM`, jesli programista nie jest czarodziejem, i `E_INVARG`, jesli nie istnieje punkt nasluchu o takim opisie. Jesli podano `ipv6` i jest ono prawdziwe, ToastStunt szuka punktu nasluchu IPv6 o takim opisie.

**Funkcja: `listeners`**

listeners -- zwraca liste opisujaca istniejace punkty nasluchu, wliczajac domyslny, tworzony automatycznie przez serwer przy starcie (chyba ze zostal on od tego czasu zniszczony wywolaniem `unlisten()`)

list `listeners` ([obj-or-port])

Jesli podano obiekt lub port, zwracane sa wylacznie pasujace punkty nasluchu. Kazdy element zwracanej listy jest mapa z nastepujacymi kluczami:

| Klucz | Wartosc |
| --- | --- |
| object | Obiekt, ktorego czasowniki nasluchujace sa wywolywane. |
| port | Port lub deskryptor punktu nasluchu. |
| print-messages | Prawda, jesli dla tego punktu nasluchu wypisywane sa komunikaty konfigurowalne z poziomu bazy danych. |
| ipv6 | Prawda, jesli ten punkt nasluchu uzywa IPv6. |
| interface | Interfejs, na ktorym prowadzony jest nasluch. |
| tls | Prawda, jesli ten punkt nasluchu uzywa TLS. Ten klucz jest obecny wylacznie, gdy ToastStunt ma wsparcie TLS. |

Dla poczatkowego punktu nasluchu, object to `#0`, port jest okreslany przez argumenty linii polecen lub domyslna wartosc specyficzna dla konfiguracji sieciowej, a print-messages jest prawdziwe.

Zauwaz, ze poczatkowy punkt nasluchu tworzony przez serwer przy starcie nie ma w sobie nic specjalnego; mozesz uzyc na nim `unlisten()` dokladnie tak, jakby zostal utworzony przez `listen()`. Moze to byc przydatne; na przyklad, w jednej z konfiguracji TCP/IP, mozesz uruchomic swoj serwer na jakims malo znanym porcie, powiedzmy 12345, polaczyc sie z nim samemu na jakis czas, a nastepnie otworzyc go dla normalnych uzytkownikow, wykonujac instrukcje:

```
unlisten(12345); listen(#0, 7777, ["print-messages" -> 1])
```

##### Operacje zwiazane z czasem i datami

**Funkcja: `time`**

time -- zwraca biezacy czas, reprezentowany jako liczba sekund, ktore uplynely od polnocy 1 stycznia 1970 czasu Greenwich (GMT)

int `time` ()

**Funkcja: `ftime`**

ftime -- Zwraca biezacy czas reprezentowany jako liczba sekund i nanosekund, ktore uplynely od polnocy 1 stycznia 1970 czasu Greenwich (GMT).

float `ftime` ([INT monotonic])

Jesli podano argument `monotonic` i ustawiono go na 1, zwrocony czas bedzie monotoniczny. Oznacza to, ze zawsze otrzymasz informacje o tym, ile czasu uplynelo od dowolnego, ustalonego punktu w przeszlosci, niezaleznie od dryfu zegara lub innych zmian czasu systemowego. Jest to przydatne przy mierzeniu, ile trwa jakas operacja, poniewaz nie zalezy to od aktualnego czasu systemowego.

Ogolna zasada jest taka, by uzywac ftime() bez argumentow do podawania czasu, a ftime() z argumentem zegara monotonicznego do mierzenia uplywu czasu.

**Funkcja: `ctime`**

ctime -- interpretuje time jako czas, uzywajac tej samej reprezentacji, co podana w opisie `time()` powyzej, i przeksztalca go w 28-znakowy, czytelny dla czlowieka string

str `ctime` ([int time])

String bedzie mial nastepujacy format:

```
Mon Aug 13 19:13:20 1990 PDT
```

Jesli biezacy dzien miesiaca jest mniejszy niz 10, pomiedzy miesiacem a dniem pojawia sie dodatkowa spacja:

```
Mon Apr  1 14:10:43 1991 PST
```

Jesli nie podano time, uzywany jest czas biezacy.

Zauwaz, ze `ctime()` interpretuje czas wedlug lokalnej strefy czasowej komputera, na ktorym dziala serwer MOO.

##### Ewaluacja kodu MOO i manipulacja zadaniami

**Funkcja: `raise`**

raise -- zglasza code jako blad, w taki sam sposob jak robia to inne wyrazenia, instrukcje i funkcje MOO

none `raise` (code [, str message [, value]])

Message, ktore domyslnie przyjmuje wartosc `tostr(code)`, oraz value, ktore domyslnie wynosi zero, sa udostepniane dowolnym instrukcjom `try`-`except` przechwytujacym ten blad. Jesli blad nie zostanie przechwycony, message pojawi sie w pierwszej linii tracebacku wypisanego uzytkownikowi.

**Funkcja: `call_function`**

call_function -- wywoluje funkcje wbudowana o nazwie func-name, przekazujac podane argumenty, i zwraca to, co zwroci ta funkcja

value `call_function` (str func-name, arg, ...)

Zglasza `E_INVARG`, jesli func-name nie zostanie rozpoznane jako nazwa znanej funkcji wbudowanej. Pozwala to obliczyc nazwe funkcji do wywolania i, w szczegolnosci, pozwala napisac wywolanie funkcji wbudowanej, ktora moze, ale nie musi, istniec w konkretnej wersji uzywanego przez Ciebie serwera.

**Funkcja: `function_info`**

function_info -- zwraca opisy funkcji wbudowanych dostepnych na serwerze

list `function_info` ([str name])

Jesli podano name, zwracany jest wylacznie opis funkcji o tej nazwie. Jesli pominieto name, zwracana jest lista opisow, po jednym dla kazdej funkcji dostepnej na serwerze. Zglaszany jest `E_INVARG`, jesli podano name, ale zadna funkcja o tej nazwie nie jest dostepna na serwerze.

Kazdy opis funkcji jest lista w nastepujacej postaci:

```
{name, min-args, max-args, types}
```

gdzie name to nazwa funkcji wbudowanej, min-args to minimalna liczba argumentow, jaka musi zostac podana funkcji, max-args to maksymalna liczba argumentow, jaka moze zostac podana funkcji, lub `-1`, jesli nie ma maksimum, a types to lista max-args liczb calkowitych (lub min-args, jesli max-args wynosi `-1`), z ktorych kazda reprezentuje typ argumentu wymagany na odpowiadajacej pozycji. Kazdy numer typu jest taki, jaki zwrocilaby funkcja wbudowana `typeof()`, z wyjatkiem tego, ze `-1` oznacza, ze akceptowana jest wartosc dowolnego typu, a `-2` oznacza, ze mozna podac albo liczby calkowite, albo zmiennoprzecinkowe. Dla przykladu, oto kilka wpisow z tej listy:

```
{"listdelete", 2, 2, {4, 0}}
{"suspend", 0, 1, {0}}
{"server_log", 1, 2, {2, -1}}
{"max", 1, -1, {-2}}
{"tostr", 0, -1, {}}
```

`listdelete()` przyjmuje dokladnie 2 argumenty, z ktorych pierwszy musi byc lista (`LIST == 4`), a drugi musi byc liczba calkowita (`INT == 0`). `suspend()` ma jeden opcjonalny argument, ktory, jesli podany, musi byc liczba (calkowita lub zmiennoprzecinkowa). `server_log()` ma jeden wymagany argument, ktory musi byc stringiem (`STR == 2`), i jeden opcjonalny argument, ktory, jesli podany, moze byc dowolnego typu. `max()` wymaga co najmniej jednego argumentu, ale moze przyjac dowolna liczbe powyzej tego, a pierwszy argument musi byc albo liczba calkowita, albo zmiennoprzecinkowa; typ(y) wymagane dla pozostalych argumentow nie moga zostac okreslone na podstawie tego opisu. Wreszcie, `tostr()` przyjmuje dowolna liczbe argumentow, ale nie mozna na podstawie tego opisu okreslic, jakie typy argumentow bylyby akceptowane na jakich pozycjach.

**Funkcja: `eval`**

eval -- kompilator kodu MOO przetwarza string tak, jakby mial byc programem powiazanym z jakims czasownikiem, i, jesli nie znaleziono bledow, ten fikcyjny czasownik zostaje wywolany

list `eval` (str string)

Jesli programista faktycznie nie jest programista, zglaszany jest `E_PERM`. Normalnym wynikiem wywolania `eval()` jest dwuelementowa lista. Pierwszy element jest prawdziwy, jesli nie bylo bledow kompilacji, a falszywy w przeciwnym razie. Drugi element to albo wynik zwrocony przez fikcyjny czasownik (jesli nie bylo bledow kompilacji), albo lista komunikatow bledow kompilatora (w przeciwnym razie).

Gdy fikcyjny czasownik zostaje wywolany, rozne zmienne wbudowane maja wartosci pokazane ponizej:

player    takie samo jak w wywolujacym czasowniku
this      #-1
caller    takie samo jak poczatkowa wartosc this w wywolujacym czasowniku

args      {}
argstr    ""

verb      ""
dobjstr   ""
dobj      #-1
prepstr   ""
iobjstr   ""
iobj      #-1

Fikcyjny czasownik dziala z uprawnieniami programisty i tak, jakby jego bit uprawnien `d` byl wlaczony.

```
eval("return 3 + 4;")   =>   {1, 7}
```

**Funkcja: `set_task_perms`**

set_task_perms -- zmienia uprawnienia, z jakimi dziala aktualnie wykonywany czasownik, na uprawnienia who

none `set_task_perms` (obj who)

Jesli programista nie jest ani who, ani czarodziejem, zglaszany jest `E_PERM`.
> Uwaga: to nie zmienia wlasciciela aktualnie dzialajacego czasownika, wylacznie uprawnienia tego konkretnego wywolania. Uzywa sie tego w czasownikach nalezacych do czarodziei, by sprawic, ze dzialaja z nizszymi (zwykle nieczarodziejskimi) uprawnieniami.

**Funkcja: `caller_perms`**

caller_perms -- zwraca uprawnienia uzywane przez czasownik, ktory wywolal aktualnie wykonywany czasownik

obj `caller_perms` ()

Jesli aktualnie wykonywany czasownik nie zostal wywolany przez inny czasownik (tj. jest pierwszym czasownikiem wywolanym w zadaniu polecenia lub zadaniu serwera), `caller_perms()` zwraca `#-1`.

**Funkcja: `task_perms`**

task_perms -- zwraca uprawnienia uzywane przez aktualnie wykonywane zadanie

obj `task_perms` ()

**Funkcja: `set_task_local`**

set_task_local -- Ustawia wartosc, ktora zostaje powiazana z biezacym dzialajacym zadaniem.

void `set_task_local`(ANY value)

Ta wartosc przetrwa wywolania miedzy czasownikami i zostaje zresetowana, gdy zadanie zostanie zabite, co czyni ja odpowiednia do bezpiecznego przekazywania wrazliwych danych posrednich miedzy czasownikami. Wartosc mozna nastepnie odczytac za pomoca funkcji `task_local`.

Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`.

```
set_task_local("arbitrary data")
set_task_local({"list", "of", "arbitrary", "data"})
```

**Funkcja: `task_local`**

task_local -- Zwraca wartosc powiazana z biezacym zadaniem. Wartosc ustawia sie funkcja `set_task_local`.

mixed `task_local` ()

Programista musi byc czarodziejem, w przeciwnym razie zglaszany jest `E_PERM`.

**Funkcja: `threads`**

threads -- Gdy jeden lub wiecej procesow MOO jest zawieszonych i pracuje w osobnym watku, ta funkcja zwraca liste uchwytow do tych watkow.

list `threads`()

**Funkcja: `set_thread_mode`**

int `set_thread_mode`()

none `set_thread_mode`(INT mode)

Bez podanych argumentow, set_thread_mode zwroci biezacy tryb watkowania dla czasownika. Wartosc 1 oznacza, ze watkowanie jest wlaczone dla funkcji, ktore je wspieraja. Wartosc 0 oznacza, ze watkowanie jest wylaczone i wszystkie funkcje beda wykonywane w glownym watku MOO, tak jak robily to funkcje w domyslnym LambdaMOO od wersji 1.

Jesli podasz argument, mozesz kontrolowac tryb watkowania biezacego czasownika. Tryb 1 wlaczy watkowanie, a tryb 0 je wylaczy. Ta forma nie zwraca zadnej wartosci. Mozesz wywolac te funkcje wielokrotnie, jesli chcesz wylaczyc watkowanie dla pojedynczego wywolania funkcji, a wlaczyc je dla reszty.

Kiedy nalezy wylaczyc watkowanie? Ogolnie rzecz biorac, watkowanie powinno byc wylaczone w czasownikach, w ktorych niepozadane byloby wywolanie suspend(). Kazda funkcja watkowana natychmiast zawiesi czasownik, podczas gdy watek wykonuje swoja prace. Moze to miec negatywny efekt, gdy chcesz uzyc tych funkcji w czasownikach, ktore nie moga lub nie powinny sie zawieszac, jak $sysobj:do_command lub $sysobj:do_login_command.

Zauwaz, ze tryb watkowania wplywa wylacznie na biezacy czasownik i NIE wplywa na czasowniki wywolywane z jego wnetrza.

**Funkcja: `thread_pool`**

void `thread_pool`(STR function, STR pool [, INT value])

Ta funkcja pozwala kontrolowac dowolne pule watkow utworzone przez serwer przy starcie. Nalezy jej uzywac ostroznie, poniewaz uzyta niepoprawnie moze wywolac katastrofalne skutki.

Parametr function to funkcja, ktora chcesz wykonac na puli watkow. Dostepne funkcje to:

INIT: Kontroluje inicjalizacje puli watkow.

Parametr pool kontroluje, do ktorej puli watkow chcesz zastosowac wskazana funkcje. W chwili pisania tego tekstu serwer tworzy nastepujaca pule watkow:

MAIN: Glowna pula watkow, w ktorej odbywa sie praca watkowanych funkcji wbudowanych.

Wreszcie, value to wartosc, ktora chcesz przekazac funkcji dla pool. Nastepujace funkcje akceptuja nastepujace wartosci:

INIT: Liczba watkow do utworzenia. UWAGA: przy wykonywaniu tej funkcji istniejaca pula zostanie zniszczona, a w jej miejsce utworzona nowa.

Przyklady:

```
thread_pool("INIT", "MAIN", 1)     => Zastap istniejaca glowna pule watkow nowa pula skladajaca sie z pojedynczego watku.
```

**Funkcja: `ticks_left`**

ticks_left -- zwraca liczbe tickow pozostalych biezacemu zadaniu, zanim zostanie ono przymusowo zakonczone

int `ticks_left` ()

**Funkcja: `seconds_left`**

seconds_left -- zwraca liczbe sekund pozostalych biezacemu zadaniu, zanim zostanie ono przymusowo zakonczone

int `seconds_left` ()

Sa one przydatne na przyklad przy decydowaniu, kiedy wywolac `suspend()`, by kontynuowac dlugotrwale obliczenia.

**Funkcja: `task_id`**

task_id -- zwraca niezerowy, nieujemny identyfikator calkowitoliczbowy dla aktualnie wykonywanego zadania

int `task_id` ()

Takie liczby sa losowane dla kazdego zadania i dlatego moga byc bezpiecznie uzywane w sytuacjach, gdzie wymagana jest nieprzewidywalnosc.

**Funkcja: `suspend`**

suspend -- zawiesza biezace zadanie i wznawia je po co najmniej seconds sekundach

value `suspend` ([int|float seconds])

Zawieszenie na czesc sekundy (np. 0.1) jest mozliwe. Jesli nie podano seconds, zadanie jest zawieszane na czas nieokreslony; takie zadanie moze zostac wznowione wylacznie za pomoca funkcji `resume()`.

Gdy zadanie zostaje wznowione, otrzymuje pelna pule tickow i sekund. Ta funkcja jest przydatna dla programow dzialajacych dlugo lub wymagajacych duzej liczby tickow. Jesli seconds jest ujemne, zglaszany jest `E_INVARG`. `Suspend()` zwraca zero, chyba ze zostalo wznowione przez `resume()`, w takim przypadku zwraca drugi argument podany tej funkcji.

W pewnym sensie ta funkcja forkuje "reszte" wykonywanego zadania. Jest jednak istotna roznica pomiedzy uzyciem `suspend(seconds)` a uzyciem `fork (seconds)`. Instrukcja `fork` tworzy nowe zadanie (_zadanie sforkowane_), podczas gdy aktualnie dzialajace zadanie nadal kontynuuje do zakonczenia, natomiast `suspend()` zawiesza aktualnie dzialajace zadanie (czyniac je tym samym _zadaniem zawieszonym_). Ta roznica moze zostac najlepiej wyjasniona nastepujacymi przykladami, w ktorych jeden czasownik wywoluje drugi:

```
.program   #0:caller_A
#0.prop = 1;
#0:callee_A();
#0.prop = 2;
.

.program   #0:callee_A
fork(5)
  #0.prop = 3;
endfork
.

.program   #0:caller_B
#0.prop = 1;
#0:callee_B();
#0.prop = 2;
.

.program   #0:callee_B
suspend(5);
#0.prop = 3;
.
```

Rozwaz `#0:caller_A`, ktory wywoluje `#0:callee_A`. Takie zadanie przypisze 1 do `#0.prop`, wywola `#0:callee_A`, sforkuje nowe zadanie, wroci do `#0:caller_A` i przypisze 2 do `#0.prop`, konczac to zadanie. Piec sekund pozniej, jesli sforkowane zadanie nie zostalo zabite, zacznie sie ono wykonywac; przypisze 3 do `#0.prop`, a nastepnie sie zatrzyma. Tak wiec ostateczna wartosc `#0.prop` (tj. wartosc po ponad 5 sekundach) wyniesie 3.

Rozwaz teraz `#0:caller_B`, ktory wywoluje `#0:callee_B` zamiast `#0:callee_A`. To zadanie przypisze 1 do `#0.prop`, wywola `#0:callee_B` i zawiesi sie. Piec sekund pozniej, jesli zawieszone zadanie nie zostalo zabite, zostanie ono wznowione; przypisze 3 do `#0.prop`, wroci do `#0:caller_B` i przypisze 2 do `#0.prop`, konczac zadanie. Tak wiec ostateczna wartosc `#0.prop` (tj. wartosc po ponad 5 sekundach) wyniesie 2.

Zadanie zawieszone, podobnie jak zadanie sforkowane, moze zostac opisane przez funkcje `queued_tasks()` i zabite przez funkcje `kill_task()`. Zawieszenie zadania nie zmienia jego identyfikatora zadania. Zadanie moze byc zawieszane wielokrotnie, kolejnymi wywolaniami `suspend()`.

Domyslnie nie ma limitu liczby zadan, jakie moze zawiesic dowolny gracz, ale taki limit mozna narzucic z poziomu bazy danych. Zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly.

**Funkcja: `resume`**

resume -- natychmiast konczy zawieszenie zawieszonego zadania o podanym task-id; wywolanie `suspend()` w tym zadaniu zwroci value, ktore domyslnie wynosi zero

none `resume` (int task-id [, value])

Jesli value jest typu `ERR`, zostanie ono zglaszane jako blad, a nie zwrocone, w zawieszonym zadaniu. `Resume()` zglasza `E_INVARG`, jesli task-id nie okresla istniejacego zawieszonego zadania, i `E_PERM`, jesli programista nie jest ani czarodziejem, ani wlascicielem wskazanego zadania.

**Funkcja: `yin`**

yin -- Zawiesza biezace zadanie, jesli konczy mu sie limit tickow lub sekund.

int `yin`([INT time, INT minimum ticks, INT minimum seconds] )

`yin` to skrot od "yield if needed" (wykonaj yield, jesli potrzeba).

Ma to zapewnic podobna funkcjonalnosc do czasownika suspend_if_needed z LambdaCore lub recznego okreslania czegos w rodzaju: ticks_left() < 2000 && suspend(0)

Time: Jak dlugo zawiesic zadanie. Domyslnie: 0

Minimum ticks: Minimalna liczba tickow, jaka musi pozostac zadaniu, zanim nastapi zawieszenie.

Minimum seconds: Minimalna liczba sekund, jaka musi pozostac zadaniu, zanim nastapi zawieszenie.

**Funkcja: `queue_info`**

queue_info -- jesli pominieto player, zwraca liste numerow obiektow nazywajacych wszystkich graczy, ktorzy aktualnie maja aktywne kolejki zadan wewnatrz serwera

list `queue_info` ([obj player])
map `queue_info` ([obj player])

Jesli podano player, zwraca liczbe zadan w tle aktualnie zakolejkowanych dla tego uzytkownika. Gwarantowane jest, ze `queue_info(X)` zwroci zero dla dowolnego X nieobecnego w wyniku `queue_info()`.

Jesli wywolujacy jest czarodziejem, zwrocona zostanie mapa informacji diagnostycznych o kolejkach zadan.

**Funkcja: `queued_tasks`**

queued_tasks -- zwraca informacje o kazdym z zadan w tle (tj. sforkowanych, zawieszonych lub odczytu) nalezacych do programisty (lub, jesli programista jest czarodziejem, o wszystkich zakolejkowanych zadaniach)

list|int `queued_tasks` ([INT show-runtime-or-count-only [, INT count-only]])

Zwracana wartosc to lista list, z ktorych kazda koduje pewne informacje o konkretnym zakolejkowanym zadaniu w nastepujacym formacie:

```
{task-id, start-time, x, y, programmer, verb-loc, verb-name, line, this, task-size}
```

gdzie task-id to identyfikator calkowitoliczbowy tego zakolejkowanego zadania, start-time to czas, po ktorym to zadanie zacznie sie wykonywac (w formacie time()), x i y to przestarzale wartosci, ktore nie sa juz interesujace, programmer to uprawnienia, z jakimi to zadanie zacznie sie wykonywac (a takze gracz, do ktorego to zadanie nalezy), verb-loc to obiekt, na ktorym byl w danym momencie zdefiniowany czasownik, ktory sforkowal to zadanie, verb-name to nazwa tego czasownika, line to numer pierwszej linii kodu w tym czasowniku, ktora to zadanie wykona, this to wartosc zmiennej `this` w tym czasowniku, a task-size to rozmiar zadania w bajtach. Dla zadan odczytu, start-time wynosi -1.

Pola x i y sa teraz przestarzale i sa zachowywane wylacznie ze wzgledow kompatybilnosci wstecznej. Moga zostac ponownie wykorzystane do nowych celow w jakiejs przyszlej wersji serwera.

Jesli podano dokladnie jeden argument i jest on prawdziwy, wszystkie zmienne obecne w zadaniu sa przedstawiane w mapie, gdzie kluczem jest nazwa zmiennej, a wartoscia jej wartosc. Wywolanie `queued_tasks(1)` wlacza zmienne czasu wykonania; wywolanie `queued_tasks(0)` ich nie wlacza.

Jesli podano dwa argumenty i drugi z nich jest prawdziwy, zwracana jest wylacznie liczba zadan. Jest to znaczaco wydajniejsze niz length(queued_tasks()). Zmienne czasu wykonania nie sa wlaczane, gdy podano dwa argumenty, wiec `queued_tasks(1, 0)` zwraca normalna liste zadan bez zmiennych czasu wykonania.

> Ostrzezenie: jesli aktualizujesz do ToastStunt z wersji LambdaMOO starszej niz 1.8.1, musisz zrzucic swoja baze danych, zrestartowac w trybie awaryjnym LambdaMOO i zabic wszystkie swoje queued_tasks() przed ponownym zrzuceniem bazy danych. W przeciwnym razie Twoja baza danych nie uruchomi sie w ToastStunt.

**Funkcja: `kill_task`**

kill_task -- usuwa zadanie o podanym task-id z kolejki oczekujacych zadan

none `kill_task` (int task-id)

Jesli programista nie jest wlascicielem tego zadania i nie jest czarodziejem, zglaszany jest `E_PERM`. Jesli w kolejce nie ma zadania o podanym task-id, zglaszany jest `E_INVARG`.

**Funkcja: `finished_tasks`**

finished_tasks -- zwraca liste ostatnich X zadan, ktore zakonczyly wykonanie, wliczajac ich calkowity czas wykonania

list `finished_tasks`()

Gdy wlaczone (przez `SAVE_FINISHED_TASKS` w options.h), serwer bedzie sledzil czas wykonania kazdego zadania przechodzacego przez interpreter. Funkcja wbudowana `finished_tasks()` jest rejestrowana wylacznie w kompilacjach z wlaczonym `SAVE_FINISHED_TASKS`. Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`. Te dane sa nastepnie udostepniane bazie danych na dwa sposoby.

Pierwszym jest funkcja finished_tasks(). Ta funkcja zwroci liste map ostatnich kilku zakonczonych zadan (konfigurowalna przez $server_options.finished_tasks_limit) z nastepujacymi informacjami:

| Wartosc | Opis |
| --- | --- |
| foreground | 1, jesli zadanie bylo zadaniem pierwszoplanowym, 0, jesli bylo zadaniem w tle |
| fullverb | pelna nazwa czasownika, wliczajac aliasy |
| object | obiekt definiujacy czasownik |
| player | gracz, ktory zainicjowal zadanie |
| programmer | programista bedacy wlascicielem czasownika |
| receiver | zwykle takie samo jak 'this', ale w przypadku wartosci prymitywnych moze byc uchwytem (handlerem) |
| suspended | czy zadanie bylo zawieszone, czy nie |
| this | faktyczny obiekt, na ktorym wywolano czasownik |
| time | calkowity czas, jaki zajelo wykonanie czasownika wewnatrz interpretera |
| verb | nazwa wywolania czasownika lub wpisanego polecenia |

Drugim sposobem jest czasownik $handle_lagging_task. Gdy przekroczony zostanie prog wykonania zdefiniowany w $server_options.task_lag_threshold, serwer zapisze wpis do pliku logu i wywola czasownik $handle_lagging_task ze stosem wywolan zadania oraz czasem wykonania.

> Uwaga: ta funkcja wbudowana musi zostac wlaczona w options.h, by moc jej uzywac.

**Funkcja: `callers`**

callers -- zwraca informacje o kazdym z czasownikow i funkcji wbudowanych aktualnie oczekujacych na wznowienie wykonania w biezacym zadaniu

list `callers` ([include-line-numbers])

Gdy jeden czasownik lub funkcja wywoluje inny czasownik lub funkcje, wykonanie wywolujacego jest tymczasowo zawieszone, w oczekiwaniu na zwrocenie wartosci przez wywolywany czasownik lub funkcje. W danym momencie moze byc kilka takich oczekujacych czasownikow i funkcji: ten, ktory wywolal aktualnie wykonywany czasownik, czasownik lub funkcja, ktora wywolala tamten, i tak dalej. Wynikiem `callers()` jest lista, ktorej kazdy element podaje informacje o jednym oczekujacym czasowniku lub funkcji w nastepujacym formacie:

```
{this, verb-name, programmer, verb-loc, player, line-number}
```

Dla czasownikow, this to poczatkowa wartosc zmiennej `this` w tym czasowniku, verb-name to nazwa uzyta do wywolania tego czasownika, programmer to gracz, z ktorego uprawnieniami dziala ten czasownik, verb-loc to obiekt, na ktorym zdefiniowano ten czasownik, player to poczatkowa wartosc zmiennej `player` w tym czasowniku, a line-number wskazuje, ktora linia kodu czasownika jest wykonywana. Element line-number jest wlaczany wylacznie, jesli podano argument include-line-numbers i jest on prawdziwy.

Dla funkcji, this, programmer i verb-loc sa wszystkie rowne `#-1`, verb-name to nazwa funkcji, a line-number to indeks uzywany wewnetrznie do okreslenia biezacego stanu funkcji wbudowanej. Najprostszym poprawnym testem na wpis funkcji wbudowanej jest

```
(VERB-LOC == #-1  &&  PROGRAMMER == #-1  &&  VERB-name != "")
```

Pierwszy element listy zwracanej przez `callers()` podaje informacje o czasowniku, ktory wywolal aktualnie wykonywany czasownik, drugi element opisuje czasownik, ktory wywolal tamten, i tak dalej. Ostatni element listy opisuje pierwszy czasownik wywolany w tym zadaniu.

**Funkcja: `task_stack`**

task_stack -- zwraca informacje podobne do tych zwracanych przez funkcje `callers()`, ale dla zawieszonego zadania o podanym task-id; argument include-line-numbers ma takie samo znaczenie, jak w `callers()`

list `task_stack` (int task-id [, INT include-line-numbers [, INT include-variables]])

Zglasza `E_INVARG`, jesli task-id nie okresla istniejacego zawieszonego zadania, i `E_PERM`, jesli programista nie jest ani czarodziejem, ani wlascicielem wskazanego zadania.

Jesli podano include-line-numbers i jest ono prawdziwe, wlaczone zostana numery linii.

Jesli podano include-variables i jest ono prawdziwe, do kazdej ramki podanego zadania wlaczone zostana zmienne.

##### Operacje administracyjne

**Funkcja: `server_version`**

server_version -- zwraca informacje o wersji dzialajacego serwera MOO

str `server_version` ()

list `server_version` (value details)

value `server_version` (str detail-path)

Bez argumentow zwraca zwykly string wersji serwera. Z argumentem niebedacym stringiem lub pustym stringiem zwraca pelna szczegolowa liste wersji, wliczajac numer wersji, ustawienia z czasu kompilacji i informacje o zrodlach; na przyklad `server_version(1)` zwraca pelna szczegolowa liste. Z niepustym argumentem-stringiem zwraca pasujacy wpis detail-path (rozdzielany ukosnikami) z tej listy wersji. Jesli zadana sciezka szczegolow nie istnieje, zglaszany jest `E_INVARG`.

**Funkcja: `load_server_options`**

load_server_options -- Powoduje, ze serwer sprawdza biezace wartosci wlasciwosci na $server_options, aktualizujac odpowiadajace im ustawienia opcji serwera

none `load_server_options` ()

Wiecej informacji znajdziesz w sekcji o opcjach serwera ustawianych z poziomu bazy danych. Jesli programista nie jest czarodziejem, zglaszany jest E_PERM.

**Funkcja: `server_log`**

server_log -- Tekst w message jest wysylany do logu serwera z charakterystycznym prefiksem (by mozna go bylo odroznic od komunikatow generowanych przez sam serwer)

none server_log (str message [, int level])

Jesli programista nie jest czarodziejem, zglaszany jest E_PERM.

Jesli podano level i jest to liczba calkowita z zakresu od 0 do 7 wlacznie, message jest oznaczane w logu serwera jako jeden z osmiu predefiniowanych typow, od zwyklego komunikatu logu po komunikat bledu. W przeciwnym razie, jesli podano level i jest ono prawdziwe, message jest oznaczane w logu serwera jako blad.

**Funkcja: `renumber`**

renumber -- numer obiektu aktualnie ponumerowanego jako object zostaje zmieniony na najmniejszy nieujemny numer obiektu aktualnie nieuzywany, a nowy numer obiektu zostaje zwrocony

obj `renumber` (obj object)

Jesli object jest niepoprawne, zglaszany jest `E_INVARG`. Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`. Jesli nie ma nieuzywanych nieujemnych numerow obiektow mniejszych niz object, zwracane jest object i zadne zmiany nie zachodza.

Odniesienia do object w hierarchiach rodzic/dzieci oraz lokalizacja/zawartosc zostaja zaktualizowane, by uzywac nowego numeru obiektu, a wszelkie czasowniki, wlasciwosci i/lub obiekty nalezace do object rowniez zostaja zmienione, by nalezec do nowego numeru obiektu. Ta ostatnia operacja moze byc dosc czasochlonna, jesli baza danych jest duza. Nie sa wykonywane zadne inne zmiany w bazie danych; w szczegolnosci nie sa aktualizowane zadne odniesienia do obiektow w wartosciach wlasciwosci ani w kodzie czasownikow.

Ta operacja jest przeznaczona do uzytku przy tworzeniu nowych wersji bazy danych ToastCore z owczesnej biezacej bazy danych ToastStunt oraz w innych podobnych sytuacjach. Jej uzycie wymaga wielkiej ostroznosci.

**Funkcja: `reset_max_object`**

reset_max_object -- wyobrazenie serwera o najwyzszym kiedykolwiek uzytym numerze obiektu zostaje zmienione na najwyzszy numer obiektu aktualnie istniejacego obiektu, co pozwala na ponowne uzycie dowolnych wyzszych numerow odnoszacych sie teraz do zrecyklingowanych obiektow

none `reset_max_object` ()

Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`.

Ta operacja jest przeznaczona do uzytku przy tworzeniu nowych wersji bazy danych ToastCore z owczesnej biezacej bazy danych ToastStunt oraz w innych podobnych sytuacjach. Jej uzycie wymaga wielkiej ostroznosci.

**Funkcja: `memory_usage`**

memory_usage -- Zwraca statystyki dotyczace zuzycia pamieci systemowej przez serwer.

list `memory_usage` ()

Wynikiem jest lista w nastepujacym formacie:

{calkowita uzyta pamiec, rozmiar zestawu rezydentnego, strony wspoldzielone, segment kodu, dane + stos}

**Funkcja: `malloc_stats`**

malloc_stats -- Zwraca statystyki alokatora, gdy ToastStunt zbudowano ze wsparciem dla jemalloc.

list `malloc_stats` ()

Ta funkcja jest dostepna wylacznie, gdy ToastStunt zbudowano z jemalloc. Zwrocona lista ma postac `{allocated, active, resident, metadata, mapped, allocated-large, active-large}`.

**Funkcja: `usage`**

usage -- Zwraca statystyki dotyczace serwera, na ktorym dziala MOO.

list `usage` ()

Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`.

Wynikiem jest lista w nastepujacym formacie:

```
{{srednie obciazenie}, czas uzytkownika, czas systemu, odzyskania stron, bledy stron, operacje wejscia blokowego, operacje wyjscia blokowego, dobrowolne przelaczenia kontekstu, niedobrowolne przelaczenia kontekstu, odebrane sygnaly}
```

**Funkcja: `run_gc`**

run_gc -- Zada wykonania przebiegu garbage collection.

none `run_gc` ()

Ta funkcja jest dostepna wylacznie, gdy ToastStunt zbudowano z wlaczonym garbage collection. Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`.

**Funkcja: `gc_stats`**

gc_stats -- Zwraca liczniki kolorow garbage collectora.

map `gc_stats` ()

Ta funkcja jest dostepna wylacznie, gdy ToastStunt zbudowano z wlaczonym garbage collection. Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`. Zwrocona mapa zawiera klucze "green", "yellow", "black", "gray", "white", "purple" i "pink".

**Funkcja: `dump_database`**

dump_database -- zada, by serwer wykonal checkpoint bazy danych przy najblizszej okazji

none `dump_database` ()

Zwykle wywolywanie tej funkcji nie jest konieczne; serwer automatycznie wykonuje checkpointy bazy danych w regularnych odstepach; zobacz rozdzial o zalozeniach serwera wobec bazy danych po szczegoly. Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`.

**Funkcja: `db_disk_size`**

db_disk_size -- zwraca calkowity rozmiar, w bajtach, najnowszej pelnej reprezentacji bazy danych jako jednego lub wiecej plikow dyskowych

int `db_disk_size` ()

Zglasza `E_QUOTA`, jesli z jakiegos powodu taka reprezentacja na dysku aktualnie nie jest dostepna.

**Funkcja: `exec`**

exec -- Asynchronicznie wykonuje podany zewnetrzny plik wykonywalny, opcjonalnie wysylajac dane wejsciowe.

list `exec` (LIST command [, STR input] [, LIST environment variables])

Zwraca kod powrotu procesu, wyjscie i blad. Jesli programista nie jest czarodziejem, zglaszany jest E_PERM.

Pierwszy argument musi byc lista stringow, w przeciwnym razie zglaszany jest E_INVARG. Pierwszy string to sciezka do pliku wykonywalnego i jest wymagany. Reszta to argumenty linii polecen przekazywane plikowi wykonywalnemu.

Sciezka do pliku wykonywalnego nie moze zaczynac sie od ukosnika (/) ani kropka-kropka (..), i nie moze zawierac ukosnik-kropka (/.) ani kropka-ukosnik (./), w przeciwnym razie zglaszany jest E_INVARG. Jesli wskazany plik wykonywalny nie istnieje lub nie jest zwyklym plikiem, zglaszany jest E_INVARG.

Jesli podano string input, jest on zapisywany na standardowe wejscie wykonywanego procesu.

Dodatkowo mozesz podac liste zmiennych srodowiskowych do ustawienia w powloce.

Gdy proces sie zakonczy, zwraca liste w postaci:

```
{code, output, error}
```

code to calkowitoliczbowy status wyjscia lub kod powrotu procesu. output i error to stringi danych zapisanych na standardowe wyjscie i standardowe wyjscie bledow procesu.

Podane polecenie jest wykonywane asynchronicznie. Funkcja zawiesza biezace zadanie i pozwala innym zadaniom dzialac, dopoki polecenie sie nie zakonczy. Zadania zawieszone w ten sposob moga zostac zabite przez kill_task().

Stringi input, output i error sa wszystkie stringami binarnymi MOO.

Wszystkie zewnetrzne pliki wykonywalne musza znajdowac sie w katalogu executables.

```
exec({"cat", "-?"})          =>   {1, "", "cat: illegal option -- ?~0Ausage: cat [-benstuv] [file ...]~0A"}
exec({"cat"}, "foo")         =>   {0, "foo", ""}
exec({"echo", "one", "two"}) =>   {0, "one two~0A", ""}
```

Na przyklad, jesli `vars.sh` w katalogu executables zawiera:

```
#!/bin/bash
echo "pizza = ${pizza}"
```

to zmienne srodowiskowe mozna podac trzecim argumentem:

```
exec({"vars.sh"}, "", {"pizza=tasty"}) => {0, "pizza = tasty~0A", ""}
exec({"vars.sh"})                      => {0, "pizza = ~0A", ""}
```

**Funkcja: `shutdown`**

shutdown -- zada, by serwer wylaczyl sie przy najblizszej okazji

none `shutdown` ([str message [, any unclean_shutdown]])

Zanim to zrobi, wszystkim polaczonym graczom wypisywane jest powiadomienie (wlaczajace message, jesli podano). Jesli programista nie jest czarodziejem, zglaszany jest `E_PERM`.

Jesli unclean_shutdown jest falszywe lub nie podano go, serwer wykonuje normalne, czyste wylaczenie i zapisuje baze danych jak zwykle.

Jesli unclean_shutdown jest prawdziwe, serwer wykonuje nieczyste wylaczenie, nasladujac zachowanie bledu krytycznego. Baza danych nie jest zrzucana do normalnego wyjsciowego pliku bazy danych; zamiast tego tworzony jest plik bazy danych paniki (panic). Komunikat wylaczenia jest tez zapisywany do logu serwera.

**Funkcja: `verb_cache_stats`**

**Funkcja: `log_cache_stats`**

list verb_cache_stats ()

none log_cache_stats ()

Serwer buforuje wyszukiwania nazwa-czasownika-na-program, by poprawic wydajnosc. Te funkcje odpowiednio zwracaja lub zapisuja do pliku logu serwera biezace statystyki cache'a. Dla verb_cache_stats zwracana wartosc bedzie lista w postaci

```
{hits, negative_hits, misses, table_clears, histogram},
```

choc moze sie to zmienic w przyszlych wydaniach serwera. Cache jest uniewazniany przez dowolne wywolanie funkcji wbudowanej, ktore moze wplynac na wyszukiwania czasownikow (np. delete_verb()).

### Polecenia serwera i zalozenia bazy danych

Ten rozdzial opisuje wszystkie polecenia wbudowane w serwer oraz kazda wlasciwosc i czasownik w bazie danych, do ktorych serwer odwoluje sie w sposob szczegolny. Poza tym, co zostalo tu wymienione, serwer nie czyni zadnych zalozen co do zawartosci bazy danych.

#### Linie polecen otrzymujace specjalne traktowanie

Jak wspomniano w rozdziale o parsowaniu polecen, istnieje szereg polecen i specjalnych prefiksow, ktorych interpretacja jest ustalona przez serwer. Przyklady to polecenie flush oraz piec wewnetrznych (intrinsic) polecen (PREFIX, OUTPUTPREFIX, SUFFIX, OUTPUTSUFFIX i .program).

Ta sekcja omawia wszystkie te wbudowane elementy procesu interpretacji polecen, w kolejnosci, w jakiej wystepuja.

##### Czyszczenie nieprzetworzonego wejscia

Czasem zdarza sie, ze uzytkownik zmienia zdanie co do jednej lub wiecej wpisanych linii wejscia i chcialby je "cofnac", zanim serwer faktycznie zabierze sie za ich przetwarzanie. Jesli zareaguje wystarczajaco szybko, moze wpisac zdefiniowane dla swojego polaczenia polecenie flush; gdy serwer po raz pierwszy odczyta to polecenie z sieci, natychmiast i calkowicie czysci wszelkie jeszcze nieprzetworzone wejscie od tego uzytkownika, wypisujac uzytkownikowi komunikat opisujacy dokladnie, ktore linie wejscia zostaly odrzucone, jesli byly jakies.

> Subtelny szczegol: polecenie flush jest obslugiwane bardzo wczesnie w procesie przetwarzania linii wejscia przez serwer, zanim linia zostanie wprowadzona do kolejki zadan dla polaczenia i na dlugo przed sparsowaniem jej na slowa, tak jak inne polecenia. Z tego powodu musi zostac wpisane dokladnie tak, jak zostalo zdefiniowane, samodzielnie w linii, bez cudzyslowow i bez zadnych spacji przed ani po nim.

Gdy polaczenie zostaje po raz pierwszy zaakceptowane przez serwer, otrzymuje poczatkowe ustawienie polecenia flush, pobrane z biezacej wartosci domyslnej. To poczatkowe ustawienie mozna pozniej zmienic za pomoca funkcji set_connection_option().

Domyslnie kazde polaczenie otrzymuje poczatkowo `.flush` jako swoje polecenie flush. Jesli istnieje wlasciwosc $server_options.default_flush_command, jej wartosc nadpisuje ta wartosc domyslna. Jesli $server_options.default_flush_command jest niepustym stringiem, ten string staje sie poleceniem flush dla wszystkich nowych polaczen; w przeciwnym razie nowe polaczenia poczatkowo w ogole nie otrzymuja polecenia flush.

##### Przetwarzanie poza pasmem

Mozliwe jest skompilowanie serwera tak, by rozpoznawal prefiks poza pasmem oraz prefiks cytowania poza pasmem dla linii wejscia. Sa to stringi, ktorych obecnosci na poczatku kazdej niewyczyszczonej linii wejscia z polaczenia niebinarnego serwer bedzie sprawdzal, niezaleznie od tego, czy gracz jest zalogowany, i niezaleznie od tego, czy jakies zadania odczytu oczekuja na wejscie na tym polaczeniu.

To sprawdzanie mozna calkowicie wylaczyc, ustawiajac opcje polaczenia "disable-oob"; w takim przypadku nic z reszty tej sekcji nie ma zastosowania, tj. wszystkie kolejne niewyczyszczone linie na tym polaczeniu beda dostepne bez zmian dla zadan odczytu lub normalnego parsowania polecen.

##### Linie cytowane

Najpierw opiszemy, jak zapewnic, ze dana linia wejscia nie zostanie przetworzona jako polecenie poza pasmem.

Jesli dana linia wejscia zaczyna sie od zdefiniowanego prefiksu cytowania poza pasmem (domyslnie `#$"`), ten prefiks zostaje usuniety. Wynikowa linia jest wtedy dostepna dla zadan odczytu lub normalnego parsowania polecen w zwykly sposob, nawet jesli ta wynikowa linia zaczyna sie teraz od prefiksu poza pasmem lub prefiksu cytowania poza pasmem.

Na przyklad, jesli gracz wpisze

```
#$"#$#mcp-client-set-type fancy
```

serwer zachowa sie dokladnie tak, jakby opcja polaczenia "disable-oob" byla ustawiona na prawde, a gracz wpisal zamiast tego

```
#$#mcp-client-set-type fancy
```

##### Polecenia

Jesli dana linia wejscia zaczyna sie od zdefiniowanego prefiksu poza pasmem (domyslnie `#$#`), nie jest traktowana jako normalne polecenie ani przekazywana jako wejscie zadnemu zadaniu odczytu. Zamiast tego linia jest parsowana na liste slow w zwykly sposob, a te slowa sa przekazywane jako argumenty w wywolaniu $do_out_of_band_command().

Jesli ten czasownik nie istnieje lub nie jest wykonywalny, dana linia zostanie calkowicie zignorowana.

Na przyklad, przy domyslnym prefiksie poza pasmem, linia wejscia

```
#$#mcp-client-set-type fancy
```

skutkowalaby nastepujacym wywolaniem wykonanym w nowym zadaniu serwera:

```
$do_out_of_band_command("#$#mcp-client-set-type", "fancy")
```

Podczas wywolania $do_out_of_band_command() zmienna player jest ustawiona na numer obiektu reprezentujacy gracza powiazanego z polaczeniem, z ktorego pochodzi linia wejscia. Oczywiscie, jesli to polaczenie nie jest jeszcze zalogowane, numer obiektu bedzie ujemny. Ponadto zmienna argstr bedzie miala jako swoja wartosc niesparsowana linie wejscia, tak jak zostala odebrana na polaczeniu sieciowym.

Polecenia poza pasmem sa przeznaczone do uzytku przez zaawansowane programy-klienty, ktore moga generowac zdarzenia asynchroniczne, o ktorych serwer musi zostac powiadomiony. Poniewaz klient generalnie nie moze znac stanu polaczenia gracza (zalogowany czy nie, zadanie odczytu czy nie), polecenia poza pasmem stanowia jedyny niezawodny kanal komunikacji klient-serwer.

Polecenia [Telnet IAC](http://www.faqs.org/rfcs/rfc854.html) rowniez zostana przechwycone i przekazane, jako stringi binarne, do czasownika `do_out_of_band_command` na obiekcie nasluchujacym.

##### Ograniczniki wyjscia polecenia

> Ostrzezenie: to funkcja przestarzala (deprecated)

Kazde polaczenie sieciowe MOO ma powiazane z soba dwa stringi: `prefiks wyjscia` i `sufiks wyjscia`. Tuz przed wykonaniem polecenia wpisanego na tym polaczeniu, serwer wypisuje graczowi prefiks wyjscia, jesli jest zdefiniowany. Podobnie, tuz po zakonczeniu polecenia, graczowi wypisywany jest sufiks wyjscia, jesli jest zdefiniowany. Poczatkowo te stringi nie sa zdefiniowane, wiec nie zachodzi zadne dodatkowe wypisywanie.

Polecenia `PREFIX` i `SUFFIX` sluza do ustawiania i czyszczenia tych stringow. Maja nastepujaca prosta skladnie:

```
PREFIX  output-prefix
SUFFIX  output-suffix
```

To znaczy, ze caly tekst po nazwie polecenia i wszelkich nastepujacych po niej spacjach jest uzywany jako nowa wartosc odpowiedniego stringa. Jesli po stringu polecenia nie ma zadnego niepustego tekstu, odpowiadajacy string zostaje wyczyszczony. Dla kompatybilnosci z niektorymi ogolnymi programami-klientami MUD, serwer rozpoznaje tez `OUTPUTPREFIX` jako synonim `PREFIX` i `OUTPUTSUFFIX` jako synonim `SUFFIX`.

Te polecenia sa przeznaczone do uzytku przez programy polaczone z MOO, tak by mogly wydawac polecenia MOO i niezawodnie okreslac poczatek i koniec wynikowego wyjscia. Na przyklad, pewien program-klient oparty na edytorze wysyla od czasu do czasu nastepujaca sekwencje polecen:

```
PREFIX >>MOO-Prefix<<
SUFFIX >>MOO-Suffix<<
@list object:verb without numbers
PREFIX
SUFFIX
```

Efektem tego, w bazie danych pochodzacej od ToastCore, jest wypisanie kodu nazwanego czasownika, poprzedzonego linia zawierajaca wylacznie `>>MOO-Prefix<<` i zakonczonego linia zawierajaca wylacznie `>>MOO-Suffix<<`. Pozwala to edytorowi niezawodnie wyodrebnic tekst programu z wyjscia MOO i pokazac go uzytkownikowi w osobnym oknie edytora. Istnieje wiele innych mozliwych zastosowan.

> Ostrzezenie: jesli tak oskrzydlone polecenie wywoluje suspend(), jego wyjscie zostanie uznane za "zakonczone" wlasnie w tym momencie; sufiks pojawia sie wiec w tym punkcie, a nie, jak mozna by oczekiwac, pozniej, gdy wynikowe zadanie w tle w koncu zwroci wynik ze swojego wywolania czasownika najwyzszego poziomu. Dlatego uzycie tej funkcji (ktora zostala zaprojektowana, zanim istnialo suspend()) nie jest juz zalecane.

Funkcja wbudowana `output_delimiters()` moze byc uzyta przez kod MOO, by dowiedziec sie, jaki prefiks i sufiks wyjscia sa aktualnie w mocy dla danego polaczenia sieciowego.

#### Polecenie .program

Polecenie `.program` to popularny sposob, w jaki programisci wiaza konkretny program w kodzie MOO z konkretnym czasownikiem. Ma nastepujaca skladnie:

```
.program object:verb
...kilka linii kodu MOO...
.
```

To znaczy, ze po wpisaniu polecenia `.program` wszystkie kolejne linie wejscia od gracza sa uznawane za czesc definiowanego programu MOO. Konczy sie to, gdy tylko gracz wpisze linie zawierajaca wylacznie kropke (`.`). Gdy ta linia zostanie odebrana, zgromadzony program MOO jest sprawdzany pod katem poprawnej skladni MOO i, jesli jest poprawny, wiazany z nazwanym czasownikiem.

Jesli w momencie przetwarzania linii zawierajacej wylacznie kropke (a) gracz nie jest programista, (b) gracz nie ma uprawnien zapisu do nazwanego czasownika, lub (c) wlasciwosc `$server_options.protect_set_verb_code` istnieje i ma wartosc prawdziwa, a gracz nie jest czarodziejem, wtedy wypisywany jest komunikat bledu, a program nazwanego czasownika nie zostaje zmieniony.

W poleceniu `.program`, object moze miec jedna z trzech form:

* Nazwe jakiegos obiektu widocznego dla gracza. Jest to dokladnie taki rodzaj dopasowania, jaki serwer wykonuje dla dopelnien blizszych i dalszych zwyklych polecen. Zobacz rozdzial o parsowaniu polecen po szczegoly. Zauwaz, ze mozna uzyc specjalnych nazw `me` i `here`.
* Numer obiektu, w postaci `#number`.
* _Wlasciwosc systemowa_ (tj. wlasciwosc na `#0`), w postaci `$name`. W tym przypadku biezaca wartosc `#0.name` musi byc prawidlowym obiektem.

#### Poczatkowa interpunkcja w poleceniach

Serwer w specjalny sposob interpretuje linie polecen zaczynajace sie od ktoregokolwiek z nastepujacych znakow:

```
"        :        ;
```

Zanim polecenie zostanie przetworzone, poczatkowy znak interpunkcyjny jest zastepowany odpowiadajacym mu ponizej slowem, po ktorym nastepuje spacja:

```
say      emote    eval
```

Na przyklad linia polecenia

```
"Hello, there.
```

zostaje przeksztalcona w

```
say Hello, there.
```

przed parsowaniem.

### Zalozenia serwera wobec bazy danych

Istnieje niewielka liczba okolicznosci, w ktorych serwer bezposrednio i w konkretny sposob odwoluje sie do okreslonego czasownika lub wlasciwosci w bazie danych. Ta sekcja podaje pelna liste takich okolicznosci.

#### Opcje serwera ustawiane z poziomu bazy danych

Wiele opcjonalnych zachowan serwera mozna kontrolowac z poziomu bazy danych, tworzac wlasciwosc `#0.server_options` (znana tez jako `$server_options`), przypisujac jej jako wartosc prawidlowy numer obiektu, a nastepnie definiujac rozne wlasciwosci na tym obiekcie. Wielokrotnie serwer sprawdza, czy wlasciwosc `$server_options` istnieje i ma jako wartosc numer obiektu. Jesli tak, serwer szuka na tym obiekcie `$server_options` rozmaitych innych wlasciwosci i, jesli istnieja, uzywa ich wartosci do kontrolowania sposobu dzialania serwera.

Kazda z konkretnych poszukiwanych wlasciwosci jest opisana w odpowiedniej sekcji ponizej, ale oto krotka lista wszystkich odpowiednich wlasciwosci dla latwiejszego odniesienia:

| Wlasciwosc | Opis |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| bg_seconds                       | Liczba sekund przydzielanych zadaniom w tle.                                                                                                        |
| bg_ticks                         | Liczba tickow przydzielanych zadaniom w tle.                                                                                                          |
| connect_timeout                  | Maksymalna liczba sekund, przez jaka niezalogowane polaczenie przychodzace moze pozostac otwarte.                                                                 |
| default_flush_command            | Poczatkowe ustawienie polecenia flush kazdego nowego polaczenia.                                                                                           |
| fg_seconds                       | Liczba sekund przydzielanych zadaniom pierwszoplanowym.                                                                                                        |
| fg_ticks                         | Liczba tickow przydzielanych zadaniom pierwszoplanowym.                                                                                                          |
| max_stack_depth                  | Maksymalna liczba poziomow zagniezdzonych wywolan czasownikow. Uzywane wylacznie, jesli jest wyzsza niz domyslna                                                                  |
| outbound_connect_timeout         | Maksymalna liczba sekund oczekiwania na pomyslne otwarcie wychodzacego polaczenia sieciowego.                                                             |
| protect_`property`               | Ogranicza odczyt/zapis wbudowanej wlasciwosci `property` wylacznie do czarodziei.                                                                                                                |
| protect_`function`               | Ogranicza uzycie wbudowanej funkcji `function` wylacznie do czarodziei.                                                                                                                            |
| queued_task_limit                | Maksymalna liczba sforkowanych lub zawieszonych zadan, jakie dowolny gracz moze miec zakolejkowane w danym momencie.                                                                |
| support_numeric_verbname_strings | Wlacza uzycie przestarzalego mechanizmu nazywania czasownikow.                                                                                                          |
| max_queued_output                | Maksymalna liczba znakow wyjscia, jaka serwer jest gotow buforowac dla danego polaczenia sieciowego, zanim zacznie odrzucac stare wyjscie, by zrobic miejsce na nowe. |
| dump_interval                    | Liczba calkowita w sekundach okreslajaca, jak czesto wykonywac checkpoint bazy danych.                                                                                                                |
| proxy_rewrite (usunieta w 2.7.2) | Dawniej kontrolowala, czy adresy IP z proxy byly przepisywane. Przepisywanie proxy nie jest juz domyslnie wlaczone. |
| trusted_proxies                  | Lista zaufanych stringow adresow IP proxy. Kazdy laczacy sie adres IP znaleziony na tej liscie bedzie mial pominiety ekran logowania i bedzie akceptowal przekazywane adresy IP przez protokol HAProxy Proxy protocol, po czym zostanie wypisany ekran powitalny. Ta wlasciwosc moze byc zdefiniowana na `$server_options` lub na samym obiekcie nasluchujacym. By przywrocic dawne zachowanie proxy dla localhost, ustaw `$server_options.trusted_proxies` na `{"127.0.0.1", "::1"}`. |
| file_io_max_files                | Pozwala na zmienialne z poziomu bazy danych limity tego, ile plikow moze byc otwartych naraz.                                                                                                        |
| sqlite_max_handles               | Pozwala na zmienialne z poziomu bazy danych limity tego, ile polaczen SQLite moze byc otwartych naraz.                                                                           |
| task_lag_threshold               | Nadpisuje domyslny task_lag_threshold do obslugi lagujacych zadan.                                                                                                             |
| finished_tasks_limit             | Nadpisuje domyslny finished_tasks_limit (wlacza funkcje finished_tasks i okresla, ile zadan jest domyslnie zapisywanych).                                 |
| no_name_lookup                   | Nadpisuje domyslny no_name_lookup (wylacza automatyczne rozwiazywanie nazw DNS na nowych polaczeniach).                                                |
| max_list_value_bytes             | Ogranicza rozmiar, w bajtach, list konstruowanych przez uzytkownika.                                                                                                        |
| max_string_concat                | Ogranicza rozmiar stringow konstruowanych przez uzytkownika.                                                                                                 |
| max_concat_catchable | Okresla, czy przekroczenie limitow rozmiaru konkatenacji powoduje blad braku sekund (out-of-seconds) czy E_QUOTA. |
| include_rt_vars                  | Gdy wlaczone, dolacza dane zmiennych czasu wykonania do tracebackow.                                                                                                   |

> Uwaga: jesli nadpisujesz wartosc domyslna zdefiniowana w options.h (taka jak no_name_lookup lub finished_tasks_limit i wiele innych), musisz wywolac `load_server_options()`, by Twoje zmiany zaczely obowiazywac.

> Uwaga: czasowniki zdefiniowane na #0 nie podlegaja juz sprawdzaniu uprawnien wylacznie-dla-czarodziei dla funkcji wbudowanych, generowanemu przez zdefiniowanie $server_options.protect_FOO z wartoscia prawdziwa. Dzieki temu mozesz teraz napisac "wrapper" dla funkcji wbudowanej bez koniecznosci ponownego implementowania wszystkich wbudowanych sprawdzen uprawnien serwera dla tej funkcji.

> Uwaga: jesli funkcja wbudowana FOO zostala uczyniona wylacznie-dla-czarodziei (przez zdefiniowanie $server_options.protect_FOO z wartoscia prawdziwa), a wywolanie tej funkcji nastepuje z nieczarodziejskiego czasownika niezdefiniowanego na #0 (tj. gdy serwer wlasnie ma zglosic E_PERM), serwer najpierw sprawdza, czy istnieje czasownik #0:bf_FOO. Jesli tak, wywoluje go zamiast zglaszac E_PERM i zwraca lub zglasza to, co ten czasownik zwroci lub zglosi.

> Uwaga: options.h domyslnie definiuje IGNORE_PROP_PROTECTED (#define). Jesli jest zdefiniowane, serwer ignoruje wszelkie proby ochrony wlasciwosci wbudowanych (takich jak $server_options.protect_location). Ochrona wlasciwosci jest znaczacym obciazeniem wydajnosci, a wiekszosc MOO nie korzysta z tej funkcjonalnosci.

#### Komunikaty serwera ustawiane z poziomu bazy danych

Istnieje szereg okolicznosci, w ktorych sam serwer generuje komunikaty na polaczeniach sieciowych. Wiekszosc z nich mozna dostosowac lub nawet wyeliminowac z poziomu bazy danych. W kazdym takim przypadku, w momencie, gdy komunikat mialby zostac wypisany, sprawdzana jest wlasciwosc na `$server_options`. Jesli wlasciwosc nie istnieje, wypisywany jest komunikat domyslny. Jesli wlasciwosc istnieje, a jej wartosc nie jest stringiem ani lista zawierajaca stringi, wtedy w ogole nie jest wypisywany zaden komunikat. W przeciwnym razie, string(i) sa wypisywane w miejsce domyslnego komunikatu, po jednym stringu na linie. Zaden z tych komunikatow nigdy nie jest wypisywany na wychodzacym polaczeniu sieciowym utworzonym przez funkcje `open_network_connection()`.

Nastepujaca lista obejmuje wszystkie konfigurowalne komunikaty, pokazujac dla kazdego z nich nazwe odpowiedniej wlasciwosci na `$server_options`, domyslny komunikat oraz okolicznosci, w ktorych ten komunikat jest wypisywany:

| Domyslny komunikat                                                                                                                   | Opis                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| boot_msg = &quot;*** Disconnected ***&quot;                                                                                       | Wywolano funkcje boot_player() na tym polaczeniu.                                                                                             |
| connect_msg = &quot;*** Connected ***&quot;                                                                                       | Obiekt uzytkownika, ktory wlasnie zalogowal sie na tym polaczeniu, istnial przed wywolaniem $do_login_command().                                                 |
| create_msg = &quot;*** Created ***&quot;                                                                                          | Obiekt uzytkownika, ktory wlasnie zalogowal sie na tym polaczeniu, nie istnial przed wywolaniem $do_login_command().                                           |
| recycle_msg = &quot;*** Recycled ***&quot;                                                                                        | Zalogowany uzytkownik tego polaczenia zostal zrecyklingowany lub przenumerowany (przez funkcje renumber()).                                                  |
| redirect_from_msg = &quot;*** Redirecting connection to new port ***&quot;                                                        | Zalogowany uzytkownik tego polaczenia wlasnie zalogowal sie na innym polaczeniu.                                                                    |
| redirect_to_msg = &quot;*** Redirecting old connection to this port ***&quot;                                                     | Uzytkownik, ktory wlasnie zalogowal sie na tym polaczeniu, byl juz zalogowany na innym polaczeniu.                                                        |
| server_full_msg Domyslnie:  *** Sorry, but the server cannot accept any more connections right now.<br> *** Please try again later. | To polaczenie przybylo w momencie, gdy serwer faktycznie nie mogl przyjac wiecej polaczen z powodu wyczerpania krytycznego zasobu systemu operacyjnego. |
| timeout_msg = &quot;*** Timed-out waiting for login. ***&quot; | To przychodzace polaczenie sieciowe bylo bezczynne i niezalogowane przez co najmniej CONNECT_TIMEOUT sekund (zgodnie z definicja w pliku options.h w momencie kompilacji serwera). |

> Subtelny szczegol: jesli dane polaczenie sieciowe zostalo odebrane w punkcie nasluchu (utworzonym przez funkcje `listen()`) obslugiwanym przez obiekt obj inny niz `#0`, komunikaty systemowe dla tego polaczenia sa szukane na `obj.server_options`; jesli ta wlasciwosc nie istnieje, uzywana jest w to miejsce `$server_options`.

#### Checkpointowanie bazy danych

Serwer utrzymuje cala baze danych MOO w pamieci glownej, a nie na dysku. Dlatego konieczne jest zrzucenie bazy danych na dysk, jesli ma ona przetrwac dluzej niz czas dzialania konkretnego uruchomienia serwera. Serwer oczywiscie dba o to, by zrzucic baze danych tuz przed wylaczeniem, ale rozsadne jest tez robienie tego w regularnych odstepach, na wypadek, gdyby stalo sie cos niepomyslnego.

By okreslic, jak czesto wykonywac te _checkpointy_ bazy danych, serwer sprawdza wartosc `$server_options.dump_interval`. Jesli istnieje i jej wartosc jest liczba calkowita wieksza lub rowna 60, jest ona przyjmowana jako liczba sekund oczekiwania miedzy checkpointami; w przeciwnym razie serwer wykonuje nowy checkpoint co 3600 sekund (godzine). Jesli wartosc `$server_options.dump_interval` zaplanowalaby nastepny checkpoint poza obslugiwanym przez platforme zakresem czasu, serwer zamiast tego uzywa domyslnej wartosci 3600 sekund w przyszlosci.

Decyzja o tym, jak dlugo czekac miedzy checkpointami, jest podejmowana ponownie natychmiast po rozpoczeciu kazdego z nich. Dlatego zmiany w `$server_options.dump_interval` zaczna obowiazywac po nastepnym checkpoincie.

Za kazdym razem, gdy serwer zaczyna wykonywac checkpoint, wykonuje nastepujace wywolanie czasownika:

```
$checkpoint_started()
```

Gdy proces checkpointowania jest zakonczony, serwer wykonuje nastepujace wywolanie czasownika:

```
$checkpoint_finished(success)
```

gdzie success jest prawdziwe wtedy i tylko wtedy, gdy checkpoint zostal pomyslnie zapisany na dysku. Checkpointowanie moze zawiesc z wielu powodow, zwykle z powodu wyczerpania roznych zasobow systemu operacyjnego, takich jak pamiec wirtualna lub miejsce na dysku. To nie jest bledem, jesli ktorys z tych czasownikow nie istnieje; odpowiadajace wywolanie jest po prostu pomijane.

### Komunikacja sieciowa

#### Akceptowanie i inicjowanie polaczen sieciowych

Gdy serwer po raz pierwszy akceptuje nowe, przychodzace polaczenie sieciowe, otrzymuje niskopoziomowy adres sieciowy komputera po drugiej stronie. Natychmiast probuje przeksztalcic ten adres w czytelna dla czlowieka nazwe hosta, ktora zostanie wpisana do logu serwera i zwrocona przez funkcje `connection_name()`. To przeksztalcenie moze, dla konfiguracji sieciowych TCP/IP, wymagac pewnej komunikacji ze zdalnymi serwerami nazw, co moze zajac dosc duzo czasu i/lub calkowicie zawiesc. Podczas wykonywania tego przeksztalcenia serwer nie robi w ogole nic innego; w szczegolnosci nie odpowiada na polecenia uzytkownikow ani nie wykonuje zadan MOO.

Domyslnie serwer probuje wykonac to wyszukiwanie nazwy dla nowych polaczen. Jesli `$server_options.no_name_lookup` jest prawdziwe, automatyczne rozwiazywanie nazw DNS jest wylaczone, a serwer uzywa w to miejsce drukowalnej reprezentacji niskopoziomowego adresu.

Gdy uzywana jest funkcja `open_network_connection()`, serwer musi ponownie wykonac przeksztalcenie, tym razem z nazwy hosta podanej jako argument na niskopoziomowy adres niezbedny do faktycznego otwarcia polaczenia. Jesli wyszukiwanie adresu zawiedzie, proba polaczenia zostaje przerwana, a `open_network_connection()` zglasza `E_INVARG` z informacjami diagnostycznymi.

Jednak nawet po pomyslnym przeksztalceniu serwer nadal musi czekac, az faktyczne polaczenie zostanie zaakceptowane przez zdalny komputer. Podobnie jak wczesniej, moze to zajac duzo czasu, w trakcie ktorego serwer znow nie robi nic innego. Domyslnie serwer bedzie czekal nie dluzej niz 5 sekund na powodzenie proby polaczenia; jesli limit czasu uplynie, `open_network_connection()` zglasza `E_QUOTA`. Ten domyslny limit czasu mozna nadpisac z poziomu bazy danych, definiujac wlasciwosc `outbound_connect_timeout` na `$server_options` z liczba calkowita jako wartoscia.

#### Kojarzenie polaczen sieciowych z graczami

Gdy polaczenie sieciowe zostaje po raz pierwszy nawiazane z MOO, jest identyfikowane unikalnym, ujemnym numerem obiektu. O takim polaczeniu mowi sie, ze jest _niezalogowane_ i nie jest jeszcze powiazane z zadnym obiektem-graczem MOO.

Kazda linia wejscia na niezalogowanym polaczeniu jest najpierw parsowana na slowa w zwykly sposob (zobacz rozdzial o parsowaniu polecen po szczegoly), a nastepnie te slowa sa przekazywane jako argumenty w wywolaniu czasownika `$do_login_command()`. Na przyklad linia wejscia

```
connect Munchkin frebblebit
```

skutkowalaby nastepujacym wywolaniem:

```
$do_login_command("connect", "Munchkin", "frebblebit")
```

W tym wywolaniu zmienna `player` bedzie miala jako wartosc ujemny numer obiektu powiazany z odpowiednim polaczeniem sieciowym. Funkcje `notify()` i `boot_player()` moga byc uzyte z takimi numerami obiektow, by wysylac wyjscie do niezalogowanych polaczen i je rozlaczac. Ponadto zmienna `argstr` bedzie miala jako wartosc niesparsowana linie polecenia, tak jak zostala odebrana na polaczeniu sieciowym.

Jesli `$do_login_command()` zwroci prawidlowy obiekt gracza, a polaczenie jest nadal otwarte, uznaje sie, ze polaczenie _zalogowalo sie_ na tego gracza. Serwer nastepnie wykonuje jedno z nastepujacych wywolan czasownika, w zaleznosci od zwroconego obiektu gracza:

```
$user_created(player)
$user_connected(player)
$user_reconnected(player)
```

Pierwsze z nich jest uzywane, jesli zwrocony numer obiektu jest wiekszy niz wartosc zwrocona przez funkcje `max_object()` przed wywolaniem `$do_login_command()`, czyli jest wywolywane, jesli zwrocony obiekt wyglada na swiezo utworzony. Jesli tak nie jest, uzywane jest jedno z pozostalych dwoch wywolan czasownika. Wywolanie `$user_connected()` jest uzywane, jesli nie bylo istniejacego aktywnego polaczenia dla zwroconego obiektu gracza. W przeciwnym razie uzywane jest zamiast tego wywolanie `$user_reconnected()`.

> Subtelny szczegol: jesli uzytkownik ponownie sie laczy, a stare i nowe polaczenie uzytkownika sa na dwoch roznych punktach nasluchu obslugiwanych przez rozne obiekty (zobacz opis funkcji `listen()` po wiecej szczegolow), wtedy `user_client_disconnected` jest wywolywane dla starego polaczenia, a `user_connected` dla nowego.

> Uwaga: jesli jakis kod zawiesi sie w do_login_command() lub w czasowniku wywolanym przez do_login_command() (read(), suspend() lub dowolna funkcja watkowana), nie mozesz juz polaczyc obiektu, zwracajac go. To dziwna, starozytna pozostalosc po MOO. Najlepszym sposobem na zalogowanie gracza po zawieszeniu jest uzycie funkcji `switch_player()`, by przelaczyc jego niezalogowany ujemny obiekt na jego obiekt gracza.

Jesli przychodzace polaczenie sieciowe nie zaloguje sie pomyslnie w ciagu pewnego okresu czasu, serwer automatycznie zamknie to polaczenie, zwalniajac tym samym zasoby zwiazane z jego utrzymywaniem. Niech L bedzie obiektem obslugujacym punkt nasluchu, na ktorym odebrano polaczenie (lub `#0`, jesli polaczenie przyszlo na poczatkowym punkcie nasluchu). By odkryc okres limitu czasu, serwer sprawdza na `L.server_options` lub, jesli nie istnieje, na `$server_options` wlasciwosc `connect_timeout`. Jesli zostanie znaleziona, a jej wartosc jest dodatnia liczba calkowita, to jest to liczba sekund, ktorej serwer uzyje jako okresu limitu czasu. Jesli wlasciwosc `connect_timeout` istnieje, ale jej wartosc nie jest dodatnia liczba calkowita, wtedy w ogole nie ma limitu czasu. Jesli ta wlasciwosc nie istnieje, domyslny limit czasu wynosi 300 sekund.

Gdy dowolne polaczenie sieciowe (nawet niezalogowane lub wychodzace) zostaje zakonczone, przez serwer lub przez klienta, wykonywane jest jedno z nastepujacych dwoch wywolan czasownika:

```
$user_disconnected(player)
$user_client_disconnected(player)
```

Pierwsze jest uzywane, jesli rozlaczenie wynika z dzialan podjetych przez serwer (np. uzycia funkcji `boot_player()` lub opisanego wyzej limitu czasu dla niezalogowanych), a drugie, jesli rozlaczenie zostalo zainicjowane po stronie klienta.

To nie jest bledem, jesli ktorykolwiek z tych pieciu czasownikow nie istnieje; odpowiadajace wywolanie jest po prostu pomijane.

> Uwaga: tylko jedno polaczenie sieciowe moze kontrolowac dany obiekt gracza w danym momencie; jesli drugie polaczenie sprobuje zalogowac sie jako ten sam gracz, pierwsze polaczenie zostaje bezceremonialnie zamkniete (i wywolane zostaje `$user_reconnected()`, jak opisano wyzej). Ulatwia to odzyskiwanie sprawnosci po roznego rodzaju problemach sieciowych, ktore pozostawiaja polaczenia otwarte, ale niedostepne.

Gdy polaczenie sieciowe zostaje po raz pierwszy nawiazane, serwer automatycznie wprowadza puste polecenie, co skutkuje poczatkowym wywolaniem `$do_login_command()` bez argumentow. Ten sygnal moze zostac uzyty przez czasownik na przyklad do wypisania wiadomosci powitalnej.

> Ostrzezenie: jesli nie zdefiniowano czasownika `$do_login_command()`, linie wejscia z niezalogowanych polaczen sa po prostu odrzucane. Dlatego _koniecznie_ kazda baza danych musi zawierac odpowiednia definicje tego czasownika.

> Zauwaz, ze baza danych z brakujacym lub zepsutym $do_login_command nadal moze zostac wykorzystana (i byc moze naprawiona), uruchamiajac serwer z opcja linii polecen -e. Zobacz sekcje o trybie awaryjnym czarodzieja (Emergency Wizard Mode).

Mozliwe jest skompilowanie serwera z opcja definiujaca `prefiks poza pasmem` dla polecen. Jest to string, ktorego obecnosci na poczatku kazdej linii wejscia od graczy serwer bedzie sprawdzal, niezaleznie od tego, czy ci gracze sa zalogowani, i niezaleznie od tego, czy jakies zadania odczytu oczekuja na wejscie od tych graczy. Jesli dana linia wejscia zaczyna sie od zdefiniowanego prefiksu poza pasmem (wiodace spacje, jesli sa, _nie_ sa usuwane przed sprawdzeniem), nie jest traktowana jako normalne polecenie ani jako wejscie dla zadnego zadania odczytu. Zamiast tego linia jest parsowana na liste slow w zwykly sposob, a te slowa sa przekazywane jako argumenty w wywolaniu `$do_out_of_band_command()`. Na przyklad, jesli prefiks poza pasmem zostal zdefiniowany jako `#$#`, linia wejscia

```
#$# client-type fancy
```

skutkowalaby nastepujacym wywolaniem wykonanym w nowym zadaniu serwera:

```
$do_out_of_band_command("#$#", "client-type", "fancy")
```

Podczas wywolania `$do_out_of_band_command()` zmienna `player` jest ustawiona na numer obiektu reprezentujacy gracza powiazanego z polaczeniem, z ktorego pochodzi linia wejscia. Oczywiscie, jesli to polaczenie nie jest jeszcze zalogowane, numer obiektu bedzie ujemny. Ponadto zmienna `argstr` bedzie miala jako wartosc niesparsowana linie wejscia, tak jak zostala odebrana na polaczeniu sieciowym.

Polecenia poza pasmem sa przeznaczone do uzytku przez wyszukane programy-klienty, ktore moga generowac asynchroniczne _zdarzenia_, o ktorych serwer musi zostac powiadomiony. Poniewaz klient generalnie nie moze znac stanu polaczenia gracza (zalogowany czy nie, zadanie odczytu czy nie), polecenia poza pasmem stanowia jedyny niezawodny kanal komunikacji klient-serwer.

#### Obsluga wejscia gracza

**$do_out_of_band_command**

Na dowolnym polaczeniu, dla ktorego nie ustawiono opcji polaczenia disable-oob, wszelkie niewyczyszczone przychodzace linie zaczynajace sie od prefiksu poza pasmem beda traktowane jako polecenia poza pasmem, co oznacza, ze jesli czasownik $do_out_of_band_command() istnieje i jest wykonywalny, zostanie wywolany dla kazdej takiej linii. Wiecej na ten temat w sekcji o przetwarzaniu poza pasmem.

**$do_command**

Jak opisalismy wczesniej w rozdziale o wbudowanym parserze polecen, na dowolnym zalogowanym polaczeniu, ktore

* nie jest przedmiotem wywolania read(),
* nie ma w toku polecenia .program, i
* nie ma ustawionej opcji polaczenia hold-input,

dowolna przychodzaca linia, ktora

* nie zostala wyczyszczona,
* jest w pasmie (tj. nie zostala skonsumowana przez przetwarzanie poza pasmem), i
* sama nie jest .program ani jednym z pozostalych czterech wewnetrznych polecen,

skutkuje wywolaniem $do_command(), pod warunkiem, ze ten czasownik istnieje i jest wykonywalny. Jesli ten czasownik zawiesi sie lub zwroci wartosc prawdziwa, przetwarzanie tej linii konczy sie w tym miejscu; w przeciwnym razie, niezaleznie od tego, czy czasownik zwrocil falsz, czy w ogole nie istnial, wywolywana jest reszta wbudowanego procesu parsowania.

### Pierwsze zadania uruchamiane przez serwer

Za kazdym razem, gdy serwer jest uruchamiany, wykonuje na samym poczatku kilka zadan, zanim zacznie akceptowac polaczenia lub pobierze wartosc $server_options.dump_interval, by zaplanowac pierwszy checkpoint (zobacz nizej po wiecej informacji o planowaniu checkpointow).

Najpierw serwer wywoluje $do_start_script() i przekazuje tresc skryptu przez wbudowana zmienna args. Tresc skryptu jest okreslana w linii polecen podczas uruchamiania serwera. Serwer moze wywolac ten czasownik wielokrotnie, po razie dla kazdego z argumentow linii polecen -c i -f.

Nastepnie serwer wywoluje $user_disconnected() raz dla kazdego uzytkownika, ktory byl polaczony w momencie zapisu pliku bazy danych; pozwala to na wszelkie porzadki zwykle wykonywane przy rozlaczaniu uzytkownikow (np. przeniesienie ich obiektow-graczy z powrotem do jakiejs lokalizacji "domowej" itp.).

Nastepnie sprawdza istnienie czasownika $server_started(). Jesli taki czasownik istnieje, serwer uruchamia zadanie wywolujace ten czasownik bez argumentow i z player rownym #-1. Jest to przydatne do starannego planowania checkpointow oraz do ponownej inicjalizacji dowolnego stanu, ktory nie jest prawidlowo reprezentowany w pliku bazy danych (np. ponowne otwarcie pewnych wychodzacych polaczen sieciowych, czyszczenie pewnych tabel itp.).

### Kontrolowanie wykonania zadan

Jak opisano wczesniej w sekcji o zadaniach MOO, serwer naklada limity na liczbe sekund, przez ktore dowolne zadanie moze dzialac nieprzerwanie, oraz na liczbe "tickow", czyli operacji niskopoziomowych, jakie dowolne zadanie moze wykonac w jednym nieprzerwanym okresie. Domyslnie zadania pierwszoplanowe moga zuzyc 60 000 tickow i piec sekund, a zadania w tle moga zuzyc 30 000 tickow i trzy sekundy. Te wartosci domyslne mozna nadpisac z poziomu bazy danych, definiujac dowolne lub wszystkie z nastepujacych wlasciwosci na $server_options i nadajac im wartosci calkowitoliczbowe:

| Wlasciwosc | Opis                                         |
| ---------- | --------------------------------------------------- |
| bg_seconds | Liczba sekund przydzielanych zadaniom w tle. |
| bg_ticks   | Liczba tickow przydzielanych zadaniom w tle.   |
| fg_seconds | Liczba sekund przydzielanych zadaniom pierwszoplanowym. |
| fg_ticks | Liczba tickow przydzielanych zadaniom pierwszoplanowym. |

Serwer ignoruje wartosci `fg_ticks` i `bg_ticks`, jesli sa mniejsze niz 100, i podobnie ignoruje `fg_seconds` i `bg_seconds`, jesli ich wartosci sa mniejsze niz 1. Moze to pomoc zapobiec kompletnej katastrofie, gdybys przez przypadek nadal im bezuzytecznie male wartosci.

Przypomnijmy, ze zadania polecen i zadania serwera sa uznawane za zadania _pierwszoplanowe_, podczas gdy zadania sforkowane, zawieszone i odczytu sa definiowane jako zadania _w tle_. Ustawienia tych zmiennych zaczynaja obowiazywac wylacznie na poczatku wykonania lub przy wznowieniu wykonania po zawieszeniu lub odczycie.

Serwer naklada tez limit na liczbe poziomow zagniezdzonych wywolan czasownikow, zglaszajac `E_MAXREC` z wyrazenia wywolania czasownika, jesli limit zostanie przekroczony. Domyslnie limit wynosi 50 poziomow, ale mozna go zwiekszyc z poziomu bazy danych, definiujac wlasciwosc `max_stack_depth` na `$server_options` i nadajac jej wartosc calkowitoliczbowa wieksza niz 50. Maksymalna glebokosc stosu dla dowolnego zadania jest ustalana w momencie utworzenia tego zadania i nie moze zostac pozniej zmieniona. Oznacza to, ze zadania zawieszone, nawet po zapisaniu w bazie danych i przywroceniu z niej, nie sa dotkniete pozniejszymi zmianami $server_options.max_stack_depth.

Wreszcie serwer moze narzucic limit na liczbe sforkowanych lub zawieszonych zadan, jakie dowolny gracz moze miec zakolejkowane w danym momencie. Za kazdym razem, gdy w jakims czasowniku wykonywana jest instrukcja `fork` lub wywolanie `suspend()`, serwer sprawdza na programiscie wlasciwosc o nazwie `queued_task_limit`. Jesli ta wlasciwosc istnieje, a jej wartosc jest nieujemna liczba calkowita, to ta liczba jest limitem. W przeciwnym razie, jesli `$server_options.queued_task_limit` istnieje, a jej wartosc jest nieujemna liczba calkowita, to ona jest limitem. W przeciwnym razie nie ma limitu. Jesli programista ma juz liczbe zakolejkowanych zadan wieksza lub rowna limitowi, zamiast forkowania lub zawieszania zglaszany jest `E_QUOTA`. Zadania odczytu sa objete limitem zakolejkowanych zadan.

### Kontrolowanie obslugi przerwanych zadan

Serwer przerwie wykonanie zadan z jednego z dwoch powodow:

1. w zadaniu zostal zgloszony blad, ktory nie zostal przechwycony

W kazdym przypadku, po przerwaniu zadania, serwer probuje wywolac okreslony _czasownik obslugujacy_ (handler verb) w bazie danych, by pozwolic kodowi tam zawartemu obsluzyc ten wypadek w odpowiedni sposob. Jesli to wywolanie czasownika zawiesi sie lub zwroci wartosc prawdziwa, uznaje sie, ze sytuacja zostala w pelni obsluzona i serwer nie wykonuje dalszego przetwarzania. Z drugiej strony, jesli czasownik obslugujacy nie istnieje, lub jesli wywolanie zwroci falsz bez zawieszenia sie, lub samo zostanie przerwane, serwer bierze sprawy we wlasne rece.

Najpierw graczowi, ktory wpisal polecenie tworzace pierwotne przerwane zadanie, wypisywany jest komunikat bledu wraz z _tracebackiem_ stosu wywolan czasownikow MOO, wyjasniajacy, dlaczego zadanie zostalo przerwane i gdzie w zadaniu wystapil problem. Nastepnie, jesli samo wywolanie czasownika obslugujacego zostalo przerwane, wypisywany jest drugi komunikat bledu i traceback, opisujacy rowniez ten problem. Zauwaz, ze jesli samo wywolanie czasownika obslugujacego zostanie przerwane, nie sa wykonywane zadne dalsze "zagniezdzone" wywolania obslugujace; ta polityka zapobiega temu, co w przeciwnym razie mogloby byc dosc zlosliwym, malym cyklem.

Konkretny czasownik obslugujacy oraz zestaw przekazywanych mu argumentow roznia sie w zaleznosci od dwoch przyczyn przerwania zadania.

Jesli blad zostanie zglaszony i nie przechwycony, wykonywane jest wywolanie czasownika

```
$handle_uncaught_error(code, msg, value, traceback, formatted)
```

gdzie code, msg, value i traceback to wartosci, ktore zostalyby przekazane do handlera w instrukcji `try`-`except`, a formatted to lista stringow bedacych liniami wyjscia bledu i tracebacku, ktore zostana wypisane graczowi, jesli `$handle_uncaught_error` zwroci falsz bez zawieszenia sie.

Jesli zadaniu skoncza sie ticki lub sekundy, wykonywane jest wywolanie czasownika

```
$handle_task_timeout(resource, traceback, formatted)
```

gdzie `resource` to odpowiedni z stringow `"ticks"` lub `"seconds"`, a `traceback` i `formatted` sa jak powyzej.

### Dopasowywanie w parsowaniu polecen

W procesie dopasowywania stringow dopelnienia blizszego i dalszego w poleceniu do faktycznych obiektow, serwer uzywa wartosci wlasciwosci `aliases`, jesli istnieje, na kazdym obiekcie w zawartosci gracza i lokalizacji gracza. Pelne szczegoly znajdziesz w rozdziale o parsowaniu polecen.

### Ograniczanie dostepu do wbudowanych wlasciwosci i funkcji

**Chronione wlasciwosci**

Wbudowana wlasciwosc prop jest uznawana za chroniona, jesli $server_options.protect_prop istnieje i ma wartosc prawdziwa. Jednak zadne takie ochrony wlasciwosci nie sa rozpoznawane, jesli podczas budowania serwera ustawiono opcje kompilacji IGNORE_PROP_PROTECTED (zobacz sekcje o opcjach kompilacji serwera).

> Uwaga: w poprzednich wersjach serwera wlaczenie tego mialo znaczacy koszt wydajnosciowy, ale zostalo to rozwiazane dzieki buforowaniu wyszukiwan, wiec ta opcja jest domyslnie wlaczona w ToastStunt.

Za kazdym razem, gdy kod czasownika probuje odczytac (na dowolnym obiekcie) wartosc wbudowanej wlasciwosci chronionej w ten sposob, serwer zglasza E_PERM, jesli programista nie jest czarodziejem.

**Chronione funkcje wbudowane**

Funkcja wbudowana func() jest uznawana za chroniona, jesli $server_options.protect_func istnieje i ma wartosc prawdziwa. Jesli dla danej chronionej funkcji wbudowanej istnieje odpowiadajacy czasownik $bf_func() z ustawionym bitem `x`, ta funkcja wbudowana jest tez uznawana za nadpisana, co oznacza, ze dowolne wywolanie func() z dowolnego obiektu innego niz #0 bedzie traktowane jako wywolanie $bf_func() z tymi samymi argumentami, zwracajace lub zglaszajace to, co ten czasownik zwroci lub zglosi.

Wywolanie chronionej funkcji wbudowanej, ktora nie zostala nadpisana, przebiega normalnie, dopoki wywolujacy jest #0 lub ma uprawnienia czarodzieja; w przeciwnym razie serwer zglasza E_PERM.

Zauwaz, ze musisz wywolac load_server_options(), by upewnic sie, ze zmiany dokonane w $server_options zaczna obowiazywac.

### Tworzenie i recyklingowanie obiektow

Za kazdym razem, gdy funkcja `create()` jest uzywana do utworzenia nowego obiektu, wywolywany jest czasownik `initialize` tego obiektu, jesli istnieje, bez argumentow. Jesli taki czasownik nie jest zdefiniowany na obiekcie, wywolanie jest po prostu pomijane.

Symetrycznie, tuz przed tym, jak funkcja `recycle()` faktycznie zniszczy obiekt, wywolywany jest czasownik `recycle` tego obiektu, jesli istnieje, bez argumentow. Ponownie, jesli taki czasownik nie jest zdefiniowany na obiekcie, wywolanie jest po prostu pomijane.

Zarowno `create()`, jak i `recycle()` sprawdzaja istnienie wlasciwosci `ownership_quota` na wlascicielu nowo utworzonego lub zniszczonego obiektu. Jesli taka wlasciwosc istnieje, a jej wartosc jest liczba calkowita, jest ona traktowana jako _limit_ (quota) na wlasnosc obiektow. W przeciwnym razie nastepujace dwa akapity nie maja zastosowania.

Funkcja `create()` sprawdza, czy limit jest dodatni; jesli tak, jest on zmniejszany o jeden i zapisywany z powrotem do wlasciwosci `ownership_quota` na wlascicielu. Jesli limit wynosi zero lub jest ujemny, uznaje sie go za wyczerpany, a `create()` zglasza `E_QUOTA`.

Funkcja `recycle()` zwieksza limit o jeden i zapisuje go z powrotem do wlasciwosci `ownership_quota` na wlascicielu.

### Przemieszczanie obiektow

Podczas ewaluacji wywolania funkcji `move()`, serwer moze wykonywac wywolania czasownikow `accept` i `enterfunc` zdefiniowanych na celu przemieszczenia oraz czasownika `exitfunc` zdefiniowanego na zrodle. Zasady i okolicznosci sa nieco skomplikowane i podane szczegolowo w opisie funkcji `move()`.

### Tymczasowe wlaczanie przestarzalych funkcji serwera

Jesli wlasciwosc `$server_options.support_numeric_verbname_strings` istnieje i ma wartosc prawdziwa, serwer wspiera przestarzaly mechanizm mniej niejednoznacznego odwolywania sie do konkretnych czasownikow w roznych funkcjach wbudowanych. Wiecej szczegolow znajdziesz w omowieniu zamieszczonym zaraz po opisie funkcji `verbs()`.

### Sygnaly do serwera

Serwer jest w stanie przechwytywac [sygnaly](https://en.wikipedia.org/wiki/Signal_(IPC)) z systemu operacyjnego i wykonywac okreslone akcje, ktorych liste mozna znalezc ponizej. Dwa sygnaly, USR1 i USR2, moga byc przetwarzane z poziomu bazy danych MOO. Gdy odebrany zostanie SIGUSR1 lub SIGUSR2, serwer wywola `#0:handle_signal()` z nazwa sygnalu jako jedynym argumentem. Jesli ten czasownik zwroci wartosc prawdziwa, zaklada sie, ze baza danych go obsluzyla i nie sa podejmowane dalsze dzialania. Jesli czasownik zwroci wartosc ujemna, serwer przystapi do wykonania domyslnej akcji dla tego sygnalu. Ponizej znajduje sie lista sygnalow i ich domyslnych akcji:

| Sygnal | Akcja                        |
| ------ | ----------------------------- |
| HUP    | Awaria serwera (panic).             |
| ILL    | Awaria serwera (panic).             |
| QUIT   | Awaria serwera (panic).             |
| SEGV   | Awaria serwera (panic).             |
| BUS    | Awaria serwera (panic).             |
| INT    | Czyste wylaczenie serwera. |
| TERM   | Czyste wylaczenie serwera. |
| USR1   | Ponowne otwarcie pliku logu.          |
| USR2   | Zaplanowanie checkpointu na najblizsza mozliwa chwile. |

Na przyklad, wyobraz sobie, ze jestes administratorem systemu zalogowanym na maszynie, na ktorej dziala MOO. Chcesz wylaczyc serwer MOO, ale chcialbys dac graczom mozliwosc pozegnania sie ze soba nawzajem, zamiast natychmiast wylaczac serwer. Mozesz to zrobic, przechwytujac sygnal w bazie danych i wywolujac polecenie @shutdown.

```
@prog #0:handle_signal
set_task_perms(caller_perms());
{signal} = args;
if (signal == "SIGUSR2" && !$code_utils:task_valid($wiz_utils.shutdown_task))
  force_input(#2, "@shutdown in 1 Shutdown signal received.");
  force_input(#2, "yes");
  return 1;
endif
.
```

Teraz mozesz zasygnalizowac MOO poleceniem kill: `kill -USR2 <MOO process ID`
