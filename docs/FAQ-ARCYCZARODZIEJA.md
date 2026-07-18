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

### 1.12 - Co nowy Arcyczarodziej powinien wiedziec o uprawnieniach/bezpieczenstwie?

Duzo. Na razie odsylamy do #34443 na LambdaMOO (lambda.moo.mud.org 8888). Albo mozesz przejrzec archiwum moo-cows, dostepne na MOO-Cows, w poszukiwaniu artykulu o nastepujacym tytule (czerwiec 1994):

`Newbie wiz FAQ: Permissions/security`

Oto kod, ktory mozesz wstawic do czasownika, by pomoc sobie znalezc zapisywalne czasowniki, ktore dzialaja z uprawnieniami czarodzieja (tj. czasownik, ktory kazdy moze zmodyfikowac, a ktory ma moc czarodzieja):

(mozna go nazwac np.: `"@seek*holes findholes"   none none none`)

```
count = 0;
wiz = "";
evil = " contains WWV";
for object in [1..tonum(max_object())]
$command_utils:suspend_if_needed(0, tostr(object, "..."));
object = toobj(object);
if (valid(object) && length(vrbs = verbs(object)) != 0)
for n in [1..length(vrbs)]
$command_utils:suspend_if_needed(0, tostr(object, "..."));
if (index(verb_info(object, tostr(n - 1))[2], "w") > 0)
count = count + 1;
if (verb_info(object, tostr(n - 1))[1].wizard == 1)
wiz = "WIZARDLY ";
else
wiz = "";
endif
player:tell(wiz, "Object ", tostr(object), evil, " ", vrbs[n]);
endif
endfor
endif
endfor
player:tell(count, " total.");
```

[wklad MudOp@ripco.com, zmodyfikowany przez Scotta Lyncha]

Dopoki naprawde nie zrozumiesz uprawnien, najlepiej robic cale swoje programowanie jako postac-programista.

---

### 1.13 - Nikomu nie zmienia sie data rozlaczenia, co jest grane?

(inaczej: nikt nie dostaje powiadomien mailowych, co jest nie tak?)

Wydaje sie, ze jest problem z czasownikami disfunc i confunc na #6, generycznym graczu w dystrybucji LambdaCore-21Oct93.db. By to naprawic, zrob @edit #6:disfunc, a takze #6:confunc, i zmien kazda linie 1 na to:

```
if (valid(caller_perms()) && caller != this && caller != #0)
```

Oczywiscie dziala to na pewno tylko dla powyzszej wersji bazy danych, i tylko jesli nie ruszales swoich czasownikow disfunc i confunc na tym obiekcie. Badz ostrozny.

---

### 1.14 - LambdaCore jest strasznie ubogi. Jak zdobyc inne obiekty i funkcje systemowe bez pisania ich od zera?

[Hmm. Coz, w tym sensie, ze nie masz pewnych funkcji systemowych (pogoda, system RPG, srodowisko dobowe itd.) ani obiektow (gadajace roboty, zmiennoksztaltna klasa gracza itd.), ktore widziales na ustabilizowanych MOO, przypuszczam, ze LambdaCore mozna nazwac ubogim. LambdaCore jest w rzeczywistosci calkiem kompletna podstawa do kodowania MOO, z MNOSTWEM podstawowych niezbednosci, ktorych kodowanie samemu nudziloby i frustrowaloby niejedna osobe do lez. W miare jak pojawia sie wiecej pochodnych LambdaCore, wymienie je tutaj. OK, dosc redakcyjnego komentarza, do rzeczy. -red.]

Zalecana procedura portowania obiektow ma obecnie dwa elementy: spoleczny i techniczny.

**Spoleczny**: sa tu w gre kwestie praw autorskich i uprzejmosci zwiazane z portowaniem cudzego kodu na twoje MOO. Praktyczna rada wynikajaca z tych rozwazan wyglada tak:

* Jesli obiekt/kod wyraznie stwierdza, ze mozesz go kopiowac, lub uzyskales pozwolenie autora, portuj go.
* Jesli nie, nie portuj go.

Moze to byc troche frustrujace, jesli chcesz obiekt xyz, ale autor xyz nie logowal sie od 8 miesiecy. Sugestia w takim przypadku to przejrzec kod i sprobowac zrozumiec, co robi, a nastepnie zaprogramowac obiekt o podobnych, ale ulepszonych funkcjach.

Wiele osob mowi, ze portowanie obiektow MOO to dobry sposob na nauke programowania w MOO; inni sa wrogo nastawieni do idei portowania obiektow przez nie-programistow w ogole. Niech czytelnik zdecyduje, ale rozumiej, ze nie kazdy uwaza portowanie za swietna rzecz, nawet gdy jestes uprzejmy i szanujesz prawa autorskie.

