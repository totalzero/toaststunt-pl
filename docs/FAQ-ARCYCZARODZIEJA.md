# FAQ Arcyczarodzieja (Newbie Wizards FAQ)

*Polskie tlumaczenie dokumentu ["Newbie Wizards FAQ"](https://lisdude.com/moo/new-archwiz-faq.html), oryginalnie napisanego przez kcary@pepperdine.edu okolo 1998 roku i od tego czasu niezmienianego. Jest linkowany z Podrecznika Programisty ToastStunt jako material zrodlowy.*

*Uwaga tlumacza: ten dokument jest silnie osadzony w historii -- odwoluje sie do konkretnych, datowanych wersji bazy LambdaCore (21-Oct-93, 1-Oct-94), do listy mailingowej moo-cows i do serwera LambdaMOO sprzed dekad. Wiele odpowiedzi (numery linii w konkretnych czasownikach, konkretne bledy w konkretnych wersjach rdzenia) moze nie miec juz zastosowania do wspolczesnej bazy `toastcore.db` uzywanej w tym forku -- zachowano je ze wzgledow historycznych i edukacyjnych (np. jako przyklady typowych pulapek przy budowie MOO), a nie jako gotowa instrukcje do zastosowania "na zywca".*

## Spis tresci

1.1 - [Wstep](#11-wstep)
1.2 - [Ile w ogole musze wiedziec o programowaniu w MOO, by prowadzic wlasne MOO?](#12-ile-w-ogole-musze-wiedziec-o-programowaniu-w-moo-by-prowadzic-wlasne-moo)
1.3 - [Wlasnie uruchomilem serwer MOO, co teraz?](#13-wlasnie-uruchomilem-serwer-moo-co-teraz)
1.4 - [Jak zrobic...?](#14-jak-zrobic)
1.5 - [Jak ograniczyc tworzenie nowych postaci do polecenia @make-player?](#15-jak-ograniczyc-tworzenie-nowych-postaci-do-polecenia-make-player)
1.6 - [Jak edytowac ekran powitalny?](#16-jak-edytowac-ekran-powitalny)
1.7 - [Dlaczego poczta do internetu zawodzi przy tworzeniu postaci?](#17-dlaczego-poczta-do-internetu-zawodzi-przy-tworzeniu-postaci)
1.8 - [O co chodzi z @make-player? Gdy probuje dodac aliasy, sklejaja sie w dlugie imie bez aliasow](#18-o-co-chodzi-z-make-player-gdy-probuje-dodac-aliasy-sklejaja-sie-w-dlugie-imie-bez-aliasow)
1.9 - [O co chodzi z @make-player? Nie ma pomocy](#19-o-co-chodzi-z-make-player-nie-ma-pomocy)
1.10 - [Jak zrobic zaufanego gracza czarodziejem?](#110-jak-zrobic-zaufanego-gracza-czarodziejem)
1.11 - [Dlaczego nikt nie moze polaczyc sie jako gosc?](#111-dlaczego-nikt-nie-moze-polaczyc-sie-jako-gosc)
1.12 - [Co nowy Arcyczarodziej powinien wiedziec o uprawnieniach/bezpieczenstwie?](#112-co-nowy-arcyczarodziej-powinien-wiedziec-o-uprawnieniachbezpieczenstwie)
1.13 - [Nikomu nie zmienia sie data rozlaczenia, co jest grane?](#113-nikomu-nie-zmienia-sie-data-rozlaczenia-co-jest-grane)
1.14 - [LambdaCore jest strasznie ubogi. Jak zdobyc inne obiekty i funkcje systemowe bez pisania ich od zera?](#114-lambdacore-jest-strasznie-ubogi-jak-zdobyc-inne-obiekty-i-funkcje-systemowe-bez-pisania-ich-od-zera)
1.15 - [Zrzucilem ten obiekt, ale ma kilkaset wlasciwosci z numerami obiektow ze zrodlowego MOO. Jak sie ich pozbyc?](#115-zrzucilem-ten-obiekt-ale-ma-kilkaset-wlasciwosci-z-numerami-obiektow-ze-zrodlowego-moo-jak-sie-ich-pozbyc)
1.16 - [Moj klient rozwala mi skrypt @dump przy wgrywaniu, wstawiajac zlamania linii tam, gdzie nie powinien. Co robic?](#116-moj-klient-rozwala-mi-skrypt-dump-przy-wgrywaniu-wstawiajac-zlamania-linii-tam-gdzie-nie-powinien-co-robic)
1.17 - [Jak zrobic, by wszyscy nowi gracze byli dziecmi okreslonej klasy gracza?](#117-jak-zrobic-by-wszyscy-nowi-gracze-byli-dziecmi-okreslonej-klasy-gracza)
1.18 - [Dlaczego dostaje range error w linii 3 #15:length_date_gt, uzywanym przez polecenia takie jak @subscribe?](#118-dlaczego-dostaje-range-error-w-linii-3-15length_date_gt-uzywanym-przez-polecenia-takie-jak-subscribe)
1.19 - [Probuje uzyc @mail-options +netmail i zawsze dostaje: Mail sending failed: 503 Need MAIL before RCPT. Co jest grane?](#119-probuje-uzyc-mail-options-netmail-i-zawsze-dostaje-mail-sending-failed-503-need-mail-before-rcpt-co-jest-grane)
1.20 - [O co chodzi z dziura bezpieczenstwa w my_huh?](#120-o-co-chodzi-z-dziura-bezpieczenstwa-w-my_huh)
1.21 - [Zawsze jest nowa wiadomosc w news. Co jest grane?](#121-zawsze-jest-nowa-wiadomosc-w-news-co-jest-grane)
1.22 - [Gdzie jest pomoc na temat $news? @examine-owalem go, ale nic nie dziala](#122-gdzie-jest-pomoc-na-temat-news-examine-owalem-go-ale-nic-nie-dziala)

2 - [Podziekowania i uwagi](#2-podziekowania-i-uwagi)

---

### 1.1 - Wstep

Ta lista FAQ ma na celu pomoc nowym arcyczarodziejom MOO (wlascicielom MOO) w znalezieniu odpowiedzi na ich pytania. Wpisy pochodza z listy mailingowej moo-cows, osobistych pytan z doswiadczenia na naszym MOO oraz od Waszych wkladow. Pytania na tej liscie odnosza sie najbardziej bezposrednio do rdzennej bazy danych, LambdaCore; w zakresie, w jakim baza, od ktorej zaczynasz, rozni sie od LambdaCore, odpowiedzi na te pytania moga sie roznic od tych przedstawionych tutaj.

Niektore ponizsze pozycje dotycza wylacznie LambdaCore z 21-Oct-93.

---

### 1.2 - Ile w ogole musze wiedziec o programowaniu w MOO, by prowadzic wlasne MOO?

Niektorzy odpowiedzieliby tak: jesli nie jestes programista z bogatym doswiadczeniem w MOO, tworzacym wlasne obiekty i pomagajacym innym naprawiac ich wlasne, powinienes naprawde zatrudnic, przekupic albo poslubic taka osobe, zanim postawisz wlasne MOO. Bedziesz potrzebowac tej osoby jako stalego partnera. Wiele rzeczy po prostu nie ma zadnej dokumentacji poza samym kodem MOO. Nie ma duzych szans na uzyskanie calej potrzebnej pomocy z jakiejkolwiek listy mailingowej.

---

### 1.3 - Wlasnie uruchomilem serwer MOO, co teraz?

Polacz sie telnetem z serwerem na porcie, na ktorym go uruchomiles (przeczytales dolaczona dokumentacje o uruchamianiu serwera, prawda? Uzyles dolaczonego skryptu restart, prawda?).

Powinienes teraz zobaczyc:

```
Trying...
Connected to SERVER
Escape character is '^]'.
Welcome to the LambdaCore database.

Type 'connect wizard' to log in.
```

Prawdopodobnie zechcesz zmienic ten tekst, ktory jest przechowywany w `$login.welcome_message`.

Wpiszesz wiec "connect wizard" i zobaczysz:

```
*** Connected ***
The First Room
This is all there is right now.
You see a newspaper here.
```

W tym momencie mozesz zrobic niemal wszystko. Najpierw zechcesz ustawic haslo czarodzieja (`help @password`). Potem mozesz wpisac

```
@display $login.
help $login
```

by zobaczyc inne wlasciwosci, ktore mozesz zechciec ustawic od razu.

---

### 1.4 - Jak zrobic...?

Czekaj! Czytales instrukcje? Nastepujace polecenia sa bardzo przydatne:

`help wiz-index`

[zawiera wszystkie aktualnie istniejace tematy pomocy dla czarodziei]

`help core-index`

[zawiera wszystkie aktualnie istniejace tematy pomocy o roznych obiektach rdzennych]

`help $login`

[opowie ci o wiadomosciach powitalnych, czarnych i czerwonych listach, wlaczaniu automatycznego tworzenia postaci (pozwalajacego, by logowania od razu tworzyly graczy, patrz nizej)]

---

### 1.5 - Jak ograniczyc tworzenie nowych postaci do polecenia @make-player? (tj. zapobiec `create <nazwa_gracza> <haslo>` z ekranu logowania?)

```
@set $login.create_enabled to 0
```

To powstrzymuje ludzi przed tworzeniem wlasnych postaci przy wiadomosci powitalnej. Jesli masz aktywna siec, domyslnie wyglada na to, ze ludzie nadal moga zalogowac sie jako gosc i stworzyc wlasna postac przez @request. Zhackowalismy czasownik @request, by to zmienic, ale to moze nie byc najlatwiejsze ani najlepsze rozwiazanie.

---

### 1.6 - Jak edytowac ekran powitalny?

Mozesz ustawic wiadomosc powitalna czyms w rodzaju:

```
@set $login.welcome_message to {"Welcome to...", "", "..."}
```

lub

```
@notedit $login.welcome_message
```

---

### 1.7 - Dlaczego poczta do internetu zawodzi przy tworzeniu postaci?

Upewnij sie, ze skompilowales serwer MOO z wlaczonymi "wychodzacymi polaczeniami sieciowymi" (w pliku options.h); moze byc tez konieczne:

```
@set $network.active to 1
```

Siec jest potrzebna, by serwer mogl automatycznie wyslac nowemu uzytkownikowi mailem jego imie postaci i haslo. Powinienes tez poprawnie ustawic wlasciwosci na $network dla swojego MOO.

---

### 1.8 - O co chodzi z @make-player? Gdy probuje dodac aliasy, sklejaja sie w dlugie imie bez aliasow.

Argument aliasow wydaje sie byc zepsuty w rdzeniu z 1-Oct-94. Dodaj aliasy pozniej. Aliasy dzialaja z tym poleceniem w poprzedniej wersji.

---

### 1.9 - O co chodzi z @make-player? Nie ma pomocy.

[Ponizsza pomoc pochodzi z bazy pomocy na LambdaMOO i jest nieaktualna w obecnym rdzeniu, ale nie masz jej, wiec by nie pytac, prawda?]

```
>help @make-player
Creates a player.

Syntax:  @make-player name[,aliases] [email-address [password]]

If no password is given, generates a random password for the player.

Email-address is stored in $registration_db and on the player object.

Comments can be added by specifying the email address "email@address comment"

Example:

@make-player George "sanford@frobozz.com George shares email with Fred Sanford (Fred #5461)"

If the email address is already in use, prompts for
confirmation. (Say no, this is a bug: it will break if you say
yes.) If you say no at one of the confirming prompts, character
is not made.

If network is enabled (via $network.active) then asks
if you want to mail the password to the user after character is
made.
```

[Od Judy Anderson, ktora napisala pomoc do tego na Lambda]

---

### 1.10 - Dobrze, potrzebuje tu pomocy. Jak zrobic zaufanego gracza czarodziejem?

Nie rob tego. Zamiast tego stworz swiezego gracza #p i zrob:

```
@chparent #p to $wiz
@programmer #p
;#p.wizard=1
```

a nastepnie podaj swojemu pomocnikowi haslo do nowego gracza. Alex Stewart zauwaza, ze dodanie wywolania @programmer pozwala uniknac pewnych klopotliwych sytuacji, na jakie mogliby natrafic czarodzieje niebedacy programistami.

Powod, dla ktorego naprawde chcesz to robic tylko na swiezo stworzonym graczu, jest taki, ze kazdy czasownik nalezacy do gracza nagle zyska uprawnienia czarodzieja. Dla istniejacego gracza musialbys przejrzec wszystko i upewnic sie, ze dany gracz nie jest wlascicielem zadnych czasownikow, ktore wyrzadza jakies szkody, jesli otrzymaja uprawnienia czarodzieja (pamietaj, kazdy moze wywolac dowolny czasownik...). [od Rogera Crewa]

---

### 1.11 - Dlaczego nikt nie moze polaczyc sie jako gosc?

Zrob

```
@make-guest <nazwa_gosc>
```

a nastepnie zedytuj opis. Tylko JEDNA z postaci gosci musi miec nazwe lub alias 'guest', by polaczenia jako gosc dzialaly. Sprobuj tak:

```
@add-alias guest to <numer# pierwszego stworzonego gosc>
```

Powtarzaj @make-guest <nazwa_gosc>, dodajac opisy w miare postepu, az uzyskasz liczbe gosci rowna pozadanej maksymalnej liczbie polaczen gosci.
