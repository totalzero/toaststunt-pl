# ToastStunt

*This is a Polish-language fork ([totalzero/toaststunt-pl](https://github.com/totalzero/toaststunt-pl)) with engine strings and the bundled ToastCore database translated into ASCII-only Polish (no diacritics, by design — see the Polski section below).*
*To jest polskojezyczny fork ([totalzero/toaststunt-pl](https://github.com/totalzero/toaststunt-pl)), w ktorym komunikaty silnika oraz dolaczona baza ToastCore zostaly przetlumaczone na polski bez znakow diakrytycznych (celowo — patrz sekcja "Polski" ponizej).*

**[English](#english)** | **[Polski](#polski)**

---

<a name="english"></a>
## English

ToastStunt is a network accessible, multi-user, programmable, interactive system used in the creation of both text-based and web-based experiences. The most common usage is the creation of MUDs (examples include [Miriani](https://www.toastsoft.net) and [ChatMud](https://www.chatmud.com/)). ToastStunt is a fork of [Stunt](https://github.com/toddsundsted/stunt), which is a fork of [LambdaMOO](https://github.com/wrog/lambdamoo). It builds upon those projects to add improved performance, modern conveniences, and an improved user experience.

* [Features](#features)
* [ChangeLog](ChangeLog.md)
* [Build Instructions](#build-instructions)
  * [Debian/Ubuntu/WSL](#debianubuntuwsl)
  * [Gentoo](#gentoo)
  * [FreeBSD](#freebsd)
  * [macOS](#macos)
* [Function Documentation](https://github.com/lisdude/toaststunt-documentation)
* [Getting Started Guide](https://lisdude.com/moo/toaststunt_newbie.txt)
* [ToastCore](https://github.com/lisdude/toastcore)
* [Stunt Information](Legacy/README/README.Stunt)

<a href = "https://discord.gg/JUz3zwZamW"><img alt="Join Discord" src="https://img.shields.io/discord/738251170140651560?label=Discord&style=plastic"></a>

### Features

- SQLite
- Perl Compatible Regular Expressions (PCRE)
- [Argon2id Hashing](https://github.com/P-H-C/phc-winner-argon2)
- 64-bit Integers (with the choice to fall back to 32-bit integers; $maxint and $minint set automatically)
- HAProxy Source IP Rewriting (see [notes](#login-screen-not-showing) below if you need to disable this)
- User friendly traceback error messages

- Networking improvements:
    - IPv6 connection support
    - Threaded DNS lookups
    - Secure TLS connections in `listen()` and `open_network_connection()`

- Waifs:
    - Call :recycle on waifs when they're destroyed
    - A WAIF type (so typeof(some_waif) == WAIF)
    - Waif dict patch (so waif[x] and waif[x] = y will call the :_index and :_set_index verbs on the waif)
    - '-w' command line option to convert existing databases with a different waif type to the new waif type
    - `waif_stats()` (show how many instances of each class of waif exist, how many waifs are pending recycling, and how many waifs in total exist)
    - Parser recognition for waif properties (e.g. thing.:property)

- Basic threading support:
    - background.cc (a library, of sorts, to make it easier to thread builtins)
    - Threaded builtins: sqlite_query, sqlite_execute, locate_by_name, sort, argon2, argon2_verify, connection_name_lookup
    - set_thread_mode (an argument of 0 will disable threading for all builtins in the current verb, 1 will re-enable, and no arguments will print the current mode)
    - `thread_pool()` (database control over the the thread pools)

- FileIO improvements:
    - Faster reading
    - Open as many files as you want, configurable with FILE_IO_MAX_FILES or $server_options.file_io_max_files
    - `file_handles()` (returns a list of open files)
    - `file_grep()` (search for a string in a file (kind of FUP in FIO, don't tell))
    - `file_count_lines()` (counts the number of lines in a file)

- Profiling and debugging:
    - `finished_tasks()` (returns a list of the last X tasks to finish executing, including their total execution time) [see options.h below]
    - Set a maximum lag threshold (can be overridden with $server_options.task_lag_threshold) that, when exceeded, will make a note in the server log and call #0:handle_lagging_task with arguments: {callers, execution time}
    - Include a map of defined variables for stack frames when being passed to `handle_uncaught_error`, `handle_task_timeout`, and `handle_lagging_task` [see options.h below]
    - Optionally capture defined variables for running tasks by providing a true argument to `queued_tasks()` or a third true argument to `task_stack()`.

- Telnet:
    - Capture IAC commands and pass them to listener:do_out_of_band_command() for the database to handle.

- Stunt Improvements:
    - Primitive types:
        - Support calling verbs on an object prototype ($obj_proto) for un-logged-in connection objects.
    - Maps:
        - `maphaskey()` (check if a key exists in a map)

- [Numerous new configuration options](Features/new_options.md)

- [Several new built-in functions](Features/new_builtins.md)

- [Many miscellaneous changes](Features/new_miscellaneous.md)

### Build Instructions
#### **Debian/Ubuntu/WSL**
```bash
apt install build-essential bison gperf cmake libsqlite3-dev libaspell-dev libpcre2-dev nettle-dev g++ libcurl4-openssl-dev libargon2-dev libssl-dev
mkdir build && cd build
cmake ../
make -j2
```

#### **Gentoo**
```bash
emerge dev-db/sqlite app-text/aspell app-dicts/aspell-en app-crypt/argon2 dev-utils/cmake dev-libs/libpcre2
mkdir build && cd build
cmake ../
make -j2
```

#### **FreeBSD**
```bash
pkg install bison gperf gcc cmake sqlite3 aspell pcre2 nettle libargon2
mkdir build && cd build
cmake ../
make -j2
```

#### **macOS**
Installing dependencies requires [Homebrew](https://brew.sh/).

If using OpenSSL, you may have to export an environment variable before running CMake:
- Apple Silicon: `export PKG_CONFIG_PATH="/opt/homebrew/opt/openssl@3/lib/pkgconfig"`
- Intel: `export PKG_CONFIG_PATH="/usr/local/opt/openssl@3/lib/pkgconfig"`

```bash
brew install pcre2 aspell nettle cmake openssl argon2
mkdir build && cd build
cmake ../
make -j2
```

### **Notes**
#### CMake Build Options
There are a few build options available to developers:

| Build Option | Effect                                                                       |
|--------------|------------------------------------------------------------------------------|
| Release      | Optimizations enabled, warnings disabled.                                    |
| Debug        | Optimizations disabled, debug enabled.                                       |
| Warn         | Optimizations enabled, warnings enabled. (Previous default behavior)         |
| LeakCheck    | Minimal optimizations enabled, debug enabled, and address sanitizer enabled. |

To change the build, use: `cmake -DCMAKE_BUILD_TYPE=BuildNameHere ../`

#### Login screen not showing
Due to the way proxy detection works in versions of the server prior to 2.7.1_22, if you're connecting to your MOO from localhost, you won't see the login screen. This is a minor inconvenience and shouldn't affect your ability to actually use your MOO. However, if it bothers you, you can disable HAProxy rewriting:

1. `@prop $server_options.proxy_rewrite 0`
2. `;load_server_options()`

**NOTE**: Newer versions of the server control proxy rewriting via the `$server_options.trusted_proxies` property instead.

---

<a name="polski"></a>
## Polski

ToastStunt to dostepny przez siec, wieloosobowy, programowalny, interaktywny system uzywany do tworzenia doswiadczen zarowno tekstowych, jak i webowych. Najczesciej sluzy do tworzenia MUD-ow (przyklady to [Miriani](https://www.toastsoft.net) i [ChatMud](https://www.chatmud.com/)). ToastStunt to fork [Stunt](https://github.com/toddsundsted/stunt), ktory z kolei jest forkiem [LambdaMOO](https://github.com/wrog/lambdamoo). Rozbudowuje te projekty o lepsza wydajnosc, nowoczesne udogodnienia i lepsze doswiadczenie uzytkownika.

* [Funkcje](#funkcje)
* [ChangeLog](ChangeLog.md)
* [Instrukcje budowania](#instrukcje-budowania)
  * [Debian/Ubuntu/WSL](#debianubuntuwsl-1)
  * [Gentoo](#gentoo-1)
  * [FreeBSD](#freebsd-1)
  * [macOS](#macos-1)
* [Dokumentacja funkcji](https://github.com/lisdude/toaststunt-documentation)
* [Przewodnik dla poczatkujacych](PRZEWODNIK-DLA-POCZATKUJACYCH.md)
* [ToastCore](https://github.com/lisdude/toastcore) ([polskie tlumaczenie README](README.ToastCore.md))
* [Informacje o Stunt](Legacy/README/README.Stunt)
* [**Tworzenie tresci po polsku**](TWORZENIE-TRESCI-PO-POLSKU.md) -- przewodnik dla programistow/budowniczych: system rodzaju, zaimki, odmiana czasownikow, zasada ASCII i jej ograniczenia

<a href = "https://discord.gg/JUz3zwZamW"><img alt="Join Discord" src="https://img.shields.io/discord/738251170140651560?label=Discord&style=plastic"></a>

### Funkcje

- SQLite
- Wyrazenia regularne kompatybilne z Perlem (PCRE)
- [Hashowanie Argon2id](https://github.com/P-H-C/phc-winner-argon2)
- Liczby calkowite 64-bitowe (z mozliwoscia powrotu do 32 bitow; $maxint i $minint ustawiane automatycznie)
- Przepisywanie adresu IP zrodlowego przez HAProxy (patrz [uwagi](#ekran-logowania-sie-nie-pojawia) ponizej, jesli chcesz to wylaczyc)
- Przyjazne dla uzytkownika komunikaty bledow (traceback)

- Usprawnienia sieciowe:
    - Obsluga polaczen IPv6
    - Watkowe (threaded) wyszukiwania DNS
    - Bezpieczne polaczenia TLS w `listen()` i `open_network_connection()`

- Waify (waifs):
    - Wywolanie :recycle na waifie w momencie jego zniszczenia
    - Typ WAIF (czyli typeof(jakis_waif) == WAIF)
    - Poprawka dict dla waifow (waif[x] i waif[x] = y wywoluja czasowniki :_index i :_set_index na waifie)
    - Opcja linii polecen '-w' konwertujaca istniejace bazy z innym typem waif na nowy typ waif
    - `waif_stats()` (pokazuje, ile jest instancji kazdej klasy waifow, ile czeka na recykling i ile jest ich w sumie)
    - Rozpoznawanie skladni waifow przez parser (np. thing.:property)

- Podstawowe wsparcie dla watkow (threading):
    - background.cc (rodzaj biblioteki ulatwiajacej watkowanie funkcji wbudowanych)
    - Watkowe funkcje wbudowane: sqlite_query, sqlite_execute, locate_by_name, sort, argon2, argon2_verify, connection_name_lookup
    - set_thread_mode (argument 0 wylacza watkowanie wszystkich funkcji wbudowanych w biezacym czasowniku, 1 wlacza je ponownie, brak argumentow wypisuje biezacy tryb)
    - `thread_pool()` (kontrola nad pulami watkow z poziomu bazy danych)

- Usprawnienia FileIO:
    - Szybszy odczyt
    - Mozliwosc otwarcia dowolnej liczby plikow, konfigurowalna przez FILE_IO_MAX_FILES lub $server_options.file_io_max_files
    - `file_handles()` (zwraca liste otwartych plikow)
    - `file_grep()` (szuka ciagu znakow w pliku, taki FUP w FIO, nikomu nie mow)
    - `file_count_lines()` (liczy linie w pliku)

- Profilowanie i debugowanie:
    - `finished_tasks()` (zwraca liste X ostatnio zakonczonych zadan wraz z calkowitym czasem wykonania) [patrz options.h ponizej]
    - Mozliwosc ustawienia maksymalnego progu opoznienia (nadpisywalnego przez $server_options.task_lag_threshold), po ktorego przekroczeniu w logu serwera pojawia sie wpis i wywolywane jest #0:handle_lagging_task z argumentami: {callers, execution time}
    - Dolaczanie mapy zdefiniowanych zmiennych dla ramek stosu przekazywanych do `handle_uncaught_error`, `handle_task_timeout` i `handle_lagging_task` [patrz options.h ponizej]
    - Opcjonalne przechwytywanie zdefiniowanych zmiennych dla dzialajacych zadan poprzez podanie wartosci true jako argumentu `queued_tasks()` lub jako trzeciego argumentu `task_stack()`.

- Telnet:
    - Przechwytywanie komend IAC i przekazywanie ich do listener:do_out_of_band_command() do obslugi przez baze danych.

- Usprawnienia Stunt:
    - Typy proste:
        - Obsluga wywolywania czasownikow na prototypie obiektu ($obj_proto) dla niezalogowanych polaczen.
    - Mapy:
        - `maphaskey()` (sprawdza, czy klucz istnieje w mapie)

- [Liczne nowe opcje konfiguracyjne](Features/new_options.md)

- [Kilka nowych funkcji wbudowanych](Features/new_builtins.md)

- [Wiele innych roznych zmian](Features/new_miscellaneous.md)

### Instrukcje budowania
#### **Debian/Ubuntu/WSL**
```bash
apt install build-essential bison gperf cmake libsqlite3-dev libaspell-dev libpcre2-dev nettle-dev g++ libcurl4-openssl-dev libargon2-dev libssl-dev
mkdir build && cd build
cmake ../
make -j2
```

#### **Gentoo**
```bash
emerge dev-db/sqlite app-text/aspell app-dicts/aspell-en app-crypt/argon2 dev-utils/cmake dev-libs/libpcre2
mkdir build && cd build
cmake ../
make -j2
```

#### **FreeBSD**
```bash
pkg install bison gperf gcc cmake sqlite3 aspell pcre2 nettle libargon2
mkdir build && cd build
cmake ../
make -j2
```

#### **macOS**
Instalacja zaleznosci wymaga [Homebrew](https://brew.sh/).

Jesli uzywasz OpenSSL, przed uruchomieniem CMake moze byc konieczne wyeksportowanie zmiennej srodowiskowej:
- Apple Silicon: `export PKG_CONFIG_PATH="/opt/homebrew/opt/openssl@3/lib/pkgconfig"`
- Intel: `export PKG_CONFIG_PATH="/usr/local/opt/openssl@3/lib/pkgconfig"`

```bash
brew install pcre2 aspell nettle cmake openssl argon2
mkdir build && cd build
cmake ../
make -j2
```

### **Uwagi**
#### Opcje budowania CMake
Deweloperzy maja do dyspozycji kilka opcji budowania:

| Opcja budowania | Efekt                                                                         |
|------------------|--------------------------------------------------------------------------------|
| Release          | Optymalizacje wlaczone, ostrzezenia wylaczone.                                 |
| Debug            | Optymalizacje wylaczone, tryb debug wlaczony.                                  |
| Warn             | Optymalizacje wlaczone, ostrzezenia wlaczone. (Poprzednie domyslne zachowanie) |
| LeakCheck        | Minimalne optymalizacje, tryb debug wlaczony, wlaczony address sanitizer.      |

Aby zmienic tryb budowania, uzyj: `cmake -DCMAKE_BUILD_TYPE=NazwaTrybu ../`

#### Ekran logowania sie nie pojawia
Ze wzgledu na sposob dzialania wykrywania proxy w wersjach serwera starszych niz 2.7.1_22, przy laczeniu sie z MOO z localhost ekran logowania nie bedzie widoczny. To drobna niedogodnosc, ktora nie powinna wplywac na mozliwosc korzystania z MOO. Jesli jednak przeszkadza, mozna wylaczyc przepisywanie HAProxy:

1. `@prop $server_options.proxy_rewrite 0`
2. `;load_server_options()`

**UWAGA**: Nowsze wersje serwera kontroluja przepisywanie proxy za pomoca wlasciwosci `$server_options.trusted_proxies` zamiast tego.
