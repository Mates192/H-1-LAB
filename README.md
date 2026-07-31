# H-1 Tail Rotor Lab

Interaktivní výuková simulace směrové dynamiky vrtulníků společné platformy **H-1**:

- **UH-1Y Venom** – víceúčelový / assault-support vrtulník;
- **AH-1Z Viper** – bitevní a eskortní vrtulník.

Aplikace běží jako jediný samostatný soubor [`index.html`](index.html). Nepoužívá framework, externí knihovny ani serverovou část a po stažení funguje offline.

> **Bezpečnostní upozornění:** Jde o neověřený kvalitativní výukový model. Není to schválený model Bell, USMC ani DoD a nesmí být použit pro plánování letu, výcvik posádek, stanovení limitů, konstrukční výpočty, certifikaci nebo vyšetřování událostí.

## Co bylo při převodu na H-1 změněno

- přidána přímá volba **UH-1Y / AH-1Z**;
- nahrazena geometrie pětilistého hlavního a třílistého ocasního rotoru společnou čtyřlistou soustavou H-1;
- změněn rozsah hmotnosti na třídu H-1 a pro každý typ přidána vlastní výchozí hmotnost a odhad směrové setrvačnosti;
- výkonový rozpočet vychází ze dvou motorů T700-GE-401C a v rozhraní se zobrazuje v `shp`;
- odstraněn původní typově specifický omezovač úhlu ocasního rotoru;
- odstraněna původní typově specifická směrová OGE korekce – dokud nebude k dispozici veřejný H-1 podklad, je korekce záměrně nulová;
- změněny rozměry, otáčky, počty listů, odhad momentového ramene, aerodynamické plochy a výchozí kalibrace;
- značka, metadata, odkazy a přístupný popis nyní odpovídají projektu H-1.

## Otevření a spuštění

### Online odkaz (GitHub Pages) — doporučený postup bez Actions

Protože jde o jediný statický soubor, nejjednodušší je publikování přímo z větve:

1. Nejdříve ověřte, že na GitHubu ve větvi `main` skutečně vidíte soubor **`index.html`** (nikoliv `index.xml`).
2. Otevřete **Settings → Pages**.
3. V **Build and deployment → Source** zvolte **Deploy from a branch** — ne `GitHub Actions`.
4. V nově zobrazených polích nastavte **Branch: `main`** a složku **`/(root)`**.
5. Klikněte **Save** a vyčkejte několik minut.

Aplikace pak bude dostupná na:

**<https://mates192.github.io/H-1-LAB/>**

Správně nasazená verze má v záhlaví text **H-1 Tail Rotor Lab**, štítek **H-1 BUILD 0.2**, volbu UH-1Y/AH-1Z a výchozí hmotnost 7,0 t. Pokud stránka ukazuje jiný typ, původní omezovač nebo výrazně vyšší původní hmotnost, GitHub Pages stále publikuje starý `index.html` z jiné větve či složky.

První nasazení vytvoří v **Actions** automatický běh typu `pages build and deployment`; není potřeba hledat ruční akci `Deploy to GitHub Pages`.

### Proč nemusí být „Deploy to GitHub Pages“ v Actions vidět

Vlastní workflow se objeví pouze tehdy, když soubor **`.github/workflows/deploy.yml` existuje přímo na GitHubu ve výchozí větvi**. Nestačí, že je připravený pouze v lokálním pracovním prostředí nebo v dosud nesloučeném commitu. Tento pracovní repozitář momentálně nemá nastavený Git remote, takže zde vytvořené commity se na účet GitHub automaticky neodeslaly.

Pokud chcete později použít vlastní workflow místo doporučeného branch deploymentu:

1. nahrajte [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) na GitHub se zachováním celé cesty;
2. commitněte jej do `main`;
3. v **Settings → Pages** změňte **Source** na **GitHub Actions**;
4. obnovte kartu **Actions** — vlevo se pak zobrazí `Deploy to GitHub Pages`;
5. workflow lze spustit ručně díky `workflow_dispatch` nebo automaticky novým pushem do `main`.

### Nejjednodušší lokální spuštění

Stáhněte repozitář nebo samotný [`index.html`](index.html) a otevřete `index.html` dvojklikem v moderním prohlížeči. Aplikace nemá externí závislosti a funguje offline.