**Techniczny**: obecnie jest mnostwo pulapek przy portowaniu obiektow, wiekszosc zwiazana z nieregularnosciami w kodowaniu oryginalnych obiektow oraz z operacjami klienta MOO. Tylko kilka z nich jest tu omowionych; dopoki ktos nie opracuje solidnego systemu przenosnosci dla MOO, od czasu do czasu bedziesz napotykac problemy. Gdy to sie stanie, nie ma nic lepszego niz bycie -- lub bycie dobrym znajomym -- doswiadczonego programisty MOO. Oto jedna zalecana procedura:

* Na MOO, na ktore portujesz obiekt, zrob @create z odpowiednim rodzicem i zanotuj nowy numer obiektu (#xxxx).
* Wlacz nagrywanie i wylacz autowrap w swoim kliencie; robisz to, by zapisac zrzut, ktory zaraz zrobisz na zrodlowym MOO.
* Na MOO, z ktorego portujesz obiekt #nnnn:

```
@wrap off
@dump #nnnn with create id=#xxxx
```

* Zedytuj zapisany zrzut.
* Usun @create z pierwszej linii zrzutu, poniewaz juz stworzyles obiekt.
* Poszukaj zakodowanych na sztywno numerow obiektow innych niz ten, ktory stworzyles. Napraw je, wskazujac na wlasciwy obiekt na twoim MOO, albo przekoduj tak, by nie byly potrzebne.
* Poszukaj rzeczy, ktore mogly zostac przypadkowo przechwycone razem ze zrzutem, np.:

```
You sense that Nern is looking for you in the Living Room:
Nern pages, "Come out and help me torture some guests."
```

* Wgraj zrzut na swoje MOO przy pomocy klienta; ten skrypt zrzutu umiesci wlasciwosci i czasowniki na obiekcie.
* Teraz przetestuj i/lub debuguj obiekt.

[Dzieki dla Judy Anderson za niektore szczegoly powyzej; jesli cos jest bledne, to jeden z moich wlasnych dopiskow -red.]

---

### 1.15 - Zrzucilem ten obiekt, ale ma kilkaset wlasciwosci z numerami obiektow ze zrodlowego MOO. Jak sie ich pozbyc?

Jednym oczywistym sposobem jest wyedytowanie ich ze zrzutu edytorem tekstu przed wgraniem. Moze to powodowac bledy i byc zmudne. Moze byc lepiej ponownie zrzucic obiekt, dodajac noprops do polecenia @dump. Nastepnie przejrzyj kod czasownikow, by sprawdzic, jakie wlasciwosci musza byc na obiekcie; dodaj je z powrotem przez @prop.

---

### 1.16 - Moj klient rozwala mi skrypt @dump przy wgrywaniu, wstawiajac zlamania linii tam, gdzie nie powinien. Co robic?

Sprawdz plik skryptu @dump, by upewnic sie, ze nie ma zlaman linii tam, gdzie nie powinno ich byc. Jesli ma, problem nie lezy w wgrywaniu, ale w twojej procedurze @dump (zrobiles @wrap off, prawda?), w nagrywaniu klienta, albo w edytorze, ktorego uzyles do przejrzenia skryptu; jedno z tych, albo cos innego, lamie linie.

Jesli twoj plik jest w porzadku, problem naprawde lezy w wgrywaniu:

* Ustaw swojego klienta, by przestal tak robic, albo
* Zdobadz lepszego klienta.

Dwa klienty ostatnio wskazywane jako dobre do wgrywania to:

* Mac - Mudweller 1.2 ma mozliwosc wgrywania plikow [wg Scotta Lyncha]
* Unix - emacs

```
M-x telnet (by otworzyc sesje telnet w biezacym oknie edycji)
C-X I (by wstawic plik ascii skryptu zrzutu)
```

[wg Dana Mehkeriego]

---

### 1.17 - Jak zrobic, by wszyscy nowi gracze byli dziecmi okreslonej klasy gracza?

Ustaw $player_class na te klase. Na przyklad, by kazdy nowy gracz byl klasy builder, chcialbys:

```
;$player_class = $builder
```

---

### 1.18 - Dlaczego dostaje range error w linii 3 #15:length_date_gt, uzywanym przez polecenia takie jak @subscribe?

Napotykasz to, gdy nie ma zadnych wiadomosci w #18, dzienniku tworzenia graczy (Player-Creation Log). To typowe, gdy MOO oparte na LambdaCore jest zupelnie nowe. Zmien czasownik na to:

```
#15:length_date_gt   this none this
if (this:ok(caller, caller_perms()))
date = args[1];
if (length(this.messages) < 2)
return 0;
endif
return this.last_msg_date <= date ? 0 | this.messages[2] - this._mgr:find_ord(this.messages, args[1], "_lt_msgdate");
else
return E_PERM;
endif
```

[dzieki uprzejmosci Fran Litterio, za posrednictwem posta Pavla Curtisa]

---

### 1.19 - Probuje uzyc @mail-options +netmail i zawsze dostaje: Mail sending failed: 503 Need MAIL before RCPT. Dostaje zarowno kopie mailem, jak i przez @mail. Co jest grane?

Wyglada na to, ze to blad w demonie sendmail Solarisa (SunOS 5.x). Kazdy i tak moze zechciec wprowadzic nastepujaca zmiane, poniewaz sprawia ona, ze procedury sendmail MOO sa bardziej technicznie zgodne ze specyfikacja SMTP.

Zedytuj $network:raw_sendmail i zmien nastepujace (linia 48):

```
if (!index("23", line[1]))
```

na:

```
if (line[4] == "-")
elseif (!index("23", line[1]))
```

[dzieki uprzejmosci Alexa Stewarta]

---

### 1.20 - O co chodzi z dziura bezpieczenstwa w my_huh?

Odkryto dziure bezpieczenstwa w procesie :my_huh (czesci parsowania :huh, ktora obsluguje obiekty-funkcje (feature objects) w LambdaCore), ktora pozwala wlascicielom klas graczy uruchamiac polecenia funkcji z uprawnieniami swoich dzieci. To zrozumiale zla dziura, zwlaszcza jesli twoje MOO przenosi funkcje z klas graczy na obiekty-funkcje i uzywa caller_perms() do sprawdzania uprawnien.

Sprawdzenie uprawnien na $player:my_huh brzmi:

```
if ((caller != this) && (!$perm_utils:controls(caller_perms(), this)))
"Standard permissions check";
return E_PERM;
endif;
```

...a nastepnie w dalszej czesci czasownika robi:

```
set_task_perms(this);
```

Zaleca sie albo zmienic ten if, usuwajac warunek (caller != this), albo zostawic go i zmienic set_task_perms() na set_task_perms(caller_perms()). To, jak twoje MOO uzywa :my_huh, bedzie najlepszym sposobem, by ocenic, ktora zmiana jest lepsza.

[dzieki uprzejmosci Setha Richa]

---

### 1.21 - Zawsze jest nowa wiadomosc w news. Co jest grane?

Nic sie nie martw. Zrob to jako czarodziej na swoim rdzeniu z 1-Oct-94:

```
;$news:_fix_last_msg_date()
;$news.last_news_time=0
;$news:set_current_news($news.current_news)
```

---

### 1.22 - Gdzie jest pomoc na temat $news? @examine-owalem go, ale nic nie dziala.

Oto jak to zrobic z rdzeniem z 1-Oct-94:

Najpierw znajdz numer obiektu $news:

```
@d $news
```

By dodac nowa wiadomosc:

```
@send *news    (dokladnie tak jak wysylanie poczty na dowolna liste mailingowa)
```

Gdy skonczysz komponowac i wysylac swoja wiadomosc do *news, zrob:

```
@mail on *news    (pokaze ci, jaka wiadomosc ma jaki numer).
```

By dodac te wiadomosc, zrob:

```
@addnews [numer wiadomosci] to [numer obiektu $news]
```

Jesli wiadomosc jest stara i chcesz ja usunac, zrob:

```
@rmnews [numer wiadomosci] from [numer obiektu $news]
```

[z postow na Moo-Cows od Setha I. Richa i Colina Moocka]

---

### 2 - Podziekowania i uwagi

Ten dokument zostal pierwotnie napisany przez kcary@pepperdine.edu. Nie byl jednak zmieniany od okolo 1998 roku, gdy zostal skopiowany (mirror) na ten serwer. Zmiana jest jednak zawsze dobra.

By wniesc wklad do tego FAQ lub skomentowac je, napisz na kenny at the-b.org; poprawki, uzupelnienia i przypisania autorstwa sa mile widziane. Nie znalazlem jeszcze sposobu, ktory by mi odpowiadal, by dodawac latki bazy danych dla rzeczy, ktore nie dotycza kazdego uzywajacego waniliowego LambdaCore.

By zadac pytanie o programowanie w MOO, zapisz sie na liste moo-cows (by zapisac sie lub wypisac z listy mailingowej moo-cows, wyslij mail na moo-cows-request@moo-cows.com z uprzejma prosba w zwyklym jezyku angielskim). Adres URL, pod ktorym mozna uzyskac te liste, to:

http://www.moo-cows.com/

Ten dokument niekoniecznie odzwierciedla opinie osob, dla ktorych pracuje; nie sa oni odpowiedzialni za bledy, zniewazenia ani inne niepozadane skutki innych stwierdzen zawartych w niniejszym dokumencie. Kazda z powyzszych procedur wykonujesz na wlasne ryzyko.
