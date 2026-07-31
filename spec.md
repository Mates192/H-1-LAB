# H-1 Tail Rotor Lab — produktová a technická specifikace

## 1. Stav dokumentu

- **Produkt:** H-1 Tail Rotor Lab
- **Varianty:** UH-1Y Venom a AH-1Z Viper
- **Formát:** jediný offline spustitelný `index.html`
- **Účel:** kvalitativní demonstrace směrové rovnováhy ve visu OGE
- **Stav validace:** nevalidovaný výukový prototyp

## 2. Zásady převodu na H-1

1. Parametry specifické pro Mi-8/Mi-171 se nesmějí potichu přenést na H-1.
2. Veřejně doložené údaje, inženýrské odhady a čistě didaktické konstanty musí být rozlišeny.
3. Chybějící H-1 tabulka se nahrazuje neutrální hodnotou, ne tabulkou jiného typu.
4. Přepnutí varianty musí přepočítat výkonové konstanty, kalibraci, trim, hmotnost a moment setrvačnosti.
5. Výstup nesmí být prezentován jako provozní limit ani jako Bell/USMC schválený model.

## 3. Konfigurace variant

### 3.1 Společná platforma

| Pole v kódu | Hodnota | Klasifikace | Poznámka |
|---|---:|---|---|
| `enginePowerShaftHp` | 3 600 shp | zjednodušený veřejně inspirovaný údaj | společný rozpočet 2 × T700-GE-401C; název pole je historický |
| `wattsPerShaftHorsepower` | 745,699872 W/shp | definice jednotky | ve skutečnosti převod mechanického horsepower |
| `maxHelicopterWeightKg` | 8 391 kg | veřejný údaj | ekvivalent 18 500 lb |
| `mainRotorRadiusM` | 7,315 m | veřejný rozměr | průměr 48 ft |
| `mainRotorBlades` | 4 | veřejný údaj | společná rotorová soustava H-1 |
| `mainRotorRpm` | 324 rpm | pracovní odhad | vyžaduje ověření z citovatelného technického podkladu |
| `tailRotorBlades` | 4 | veřejně pozorovatelná konfigurace | přesná geometrie není validována |
| `tailRotorRadiusM` | 1,46 m | pracovní odhad | neprovozní hodnota |
| `tailRotorRpm` | 1 660 rpm | pracovní odhad | neprovozní hodnota |
| `tailMomentArmM` | 9,0 m | geometrický odhad | vzdálenost účinné síly od těžiště |
| `tailRotorMinPitchDeg` | −10° | didaktická konstanta | není řídicí doraz H-1 |
| `tailRotorPhysicalMaxPitchDeg` | +20° | didaktická konstanta | není řídicí doraz H-1 |
| `criticalAlphaRad` | 12° | didaktický airfoil model | není typová mez LTE |

### 3.2 UH-1Y Venom

- výchozí modelová hmotnost: 7 000 kg;
- rozsah: 5 400–8 391 kg;
- výchozí odhad `I_z`: 48 000 kg·m²;
- modelová boční plocha: 18 m²;
- rameno středu tlaku: −0,9 m.

### 3.3 AH-1Z Viper

- výchozí modelová hmotnost: 6 800 kg;
- rozsah: 5 600–8 391 kg;
- výchozí odhad `I_z`: 44 000 kg·m²;
- modelová boční plocha: 14 m²;
- rameno středu tlaku: −0,7 m.

Rozdíly mezi variantami jsou záměrně omezeny na parametry, které lze v tomto stupni modelu obhájit kvalitativně. Zbraňové konfigurace, vnější závěsníky, kabina, užitečné zatížení a konkrétní poloha těžiště zatím nejsou samostatné volby.

## 4. Výpočtový model

### Atmosféra

Aplikace počítá standardní tlak v troposféře a hustotu ze zadané skutečné teploty. Výkon motorů nad hladinou moře klesá generickým poměrem hustot. Toto není T700 engine deck.

### Výkon a hlavní rotor

Ocasní rotor odebírá požadovaný výkon ze společného rozpočtu jako první. Zbytek připadne hlavnímu rotoru. Tah hlavního rotoru se řeší numericky z teorie hybnosti, indukovaných a profilových ztrát a kalibrovaného figure of merit.

### Ocasní rotor

Disk je rozdělen na 12 radiálních a 24 azimutálních vzorků. Výpočet používá lokální relativní rychlost, úhel proudění, lineární vztlakovou charakteristiku, odporovou poláru a sedm relaxovaných iterací indukované rychlosti.

### Směrová dynamika

Do výsledného momentu vstupuje reakční moment hlavního rotoru, síla ocasního rotoru na modelovém rameni, moment bočního větru a lineárně-kvadratické tlumení. Stav je integrován explicitním Eulerovým krokem `1/120 s`.

### OGE vítr

Všechny křivky `OGE_WIND_NOMOGRAM` jsou nulové. Vítr nadále ovlivňuje ocasní rotor a boční moment trupu, ale nemění mezní hmotnost visu. Jde o záměrnou ochranu proti chybnému použití nomogramu Mi-8 na H-1.

## 5. Přepínání varianty

Funkce `selectAircraft()`:

1. vybere záznam z `AIRCRAFT_CONFIGS`;
2. přepočítá společný výkon, úhlovou rychlost hlavního rotoru a výchozí indukovanou rychlost;
3. nastaví výchozí hmotnost a setrvačnost varianty;
4. upraví meze a popisky ovladačů;
5. přepočítá nominální kalibraci;
6. provede reset a nový hover/yaw trim.

Tím se zabrání tomu, aby po změně typu zůstala kalibrace nebo neplatná hmotnost předchozí varianty.

## 6. Akceptační kritéria

- dokument je validní HTML a JavaScript projde syntaktickou kontrolou;
- v kódu ani viditelném rozhraní nezůstane SPUU-52 nebo Mi-17 konfigurace;
- hlavní rotor má čtyři vykreslené listy;
- volba varianty obsahuje právě UH-1Y a AH-1Z;
- každá varianta po výběru vytvoří konečný numerický trim bez výjimky;
- dokumentace jasně rozlišuje veřejné údaje a odhady;
- směrová OGE korekce je nulová, dokud není doložen H-1 podklad.

## 7. Veřejné zdroje

- Bell: <https://www.bellflight.com/products/bell-ah-1z>
- Bell: <https://www.bellflight.com/products/bell-uh-1y>
- U.S. Navy AH-1Z fact file: <https://www.navy.mil/Resources/Fact-Files/Display-FactFiles/Article/2160217/ah-1z-viper/>
- U.S. Navy UH-1Y fact file: <https://www.navy.mil/Resources/Fact-Files/Display-FactFiles/Article/2160216/uh-1y-venom/>
- GE Aerospace T700: <https://www.geaerospace.com/propulsion/military/t700>

Před další kalibrací je nutné dostupnost, aktuálnost a konkrétní tvrzení ve zdrojích znovu ověřit. Neveřejné nebo exportně omezené podklady se do repozitáře nesmějí přidávat.
