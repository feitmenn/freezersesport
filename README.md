# Freezers ESPORT Team Hub

Responzivní webová aplikace pro CS2 tým Freezers ESPORT. Vanilla HTML, CSS a JavaScript; JSON soubory slouží jako datové úložiště. Není potřeba externí databáze ani build krok.

## Spuštění

Otevřete složku `outputs` ve webovém serveru, například pomocí VS Code Live Server nebo příkazem `python -m http.server 8000`, a přejděte na `http://localhost:8000`. Nepoužívejte `file://`: načítání JSON přes `fetch` prohlížeč blokuje.

## Moduly

- Přehled týmu, nadcházející události, statistiky, roster a partneři
- Kalendář s měsíčním, týdenním a denním přepnutím; tvorba i mazání událostí
- RSVP, odeslání omluvenky a evidence docházky
- Upozornění oranžovým zvýrazněním po pěti neomluvených absencích
- Playbook rozdělený podle map včetně videí a místních mapových obrázků
- Interní tipovačka s body bez sázek o peníze
- Admin panel s přehledem uživatelů a živým feedem změn
- Automatické ukládání do Local Storage, export a import JSON zálohy, cookies pro drobné preference a synchronizace souborů přes GitHub Contents API

## GitHub synchronizace

V aplikaci otevřete **Administrace → GitHub Sync**. Vyplňte vlastníka, repozitář, větev a volitelnou podsložku, vložte fine-grained GitHub token a zvolte **Připojit a načíst data**. Token potřebuje `Contents: read and write` pouze na cílovém repozitáři. Změny v kalendáři, playbooku, RSVP, docházce, omluvenkách a logu se následně zapisují jako Git commity. Synchronizace pracuje s aktuálními soubory v nastavené větvi.

Token se drží pouze v paměti aktuální karty; při obnovení stránky ho znovu vložte. Ostatní nastavení synchronizace je uloženo lokálně v prohlížeči. Přímé volání GitHub API z prohlížeče znamená, že token může být během použití viditelný uživateli prohlížeče. Tato architektura se proto hodí pro soukromý týmový dashboard na důvěryhodných zařízeních. Pro veřejně dostupnou aplikaci s více uživateli použijte serverless proxy nebo vlastní backend, který ověří identitu a token uloží jako serverový secret.

## Důležité k ukázkovým účtům

Dodané soubory `users.json` a `admins.json` obsahují uživatelská jména a SHA-256 hashe hesel. Jde o neosolené hashe: před veřejným nasazením je odstraňte nebo migrujte na bezpečné ověřování přes server. Statický front-end nemůže vynutit administrátorská oprávnění ani autentizaci. Přístup k write tokenu dává možnost měnit obsah repozitáře; udělujte ho jen lidem, kterým důvěřujete.

## Datové soubory

Zachovány jsou poskytnuté formáty `calendar.json`, `roster.json`, `playbook.json`, `rsvps.json`, `attendance.json`, `users.json`, `admins.json` a `staff.json`. Pro omluvenky a logy aplikace přidává `excuses.json` a `activity.json`. Mapy a obrázky partnerů jsou v `assets/`.


## Místní úložiště a soubory

V **Administrace → Data & zálohy** stáhněte kompletní JSON zálohu nebo nahrajte existující zálohu. Změny se automaticky drží v Local Storage daného prohlížeče. Tlačítko **Obnovit původní data** odstraní jen místní změny a znovu načte přiložené JSON soubory. Cookies si pamatují pouze jméno a vybraný pohled kalendáře; neukládají týmová data ani tokeny.
