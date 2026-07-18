# Budowa pliku bazy danych LambdaMOO

*Polskie tlumaczenie dokumentu ["Anatomy of a LambdaMOO db file"](https://lisdude.com/moo/lmdb.html) autorstwa Roberta Lesliego i Alexa Stewarta. Ten dokument jest linkowany z Podrecznika Programisty ToastStunt jako materialy zrodlowe. Opisuje **stary** format bazy danych LambdaMOO (do wersji 4 wlacznie); ToastStunt uzywa nowszego formatu, opisanego w [Budowie bazy danych ToastStunt](BUDOWA-BAZY-DANYCH-TOASTSTUNT.md).*

Autorzy: Robert Leslie `<rob@ccs.neu.edu>`, Alex Stewart `<stewarta@netcom.com>`

Zastrzezenie: Ingerowanie w wewnetrzna strukture plikow bazy danych LambdaMOO jest z natury niebezpieczne i nie jest zalecane. Ponizsze informacje nalezy wykorzystywac na wlasne ryzyko.

Plik bazy danych to plaski plik tekstowy ASCII zorganizowany w linie.

Pierwsze cztery linie stanowia naglowek zlozony z:

* calkowitej liczby obiektow w bazie danych, wliczajac obiekty zrecyklingowane (rowniez wartosc max_object() plus jeden);
* calkowitej liczby zaprogramowanych czasownikow w bazie danych, nie wliczajac czasownikow niezaprogramowanych;
* liczby, ktorej wartosc jest nieistotna, oraz
* calkowitej liczby obiektow, ktore maja ustawiona flage player.

Kolejne N linii stanowi liste numerow obiektow-graczy. N jest rowne wartosci z 4. linii naglowka bazy danych.

Kolejna sekcja zawiera opis kazdego obiektu w bazie danych. Kazdy obiekt ma nastepujaca strukture:

* linia znacznikowa zawierajaca znak funta (#) i numer obiektu. Jesli obiekt zostal zrecyklingowany, pojawia sie tez slowo "recycled".

Dla obiektow niezrecyklingowanych:

* lancuch znakow zawierajacy wartosc wlasciwosci .name obiektu;
* lancuch znakow, ktory mozna zignorowac;
* liczba zawierajaca zestaw flag, opisany ponizej [1];
* numer obiektu bedacego wlascicielem (.owner) tego obiektu;
* numer obiektu bedacego lokalizacja (.location) tego obiektu;
* numer obiektu pierwszego obiektu na liscie wiazanej zawartosci (.contents) tego obiektu (lub -1, jesli nic nie zawiera);
* numer obiektu nastepnego obiektu na liscie wiazanej zawartosci (.contents) lokalizacji (.location) tego obiektu (lub -1, jesli to koniec listy);
* numer obiektu bedacego rodzicem tego obiektu;
* numer obiektu pierwszego obiektu na liscie wiazanej dzieci tego obiektu (lub -1, jesli nie ma dzieci);
* numer obiektu nastepnego obiektu na liscie wiazanej dzieci rodzica tego obiektu (lub -1, jesli to koniec listy);
* liczba czasownikow zdefiniowanych na tym obiekcie, niezaleznie od tego, czy zostaly zaprogramowane;

Dla kazdego czasownika:

* lancuch znakow zawierajacy nazwe (nazwy) czasownika;
* numer obiektu bedacego wlascicielem czasownika;
* liczba zawierajaca flagi uprawnien, opisane ponizej [2];
* liczba zawierajaca kod przyimka argumentu;

Kolejna linia zawiera liczbe wlasciwosci zdefiniowanych na tym obiekcie, N. Nastepnie wystepuje N linii lancuchow znakow zawierajacych nazwe kazdej wlasciwosci.

Na koniec zapisywane sa wartosci wszystkich wlasciwosci tego obiektu. Wartosci sa uporzadkowane sekwencyjnie -- najpierw wartosci dla kazdej wlasciwosci zdefiniowanej na tym obiekcie, potem wartosci dla kazdej wlasciwosci zdefiniowanej na rodzicu tego obiektu, potem na rodzicu rodzica, i tak dalej, az do samego szczytu drzewa rodowego obiektu.

Pierwsza linia zawiera calkowita liczbe wartosci wlasciwosci, ktore nastepuja. Dla kazdej wartosci wlasciwosci:

* liczba wskazujaca typeof() typu danych, lub liczba 5 reprezentujaca wartosc pusta (clear);

Dla wartosci niepustych:

* dla typu danych string, zawartosc lancucha znakow; dla typow danych object, error lub number, wartosc jako liczba; dla list, dlugosc listy, N;

Dla wartosci typu list nastepuje N kolejnych definicji danych (po jednej dla kazdego elementu listy) w tej samej formie (typ calkowity nastepnie odpowiednie dodatkowe dane).

Na koniec, po kazdej wartosci wlasciwosci nastepuje:

* numer obiektu bedacego wlascicielem tej wlasciwosci (na tym obiekcie);
* liczba zawierajaca flagi uprawnien, opisane ponizej [3];

Po opisach obiektow nastepuje kod programu czasownikow dla kazdego zaprogramowanego czasownika. Czasowniki niezaprogramowane sa pomijane. Dla kazdego programu:

* linia znacznikowa zawierajaca znak funta, numer obiektu, na ktorym znajduje sie ten czasownik, dwukropek, oraz liczony od zera indeks do zdefiniowanych czasownikow obiektu, wskazujacy czasownik powiazany z nastepujacym kodem.

Nastepuje kod programu czasownika w formie zrodlowej. Kod jest zakonczony pojedyncza kropka.

Ostatnia sekcja pliku bazy danych zawiera informacje o zawieszonych zadaniach.

Pierwsza linia na liscie zakolejkowanych zadan ma postac "<num> clocks" (gdzie <num> to liczba). Jest to zasadniczo przestarzaly aspekt obslugi zadan z wczesniejszych dni serwerow MOO i jest po prostu raportowany jako "0 clocks" we wspolczesnych serwerach. Jesli jest niezerowy, nastepuje po nim <num> linii danych zegara, ktore i tak mozna zignorowac.

Nastepnie wystepuje linia stwierdzajaca "<num> queued tasks", czyli liczba sforkowanych zadan w kolejce zadan. Nastepuje po niej <num> blokow danych zawierajacych stan MOO dla kazdego zadania, zdefiniowane zmienne oraz fragment kodu czasownika, ktory jest wykonywany. Kazdy z tych blokow zaczyna sie od linii postaci:

```
0 <lineno> <start-time> <task-id>
```

Nastepnie dwie kolejne linie, ktore juz nic nie znacza:

```
0
-111
```

Nastepnie linia postaci:

```
<this> -7 -8 <player> -9 <programmer> <verb-location> -10 <debug>
```

(miejsca -7 -8 -9 i -10 nie sa juz do niczego uzywane) Nastepnie 4 kolejne nieuzywane linie:

```
No
More
Parse
Info
```

nastepnie wartosc zmiennej "verb" w danym momencie, a po niej nazwa faktycznego czasownika powiazanego z wykonywanym kodem czasownika.

Nastepnie pojawiaja sie informacje o srodowisku wykonawczym (definicje zmiennych), a potem blok kodu czasownika, ktory zostal sforkowany, konczacy sie linia zawierajaca samotna kropke.

Po wszystkich sforkowanych zadaniach nastepuje linia postaci "<num> suspended tasks", po ktorej nastepuje <num> blokow informacji o zawieszonych zadaniach.

O ile moglbym wchodzic w wielkie szczegoly na temat zawartosci pliku od tego miejsca, prawdopodobnie nie przyniosloby to wielu ludziom wielkiego pozytku, poniewaz niemal niemozliwe jest sledzenie wszystkich drobnych szczegolow recznie, a poza tym nie jestem pewien, dlaczego ktokolwiek chcialby to robic dla zawieszonych zadan.. Jesli po prostu przegladasz plik i chcesz wiedziec, na co patrzysz -- jest tam <num> blokow danych (po jednym dla kazdego zadania). Kazdy z tych blokow ma dane dla kazdego punktu na stosie callers() (w kolejnosci od pierwszego wykonanego (najplytszego) do aktualnie wykonywanego (najglebszego)). Dla kazdego wpisu na stosie callers() wymienia kod czasownika wykonywanego czasownika, wszystkie zmienne zdefiniowane dla tego wywolania, blok danych podobny do tego wymienionego dla sforkowanych zadan (0, -111, linia this/player/itd., "No", "More", "Parse", "Info", verb, verb-name) oraz troche innych, mniej informacyjnych rzeczy wetknietych tu i owdzie miedzy nimi wszystkimi.

A potem jest koniec.

[1] Flagi obiektu:

```
player      0x01
programmer  0x02
wizard      0x04
read        0x10
write       0x20
fertile     0x80
```

[2] Uprawnienia czasownika:

```
read        0x01
write       0x02
execute     0x04
debug       0x08
dobj arg    0x30  ("none", "any", "this")
iobj arg    0xC0  ("none", "any", "this")
```

[3] Uprawnienia wlasciwosci:

```
read        0x01
write       0x02
chown       0x04
```

## Odpowiedzi na czeste pytania

**Jak znalezc konkretny obiekt?**

Przeszukaj plik bazy danych od poczatku w poszukiwaniu lancucha "#X" w pojedynczej linii, gdzie X to szukany numer obiektu. Oczywiscie, mozesz zamiast tego trafic na wartosc wlasciwosci typu string na jakims obiekcie, ktora przypadkiem zawiera ten sam tekst, wiec upewnij sie, ze sprawdzasz tez nastepna linie, ktora powinna zawierac nazwe szukanego obiektu.

**Jak usunac/dodac/zmodyfikowac wlasciwosci?**

Dodawanie lub usuwanie wlasciwosci jest zdradliwe; liczby definicji wlasciwosci i liczby wartosci musza sie dokladnie zgadzac, a nalezy tez uwzglednic wartosci wlasciwosci na wszystkich potomkach danego obiektu.

Byc moze uda ci sie zmodyfikowac wartosc wlasciwosci, jesli bedziesz bardzo ostrozny. Znalezienie faktycznej wartosci w pliku bazy danych moze byc trudne, poniewaz nie jest oczywiste, ktore wartosci sa powiazane z ktorymi nazwami wlasciwosci. Jesli biezaca wartosc jest czyms, czego mozna by szukac (powiedzmy, gdybys znal zaszyfrowane haslo z wyprzedzeniem i mogl go szukac), moze ci sie poszczescic bardziej.

**Jak usunac/dodac/zmodyfikowac czasowniki?**

Usuwanie czasownikow jest w porownaniu latwiejsze. Musisz usunac cztery linie zawierajace definicje czasownika w opisie obiektu, na ktorym ten czasownik sie znajduje, oraz zmniejszyc liczbe czasownikow w 12. linii definicji obiektu. Jesli czasownik zostal zaprogramowany, powinienes tez usunac powiazany kod czasownika w dalszej czesci pliku bazy danych i zmniejszyc globalna liczbe czasownikow w 2. linii pliku. Jest jeden haczyk: usuwajac czasownik, wszystkie pozniejsze czasowniki na obiekcie zostaly przenumerowane (przypomnijmy, ze sekcja kodu czasownikow przypisuje kod do czasownikow za pomoca indeksu liczonego od zera), wiec musisz odpowiednio przenumerowac linie znacznikowe dla dotknietych programow czasownikow.

Dodanie nowego czasownika byloby wykonalne, robiac odwrotnosc powyzszego.

**Jak usunac aktywne zadania?**

Mozna wyeliminowac wszystkie zawieszone zadania, zastepujac ostatnia sekcje pliku bazy danych zawierajaca informacje o zadaniach nastepujacymi trzema liniami:

```
0 clocks
0 queued tasks
0 suspended tasks
```

Te linie powinny wystepowac bezposrednio po ostatnim programie czasownika i powinny byc bezposrednio nastepowane przez koniec pliku.

**Czy sa jakies proste sprawdziany integralnosci, ktore moge wykonac recznie?**

Powyzszy opis jest prawdopodobnie wystarczajaco kompletny, bys mogl zdecydowac, jakie sprawdziany integralnosci sa wykonalne i jak je przeprowadzic. Niemniej jednak, przetestowanie zmodyfikowanej bazy danych z prawdziwym serwerem LambdaMOO jest prawdopodobnie najlepszym sposobem, by upewnic sie, ze jest ona nadal chociaz uzywalna. Jesli wystapia drobne problemy, serwer moze byc nawet w stanie skompensowac niektore z nich podczas wlasnych rygorystycznych weryfikacji.

Nie powinienem musiec podkreslac, ze edytowanie plikow bazy danych recznie jest z natury niebezpieczne. Naprawde nie polecam zadnego znaczacego "hackowania".

Ponadto, chociaz jestem dosc pewny, ze powyzszy opis jest poprawny, w zaden sposob nie gwarantuje jego dokladnosci i z pewnoscia nie jestem gotow przyjac odpowiedzialnosci za jakiekolwiek szkody wyrzadzone czyjejs bazie danych w wyniku upublicznienia przeze mnie tego dokumentu. Niemniej jednak, mam nadzieje, ze komus sie przyda.
