# ToastCore

*Polskie tlumaczenie oryginalnego README ToastCore, dostepnego pod adresem [https://github.com/lisdude/toastcore](https://github.com/lisdude/toastcore) (pobrane 2026-07-18). Tresc zweryfikowana wzgledem faktycznej bazy `toastcore.db` dolaczonej do tego forka -- wymienione tu funkcje (MCP 2.1, hashowanie Argon2id, `$recycler`, MSSP, ANSI PC) sa w niej obecne i dzialaja.*

ToastCore to zaktualizowana wersja nieoficjalnej [bazy LambdaCore z 2018 roku](https://lisdude.com/moo/LambdaCore-20Jun18.db.gz) (plik binarny, bez tlumaczenia). Ma sluzyc albo jako zamiennik LambdaCore przy zakladaniu nowego MOO, albo jako punkt odniesienia przy wdrazaniu funkcji specyficznych dla ToastStunt we wlasnych bazach danych.

## Funkcje

- Zaktualizowane podstawowe czasowniki narzedziowe, z odpowiednikami dla ToastStunt tam, gdzie to zasadne
- ANSI 2.6
- MCP 2.1
- Zastapienie `crypt()` hashowaniem hasel Argon2id
- Szkieletowe obiekty typu waif oraz obiekty anonimowe
- Rozne prototypy typow wbudowanych, ktore przekierowuja do odpowiednikow w `$generic_utils`
    - np. `"Moj fajny string":explode()`
- Serializator obiektow Stunt Shapes
- Aktualizacje MCP SimpleEdit
    - Obsluga list
    - Obsluga komentarzy w stylu `//`
- Edytor liniowy (inline editor) uzywany na ChatMUD i Miriani (dawniej znany jako 'Flexible Editor')
- "Ubogie" przestrzenie nazw (poor man's namespaces)
    - Mapy na `#0` moga byc rozwijane przy dopasowywaniu
    - np. `@edit $help_db["toaststunt"].argon2`
- `$recycler` korzystajacy z `recycle()` i `recreate()` zamiast obiektow `$garbage`
- Wyszukiwanie nazw sieciowych obslugiwane wewnatrz bazy danych, w osobnym watku
- Podstawowa obsluga telnet z obsluga MSSP
- Ogolne posprzatanie przestarzalych / nieuzywanych elementow LambdaCore

Pelna lista zmian znajduje sie w [changelogu](https://github.com/lisdude/toastcore/blob/master/changelog.txt) (w jezyku angielskim -- changelogi w tym projekcie swiadomie pozostaja nieprzetlumaczone, tak jak [ChangeLog.md](ChangeLog.md) tego forka).

## Wymagania

- [ToastStunt v2.6.0 lub nowszy](https://github.com/lisdude/toaststunt)

## Uwagi

- **UWAGA**: jesli uruchamiasz baze danych MOO na wlasnym komputerze lokalnym, ToastStunt nie wyswietli ekranu powitalnego z powodu sposobu dzialania przepisywania (rewriting) adresu przez proxy -- zobacz [uwagi w README ToastStunt](README.md#ekran-logowania-sie-nie-pojawia). Aby polaczyc sie z glownym czarodziejem (wizardem) swiezo zainstalowanego ToastCore, wpisz: `connect wizard`