### Lokální HTTP server

V adresáři projektu spusťte:

```bash
python3 -m http.server 8000
```

Poté otevřete **<http://localhost:8000/>**. Server ukončíte klávesami `Ctrl+C`.

## Ovládání

1. Vyberte **H-1 variant**.
2. Při pozastavené simulaci nastavte hmotnost, rozložení hmoty, výšku, teplotu a vítr.
3. **Power** určuje procento dostupného společného výkonu obou motorů.
4. **Yaw Pedals** představují zjednodušený geometrický úhel listu ocasního rotoru v referenčním poloměru.
5. Stiskněte **Start** a sledujte tah, momenty, úhlovou rychlost, výkon a zjednodušený stav LTE.
6. **Reset** zachová prostředí, ale znovu vypočítá vis a směrový trim vybrané varianty.

Přepnutí UH-1Y/AH-1Z simulaci bezpečně pozastaví, načte parametry varianty a znovu vypočítá kalibraci a trim.

## Co je veřejný údaj a co je odhad

Veřejné produktové informace spolehlivě popisují společnou H-1 platformu, čtyřlistou rotorovou soustavu, dvojici motorů T700-GE-401C, průměr hlavního rotoru a maximální vzletovou hmotnost. Detailní hodnoty potřebné pro blade-element model – například přesná tětiva a kroucení listů, otáčky ocasního rotoru, převodový poměr, kolektivní dorazy, polára profilu, poloha těžiště a moment setrvačnosti – nejsou v použitých veřejných produktových podkladech úplné.

Proto jsou parametry rozděleny takto:

| Parametr | Hodnota v modelu | Stav |
|---|---:|---|
| motory | 2 × T700-GE-401C, společně 3 600 shp | veřejný typ motoru; výkon zjednodušený na nominální modelový rozpočet |
| maximální hmotnost | 8 391 kg / 18 500 lb | veřejný údaj |
| průměr hlavního rotoru | 14,63 m / 48 ft | veřejný údaj |
| listy hlavního / ocasního rotoru | 4 / 4 | veřejně pozorovatelná konfigurace |
| otáčky hlavního rotoru | 324 rpm | pracovní odhad pro výukový model |
| průměr ocasního rotoru | 2,92 m | pracovní geometrický odhad |
| otáčky ocasního rotoru | 1 660 rpm | pracovní odhad odvozený z nezaručeného převodového poměru |
| rameno ocasního rotoru | 9,0 m | geometrický odhad |
| mez úhlu listu | −10° až +20° | modelový rozsah, nikoliv provozní limit H-1 |
| směrová OGE korekce | 0 | záměrně vypnuta bez veřejného H-1 nomogramu |
| momenty setrvačnosti a boční plochy | odlišné pro UH-1Y/AH-1Z | inženýrské odhady pro kvalitativní porovnání |

Úplný registr parametrů a jejich původu je v [`spec.md`](spec.md).

## Co je potřeba pro skutečně H-1 specifičtější výpočty

Největší přínos nemá přidávání dalších odhadovaných konstant, ale získání **legálně použitelné dokumentace a referenčních bodů**. Podklady by měly vždy uvádět variantu, konfiguraci, jednotky, atmosférické podmínky, režim motorů a číslo strany nebo obrázku.

| Priorita | Potřebný podklad | Co v modelu zpřesní |
|---:|---|---|
| 1 | otáčky hlavního a ocasního rotoru, převodové poměry a limity převodovek | moment z výkonu, rychlosti listů a dostupný výkon ocasního rotoru |
| 1 | skutečný rozsah kolektivního úhlu ocasního rotoru a jeho vazba na pedál | trim, maximální tah a rezerva směrového řízení |
| 1 | OGE hover charts pro hmotnost, pressure altitude, OAT a výkonový režim | vis, přebytek výkonu a vertikální rychlost bez generického density-lapse odhadu |
| 1 | alespoň několik ověřených hover trim bodů | kalibraci tahu, momentu a podílu výkonu ocasního rotoru |
| 2 | geometrie listů: tětiva, kroucení, kořenový výřez, profil a poláry `Cl/Cd` | blade-element tah, výkon a počátek odtržení |
| 2 | T700-GE-401C engine deck a limity podle teploty/výšky | dostupný výkon, flat-rating a výkon OEI/AEO |
| 2 | poloha těžiště a rameno náboje ocasního rotoru pro běžné konfigurace | správný moment ocasního rotoru |
| 3 | hmotové konfigurace a `I_z`, případně CAD/weight-and-balance data | rychlost směrové odezvy AH-1Z vs. UH-1Y |
| 3 | boční aerodynamické derivace, kýlové plochy a rotorová interference podle azimutu větru | korouhvičkový moment, tlumení a realistický LTE model |
| 3 | letová nebo testovací časová data pedál → yaw rate | validaci dynamiky, tlumení a časových konstant |

