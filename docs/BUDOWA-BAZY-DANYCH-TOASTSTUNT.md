# Budowa bazy danych ToastStunt

*Polskie tlumaczenie dokumentu ["Anatomy of a ToastStunt Database File"](https://lisdude.com/moo/toaststunt_anatomy/) (stan na 2022-12-15, wersja formatu bazy danych 17). Ten dokument opisuje **aktualny** format bazy danych ToastStunt -- w odroznieniu od starszego formatu LambdaMOO opisanego w [Budowie pliku bazy danych LambdaMOO](BUDOWA-PLIKU-LMDB.md). Jest linkowany z Podrecznika Programisty ToastStunt jako material zrodlowy.*

## Wstep

Plik bazy danych ToastStunt to plaski plik tekstowy ASCII, w ktorym odpowiednie fragmenty informacji sa oddzielone znakami nowej linii. Ten dokument omowi strukture tego pliku i wyjasni, jak wyprowadzane sa poszczegolne wartosci. Jest malo prawdopodobne, ze bedziesz w stanie wprowadzic w bazie danych recznie wiecej niz drobne zmiany, ale ta informacja powinna okazac sie cenna, jesli bedziesz musial sparsowac baze danych lub probowac odzyskac baze danych albo dane z niej.

Informacje ponizej sa napisane w dokladnie takiej kolejnosci, w jakiej napotkasz je w rzeczywistym pliku bazy danych. Gdy oczekiwany jest konkretny typ wartosci MOO, dany element bedzie odsylal do sekcji wyjasniajacej, jak interpretowac ten konkretny typ w bazie danych.

Osoby ciekawe kodu zrodlowego serwera powinny zainteresowac sie zwlaszcza funkcja `write_db_file` w `db_file.cc`: punktem wejscia do zapisu bazy danych.

## Obserwacje do zapamietania

Warto pamietac o kilku rzeczach podczas czytania, parsowania lub myslenia o formacie bazy danych:

* Typy sa identyfikowane przez ich liczbowa wartosc typu (tj. wynik `typeof()`) bezposrednio przed ich wartoscia.
* Jesli typ to CLEAR lub NONE (5 lub 6), po nim nie wystapi zadna wartosc.
* O ile nie zaznaczono inaczej, numery obiektow sa liczbami calkowitymi i nie zawieraja poczatkowego znaku funta (#).
* Zobacz sekcje "Interpretowanie typow" ponizej po informacje o tym, jak interpretowac poszczegolne typy.

## Baza danych

### Blok poczatkowy

Kazdy plik bazy danych zaczyna sie od rozpoznawalnego, czytelnego dla czlowieka naglowka. Zwykle jest to cos w rodzaju: `** LambdaMOO Database, Format Version 17 **`. Wskazuje to, ze jest to (oczywiscie) baza danych LambdaMOO oraz wersje uzywanego formatu. Wersja jest wazna, poniewaz informuje serwer, jakie funkcje sa dostepne w chwili zapisu bazy danych, co wplywa na sposob jej odczytu. (Na przyklad bazy danych sprzed wersji formatu 15 nie zawieraly wlasciwosci `last_move` dla kazdego obiektu. Bez wlasciwej wersji serwer zalozylby, ze ta baza danych ma te wlasciwosc, i probowalby ja odczytac, co by sie nie powiodlo.) (Zobacz `version.h`, jesli jestes ciekawy, co zmienila kazda rewizja bazy danych.)

* Calkowita liczbe obiektow z ustawiona flaga player.
* Liste numerow kazdego obiektu z ustawiona flaga player.

### Dane przejsciowe

`X values pending finalization`: Ten naglowek wskazuje calkowita liczbe obiektow anonimowych, ktore zostaly zrecyklingowane, ale ich czasownik recycle() nie zostal jeszcze wywolany.

Kolejne X linii to kazdy obiekt oczekujacy na finalizacje. Kazdy obiekt to dwie linie:

* Typ obiektu (np. 12 dla ANON)
* Numer obiektu (np. 4 dla #4)

`0 clocks`: Teraz bez znaczenia. Byla to czesc wczesnej obslugi zadan w MOO, ktora jest teraz przestarzala. Kazda baza danych z informacjami o zegarze bedzie uzywac formatu bazy danych LambdaMOO w wersji 4 lub nizszej -- w takim wypadku powinienes zapoznac sie z "Budowa pliku bazy danych LambdaMOO".

`X queued tasks`: Ten naglowek wskazuje calkowita liczbe zakolejkowanych (sforkowanych) zadan.

Zobacz "Zadania zakolejkowane / sforkowane" ponizej.

`X suspended tasks`: Ten naglowek wskazuje calkowita liczbe zawieszonych zadan.

Zobacz "Zadania zawieszone" ponizej.

`X interrupted tasks`: Ten naglowek wskazuje calkowita liczbe zadan interaktywnych, ktore zostaly przerwane (np. przez read() lub read_http())

`X active connections with listeners`: Ten naglowek wskazuje calkowita liczbe aktywnych polaczen w chwili wylaczenia serwera. Kolejne X linii sklada sie z:

Lancucha znakow z dwoma liczbami oddzielonymi spacja:

* Numer obiektu polaczonego gracza.
* Numer obiektu nasluchujacego, do ktorego przypisany jest gracz. (Zwykle #0.)

## Obiekty

Liczba wskazujaca calkowita liczbe obiektow, wliczajac obiekty zrecyklingowane, w bazie danych. Nie wlicza obiektow anonimowych. (`max_object()` plus jeden dla #0)

Lista kazdego obiektu w bazie danych. Dla kazdego obiektu:

JESLI ZRECYKLINGOWANY: Pojedyncza linia z numerem obiektu i slowem `recycled` (np. `#5 recycled`). Koniec tego obiektu.

Jesli NIE zrecyklingowany: Pojedyncza linia zaczynajaca sie znakiem funta (#) i numerem obiektu. (np. `#5`)

* Nazwa obiektu.
* Liczba calkowita wskazujaca flagi obiektu. Zobacz "Flagi obiektu" ponizej.
* Wlasciciel obiektu. (UWAGA: to pojedyncza liczba calkowita, nie typ obiektowy.)
* Lokalizacja obiektu.
* Wartosc last_move obiektu.
* Zawartosc (contents) obiektu.
* Rodzice obiektu. Jesli pierwsza liczba to 1, obiekt ma tylko jednego rodzica i jest sformatowany jako obiekt. Jesli pierwsza liczba to 4, obiekt ma wielu rodzicow (lub zostal zmieniony przez chparents() na pojedynczego rodzica) i jest sformatowany jako lista.
* Dzieci obiektu.
* Liczbe czasownikow zdefiniowanych na obiekcie.

Lista kazdego czasownika. Dla kazdego czasownika:

* Nazwa czasownika.
* Wlasciciel czasownika.
* Uprawnienia czasownika (zobacz "Flagi uprawnien czasownika" ponizej).
* Przyimki czasownika (zobacz "Flagi przyimkow czasownika" ponizej).

* Liczbe wlasciwosci zdefiniowanych na obiekcie.
* Kazda wlasciwosc wymieniona po nazwie.
* Liczbe wartosci wlasciwosci ustawionych na obiekcie.

Wartosci wlasciwosci. Te wartosci sa wymienione w kolejnosci, w jakiej wystepuja w `properties(object)`. Obejmuje to wszystkie wlasciwosci zdefiniowane na obiekcie oraz wlasciwosci zdefiniowane na kazdym przodku. (Gdy w gre wchodzi dziedziczenie wielokrotne, stosowana jest kolejnosc `parents()` dla kazdego obiektu.) Dla kazdej wlasciwosci:

* Wartosc wlasciwosci. Moze to byc dowolny prawidlowy typ, wiec typ nalezy ustalic na podstawie pierwszej liczby i sprawdzic w sekcji "Interpretowanie typow". UWAGA: jesli napotkasz typ 5, wlasciwosc jest pusta (clear) i kolejne dwie linie nie wystapia.
* Numer obiektu wlasciciela wlasciwosci. (Liczba calkowita)
* Uprawnienia wlasciwosci (zobacz "Flagi uprawnien wlasciwosci" ponizej).
* Liczba 0.

## Czasowniki

Calkowita liczba zaprogramowanych czasownikow w bazie danych.

Wszystkie zaprogramowane czasowniki. Dla kazdego czasownika:

* Lancuch znakow wskazujacy numer obiektu (zaczynajacy sie znakiem funta) oraz numer czasownika. Ta liczba to pozycja czasownika w `verbs(object)` minus 1 (numeracja czasownikow zaczyna sie od 0). (np. `#0:0`)
* Kod czasownika, zakonczony kropka (.) w osobnej linii.

## Zadania zakolejkowane / sforkowane

Dla kazdego sforkowanego zadania zapisywane jest nastepujace:

Pierwsza linia dla kazdego zakolejkowanego zadania sklada sie z czterech liczb oddzielonych spacjami:

* Liczba 0
* Nastepna linia do wykonania w czasowniku, ktory sforkowal zadanie.
* Czas uniksowy, w ktorym zadanie ma sie rozpoczac.
* `task_id()` sforkowanego zadania.

Informacje o aktywacji.

`X variables`: Ten naglowek wskazuje calkowita liczbe zmiennych w czasowniku, ktory sforkowal zadanie. Dla kazdej zmiennej:

* Nazwa zmiennej. UWAGA: obejmuje to takze zmienne wbudowane, wiec zobaczysz rzeczy takie jak NUM, player, caller itd.
* Wartosc zmiennej.
* Typ zmiennej (np. 0 dla INT).
* Wartosc zmiennej. Zobacz "Interpretowanie typow" ponizej.

* Kod czasownika sforkowanego zadania.
* Pojedyncza kropka.

## Zadania zawieszone

Dla kazdego zawieszonego zadania zapisywane jest nastepujace:

Linia zlozona z trzech liczb:

* Czas uniksowy, w ktorym zadanie jest zaplanowane do wykonania. (Lub -1, jesli zadanie zostalo zawieszone na czas nieokreslony.)
* `task_id()` zawieszonego zadania.
* Typ wartosci zwracanej z wywolania resume(), ktore nie mialo jeszcze szansy sie wykonac. Jesli nie ma wartosci zwracanej, typem bedzie 0 (INT).

* Faktyczna wartosc zwracana z resume(). W wiekszosci przypadkow bedzie to 0.
* Wartosc zmiennej task_local().

Cztery liczby oddzielone spacjami z informacjami maszyny wirtualnej:

* Najwyzsza ramka stosu (liczac od 0). (To aktywacja (czasownik), ktora aktualnie sie wykonuje.)
* Wektor aktywacji korzenia.
* `func_id` (nieuzywane?)
* Maksymalny rozmiar stosu: wartosc opcji serwera max_stack_depth.

Zrzut stosu aktywacji (po jednym dla kazdego czasownika na stosie). Dla kazdej ramki:

* Naglowek wskazujacy uzywana wersje jezyka. Bedzie ona zgodna z wersja bazy danych obowiazujaca w chwili zapisu zadania. (np. `language version 17`)
* Kod czasownika dla tej konkretnej ramki. Zawsze konczy sie pojedyncza kropka.
* `X variables`: To naglowek sekcji zmiennych. Wskazuje calkowita liczbe zmiennych dla tej ramki.
* Nazwa zmiennej. (UWAGA: obejmuje to takze zmienne wbudowane, wiec zobaczysz rzeczy takie jak NUM, player, caller itd.)
* Wartosc zmiennej.
* Typ zmiennej (np. 0 dla INT).
* Wartosc zmiennej. Zobacz "Interpretowanie typow" ponizej.

* `X rt_stack slots in use`: Naglowek wskazujacy liczbe uzywanych stosow aktywacji.
* Kolejne linie opisuja X `stack Vars`. Cokolwiek to jest.
* Informacje o aktywacji.
* Wartosc rejestru `temp` maszyny wirtualnej.
* Typ zmiennej. (np. 6 dla NONE)
* Wartosc zmiennej. UWAGA: jesli typ to 5 lub 6 (pusty lub none), nie wystapi tu zadna wartosc. Zobacz "Interpretowanie typow".

Trzy liczby oddzielone spacja:

* Licznik programu aktywacji.
* Licznik programu funkcji wbudowanej aktywacji.
* Licznik programu bledu aktywacji.

OPCJONALNIE: jesli druga z powyzszych liczb (licznik programu funkcji wbudowanej) nie wynosi 0, ta linia bedzie zawierac nazwe funkcji wbudowanej. (np. `eval`)

OPCJONALNIE: jesli licznik programu funkcji wbudowanej jest prawdziwy i istnieja dane funkcji wbudowanej, znajda sie tutaj.

Faktycznie zapisane dane zaleza od konkretnej funkcji. By dowiedziec sie, jakie dane zapisuje dana funkcja tutaj, poszukaj `register_function_with_read_write` w zrodlach serwera, znajdz swoja funkcje wbudowana MOO, znajdz jej funkcje zapisu w C (6. argument `register_function_with_read_write`) i przeczytaj kod zrodlowy tam.

## Aktywacja

* Zmienna-atrapa, ktora zawsze ma wartosc -111.
* Wartosc this.
* Obiekt, na ktorym zdefiniowany jest czasownik wywolujacy. (Czasownik wywolujacy to czasownik, ktory wywolal fork())
* Tryb watkowania sforkowanego zadania. To 1, jesli watkowanie jest wlaczone, lub 0, jesli jest wylaczone.

Dziewiec liczb oddzielonych spacjami:

* Numer obiektu "odbiorcy" (receiver) czasownika. W przypadku wywolan czasownikow na wartosciach prymitywnych (np. `"toast":explode()`), bedzie to numer obiektu obslugi dla wartosci prymitywnej (np. `$str_proto`). W przeciwnym razie jest to wartosc this.
* Wartosc-atrapa -7.
* Wartosc-atrapa -8.
* Numer obiektu gracza, ktory wywolal czasownik.
* Wartosc-atrapa -9.
* Numer obiektu programisty czasownika.
* Numer obiektu, na ktorym zdefiniowany jest czasownik.
* Wartosc-atrapa -10.
* Stan flagi debug.
* Slowo `No`
* Slowo `More`
* Slowo `Parse`
* Slowo `Infos`
* Lancuch znakow wskazujacy nazwe czasownika, pod jaka zostal wywolany przez gracza. To to samo, co zmienna verb. (np. `shr`, jesli wpisales to, by wywolac czasownik `shr*iek`)
* Lancuch znakow wskazujacy pelna nazwe czasownika. (np. `shr*iek`)

## Flagi obiektu

Liczba calkowita flag obiektu jest uzyskiwana przez zsumowanie jednej lub wiecej wartosci z tej tabeli:

| # | Wartosc | Flaga |
| - | ------- | ----- |
| 0 | 1 | Player |
| 1 | 2 | Programmer |
| 2 | 4 | Wizard |
| 3 | 8 | Obsolete |
| 4 | 16 | Read |
| 5 | 32 | Write |
| 6 | 64 | Obsolete |
| 7 | 128 | Fertile |
| 8 | 256 | Anonymous |
| 9 | 512 | Invalid |
| 10 | 1024 | Recycled |

Na przyklad: jesli chcesz, by obiekt byl graczem, programista i czarodziejem, sumujesz wartosci z kolumny "Wartosc" dla kazdej z nich: 1 + 2 + 4, co daje w sumie 7.

Jesli probujesz rozszyfrowac flage, jest to nieco bardziej skomplikowane. Bez wchodzenia zbyt gleboko w bity, mozesz to osiagnac za pomoca evala MOO. Zamiast patrzec na kolumne "Wartosc", spojrz na kolumne "#". Nasz eval bedzie brzmial: `FLAG &. (1 << #) != 0`

Powiedzmy, ze mamy obiekt z flaga 7. By sprawdzic, czy ten obiekt jest czarodziejem (# 2 w tabeli), podstawiamy do naszego evala: `7 &. (1 << 2) != 0`

Jesli zwroci 1, obiekt ma te flage. W naszym przypadku, tak, jest czarodziejem! Pamietaj tylko, by uzywac liczby z kolumny "#", a nie "Wartosc".

## Flagi uprawnien czasownika

Uprawnienia czasownika sa uzyskiwane przez zsumowanie jednej lub wiecej wartosci z tej tabeli:

| # | Wartosc | Flaga |
| - | ------- | ----- |
| 0 | 1 | Readable (+r) |
| 1 | 2 | Writable (+w) |
| 2 | 4 | Executable (+x) |
| 3 | 8 | Debug (+d) |

Co dosc dziwne, dobj i iobj sa rowniez czescia flag uprawnien czasownika:

| # | Wartosc | Flaga |
| - | ------- | ----- |
| 4 | 16 | dobj = any |
| 5 | 32 | dobj = this |
| 6 | 64 | iobj = any |
| 7 | 128 | iobj = this |

Na przyklad: jesli chcesz, by czasownik byl czytelny (+r) i debug (+d) z argumentami {"any", "out of/from inside/from", "this"}, sumujesz wartosci z kolumny "Wartosc" dla kazdej z nich: 1 + 8 + 16 + 128, co daje w sumie 153.

Jesli probujesz rozszyfrowac flage, jest to nieco bardziej skomplikowane. Bez wchodzenia zbyt gleboko w bity, mozesz to osiagnac za pomoca evala MOO. Zamiast patrzec na kolumne "Wartosc", spojrz na kolumne "#". Nasz eval bedzie brzmial: `FLAG &. (1 << #) != 0`

Wiec jesli masz flagi uprawnien o wartosci 9, mozesz sprawdzic, czy jest zapisywalny (writable), podstawiajac do naszego evala: `9 &. (1 << 1) != 0`

Jesli zwroci 1, dany bit uprawnien jest ustawiony. W tym przypadku, nie, nie jest zapisywalny!

## Flagi przyimkow czasownika

Flaga przyimka to po prostu liczba odpowiadajaca wartosci. Standardowe przyimki sa wymienione tutaj. Jesli twoj serwer jest osobliwy i dodaje wiecej, znajdziesz je w `db_verbs.cc`

| Wartosc | Przyimek |
| ------- | -------- |
| -2 | any |
| -1 | none |
| 0 | with/using |
| 1 | at/to |
| 2 | in front of |
| 3 | in/inside/into |
| 4 | on top of/on/onto/upon |
| 5 | out of/from inside/from |
| 6 | over |
| 7 | through |
| 8 | under/underneath/beneath |
| 9 | behind |
| 10 | beside |
| 11 | for/about |
| 12 | is |
| 13 | as |
| 14 | off/off of |

## Flagi uprawnien wlasciwosci

| # | Wartosc | Flaga |
| - | ------- | ----- |
| 0 | 1 | Readable (+r) |
| 1 | 2 | Writable (+w) |
| 2 | 4 | Chown (+c) |

Na przyklad: jesli chcesz, by wlasciwosc byla czytelna (+r) i zapisywalna (+w), sumujesz wartosci z kolumny "Wartosc" dla kazdej z nich: 1 + 2, co daje w sumie 3.

Jesli probujesz rozszyfrowac flage, jest to nieco bardziej skomplikowane. Bez wchodzenia zbyt gleboko w bity, mozesz to osiagnac za pomoca evala MOO. Zamiast patrzec na kolumne "Wartosc", spojrz na kolumne "#". Nasz eval bedzie brzmial: `FLAG &. (1 << #) != 0`

Powiedzmy, ze mamy wlasciwosc z flaga 7. By sprawdzic, czy ta wlasciwosc jest zapisywalna, podstawiamy do naszego evala: `7 &. (1 << 1) != 0`

Jesli zwroci 1, wlasciwosc ma te flage. W naszym przypadku, tak, jest zapisywalna! Pamietaj tylko, by uzywac liczby z kolumny "#", a nie "Wartosc".

## Interpretowanie typow

### CLEAR

Liczbowa wartosc typu: 5

### NONE

Liczbowa wartosc typu: 6

### STRING

Liczbowa wartosc typu: 2

Lancuch znakow.

Przyklad:

```
"Hello world!"

2
Hello world!
```

### OBJECT

Liczbowa wartosc typu: 1

Numer obiektu jako liczba calkowita. (UWAGA: nie zawiera znaku funta.)

Przyklad:

```
#2

1
2
```

### ERROR

Liczbowa wartosc typu: 3

Liczba calkowita reprezentujaca wartosc bledu. Zobacz tabele ponizej.

| Liczba calkowita | Blad |
| ----------------- | ---- |
| 0 | E_NONE |
| 1 | E_TYPE |
| 2 | E_DIV |
| 3 | E_PERM |
| 4 | E_PROPNF |
| 5 | E_VERBNF |
| 6 | E_VARNF |
| 7 | E_INVIND |
| 8 | E_RECMOVE |
| 9 | E_MAXREC |
| 10 | E_RANGE |
| 11 | E_ARGS |
| 12 | E_NACC |
| 13 | E_INVARG |
| 14 | E_QUOTA |
| 15 | E_FLOAT |
| 16 | E_FILE |
| 17 | E_EXEC |
| 18 | E_INTRPT |

Przyklad:

```
E_ARGS

3
11
```

### INTEGER

Liczbowa wartosc typu: 0

Liczba calkowita.

Przyklad:

```
123

0
123
```

### BOOL

Liczbowa wartosc typu: 14

1, jesli prawda, 0, jesli falsz.

### CATCH

Liczbowa wartosc typu: 7

Liczba calkowita.

### FINALLY

Liczbowa wartosc typu: 8

Liczba calkowita.

### FLOAT

Liczbowa wartosc typu: 9

Liczba zmiennoprzecinkowa.

Przyklad:

```
123.45

9
123.45
```

### MAP

Liczbowa wartosc typu: 10

Liczba kluczy w mapie.

Dla kazdego klucza w mapie...

* Klucz mapy
* Wartosc mapy. UWAGA: to moze byc dowolny typ, wiec musisz ustalic typ na podstawie pierwszej liczby, a nastepnie odwolac sie do sekcji "Interpretowanie typow".

Przyklad:

```
["source" -> #123, "time" -> 1670634392]

10
2
2
source
1
123
2
time
0
1670634392
```

### LIST

Liczbowa wartosc typu: 4

Liczba elementow na liscie.

Jesli lista nie jest pusta, wartosci kazdego elementu listy. UWAGA: te elementy moga byc dowolnego typu, wiec musisz ustalic typ kazdego elementu na podstawie pierwszej liczby i odwolac sie do sekcji "Interpretowanie typow".

Przyklad:

```
{#2, "Hey, that's wizard!", 2, 2.22, {"A list in a list, oh NO!"}}

4
5
1
2
2
Hey, that's wizard!
0
2
9
2.22
4
1
2
A list in a list, oh NO!
```

### ANON

Liczbowa wartosc typu: 12

Referencja liczbowa.

Jesli obiekt anonimowy nie zostal jeszcze zapisany, otrzymuje nowy numer obiektu. Numery obiektow anonimowych moga byc przypisywane obiektom zrecyklingowanym lub, jesli zaden nie jest dostepny, sa tworzone po ostatnim rzeczywistym obiekcie (`max_object()` + 1).

Jesli obiekt anonimowy odwoluje sie do obiektu anonimowego, ktory zostal juz zapisany, numer bedzie zgodny z oryginalnym anonem.

Podczas szukania wartosci wlasciwosci na obiektach anonimowych musisz szukac obiektu utworzonego w tym kroku. Pojawi sie on na standardowej liscie obiektow jak kazdy inny obiekt.

Przyklad:

```
*anonymous*

12
5
```

### WAIF

Liczbowa wartosc typu: 13

Jesli waif jest referencja do istniejacego waifa:

* Lancuch znakow zaczynajacy sie od r i konczacy liczbowa referencja do waifa w indeksie waifow.
* Pojedyncza kropka (.)

Jesli waif jest nowy:

* Lancuch znakow zaczynajacy sie od c i konczacy liczbowa referencja do waifa w indeksie waifow.
* Klasa waifa (liczba calkowita)
* Wlasciciel waifa (liczba calkowita)
* Liczba wlasciwosci, ktore mozna ustawic na tym waifie. To calkowita liczba wlasciwosci instancji (tych zaczynajacych sie od :) na klasie waifa i wszystkich przodkach tej klasy.
* Wartosci kazdej niepustej wlasciwosci ustawionej na instancji waifa. Dla kazdej wlasciwosci:

  * Liczba calkowita definiujaca indeks wlasciwosci w mapie wlasciwosci. Wlasciwosci sa liczone od 0, zaczynajac od wlasciwosci na klasie i schodzac w dol drzewa rodowego.
  * Wartosc wlasciwosci. UWAGA: to moze byc dowolny typ MOO. Musisz uzyc pierwszej liczby, by ustalic typ, a nastepnie odwolac sie do sekcji "Interpretowanie typow".

* Liczba -1
* Pojedyncza kropka (.)

Przyklad:

Mamy dwie klasy waif:

* #4: Waifilicious z jedna wlasciwoscia: :flavor
* #5: Waiftastic z jedna wlasciwoscia: :activity

Waif #5 jest dzieckiem waifa #4. Nasz waif jest instancja #5 z wlasciwoscia .flavor ustawiona na "toast":

```
[[class = #5, owner = #2]]

13
c 0
5
2
2
1
2
toast
-1
.
```

---

Ostatnia aktualizacja: 2022-12-15 dla wersji bazy danych 17.

Poprawki? Komentarze? Wybuchy irracjonalnej nienawisci? Skontaktuj sie ze mna: lisdude@lisdude.com
