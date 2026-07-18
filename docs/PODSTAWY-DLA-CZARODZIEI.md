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

### Jestem polaczony z moim MOO, co powinienem zrobic najpierw?

Pierwsza rzecza, jaka powinienes zrobic, jest zmiana hasla czarodzieja.

Jak zauwazyles, nie potrzebowales go przy pierwszym polaczeniu. Jesli go nie zmienisz, kazdy moze polaczyc sie z tym loginem, a to moze sprowadzic klopoty...

```
;#2.password=crypt("nowe_haslo")
```

Jako ogolna zasada dla hasel, zwlaszcza tych dotyczacych postaci czarodziejow, wybierz takie, ktore nie jest slowem ze slownika i ma co najmniej osiem znakow, uzywajac wielkich liter i znakow takich jak !@#$%^&*() na przyklad. Bezpieczenstwo twojego MOO w duzej mierze zalezy od wyboru hasel.

Nadaj nazwe swojemu MOO!

```
@set $network.MOO_name to "Moje_MOO"
```

Ustaw poprawna nazwe domeny lub adres IP, z ktorego dziala twoje MOO:

```
@set $network.site to "moja_nazwa_domeny"
```

Jesli zdecydowales sie uzyc innego portu niz 7777 (zdefiniowanego w pliku options.h podczas kompilacji), dobrym pomyslem jest zaktualizowanie tego rowniez tutaj.

```
@set $network.port to twoj_numer
```

(nie uzywaj cudzyslowow dla powyzszego ustawienia portu).

To tez dobry moment, by sprawdzic:

```
help $login
```

Informacje tam zawarte beda przydatne, a takze omowione w kolejnych sekcjach.

### Chce zmienic ekran logowania... domyslny jest nudny.

Edytuj wlasciwosc $login.welcome_message:

```
@set $login.welcome_message to <twoja_wiadomosc>
```

<twoja_wiadomosc> musi byc lista:

```
{"Witamy w moim nowym MOO", "", "Wpisz connect guest, by polaczyc sie jako
gosc, albo uzyj: connect nazwa_gracza haslo", "", "Milej zabawy!"}
```

Jesli twoja wiadomosc jest dosc dluga i czujesz, ze powyzsza metoda jest barbarzynska, uzyj edytora notatek:

```
@notedit $login.welcome_message
```

(Upewnij sie, ze wiesz, jak uzywac @notedit! Za pierwszym razem, gdy go uzylem, utknalem w edytorze na wiele godzin...)

### Chce stworzyc goscie.

By stworzyc goscia, uzyj: @make-guest

```
@make-guest Poirot
```

Jak sugeruje pomoc @make-guest, dodaj alias guest do swojego pierwszego goscia (lub dowolnego innego).

Jesli numer obiektu twojego pierwszego goscia to #95, uzyj:

```
@add-alias guest to #95
```

### Jak dziala tworzenie graczy?

Domyslnie kazdy moze stworzyc gracza z ekranu logowania. Skladnia jest nastepujaca:

```
create <nazwa_gracza> <haslo>
```

Problemem z ta opcja jest to, ze wlasciwosc .email_address pozostaje pusta. Sugerowalbym wylaczenie tej opcji i zmuszenie goscinnych graczy do uzycia @request lub innego systemu, ktory wolisz i ktory ustawisz na swoim MOO.

```
@set $login.create_enabled to 0
```

Wylaczajac te opcje, uzytkownik otrzyma zawartosc $login.registration_string przy probie stworzenia postaci z ekranu logowania. Dlatego mozesz zechciec zedytowac ten lancuch, wskazujac uzytkownikowi procedure, jaka wybierzesz do tworzenia konta:

```
@set $login.registration_enable to "jakakolwiek metoda jest lepsza, uzyj
jej!"
```

Mozliwe jest jeszcze bardziej dostosowanie wiadomosci $login.registration_enable, ustawiajac $login.registration_address. Ta wlasciwosc bedzie zawierac adres e-mail do kontaktu w celu uzyskania konta gracza (jesli zdecydujesz sie uzyc tej opcji do tworzenia graczy). Dlatego zedytuj ja najpierw:

```
@set $login.registration_address to "ktos@tworzeniegraczy.edu"
```

I zedytuj $login.registration_enable odpowiednio:

```
@set $login.registration_enable to "Prosze skontaktowac sie z %e, by
uzyskac gracza, albo polacz sie jako gosc i uzyj @request (lub inaczej!)"
```

(%e zostanie zastapione przez $login.registration_address).

Dobrym pomyslem jest zdefiniowanie $login.registration_address tak czy inaczej, poniewaz to ten adres e-mail zostanie zaproponowany przez @request, jesli wystapia problemy w trakcie procesu.

Teraz @request jest wciaz opcja dla goscia, by poprosic o konto gracza.

