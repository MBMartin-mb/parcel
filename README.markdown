# Aplikace pro vyhledávání detailů balíku

Jednoduchá webová aplikace pro načtení a zobrazení detailů balíku (telefonní číslo příjemce a datum vložení) na základě čísla balíku pomocí testovacího API.

## Funkce
- Vstupní pole pro číslo balíku s předvyplněnou testovací hodnotou (`A000DBZ806-700-000-000000`).
- Načítá data z `GET /api/parcelDetails/{parcelNumber}` na adrese `https://parcelpointtest.cleverlance.com/parcelserver`.
- Zobrazuje `notificationMsisdn` (telefon) a `storedDateTime` (formátováno jako `YYYY-MM-DD HH:MM:SS`).
- Zpracovává chyby (např. 404, 5xx, timeouty) srozumitelnými hláškami.
- Bez externích závislostí; používá nativní `fetch` API.
- Čistý, okomentovaný kód s Basic Authentication (uživatel: `marbusek`, heslo: `marbusek`).

## Instalace a spuštění
1. **Vytvořte GitHub repozitář**:
   - Vytvořte nový repozitář na GitHubu (např. `parcel-lookup`).
   - Nahrajte poskytnuté soubory (`index.html`, `README.md`, `.gitignore`, `LICENSE`) do repozitáře.
2. **Lokální spuštění**:
   - Naklonujte repozitář: `git clone <repo-url>`.
   - Otevřete `index.html` v moderním prohlížeči (Chrome, Firefox apod.).
   - Není potřeba server, jedná se o statický HTML soubor.
3. **Spuštění přes GitHub Pages** (volitelné):
   - V repozitáři na GitHubu přejděte do **Settings > Pages**.
   - Nastavte zdroj na větev `main` a složku `/ (root)`.
   - Po nasazení bude aplikace dostupná na adrese typu `https://<username>.github.io/<repo-name>`.
4. **Testování**:
   - Zadejte testovací číslo balíku `A000DBZ806-700-000-000000` nebo jiné platné číslo.
   - Klikněte na tlačítko **Načíst** pro zobrazení výsledků.

## Vzorový výstup
Pro číslo balíku `A000DBZ806-700-000-000000` (za předpokladu, že API vrátí platná data):
```
Telefon příjemce: +420123456789
Datum vložení: 2025-06-19 14:30:00
```

## Zpracování chyb
- **Prázdný vstup**: "Prosím, zadejte číslo balíku."
- **404 Nenalezeno**: "Balík nenalezen (404)."
- **5xx Chyba serveru**: "Chyba serveru. Zkuste to prosím znovu později."
- **Síť/Timeout**: "Chyba: Nepodařilo se načíst detaily balíku."

## Kvalita kódu
- Prochází ESLintem se standardními pravidly JavaScriptu (bez kritických chyb).
- Jasné oddělení logiky API (`fetchParcelDetails`) a aktualizací UI.
- Komentáře označují klíčové části kódu (např. `BASE_URL` a `HEADERS`).
- Formátování data používá `toLocaleString` pro lokalizovaný výstup (cs-CZ).

## Možnosti rozšíření
- **Kopírování do schránky**: Přidat tlačítko pro kopírování výsledků pomocí `navigator.clipboard.writeText()`.
- **Logování do CSV**: Ukládat výsledky do localStorage nebo stahovat jako CSV pomocí `data:text/csv`.
- **Další pole**: Rozšířit UI pro zobrazení dalších polí z odpovědi API, pokud jsou k dispozici.

## Poznámky
- API adresa je nastavena na `https://parcelpointtest.cleverlance.com/parcelserver`.
- Aplikace používá Basic Authentication s přihlašovacími údaji `marbusek:marbusek`.
- Timeout je nastaven na 5 sekund, aby se předešlo zaseknutí požadavků.
- Pokud potřebujete změnit přihlašovací údaje, upravte hlavičku `Authorization` v `index.html`.