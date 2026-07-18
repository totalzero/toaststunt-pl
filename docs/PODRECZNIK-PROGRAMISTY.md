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