Ta procedura bedzie uzywac wielu wlasciwosci na $network, a takze opcji uzycia mozliwej funkcji OUTBOUNDED.

Zalozmy, ze ja wlaczyles (jak wiekszosc ludzi zwykle robi); jesli nie, nie ma sie czym martwic i nie dotyczy cie to, co nastepuje.

Pierwsza rzecza do wlaczenia jest $network.active. Domyslnie jej wartosc to 0. By ja wlaczyc, wpisz:

```
@set $network.active to 1
```

W tym momencie MOO uzyje serwera SMTP maszyny, na ktorej dziala serwer. Dlatego musisz sie upewnic, ze uzytkownik, pod ktorym dziala serwer MOO, ma dostep do tej uslugi.

Jesli wolisz uzyc SMTP innego serwera, zedytuj $network.maildrop

```
@set $network.maildrop to "serwer_SMTP"
```

Ta wlasciwosc moze zawierac albo nazwe domeny, albo adres IP. Musisz sie jednak upewnic, ze SMTP przekazuje dalej (relay) e-maile pochodzace z twojej maszyny. Dzisiaj, przy calym biznesie odbywajacym sie przez e-mail, wiekszosc serwerow SMTP domyslnie NIE przekazuje dalej.

Dobrym pomyslem byloby teraz ustawienie adresow e-mail uzywanych w przypadku zwracanych wiadomosci lub innych problemow, jakie moga wystapic:

Nie znam szczegolow wszystkich tych roznych wlasciwosci, wiec po prostu ustawilem je wszystkie. Wpisz prawidlowy adres e-mail w nastepujacych wlasciwosciach:

```
$network.postmaster
$network.errors_to_address
$network.envelope_from
$network.usual_postmaster
$network.password_postmaster
```

Teraz, gdy mozesz juz tworzyc graczy, musisz sie zastanowic, ilu z nich zaakceptujesz jednoczesnie? Czy chcesz ustawic limit liczby polaczen? Rodzaj sprzetu, jaki masz (RAM), moze narzucac limit.

Domyslny limit jest ustawiony na 99999. Innymi slowy, nie ma limitu. Jesli czujesz, ze go potrzebujesz, zedytuj:

```
$login.max_connections
```

By powiadomic osoby, ktore chca sie polaczyc, ale zostana wyrzucone z powodu tego limitu, zedytuj:

```
$login.connection_limit_msg
```

Zauwaz, ze konta czarodziejow nie podlegaja temu ograniczeniu, a $login.lag_exemptions pozwala dodac graczy niebedacych czarodziejami do listy.

### E-maile nie sa wysylane przy tworzeniu graczy!!

Kilka rzeczy, ktore mozesz sprawdzic:

Czy usunales /* i */ wokol

```
#define OUTBOUND_NETWORK
```

gdy edytowales options.h przed kompilacja serwera?

Czy poprawnie ustawiles $network.active?

```
@set $network.active to 1
```

Czy sprawdziles, ze masz dzialajaca usluge SMTP na serwerze, na ktorym zainstalowane jest twoje MOO?

Jesli nie i musisz polegac na innym serwerze, by uzyc SMTP, zedytuj odpowiednio $network.maildrop i odwolaj sie do drugiej czesci powyzszej sekcji po wiecej informacji.

### Jak powinienem uruchamiac baze danych? restart? moo?

Po skompilowaniu serwera MOO w katalogu roboczym powinny znajdowac sie 2 pliki wykonywalne:

```
moo
restart
```

Oba moga byc uzyte do uruchomienia bazy danych MOO, choc moo jest tak naprawde plikiem wykonywalnym, a restart to tylko skrypt. Zdecydowanie sugerowalbym przeczytanie pliku README dolaczonego do pakietu serwera, by uzyskac pelne wyjasnienie, jak mozna uzywac obu tych plikow.

Wierze, ze to naprawde od ciebie zalezy, jak chcesz to robic, ale zasadniczo skladnia wyglada tak:

```
./restart twojemoo
./restart twojemoo port
```

Port jest opcjonalny, ale sugerowalbym, by go i tak dodac. Jesli go nie podasz, uzyty zostanie ten z $network.port (czyli ten, ktory wybrales w options.h przed kompilacja). Jest wiec oczywiste, ze dzieki tej opcji mozesz nadpisac domyslny port, podajac inny, jesli przyjdzie ci na to ochota. Jesli to zrobisz, nie zapomnij odpowiednio zmodyfikowac #72.port przy polaczeniu, w przeciwnym razie moga sie zdarzyc dziwne rzeczy -- nie wiem...

```
./moo twojemoo.db twojenowemoo.db
./moo twojemoo.db twojenowemoo.db port
```

Tu ta sama historia z portem.

Zauwaz, ze uzywajac ./restart NIE potrzebujesz rozszerzenia .db, podczas gdy uzywajac ./moo -- POTRZEBUJESZ go.

