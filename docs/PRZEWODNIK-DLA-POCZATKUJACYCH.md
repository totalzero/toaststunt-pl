# Przewodnik dla poczatkujacych

*Polskie tlumaczenie oryginalnego przewodnika autorstwa lisdude, dostepnego pod adresem [https://lisdude.com/moo/toaststunt_newbie.txt](https://lisdude.com/moo/toaststunt_newbie.txt) (stan na 2022-02-28). Nazwy plikow, katalogow, pakietow oraz polecenia do wpisania w terminalu pozostaly w oryginalnej, angielskiej formie, poniewaz sa to realne komendy i identyfikatory -- tlumaczeniu podlega tylko tekst wyjasniajacy.*

Witaj w ToastStunt! Ten przewodnik zaklada, ze masz niewielka lub zadna znajomosc linii polecen i jest przeznaczony dla zupelnych poczatkujacych. Gdy zobaczysz linie zaczynajaca sie od znaku wiekszosci (`>`), oznacza to polecenie do wpisania. Jesli linia zaczyna sie od znaku rownosci i znaku wiekszosci (`=>`), oznacza to wyjscie, ktore otrzymano z polecenia jako przyklad. W pozostalych przypadkach caly tekst to po prostu wyjasnienia.

Ten przewodnik nalezy traktowac jako uzupelnienie Archwizard FAQ ([https://lisdude.com/moo/archwizard_faq.html](https://lisdude.com/moo/archwizard_faq.html)), README ToastStunt ([README.md](README.md)) oraz README ToastCore ([polskie tlumaczenie](README.ToastCore.md), [oryginal](https://github.com/lisdude/toastcore/blob/master/README.md)).

Po pierwsze, wazne jest, by zrozumiec, gdzie umieszczasz swoj serwer i baze danych. (Nie znasz roznicy miedzy serwerem a baza danych? Sprawdz Archwizard FAQ! [https://lisdude.com/moo/archwizard_faq.html#toc_3](https://lisdude.com/moo/archwizard_faq.html#toc_3)). Domyslnie powinienes byc w swoim katalogu domowym:

```
>pwd
=> /home/lisdude
```

Polecenie `pwd` pokaze ci, w jakim katalogu obecnie jestes. Na potrzeby tego przewodnika zalozymy, ze chcesz miec wszystkie rzeczy zwiazane z MOO w katalogu MOO wewnatrz swojego katalogu domowego. Zrobmy to teraz:

```
>mkdir moo
=> mkdir: created directory 'moo'
```

Teraz przejdz do tego katalogu:

```
>cd moo
>pwd
=> /home/lisdude/moo
```

Powyzsze polecenie `pwd` nie jest konieczne, ale pomaga potwierdzic, ze jestes we wlasciwym miejscu. Teraz, gdy mamy juz dom dla wszystkich naszych rzeczy zwiazanych z MOO, zainstalujmy wymagania do zbudowania serwera. Musisz to zrobic tylko raz, a przebieg zalezy od uzywanego systemu operacyjnego. Plik README zawiera wiele informacji o kompilowaniu na roznych platformach, wiec prawdopodobnie zechcesz do niego zajrzec ([https://github.com/lisdude/toaststunt#build-instructions](https://github.com/lisdude/toaststunt#build-instructions)) dla swojego konkretnego systemu operacyjnego. Dla przykladu zalozymy, ze uzywasz dystrybucji opartej na Debianie, takiej jak Ubuntu.

By zainstalowac potrzebne biblioteki i narzedzia, zazwyczaj potrzebujesz dostepu root albo bycia administratorem z uprawnieniami do instalowania oprogramowania w twoim srodowisku. Zaloze, ze masz juz taki poziom dostepu. Teraz zainstalujmy kilka rzeczy:

```
>sudo apt install build-essential bison gperf cmake libsqlite3-dev libaspell-dev libpcre3-dev nettle-dev g++ libcurl4-openssl-dev libargon2-dev libssl-dev
```

Prawdopodobnie zobaczysz duzo wyjscia. Jesli jestes ciekawy, do czego sluza te wszystkie pakiety, rozpisze to ponizej. Jesli cie to nie obchodzi, smialo przejdz do nastepnej sekcji!

- **build-essential**: Ten pakiet zawiera oprogramowanie niezbedne do budowania innego oprogramowania, takie jak kompilator C/C++.
- **bison**: Generator parserow. Pozwala nam to latwo definiowac jezyk programowania MOO.
- **gperf**: Generator funkcji haszujacych uzywany przy generowaniu slow kluczowych.
- **cmake**: System budowania uzywany do upewnienia sie, ze wymagania sa spelnione i serwer buduje sie pomyslnie.
- **libsqlite3-dev**: Biblioteka wymagana do uzywania SQLite.
- **libaspell-dev**: Biblioteka wymagana do uzywania sprawdzania pisowni.
- **libpcre3-dev**: Biblioteka wymagana do uzywania wyrazen regularnych kompatybilnych z Perl.
- **nettle-dev**: Biblioteka kryptograficzna.
- **libcurl4-openssl-dev**: Biblioteka wymagana do uzywania curl.
- **libargon2-dev**: Biblioteka argon2 do bezpiecznego haszowania hasel.

Teraz, gdy masz juz wszystkie wymagania, czas pobrac kod zrodlowy serwera ToastStunt:

```
>git clone https://github.com/lisdude/toaststunt.git
```

Powinno pojawic sie kilka linii wyjscia i powinienes otrzymac katalog `toaststunt`. Mozesz to zweryfikowac poleceniem `ls`, ktore wypisze zawartosc katalogu, w ktorym jestes.

```
>ls
=> toaststunt
```

Dobrze! Teraz musimy przejsc do katalogu `toaststunt`:

```
>cd toaststunt
>pwd
=> /home/lisdude/moo/toaststunt
```

Ponownie, `pwd` nie jest konieczne. Chodzi tylko o to, by upewnic sie, ze kazdy jest we wlasciwym miejscu! Ten katalog zawiera caly kod zrodlowy serwera. Wiekszosc plikow tutaj nie jest dla ciebie wazna, ale jest jeden, ktory moze warto edytowac. Zawiera on szereg opcji konfigurujacych zachowanie serwera. Jest dobrze skomentowany i jesli bedziesz musial zmienic jakas opcje, prawdopodobnie rozpoznasz ja, gdy ja zobaczysz. Nie omowimy zadnych szczegolow, ale jesli chcesz go edytowac, mozesz to zrobic czyms takim jak `nano`:

```
>nano src/include/options.h
```

To otworzy edytor tekstu i mozesz wprowadzic potrzebne zmiany. Gdy skonczysz, wcisnij CTRL-x.

Wreszcie mozemy zbudowac serwer. By to zrobic, musisz utworzyc tymczasowy katalog budowania i przejsc do niego:

```
>mkdir build
=> mkdir: created directory 'build'
>cd build
>pwd
=> /home/lisdude/moo/toaststunt/build
```

Jeszcze dwa kroki i gotowe!

```
>cmake ../
```

To polecenie uruchomi rozne sprawdzenia, by upewnic sie, ze masz wszystko, czego potrzeba do zbudowania serwera.

```
>make -j2
```

To polecenie wykonuje faktyczne budowanie. Zakladajac, ze nic nie poszlo zle, powinienes miec plik `moo` w katalogu. Gratulacje!

------------

Teraz, gdy mamy plik wykonywalny serwera, czas skonfigurowac nasza baze danych. Zalozymy, ze zaczynasz ponownie w swoim katalogu domowym. Jesli wlasnie skompilowales serwer, wroc teraz do domu:

```
>cd
>pwd
=> /home/lisdude
```

Teraz przejdz z powrotem do katalogu MOO:

```
>cd moo
```

Teraz czas wybrac baze danych core. Jest ich wiele do wyboru ([https://lisdude.com/moo/#cores](https://lisdude.com/moo/#cores)), ale niektore moga byc bardziej skomplikowane na start niz inne. Najczestsze opcje to:

- **LambdaCore**: To baza danych core wyodrebniona z samego LambdaMOO. Byla ostatnio aktualizowana w 2004 roku i byla przeznaczona do uzytku z serwerem LambdaMOO. Jest jednak w pelni kompatybilna z ToastStunt i nadal stanowi niezly punkt startowy.
- **JHCore**: Ta baza danych core pochodzi z Waterpoint i ma kilka ulepszen w stosunku do standardowego LambdaCore, choc moze byc trudniejsza na start.
- **ToastCore**: Ta baza danych pochodzi z bazy LambdaCore i zostala zaktualizowana, by w pelni wykorzystac nowe funkcje serwera ToastStunt. Zawiera tez wszelkie poprawki, ktore pojawily sie w samym LambdaMOO, ale nie trafily jeszcze do nowego LambdaCore.

W tym przewodniku bedziemy uzywac ToastCore, poniewaz jest to najnowoczesniejsza opcja i zostala zmodyfikowana, by w pelni wykorzystac serwer ToastStunt. Zanim ja pobierzemy, stworzmy strukture katalogow dla naszego MOO. Dla przykladu nazwiemy nasze MOO `TestMOO`.

```
>mkdir testmoo
=> mkdir: created directory 'testmoo'
>cd testmoo
>pwd
=> /home/lisdude/moo/testmoo
>mkdir files
=> mkdir: created directory 'files'
```

Katalog `files` bedzie przechowywal wszelkie zewnetrzne pliki lub bazy danych SQLite, do ktorych chcesz miec dostep z wnetrza swojego MOO. Teraz pobierzmy ToastCore:

```
>curl -O https://raw.githubusercontent.com/lisdude/toastcore/master/toastcore.db
```

*Uwaga: jesli chcesz od razu zaczac od bazy danych przetlumaczonej na polski (tej, ktora jest dolaczona do tego forka), pobierz zamiast tego `toastcore.db` z [totalzero/toaststunt-pl](https://github.com/totalzero/toaststunt-pl) badz skopiuj plik `toastcore.db` z glownego katalogu tego repozytorium.*

Teraz mozemy ja przemianowac:

```
>mv toastcore.db testmoo.db
```

W tym momencie powinnismy miec katalog, ktory wyglada tak:

```
>pwd
=> /home/lisdude/moo/testmoo
>ls
=> files  testmoo.db
```

Przyznajemy, niezbyt uzyteczny. Musimy zrobic dwie rzeczy: skopiowac plik wykonywalny serwera wraz ze skryptem restartu. Zakladajac, ze poszedles za powyzszym przewodnikiem, by skompilowac ToastStunt, powinien on znajdowac sie w katalogu `moo`:

```
>cp ../toaststunt/build/moo ./
>cp ../toaststunt/restart.sh ./
```

Krotka dygresja, by wyjasnic, co sie wlasnie stalo. `cp` to polecenie kopiowania. `../` oznacza "jeden katalog wstecz" (np. `/home/lisdude/moo/`), a `./` oznacza biezacy katalog (np. `/home/lisdude/moo/testmoo`).

Wszystko, co pozostalo do zrobienia, to uruchomienie serwera i polaczenie sie!

```
>./restart.sh mymoo 7777
```

Jesli wszystko pojdzie zgodnie z planem, twoje MOO powinno dzialac na porcie 7777!

------------

A co sie dzieje jutro? Jak wrocic? Zakladajac, ze zaczynasz od swojego katalogu domowego (pamietaj, polecenie `cd` zabierze cie z powrotem), musisz po prostu przejsc z powrotem do katalogu swojego MOO i ponownie uruchomic skrypt restartu:

```
>cd moo/testmoo
>./restart.sh mymoo 7777
```

------------

Ostatnia mysl: serwer ToastStunt aktualizuje sie dosc szybko. Ta sekcja przewodnika wyjasni, jak zaktualizowac do najnowszej wersji rozwojowej. UWAGA: Przed aktualizacja ZAWSZE przeczytaj changelog ToastStunt! Jesli wprowadza jakiekolwiek zmiany lamiace kompatybilnosc, MUSISZ podjac dzialania, by przygotowac swoja baze danych PRZED aktualizacja. Sprawdz changelog tutaj: [https://github.com/lisdude/toaststunt/blob/master/docs/ChangeLog.md](https://github.com/lisdude/toaststunt/blob/master/docs/ChangeLog.md)

Pierwszy krok: wroc do katalogu swojego serwera. Ten przewodnik zaklada, ze jestes z powrotem w swoim katalogu domowym (`cd`).

```
>cd moo/toaststunt
```

Teraz pobierz najnowsze aktualizacje:

```
>git pull
```

Teraz przekompiluj. Na tym etapie polecalibysmy usuniecie starego katalogu budowania i zaczecie od nowa. Nie MUSISZ tego robic, ale moze to pomoc przy okazjonalnych dziwnych problemach.

```
>rm -rf ./build
>mkdir build
>cd build
```

Teraz po prostu powtorz kroki, ktore wykonalismy powyzej:

```
>cmake ../
>make -j2
```

I na koniec skopiuj nowy plik wykonywalny do katalogu swojego MOO. Zalozymy, ze nadal pracujesz z TestMOO, ale zmien nazwy wedlug potrzeb:

```
>cp ./moo ../../testmoo
```

Gotowe! Zrestartuj swoje MOO jak zwykle.

------------

Ostatnia aktualizacja oryginalu: 2022-02-28