### Minimální použitelný kalibrační balíček

Pro první výrazné zpřesnění stačí dodat:

1. potvrzené `NR` a otáčky/převod ocasního rotoru;
2. průměr, počet listů, tětivu a pracovní rozsah úhlu ocasního rotoru;
3. 5–10 OGE bodů ve formátu `typ, hmotnost, PA, OAT, výkonový režim, požadovaný výkon`;
4. 3–5 trim bodů ve formátu `typ, hmotnost, PA, OAT, vítr, hlavní výkon/moment, poloha pedálu nebo tah TR`;
5. zdroj každé hodnoty a informaci, zda smí být veřejně publikována.

Citlivé, exportně omezené, neveřejné nebo autorsky neoprávněné podklady do veřejného repozitáře nepatří. Pokud lze sdílet pouze výsledné anonymizované referenční body, je možné model kalibrovat proti nim bez zveřejnění původního dokumentu; původ a omezení ale musí být zaznamenány mimo veřejný repozitář.

## Fyzikální jádro

Model zachovává:

- ISA tlak, volitelnou teplotu a hustotu vzduchu;
- rozdělení společného výkonu mezi ocasní a hlavní rotor;
- teorii hybnosti a zjednodušený blade-element výpočet;
- zpětnou vazbu větru a pohybu náboje ocasního rotoru při zatáčení;
- reakční moment hlavního rotoru, moment ocasního rotoru, moment bočního větru a tlumení;
- integraci směrové dynamiky pevným krokem `1/120 s`;
- názorný, nikoliv typově validovaný model ztráty tahu za kritickým úhlem.

## Důležitá omezení

Model nezahrnuje skutečné H-1 performance charts, FADEC, limity T700, transientní výkon, limity převodovek, pokles otáček, řízení stabilizačním systémem, rotorovou interferenci, detailní kýlové plochy, přízemní efekt, dopředný let, dynamické odtržení ani skutečnou typovou definici LTE. Výpočet výkonu s výškou je generický hustotní lapse model, nikoliv engine deck T700-GE-401C.

AH-1Z a UH-1Y sdílejí v aplikaci pohonnou a rotorovou soustavu. Rozdíl modelu je zatím v roli, výchozí/minimální hmotnosti, odhadovaném momentu setrvačnosti a boční aerodynamické ploše. To umožňuje poctivé kvalitativní porovnání bez předstírání neveřejné přesnosti.

## Veřejné výchozí zdroje

- [Bell AH-1Z Viper](https://www.bellflight.com/products/bell-ah-1z)
- [Bell UH-1Y Venom](https://www.bellflight.com/products/bell-uh-1y)
- [U.S. Navy – AH-1Z Viper](https://www.navy.mil/Resources/Fact-Files/Display-FactFiles/Article/2160217/ah-1z-viper/)
- [U.S. Navy – UH-1Y Venom](https://www.navy.mil/Resources/Fact-Files/Display-FactFiles/Article/2160216/uh-1y-venom/)
- [GE Aerospace – T700 family](https://www.geaerospace.com/propulsion/military/t700)

Odkazy jsou určeny k dohledání základních veřejných údajů. Hodnota v aplikaci označená jako odhad se nestává schváleným údajem jen proto, že je odvozena z veřejné geometrie.

## Licence a další rozvoj

Nejdůležitější další krok je získat legálně sdílitelný a citovatelný podklad pro otáčky/převod ocasního rotoru, pracovní rozsah kolektivu, rotorové profily a OGE výkonové grafy. Po jejich získání je nutné aktualizovat registr v `spec.md`, doplnit testovací referenční body a teprve poté zpřesňovat kalibraci.