Teraz z pewnoscia zechcesz miec zwiazany z tym plik logu; by to zrobic, dodaj -l:

```
./moo -l plik_logu.log twojemoo.db twojenowemoo.db port
```

-l moze byc uzyte zarowno z ./moo, jak i ./restart

ZDECYDOWANIE sugeruje sie, by NIE uzywac tej samej nazwy dla swojej bazy danych przy uzyciu ./moo!!!

twojemoo.db to twoja oryginalna baza danych, a twojenowemoo.db to ta, do ktorej checkpoint zrzuci kopie zapasowa.

Zauwaz tez, ze gdy uzywasz ./restart, zadanie jest automatycznie forkowane, a identyfikator zadania zostaje ci podany w prezencie (eeeh..:). Jednak jesli uzyjesz ./moo, twoja konsola utknie w tym miejscu (yyyargh!). To wlasnie chcesz, jesli jestes w trybie awaryjnym (uzywajac -e), ale przez wiekszosc czasu wolelibysmy miec wolne rece po uruchomieniu serwera MOO. By to osiagnac, dodaj & do swojej linii polecen.

```
./moo -l plik_logu.log twojemoo.db twojenowemoo.db port &
```

Zobacz nastepna sekcje o robieniu kopii zapasowej bazy danych po wiecej informacji o checkpointowaniu.

### Jak zapisywane jest moje MOO? jak zrobic jego kopie zapasowa?

Odwolaj sie do Podrecznika Programisty w sekcji o checkpointowaniu po pelny opis.

Glowna idea jest nastepujaca:

Co jakis czas serwer MOO zrobi kopie zapasowa twojego pliku bazy danych i zapisze ja do innego pliku.

Jesli uzyles ./restart, nowy plik bedzie mial te sama nazwe co twoja oryginalna baza danych, z dodanym rozszerzeniem .new (podobnie dla pliku logu).

Jesli uzyles ./moo, nowy plik zostanie zrzucony do tego, ktory podales; w przypadku poprzedniej sekcji byl to twojenowemoo.db

To dlatego chcesz uzywac innej nazwy, by jesli stanie sie cos dziwnego, wciaz miec pod reka swoj oryginalny plik.

Jak czesto to "co jakis czas" oznacza wystapienie zrzutu?

Mozesz to zrobic recznie w dowolnym momencie (z uprawnieniami czarodzieja), wpisujac:

```
@dump-database
```

Gdy wykonujesz @shutdown serwera, robi sie to automatycznie.

Zrzut wystepuje domyslnie co 3600 sekund (czyli co godzine); ale mozesz zmienic te wartosc, ktora jest przechowywana w #0.dump_interval

Zauwaz, ze proces zrzucania jest domyslnie forkowany, co jest dobra rzecza, jesli masz duza baze danych (mozesz to jednak zmienic w pliku options.h).

Jest tez mila, mala funkcja, ktora mozesz wlaczyc w pliku options.h, zwana

```
/* #define LOG_COMMANDS */
```

Jesli ja odkomentujesz, bedzie logowac wszystko, co jest wpisywane od ostatniego checkpointu. Gdy nastapi nowy checkpoint i zostanie zakonczony, ta czesc logu znika. Moze to byc przydatne, jesli twoj serwer ulegnie awarii z nieznanych powodow.

Teraz, jesli jestes neurotykiem kopii zapasowych (co jest dobra rzecza....;), mozesz tez uzyc cron, by zautomatyzowac wiecej kopii zapasowych. Upewnij sie tylko, ze uzytkownik, pod ktorym dzialasz, ma prawo uruchamiac crontab (niektore zapory sieciowe moga to ograniczac do roota)

### FUP nie kompiluje sie poprawnie, co jest grane?

W dokumentacji pakietu FUP pominieto pewien szczegol, co spowoduje blad podczas kompilacji serwera MOO. Jesli plik FUP.README nie zostal zaktualizowany, oto poprawka:

Zedytuj plik version.h i dodaj nastepujaca linie:

```
extern const char *FUP_version;
```

Podziekowania dla Billa Garretta i Gavina Lamberta za ich pomoc w tej sprawie.

Dostepna jest teraz kolejna wersja FUP (v 1.9). Pozwala na opcje fileinsert() i filecut() i mozna ja znalezc tutaj.

Kazdy zainteresowany napisaniem dla niej fup.dll jest bardzo mile widziany.

### Uzywam Mac OS X, czy kompiluje sie to tak samo jak dla UNIX-a?

Mozna znalezc wersje serwera na MAC-a na stronie zasobow MOO Fringe'a, jesli chodzi o MAC OS 8 lub 9.

Istnieje dobra dokumentacja napisana przez Jerry'ego o tym, jak skompilowac serwer MOO na OS X, ktora zostala zaktualizowana dla OS X 10.4.
