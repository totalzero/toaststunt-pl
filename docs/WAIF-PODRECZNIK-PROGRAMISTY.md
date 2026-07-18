# Podrecznik Programisty WAIF

*Polskie tlumaczenie dokumentu ["WAIF Programmers' Manual"](http://ben.com/MOO/waif-progman.html) autorstwa Bena Jacksona, tworcy typu WAIF. Formalny opis typu danych WAIF, uzupelniajacy nieformalny [Typ danych WAIF w MOO](WAIF-DATATYPE.md). Zobacz takze rozdzial "Praca z WAIF-ami" w [Podreczniku Programisty ToastStunt](PODRECZNIK-PROGRAMISTY.md) po opis WAIF-ow w kontekscie samego ToastStunt.*

Napisalem tu kolejny opis.

Latki sa dostepne jako waif-0.95.tgz.

> UWAGA DLA UZYTKOWNIKOW MOO-1.8.1: Dwa fragmenty diff zostana odrzucone, jeden dla Makefile.in i jeden dla tasks.c. Musisz je scalic recznie. Obie to jednoliniowe zmiany. Najbardziej krytyczna jest zmiana w tasks.c, ktora nie uniemozliwi kompilacji, ale w koncu doprowadzi do paniki serwera.

Typ danych WAIF to lata dla serwera LambdaMOO. Galaz WAIF w CVS na sf.net ma najnowszy kod i jest oparta na serwerze 1.8.2.

## Wstep

Struktura obiektow MOO jest wyjatkowa w tym, ze wszystkie klasy sa instancjami, a wszystkie instancje sa (potencjalnie) klasami. Znaczy to, ze instancje niosa ze soba duzo bagazu, ktory jest przydatny tylko wtedy, gdy staja sie klasami. Ponadto kazdy obiekt przychodzi z zestawem wbudowanych wlasciwosci i atrybutow, ktore sluza glownie do budowania rzeczy VR. Moim pomyslem na lekki obiekt jest cos, co jest wylacznie instancja. Brakuje mu wielu rzeczy, ktore maja "prawdziwe obiekty MOO" w swojej roli klas i obiektow VR:

* nazw
* informacji o lokalizacji/zawartosci
* dzieci
* flag
* definicji czasownikow
* definicji wlasciwosci
* slabych referencji (?)
* jawnego niszczenia

Sprowadzony do sedna, WAIF ma nastepujace atrybuty:

* Klase (jak rodzic)
* Wlasciciela (informacje o uprawnieniach)
* Wartosci wlasciwosci

## Czym jest WAIF?

Wlasciwosci i zachowanie WAIF-a sa hybryda kilku istniejacych typow MOO. Warto je porownac:

* WAIF-y sa wartosciami zliczanymi przez referencje, jak LISTY. Po stworzeniu istnieja tak dlugo, jak sa przechowywane gdzies w zmiennej lub wlasciwosci. Gdy znika ostatnia referencja, WAIF jest niszczony bez ostrzezenia.
* Nie ma skladni do tworzenia literalu WAIF. Mozna je stworzyc tylko funkcja wbudowana.
* Nie ma skladni do odwolywania sie do istniejacego WAIF-a. Mozna uzyc go tylko przez dostep do wlasciwosci lub zmiennej, gdzie zostal zapisany.
* WAIF-y moga sie zmieniac, jak obiekty. Gdy zmieniasz WAIF-a, wszystkie referencje do niego zobacza te zmiane (jak OBJ, w odroznieniu od LISTY).
* Mozesz wywolywac czasowniki i odwolywac sie do wlasciwosci na WAIF-ach. Sa one dziedziczone z jego obiektu klasy (z mapowaniem opisanym ponizej).
* WAIF-y sa tanie w tworzeniu, mniej wiecej tyle, co LISTY.
* WAIF-y sa male. WAIF ze wszystkimi pustymi (clear) wlasciwosciami (jak zaraz po stworzeniu) jest tylko o kilka bajtow dluzszy niz LISTA wystarczajaco duza, by pomiescic {class, owner}. Jesli przypiszesz wartosc do wlasciwosci, rosnie o tyle samo, o ile roslaby LISTA, gdybys dodal do niej wartosc.
* Dostep do wlasciwosci WAIF-a jest kontrolowany tak jak dostep do wlasciwosci OBJ. Posiadanie referencji do WAIF-a nie znaczy, ze widzisz, co jest w srodku.
* WAIF-y nigdy nie moga definiowac nowych czasownikow ani wlasciwosci.
* WAIF-y nigdy nie moga miec zadnych dzieci.
* Obecnie WAIF-y nie moga zmienic klasy ani wlasciciela.
* Jedynymi wbudowanymi wlasciwosciami WAIF-a sa .owner i .class.
* WAIF-y nie uczestnicza w hierarchii .location/.contents, manipulowanej przez move(). Klasa WAIF-a moze jednak zdefiniowac te wlasciwosci (jak opisano ponizej).
* WAIF-y nie maja flag OBJ takich jak .r czy .wizard.

## Przestrzen nazw czasownikow/wlasciwosci WAIF-a

Aby oddzielic czasowniki i wlasciwosci zdefiniowane dla WAIF-ow danego obiektu, WAIF-y dziedzicza wylacznie czasowniki i wlasciwosci, ktorych nazwy zaczynaja sie od : (dwukropka). Innymi slowy, stosowane jest nastepujace mapowanie:

```
waif:czasownik(@args) staje sie
waif.class:(":"+czasownik)(@args)
```

Wewnatrz czasownika WAIF-a (dalej zwanego metoda) zmienna lokalna verb nie ma dodatkowego dwukropka. Wartoscia this jest sam WAIF (moze on ustalic, na jakim obiekcie sie znajduje, przez this.class). Jesli metoda wywoluje inny czasownik na WAIF-ie lub OBJ, caller bedzie WAIF-em.

```
waif.wlasciwosc jest zdefiniowana przez
waif.class.(":"+wlasciwosc)
```

Definicja wlasciwosci dostarcza flag wlasnosci i uprawnien dla wlasciwosci, a takze jej domyslnej wartosci, tak jak przy kazdym OBJ. Oczywiscie faktyczna wartosc wlasciwosci jest czescia samego WAIF-a i moze sie zmieniac przez cale zycie WAIF-a.

W przypadku wlasciwosci +c, za wlasciciela wlasciwosci uznaje sie wlasciciela WAIF-a.

## Przykladowy obiekt, $waif

Oto wyjscie @display dla szkieletowego $waif, plus kilka dodatkowych wlasciwosci dla przykladu:

```
root waif (#234) [ readable fertile ]
Child of root class (#1).
Location Ben (#2).
#234:new                      Ben (#2)             rxd
#234::initialize              Ben (#2)             rxd
.type                    Ben (#2)              r      10
.:example                Ben (#2)              r      "hello"
.:plusc                  Ben (#2)              r c    {1, 2, 3}
--------------------------- finished ----------------------------
```

Ten obiekt MOO definiuje 2 czasowniki i 3 wlasciwosci (i dziedziczy wiele innych, ktore tu po prostu ignorujemy). Definiuje czasownik new, taki jak czasowniki, ktore juz znasz. W tym przypadku tworzy nowy WAIF:

```
1:  set_task_perms(caller_perms());
2:  w = new_waif();
3:  w:initialize(@args);
4:  return w;
```

Funkcja wbudowana new_waif() tworzy nowy WAIF, ktorego klasa jest wywolujacy obiekt, a wlascicielem sa uprawnienia wywolujacego czasownika. Ta czarodziejska wersja sprawia, ze jest on wlasnoscia wywolujacego (caller) czasownika.

Gdy WAIF zostal juz utworzony, mozesz wywolywac na nim czasowniki. Zauwaz, jak WAIF dziedziczy $waif::initialize. Zauwaz, ze nie moze on odziedziczyc $waif:new, poniewaz nazwa tego czasownika nie zaczyna sie od dwukropka.

Nowo utworzony WAIF ma dwie wlasciwosci, jedna o nazwie example i jedna o nazwie plusc. Ich domyslne wartosci sa dziedziczone z obiektu. Wlasciwosc example jest +r i moze byc czytana przez kazdego, ale zapisac ja moze tylko Ben (#2). Trafnie nazwana wlasciwosc plusc jest +c i jest wlasnoscia wlasciciela WAIF-a (kimkolwiek jest wywolujacy $waif:new() w tym przykladzie).

Jest tez wlasciwosc $waif.type, ktora ma wartosc liczbowa zwracana przez typeof(new_waif()). To nie zmienia wyniku typeof(). To po prostu miejsce w bazie danych, by zawrzec stala, ktora bylaby zmienna WAIF (jak STR czy FLOAT), gdybym taka dodal. To po prostu zwykla wlasciwosc. Nic wiecej do zobaczenia.

Generyczny waif jest plodny ($waif.f == 1), by nowe klasy waif mogly byc z niego wywodzone. Plodnosc OBJ jest nieistotna przy tworzeniu WAIF-a. Zdolnosc do tego jest ograniczona do samego obiektu (poniewaz new_waif() zawsze zwraca WAIF z class=caller).

## Referencje do WAIF-ow

Nie ma formatu lancucha znakow dla WAIF-a. tostr() po prostu zwraca {waif}. toliteral() obecnie zwraca wiecej informacji, ale to tylko do celow debugowania. Nie ma towaif(). Jesli chcesz odwolac sie do WAIF-a, musisz odczytac go bezposrednio ze zmiennej lub wlasciwosci gdzies. Jesli nie mozesz go odczytac z wlasciwosci (lub wywolac czasownika, ktory go zwraca), nie masz do niego dostepu. Nie ma sposobu na skonstruowanie referencji do WAIF-a z innego typu.
