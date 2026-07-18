# Typ danych WAIF w MOO

*Polskie tlumaczenie dokumentu ["MOO WAIF Datatype"](http://ben.com/MOO/waif.html) autorstwa Bena Jacksona, tworcy typu WAIF. Ten nieformalny, historyczny opis Q&A tlumaczy geneze i motywacje stojace za typem WAIF; jest linkowany z Podrecznika Programisty ToastStunt jako material zrodlowy. Zobacz takze [Podrecznik Programisty WAIF](WAIF-PODRECZNIK-PROGRAMISTY.md) po bardziej formalny opis.*

Typ danych WAIF to lata dla serwera LambdaMOO. Dodaje obsluge nowego typu wartosci zwanego WAIF. Galaz WAIF w CVS na sf.net ma najnowszy kod i jest oparta na serwerze 1.8.2.

Kod zostal napisany przez Bena Jacksona.

## Czym jest WAIF?

To lekki obiekt. To wartosc, ktora mozesz przechowywac we wlasciwosci, zmiennej, wewnatrz LISTY lub innego WAIF-a.

**Co znaczy "lekki"?**

Mam na mysli, ze jest mniejszy rozmiarem (mierzonym w bajtach) niz zwykly obiekt i szybszy w tworzeniu oraz niszczeniu. Jest tez zliczany przez referencje, co znaczy, ze jest niszczony automatycznie, gdy przestaje byc uzywany.

**Co znaczy "mniejszy"?**

Na maszynie 32-bitowej, jak i386, najmniejszy mozliwy obiekt typu OBJ ma okolo 100 bajtow. W bazie danych wywodzacej sie z LambdaCore bylby to rozmiar dziecka $garbage (tj. Recyclable #1234). Typowy OBJ pochodzacy od #1 jest wiekszy, poniewaz dziedziczy wiecej wlasciwosci, okolo 176 bajtow.

W przeciwienstwie do tego, pusta LISTA to 16 bajtow (wedlug value_bytes({})), a pusty STRING to 9 bajtow. WAIF bez ustawionych wlasciwosci (dopoki klasa nie definiuje wiecej niz okolo 100 wlasciwosci) to 36 bajtow.

Poniewaz WAIF ma dwie wbudowane wlasciwosci typu OBJ, .class i .owner, mozna go porownac do LISTY {class, owner}, ktora ma 32 bajty.

Wiec WAIF jest calkiem maly.

Obiekty OBJ rosna o value_bytes(value) - value_bytes(0) dla kazdej wlasciwosci, ktora ustawisz (czyli kazdej wlasciwosci, ktora przestaje byc pusta (clear) i przyjmuje wlasna wartosc, odrebna od rodzica). LISTY i WAIF-y obie rosna o value_bytes(value) dla kazdego nowego elementu listy (w LISCIE) lub kazdej ustawionej wlasciwosci (w WAIF-ie). Wiec WAIF nigdy nie jest wiecej niz 4 bajty wiekszy niz LISTA przechowujaca te same wartosci, z tym ze WAIF-y nadaja kazdej wartosci nazwe (nazwe wlasciwosci), a LISTY nadaja im tylko numery.

**Co znaczy "szybszy"?**

Mam na mysli, ze tworzenie i niszczenie WAIF-ow jest szybsze niz OBJ-ow. Powinienem to zmierzyc, ale nigdy sie do tego nie zabralem (a wlasciwie zabralem sie lata temu i zapomnialem dokladnych wynikow). WAIF kosztuje mniej wiecej tyle co LISTA do zrobienia. Tworzenie obiektow (a bardziej prawdopodobnie, uzycie czasownika bazy danych, ktory wykonuje chparent() na obiekcie z $garbage za ciebie) jest drozsze. Uniewaznia tez pamiec podreczna wyszukiwania czasownikow.

Zasadniczo powinienes uwazac WAIF za cos, czego mozesz zrobic tysiace w czasowniku bez zastanowienia. Mozesz zrobic liste mailingowa z 1000 wiadomosciami, kazda jako WAIF (zamiast LISTY), ale prawdopodobnie nie uzylbys 1000 obiektow OBJ.

**Co znaczy "zliczany przez referencje"?**

Tworzysz i niszczysz obiekty OBJ jawnie, funkcjami wbudowanymi create() i recycle() (lub alokujesz je z puli, uzywajac czasownikow z rdzenia). Pozostaja, dopoki ich jawnie nie zniszczysz, bez wzgledu na to, co robisz.

Wszystkie inne typy uzywane w MOO (ktore wymagaja zaalokowanej pamieci) sa zliczane przez referencje. Niezaleznie od tego, jak je stworzysz, pozostaja, dopoki trzymasz je gdzies we wlasciwosci lub zmiennej, a nastepnie po cichu znikaja i nie mozesz ich odzyskac.

**Dlaczego/kiedy chcialbym uzywac WAIF-ow?**

Jak opisano powyzej, WAIF nigdy nie jest wiecej niz 4 bajty dluzszy niz LISTA z tymi samymi wartosciami. Ale masz ladne nazwy dla kazdej wartosci i sposob na wywolywanie czasownikow zwiazanych z funkcja listy. Po co pisac subj = message[1], skoro mozesz miec subj = message.subject?

Innymi slowy, uzywaj WAIF-a zawsze, gdy chcesz zebrac wartosci razem i nadac kazdej wartosci znaczaca nazwe zamiast tylko indeksu w LISCIE. WAIF-y sa idealne do zastapienia alist, gdzie zbior kluczy alist jest staly, poniewaz nadal mozesz odwolywac sie do kazdej wartosci po nazwie, ale musisz trzymac liste kluczy tylko w jednym miejscu.

**Dlaczego chcialbym miec WAIF-y na swoim serwerze?**

Jesli prowadzisz MOO deweloperskie, zwlaszcza z duza iloscia hackowania rdzenia, mozesz uznac WAIF-y za bardzo przydatne przy implementowaniu infrastruktury takiej jak wiadomosci, opcje graczy, funkcje, systemy wspolrzednych, serwery webowe, zastepcze parsery, systemy obiektow skladowych itp.

**Czy WAIF-y kiedykolwiek trafia do glownej galezi serwera?**

Jestem jednym z opiekunow serwera, wiec moge przynajmniej zagwarantowac, ze WAIF-y nie zostana zepsute przez nowe wersje serwera. Ale mimo ze maja niemal 3 lata, WAIF-y nie mialy tyle rozglosu, ile bym chcial, wiec prawdopodobnie nie trafia do glownej galezi serwera bez wiekszego odzewu od uzytkownikow.

**Jak zaczac uzywac WAIF-ow na moim serwerze?**

Bedziesz potrzebowac pewnych zmian w rdzeniu, by ulatwic manipulowanie wlasciwosciami WAIF-ow (ktore zaczynaja sie od :), zwlaszcza w $code_utils:parse_verbref, ktory musi wiedziec, ze lancuch taki jak foo.:bar to wlasciwosc :bar na foo, a nie czasownik bar na foo. Mozesz tez pobawic sie z :isa i valid() w zaleznosci od zastosowania. Rowniez, jesli chcesz przemycic je tam, gdzie normalnie ida obiekty OBJ (jak w pronoun_sub), moze byc konieczna zmiana miejsc z jawnym testowaniem typu typeof(x) == OBJ ? x.y | ... na proste probowanie z obsluga bledow: `x.y ! E_PROPNF, E_INVIND => ...`.

Zrob obiekt, ktory posluzy jako klasa WAIF-a. Mozesz zrobic specjalny korzenny WAIF, ktory bedzie rodzicem wszystkich klas WAIF dla wygody, i nazwac go $waif. Nie ma znaczenia, czyim dzieckiem jest ten obiekt, poniewaz WAIF-y, ktore z niego zrobisz, dziedzicza tylko wlasciwosci i czasowniki, ktorych nazwy zaczynaja sie od dwukropka (:).

Nowe WAIF-y sa tworzone tylko przez funkcje wbudowana new_waif(). Nie przyjmuje ona argumentow, poniewaz zawsze tworzy nowy WAIF z klasa rowna obiektowi, ktory wywoluje new_waif(). Wiec twoim pierwszym czasownikiem jest $waif:new:

```
1:  // CZARODZIEJSKI
2:  set_task_perms(caller_perms());
3:  w = new_waif();
4:  w:initialize(@args);
5:  return w;
```

Zauwazysz, ze linia 4 wywoluje czasownik na nowym WAIF-ie. Ze wzgledu na reguly tlumaczenia, uruchamia to czasownik $waif::initialize. To tylko dla wygody. Wersja, ktorej uzywam, nic nie robi, po prostu dokumentuje szablon dla tworcow klas WAIF do wykorzystania:

```
1:  // sprawdzenie uprawnien, ktorego prawdopodobnie chcesz:
2:  if (caller == this || caller == this.class)
3:    // pozwala na pass() i :new()
4:  else
5:    raise(E_PERM);
6:  endif
```

Zauwaz, jak w linii 2 zmienna THIS zawiera WAIF. By znalezc obiekt OBJ z tymi czasownikami, mozesz uzyc this.class.

Teraz mozesz zrobic dziecko $waif i wywolac child:new(), co zwroci WAIF z waif.class == child. Teraz zrob child.:wlasciwosci i child::czasowniki do uzycia na WAIF-ach, ktore z niego robisz.

**Jak zaczac uzywac WAIF-ow jako programista?**

Jesli twoj rdzen ma $waif, zrob jego dziecko. Dodaj do niego wlasciwosci takie jak:

```
> @create $waif named my waif class,class
> @prop class.:x 0
> @prop class.:y 0
> @prop me.tmp 0 ""
> #class
=> #1234
> ;me.tmp = #1234:new()
=> [[class = #1234, owner = #100]]
> ;me.tmp.x
=> 0
> ;me.tmp.x = 57
=> 57
> ;me.tmp.x
=> 57
> @verb class::length this none this rxd
> @prog class::length
> return sqrt(tofloat(this.x) ^ 2 + tofloat(this.y) ^ 2);
> ;me.tmp:length()
=> 57.0
> ;me.tmp.y = 91
=> 91
> ;me.tmp:length()
=> 107.377837564369
```

**Gdzie moge sie tym pobawic?**

Zwykle mam MOO deweloperskie postawione pod place.org:7777 z wolnym tworzeniem postaci, by sie tym pobawic. Albo mozesz mnie znalezc na Waterpoint, a nawet na YibMOO, ktore niedawno dodalo WAIF-y do swojego serwera.

## Wiecej informacji

Mozesz tez przeczytac moj oryginalny opis, ktory ma wiecej szczegolow porownujacych typy wartosci MOO i opisujacych tlumaczenie wlasciwosci/czasownikow.

## Przypis: Dlaczego OBJ-y rosna tak, jak rosna

OBJ zaczyna od listy z wystarczajaca liczba slotow, by pomiescic jedna wartosc dla kazdej wlasciwosci, ktora definiuje lub dziedziczy. Wiec mysl o zupelnie nowym OBJ jak o liscie {0, 0, 0, ...}. Gdy ustawiasz wartosc wlasciwosci, zastepujesz 0 inna wartoscia, wiec rozmiar rosnie tylko o value_bytes(value) - value_bytes(0).
