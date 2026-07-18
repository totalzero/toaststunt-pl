# Podstawy dla Czarodziei i Pomoc w Utrzymywaniu Wlasnego MOO

*Polskie tlumaczenie dokumentu ["Wizard Basics and Help On maintaining your own MOO"](https://lisdude.com/moo/wizbasics.html). Jest linkowany z Podrecznika Programisty ToastStunt jako material zrodlowy.*

*Uwaga tlumacza: dokument jest oparty na serwerze Lambda Server 1.8.1 i bazie LambdaCore z 6 stycznia 2000 roku, ostatnio aktualizowany 16 stycznia 2007 roku -- jest wiec silnie historyczny i skupiony na "goym" LambdaCore, a nie na ToastCore czy ToastStunt. Wiele odpowiedzi (nazwy plikow, sciezki kompilacji, konkretne wlasciwosci) moze byc nieaktualnych wzgledem tego forka -- zachowano je ze wzgledow historycznych i edukacyjnych, jako przyklad typowego watku pytan poczatkujacego czarodzieja, a nie jako scisla instrukcje do zastosowania na `toastcore.db`. Sekcja "Utility Objects - by Examples" ponizej byla w oryginale niedokonczonym szkicem (sama lista nazw funkcji bez tresci) -- zachowano to tak, jak jest w zrodle, zamiast dopisywac brakujaca tresc.*

Ten dokument jest oparty na serwerze Lambda Server w wersji 1.8.1 oraz najnowszej bazie danych LambdaCore (6 stycznia 2000).

Autorzy tego dokumentu (w chronologicznej kolejnosci wkladu):

Herve Collin, Judi Kirkpatrick, Lennie Irvin, Cynthia Haynes, Jan Rune Holmevik, Laura Kramarsky, Bradley Dilger, Claudijo Borovic oraz Alexandre Borgia

**Cel tego dokumentu:**

Zebrac jak najwiecej przydatnych informacji dla osob, ktore chca zaczac prowadzic wlasne MOO. Ten dokument sluzy jako uzupelnienie innych zrodel, takich jak New Archwiz (patrz nasze [tlumaczenie FAQ Arcyczarodzieja](FAQ-ARCYCZARODZIEJA.md)) oraz MOO-COWS FAQ, do ktorych zdecydowanie zaleca sie sie odwolywac. Wiele zagadnien z tamtych dokumentow jest tu rowniez poruszanych, a takze -- miejmy nadzieje -- wiele innych; jednak pozostaja one nieoficjalne.

Zawartosc tego dokumentu nie zostala zweryfikowana ani potwierdzona przez autorow ani opiekunow oficjalnego LambdaMOO. Dlatego korzystaj z niego na wlasne ryzyko.

Zauwaz tez, ze niektore dokumenty lub zasoby zostaly skopiowane (zmirrorowane) na tej stronie. Powodem jest mozliwa czasowa niedostepnosc niektorych stron cytowanych w tym dokumencie. Miej wiec na uwadze, ze moga byc nieaktualne. Zaleca sie odwolywac do nich tylko wtedy, gdy nie mozna znalezc potrzebnej informacji na stronach oficjalnych.

PROSIMY! Wnies swoj wklad do tego dokumentu!!: dodaj wiecej informacji, dodaj linki do innych przydatnych stron zwiazanych z MOO, popraw obecne bledy, uzupelnij konkretne sekcje, dodaj inne sekcje, zaproponuj kody MOO, ktore napisales. Wnies wszystko, co uwazasz za przydatne przy zarzadzaniu MOO jako czarodziej, albo zaproponuj lepszy sposob formatowania tego pliku pomocy. Wiele zagadnien i aspektow MOO jest dla mnie wciaz niejasnych lub calkowicie nieznanych; im wiecej osob wniesie wklad do tego projektu, tym bardziej przydatny bedzie ten dokument.

Aloha,

Jesli czujesz, ze jakis konkretny aspekt lub temat powinien pojawic sie w tym dokumencie, PROSZE, daj mi znac, a zbadam go/dodam.

## Spis tresci

**Zaczynamy**
* Gdzie znajde zrodla i dokumentacje?
* Czego potrzebuje, by zainstalowac MOO?
* Jak rozpakowac serwer i baze danych MOO?
* Jak skompilowac serwer MOO?
* Jak sprawic, by moje MOO obslugiwalo akcenty?
* Jak dodac nowe przyimki?
* Jak skompilowac MOO na komputerze z Windows?
* Moje MOO dziala! Jak sie z nim polaczyc?
* Jestem polaczony z moim MOO, co powinienem zrobic najpierw?
* Chce zmienic ekran logowania... domyslny jest nudny.
* Chce stworzyc goscie.
* Jak dziala tworzenie graczy?
* E-maile nie sa wysylane przy tworzeniu graczy!!
* Jak powinienem uruchamiac baze danych? restart? moo?
* Jak zapisywane jest moje MOO? jak zrobic jego kopie zapasowa?
* FUP nie kompiluje sie poprawnie, co jest grane?
* Uzywam Mac OS X, czy kompiluje sie tak samo jak dla UNIX-a?

**Utrzymywanie bazy danych**
* Jak sledzic tworzenie graczy?
* Jak sprawdzic, czy ludzie naprawde uzywaja swoich postaci?
* Jak tworzyc czarodziei?
* Jak tworzyc programistow?
* Limit czego, i jak nim zarzadzac?
* Musze zmienic haslo gracza...
* Jak tworzyc listy mailingowe?
* Jak ustawic domyslny pokoj polaczenia?
* Ojej, moja baza danych juz sie nie wczytuje przy restarcie... co teraz?
* Zgubilem haslo czarodzieja, jak je zmienic?

**Rozne wskazowki**
* Modyfikowanie wlasciwosci obiektow rdzennych.
* Pulapka @set (kontra @grant).
* Jak zablokowac moj pokoj dla kilku osob?
* Jak szybko uzyskac informacje o obiekcie?
* Jak ponownie uzyc zrecyklingowanych obiektow?
* Jak poznac numer obiektu ostatnio stworzonego obiektu?
* Jak stworzyc nowa pomoc (Help)?
* Problem match() ze znakami akcentowanymi

**Obiekty narzedziowe -- na przykladach**

W tej sekcji zastosujemy nastepujace podejscie: NA PRZYKLADZIE.

To jak z fizyka: 200 slow moze ladnie cos opisac, ale prosty wykres jest znacznie lepszy. Podsumujemy wiec wszystkie obiekty narzedziowe, ich czasowniki, co robia (informacje pochodzace bezposrednio z bazy danych LambdaMOO), i wypiszemy kilka przykladow pokazujacych, co mozna z nimi zrobic, by lepiej zrozumiec, o co chodzi, i jaki jest potencjal kazdego czasownika.

Lista przykladow nie jest wyczerpujaca. Jesli wpadniesz na inne, ktore pokazuja i ujawniaja glebsze aspekty, prosimy o wklad!!

$String_Utils

* $string_utils:from_list()
* $string_utils:english_list()
* $string_utils:title_list*c/list_title*c()
* $string_utils:from_value()
* $string_utils:print()
* $string_utils:abbreviated_value()
* $string_utils:to_value()
* $string_utils:prefix_to_value()
* $string_utils:english_number()
* $string_utils:english_ordinal()
* $string_utils:ordinal()
* $string_utils:group_number()
* $string_utils:from_ASCII()

*(Uwaga tlumacza: w tym miejscu urywa sie tresc tej sekcji w oryginale -- ponizsza lista nazw czasownikow nie ma w zrodlowym dokumencie towarzyszacych przykladow. Pozostawiono to bez zmian, jako wierny odzwierciedlenie stanu oryginalu.)*

---

### Gdzie znajde zrodla i dokumentacje?

Pierwszym miejscem do szukania pomocy jest system pomocy bazy danych MOO. Mozesz uzyskac do niego dostep, wpisujac nastepujace polecenia po polaczeniu z MOO:

```
help (ogolna pomoc MOO)
help full-index (polecenia MOO).
```

Potem mozesz zawezac wyszukiwanie, wpisujac help, a nastepnie albo podmenu (podane ci przez help), albo polecenie (podane ci przez help full-index).

Dalej nastepuje lista zewnetrznych zasobow (strona domowa MOO, MOO-Cows FAQ i archiwum listy mailingowej, oficjalny serwer FTP LambdaMOO, Podrecznik Programisty LambdaMOO, zasoby MOO Fringe'a, Encore i jego lista mailingowa, MOOprog, lista Super MOO Rachel, MOO Faq-o-Matic, Biblioteka Dokumentow MOO/MU*, przewodnik uzytkownika EnCore MOO) -- wszystkie to zewnetrzne strony sprzed dekad, czesc z nich moze juz nie dzialac; nie sa tu powtarzane pojedynczo, gdyz sa to wylacznie nazwy wlasne i adresy bez tresci do przetlumaczenia.

### Czego potrzebuje, by zainstalowac MOO?

Potrzebujesz 2 rzeczy:

- Serwera
- Bazy danych

Obie mozna znalezc na tej stronie, ale warto tez sprawdzic oficjalna strone (moo-cows). Serwer nazywa sie zazwyczaj: LambdaMOO-X.X.X.tar.gz (gdzie X odpowiada numerowi wersji), a baza danych zwykle nazywa sie: LambdaCore.*.db.gz

Jesli pobierzesz te pakiety w postaci skompresowanej (czyli maja na koncu gz lub Z), mozesz pobrac je w trybie binarnym.

Wszystko, co nastepuje, zaklada, ze uzywasz jakiejs odmiany *nix.

### Jak rozpakowac serwer i baze danych MOO?

Dla bazy danych uzyj:

```
gunzip LambdaCore*.db.gz
```

Upewnij sie, ze zastapiles * tym, co masz w nazwie pobranego pliku.

Dla serwera masz dwie opcje:

```
tar -xzvf LambdaMOO-X.X.X.tar.gz
```

lub

```
gunzip < LambdaMOO-X.X.X.tar.gz | tar xvf -
```

Po rozpakowaniu bazy danych zostaniesz z plikiem o nazwie:

```
LambdaCore*.db
```

(rozszerzenie .gz zniknelo)

Po rozpakowaniu (uncompress i untar) pliku serwera zostaniesz z katalogiem o nazwie:

```
MOO-X.X.X
```

To tutaj skompilujesz swoj serwer.

### Jak skompilowac serwer MOO?

RTFM (Read The Fantastic Manual)

Innymi slowy: PRZECZYTAJ plik README.

Wszystko jest tam szczegolowo wyjasnione. Wszystko, co moglibysmy tu zrobic, to zle to sparafrazowac; wiec tego nie zrobimy.

Jesli ktos ma pytania dotyczace czesci options.h, smialo je zadawaj, a sekcje na temat poszczegolnych parametrow options.h, ich znaczenia itd. moga zostac dodane.

### Jak sprawic, by moje MOO obslugiwalo akcenty?

To dobre pytanie, ktore warto sobie zadac PRZED skompilowaniem serwera...;)

Odwolaj sie do latki serwera napisanej przez Sindre Sorensena.

### Jak dodac nowe przyimki?

To pytanie jest tutaj, poniewaz dodanie przyimkow wymaga rekompilacji serwera.

Jesli chcesz dodac przyimki we wlasnym jezyku (lub jakimkolwiek innym), zhackuj plik db_verbs.c, szukajac `static const char *prep_list[]` gdzies w poblizu drugiego ekranu. Wszystko jest tam wyjasnione.

### Jak skompilowac MOO na komputerze z Windows?

Odwolaj sie do dokumentacji WINMOO.

Niektorzy znalezli dobra alternatywe w postaci CYGWIN, dzieki czemu moga trzymac sie wersji *nix serwera MOO (co jest oczywiscie zawsze przyjemniejsze).

Jesli ktos chce podzielic sie swoim doswiadczeniem z cygwin, byloby wspaniale.

### Moje MOO dziala! Jak sie z nim polaczyc?

Istnieje wiele sposobow, bracia i siostry...

Najlatwiejszym sposobem (na poczatek) jest aplikacja telnet.

Jesli masz system oparty na uniksie, wystarczy terminal. Dla systemu opartego na Windows istnieje takze aplikacja telnet.exe, ktora powinna byc dolaczona do pakietu. Na Macintoshach najczesciej uzywanym rozwiazaniem moze byc NCSA telnet, ale nie sadze, by byl dolaczony do systemu operacyjnego. Na najnowszych wersjach systemu MAC nie powinno to jednak byc potrzebne.

Pamietaj jednak, ze telnet jest najmniej przyjaznym sposobem laczenia sie z MOO. Warto poszukac alternatyw do laczenia sie z MOO, opisanych ponizej.

Drugim sposobem jest uzycie klienta MOO.

Klienci MOO oferuja najwiecej funkcji i elastycznosci podczas laczenia sie z MOO. To zazwyczaj wybor, jaki wybiera sie do programowania.

*(Uwaga tlumacza: oryginal wymienia tu obszerna, skategoryzowana wedlug systemu operacyjnego liste nazw klientow MOO/MUD/MUSH z lat 90./2000. -- Unix: AMCL, Crescendo, gMOO, Kmud, Mcl, Mmucl, Papaya, Powwow, RMC, SClient, SMM+, Tintin++, TinyFugue, TkMOO; Macintosh: Cantrip, Legend Weaver, MacMOOse, MacMUSH, Mud-Haven, MUD-wrestler, Mudling, MUDweller, Rapscallion, Savitar, TkMOO; Windows: BeipMU, DragonStone, ELFxWINSOCK, FireBolt, GMUD, JMC, LambdaMOO Builder, MuckClient, Monkey Term, Mud Master, Mush Client, Papaya, Phoca MU, Pueblo, RoaClient, SimpleMU, SMud, Tinkeri View, Tinyfugue, TkMOO, Trebuchet, VMOO, WinMOOSE, Wintin++, zMUD; a takze trzeci sposob polaczenia przez aplety Javy: MOOca, MOOtcan, Surf & Turf, Cup of Mud, Aloha. Sa to wylacznie nazwy wlasnego oprogramowania bez tresci do przetlumaczenia, a wiekszosc linkow do nich jest dzis martwa -- zachowano je tutaj w formie zbiorczej notatki zamiast reprodukowac oryginalna liste linia-po-linii. Pelna lista z linkami znajduje sie w oryginale.)*

Zwroc uwage, ze zadne z ponizszych oprogramowan nie zostalo przetestowane. Jesli ich uzywasz, robisz to na wlasne ryzyko.

Oprogramowanie niekomercyjne i komercyjne jest wymieniane bez rozroznienia. Popytaj o opinie na temat takiego czy innego oprogramowania i wyprobuj je. Twoje preferencje moga zalezec od tego, co chcesz z nimi robic (programowanie czy cos innego).
