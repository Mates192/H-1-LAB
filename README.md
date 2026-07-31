# Tail Rotor Thrust Simulator

Interaktivní výuková simulace ukazuje, jak se při visu mimo vliv země (OGE, *out of ground effect*) vzájemně ovlivňují výkon motorů, reakční moment hlavního rotoru, tah ocasního rotoru, vítr, hustota vzduchu a rozložení hmotnosti vrtulníku.

Aplikace je tvořena jediným souborem [`index.html`](index.html), nevyžaduje instalaci ani připojení k internetu a veškeré výpočty provádí lokálně v prohlížeči.

> **Upozornění:** Jde o zjednodušený kvalitativní a výukový model obecného vrtulníku o hmotnosti 9–13 tun. Není určen pro konstrukční výpočty, plánování letu, výcvik posádek, certifikaci ani analýzu skutečných nehod.

## Smysl aplikace

Hlavní rotor se při pohledu shora otáčí po směru hodinových ručiček. Na trup proto působí opačný, tedy kladný moment proti směru hodinových ručiček. Ocasní rotor vytváří boční sílu ve vzdálenosti od těžiště a tím tento moment vyrovnává. Pokud součet momentů není nulový, vznikne úhlové zrychlení a vrtulník začne měnit směr.

Simulace názorně ukazuje zejména to, že:

- poloha pedálů určuje geometrické nastavení listů ocasního rotoru, nikoliv přímo jeho tah;
- úhel náběhu a tah ocasního rotoru se mění také s větrem a s rychlostí otáčení vrtulníku;
- skutečný tah ocasního rotoru se může lišit od tahu potřebného pro ustálený směr;
- oba rotory čerpají výkon ze společného výkonového rozpočtu motorů;
- výška a teplota mění hustotu vzduchu, aerodynamické síly i dostupný výkon;
- překročení kritického úhlu náběhu může v použitém zjednodušeném modelu způsobit prudký pokles tahu ocasního rotoru a stav označený jako LTE;
- velikost momentu setrvačnosti určuje, jak rychle vrtulník na nevyvážený moment zareaguje.

## Spuštění

Aplikaci lze spustit online přes GitHub Pages na adrese [https://vrabczak.github.io/TailRotorLab/](https://vrabczak.github.io/TailRotorLab/).

Nejjednodušší způsob je otevřít soubor [`index.html`](index.html) ve webovém prohlížeči. Na Windows jej lze otevřít dvojitým kliknutím.

## Návod k použití

1. Nastavte podmínky a konfiguraci vrtulníku. Na začátku je simulace pozastavena a tlačítko zobrazuje **Start**.
2. Pomocí **Yaw Pedals** nastavte úhel listů ocasního rotoru a pomocí **Power** společný výkon motorů.
3. Stiskněte **Start**. Vrtulník se začne otáčet, pokud nejsou momenty v rovnováze.
4. Během běhu lze měnit pedály a výkon. Pro změnu větru, výšky, teploty, hmotnosti nebo momentu setrvačnosti simulaci nejprve pozastavte tlačítkem **Pause**.
5. Sledujte směr a rychlost otáčení, skutečný a požadovaný tah, úhly náběhu, rozdělení výkonu, stav LTE a jednotlivé momenty.
6. **Reset** zachová nastavení větru, hmotnost, výšku, teplotu a moment setrvačnosti. Vrtulník vrátí do výchozí polohy a kurzu, vynuluje jeho rychlost otáčení a simulaci pozastaví. Výkon automaticky nastaví tak, aby vrtulník visel bez stoupání nebo klesání, a pedály nastaví tak, aby tah ocasního rotoru vyvažoval reakční moment hlavního rotoru.

Při pozastavené simulaci změna výkonu automaticky přestaví ocasní rotor do přibližného směrového vyvážení. Za běhu jsou výkon a pedály nezávislé, takže lze přímo vyvolat změnu směru.

### Ovládací prvky

| Ovládání | Rozsah | Význam |
|---|---:|---|
| **Yaw Pedals** | −6° až limit SPUU-52 | Geometrický úhel listu ocasního rotoru; atmosférický limit je přibližně 20,6–23,2°. |
| **Power** | 0–100 % | Podíl z maximálního výkonu dostupného v daných atmosférických podmínkách. |
| **Wind speed** | 0–25 m/s | Rychlost větru. |
| **Wind from** | 0–359° | Meteorologický směr, **odkud** vítr vane; 0° = sever, 90° = východ. |
| **MSA altitude** | 0–6 000 m | Nadmořská výška. Její změna nastaví standardní ISA teplotu pro danou výšku. |
| **Temperature** | −50 až +50 °C | Skutečná zvolená teplota; její ruční změna již výšku nemění. |
| **Weight** | 9,0–13,0 t | Hmotnost vrtulníku pro vis a vertikální výkon. |
| **Angular Momentum** | podle hmotnosti | Ve skutečnosti zjednodušený moment setrvačnosti kolem svislé osy. Vyšší hodnota znamená pomalejší změny rychlosti otáčení. |

Klávesové zkratky fungují, pokud kurzor není v editačním poli:

- `←` / `→`: změna pedálů o 1°;
- `Shift` + `←` / `→`: změna pedálů o 1°;
- při pozastavení `↑` / `↓`: změna výkonu o 1 %;
- při pozastavení `Shift` + `↑` / `↓`: změna výkonu o 5 %.

### Jak číst výstupy

- **Yaw rate** a **Heading** udávají rychlost a aktuální směr otáčení. CCW znamená proti směru, CW po směru hodinových ručiček při pohledu shora.
- **Actual tail-rotor thrust** je skutečný výsledek listového výpočtu.
- **Required tail-rotor thrust** je okamžitě potřebný tah pro vyrovnání momentu hlavního rotoru a větru; nezahrnuje obecné rotační tlumení.
- **Mean blade angle of attack** a jeho rozsah ukazují, jak se podmínky liší po poloměru a azimutu rotoru.
- **Relative axial airflow** je podepsaná složka proudění kolmá k disku ocasního rotoru.
- **Main-rotor OGE lift capability** vyjadřuje vypočtenou nosnost hlavního rotoru v kgf.
- **Power split** ukazuje rozdělení společného výkonu mezi hlavní a ocasní rotor.
- **Hover efficiency** je *figure of merit* obou rotorů; vyšší hodnota znamená menší rozdíl mezi ideálním a skutečně požadovaným výkonem.
- **Blade elements above critical α** a **Simplified LTE state** upozorňují na oblast ztráty tahu za kritickým úhlem 12°.
- Graf **Live tail-rotor thrust curve** zobrazuje pevnou referenční křivku a aktuální pracovní bod. Osa tahu má stálý rozsah 0–35 kN.

## Souřadnice a znaménka

- Osa tělesa (x) míří dopředu, (y) doleva a (z) nahoru.
- Kladné otáčení je proti směru hodinových ručiček při pohledu shora.
- Reakční moment hlavního rotoru je kladný, moment běžného tahu ocasního rotoru záporný.
- Počáteční kurz je sever, tedy 000°.
- Směr větru je meteorologický: údaj 090° označuje vítr z východu, jeho vektor proudění proto míří na západ.

## Použité fyzikální a aerodynamické jevy

### Standardní atmosféra, teplota a hustota

Standardní teplota ve výšce $h$ a standardní tlak jsou počítány jako

$$
T_{ISA}(h)=T_0-Lh,
$$

$$
p(h)=p_0\left(1-\frac{Lh}{T_0}\right)^{\frac{g}{R L}},
$$

kde $T_0=288{,}15\ \mathrm{K}$, $L=0{,}0065\ \mathrm{K/m}$, $g=9{,}80665\ \mathrm{m/s^2}$ a $R=287{,}05287\ \mathrm{J/(kg\,K)}$. Hustota vychází ze stavové rovnice ideálního plynu a používá zvolenou, nikoliv nutně standardní teplotu:

$$
\rho(h,T_C)=\frac{p(h)}{R(T_C+273{,}15)}.
$$

Nižší hustota zmenšuje aerodynamické síly při stejné rychlosti listu a zvyššuje indukovaný výkon potřebný k vytvoření daného tahu.

### Dostupný výkon motorů

Model vychází ze společného jmenovitého výkonu $P_{max}=4\,000$ metrických koní, tedy přibližně $2{,}942\ \mathrm{MW}$. Zjednodušený model inspirovaný motory TV3-117VM drží výkon konstantní do výšky $h_{flat}=3\,600\ \mathrm{m}$, nad ní jej snižuje poměrem hustot:

$$
f_{eng}(h,T_C)=
\begin{cases}
1, & h\le h_{flat},\\
\dfrac{\rho(h,T_C)}{\rho(h_{flat},T_{ISA}(h_{flat}))}, & h>h_{flat}.
\end{cases}
$$

Pro zvolenou polohu ovladače $u\in\langle0,1\rangle$ je

$$
P_{available}=uP_{max}f_{eng}.
$$

Ocasní rotor má při rozdělení výkonu přednost; zbytek připadne hlavnímu rotoru:

$$
P_{mr}=\max(0,P_{available}-P_{tr}).
$$

Pokud požadovaný aerodynamický výkon překročí dostupný výkon, aplikace zachová jmenovité otáčky rotorů a upozorní na neudržitelný pracovní bod. Dynamiku motorů, regulátoru ani pokles otáček nepočítá.

### Reakční moment hlavního rotoru

Výkon na rotujícím hřídeli a moment souvisejí vztahem

$$
Q_{mr}=\frac{P_{mr}}{\Omega_{mr}},
$$

kde hlavní rotor používá pevné otáčky 192 rpm. Tento moment působí na trup proti směru otáčení rotoru.

Tah hlavního rotoru se neurčuje prostou přímou úměrou výkonu. Ideální výkon pro vis podle teorie hybnosti je

$$
P_{ideal,mr}=\frac{T_{mr}^{3/2}}{\sqrt{2\rho A_{mr}}}.
$$

Model k němu přidává indukované a profilové ztráty:

$$
P_{i,mr}=\kappa_{mr}
\frac{T_{mr}^{3/2}}{\sqrt{2\rho A_{eff,mr}}},
$$

$$
P_{0,mr}=\rho A_{mr}(\Omega_{mr}R_{mr})^3
\frac{\sigma_{mr}\bar C_{d,mr}}{8}.
$$

Požadovaný výkon je omezen také kalibrovanou účinností (*figure of merit*, $FM$):

$$
P_{req,mr}(T)=\max\left(P_{i,mr}+P_{0,mr},\frac{P_{ideal,mr}}{FM_{mr,ref}}\right).
$$

Simulace numericky hledá takový tah $T_{mr}$, pro který se požadovaný výkon rovná výkonu dostupnému hlavnímu rotoru. Referenční bod odpovídá přibližně 14 000 kgf OGE nosnosti při plném výkonu na hladině moře.

### Proudění a listový model ocasního rotoru

Ocasní rotor má tři listy, poloměr $R_{tr}=1{,}954\ \mathrm{m}$, otáčky 1 120 rpm a aerodynamický kořenový výřez do $0{,}2R$. Rotor je rozdělen na 12 radiálních a 24 azimutálních vzorků. Výsledky se průměrují za celou otáčku.

Rychlost vzduchu vůči náboji zahrnuje vítr i pohyb náboje způsobený otáčením vrtulníku:

$$
\vec V_{ext,tr}=\vec V_{air,body}-(\vec\omega\times\vec r_{tr}).
$$

Toto je důležitá zpětná vazba: již vzniklá rychlost otáčení změní místní proudění, úhel náběhu a následně tah ocasního rotoru.

Pro element ve vzdálenosti $r$ a azimutu $\beta$ jsou tangenciální a kolmá složka relativní rychlosti

$$
U_t=\Omega_{tr}r-V_{plane,t},
\qquad
U_p=v_i+V_{ax,ext}.
$$

Úhel proudění a úhel náběhu listu jsou

$$
\phi=\mathrm{atan2}(U_p,U_t),
\qquad
\alpha=\theta_{tr}-\phi.
$$

Proto není geometrický úhel $\theta_{tr}$ totožný s aerodynamickým úhlem náběhu $\alpha$.

V lineární oblasti je součinitel vztlaku profilu

$$
C_{l,lin}=\mathrm{clamp}\!\left[a(\alpha-\alpha_{0L}),C_{l,min},C_{l,max}\right],
$$

kde $a=5{,}7\ \mathrm{rad^{-1}}$, $\alpha_{0L}=-1{,}2^\circ$, $C_{l,min}=-1{,}2$ a $C_{l,max}=1{,}5$. Odporová polára je

$$
C_d=C_{d,0}+k_dC_l^2.
$$

Pro velikost relativní rychlosti $W=\sqrt{U_t^2+U_p^2}$ vzniknou na elementu šířky $dr$ síly

$$
dL=\frac12\rho W^2c_{tr}C_l\,dr,
\qquad
dD=\frac12\rho W^2c_{tr}C_d\,dr,
$$

a příspěvek k užitečnému tahu

$$
dT=dL\cos\phi-dD\sin\phi.
$$

Celkový tah je součtem přes listy a radiální prvky a průměrem přes azimut:

$$
T_{tr}=\frac{1}{N_\beta}\sum_\beta\sum_b\sum_r dT.
$$

### Indukovaná rychlost a výkon ocasního rotoru

Rotor urychluje proud vzduchu skrz svůj disk. Kvazistacionární indukovaná rychlost podle teorie hybnosti je

$$
v_i=\sqrt{\frac{\max(T_{tr},0)}{2\rho A_{tr}}},
\qquad A_{tr}=\pi R_{tr}^2.
$$

Protože tah závisí na $v_i$ a $v_i$ současně závisí na tahu, aplikace používá sedm relaxovaných iterací. Potřebný výkon dále zahrnuje indukovanou složku, profilový odpor, ztrátu na konci listů a kalibrační ztrátu tak, aby účinnost ocasního rotoru nepřekročila $FM_{tr,max}=0{,}52$.

### Ztráta účinnosti ocasního rotoru (zjednodušené LTE)

Do kritického úhlu $\alpha_{crit}=12^\circ$ se používá lineární vztlaková charakteristika. Nad kritickým úhlem je součinitel vztlaku plynule redukován pomocí funkce

$$
s(t)=3t^2-2t^3,
\qquad
t=\mathrm{clamp}\left(\frac{\alpha-\alpha_{crit}}{\alpha_{collapse}-\alpha_{crit}},0,1\right),
$$

$$
C_l=C_l(\alpha_{crit})\left[1-s(t)(1-f_{post})\right],
$$

kde $\alpha_{collapse}=19^\circ$ a po úplném rozvinutí poklesu zůstává $f_{post}=0{,}18$ původního vztlaku. Stav se klasifikuje následovně:

- **Normal:** žádný vzorek nepřekročil 12°;
- **LTE onset:** kritický úhel překročilo méně než 20 % vzorků;
- **LTE — thrust loss:** kritický úhel překročilo alespoň 20 % vzorků.

Jde pouze o názorný model lokálního odtržení proudění. Skutečná LTE (*loss of tail-rotor effectiveness*) může vznikat kombinací interakce vírů hlavního a ocasního rotoru, bočního větru, korouhvičkové stability a dalších jevů; není definována jedním univerzálním úhlem náběhu.

### Moment ocasního rotoru a potřebný tah

Ocasní rotor je ve vzdálenosti $L_{tr}=12{,}748\ \mathrm{m}$ od těžiště. Jeho moment je

$$
Q_{tr}=-T_{tr}L_{tr}.
$$

Tah potřebný k okamžitému vyrovnání reakce hlavního rotoru a větru je

$$
T_{tr,required}=\frac{Q_{mr}+Q_{wind}}{L_{tr}}.
$$

Rozdíl mezi touto hodnotou a skutečným tahem určuje, zda se nezahrnutím tlumení vytváří moment po, nebo proti směru hodinových ručiček.

### Aerodynamický moment větru na trup

Boční složka větru $V_y$ působí na zjednodušenou boční plochu trupu:

$$
F_{wind,y}=\frac12\rho C_{d,y}A_yV_y|V_y|,
$$

$$
Q_{wind}=x_{cp}F_{wind,y},
$$

kde $C_{d,y}=1$, $A_y=25\ \mathrm{m^2}$ a střed tlaku leží $x_{cp}=-1{,}2\ \mathrm{m}$ za těžištěm. Kvadratický člen zachová znaménko směru a současně vytváří obvyklou závislost síly na druhé mocnině rychlosti. Jde o souhrnný korouhvičkový model, nikoliv detailní výpočet jednotlivých částí trupu a ocasních ploch.

### Vliv směru větru na OGE výkon

Vedle přímého působení větru na trup a ocasní rotor používá model digitizovanou korekci mezní hmotnosti visu ve výšce 20 m z grafu pro Mi-8MTV-5-1. Korekce $\Delta G$ je tabulkově určena pro přední, boční a zadní vítr, mezi rychlostmi a směry se interpoluje. Kladná hodnota zlepšuje podmínky visu:

$$
G_{equiv}=G-\Delta G.
$$

Tabulka pokrývá 0–10 m/s. Do 11,11 m/s pokračuje poslední známý sklon a nad touto rychlostí se OGE korekce drží konstantní, protože další režim již přesahuje rozsah modelu visu. Proudění u ocasního rotoru však reaguje na celý rozsah větru až do 25 m/s.

Vertikální rychlost vychází z přebytku výkonu:

$$
v_{target}=\mathrm{clamp}\left(\frac{P_{mr}-P_{hover}}{mg},-25,25\right).
$$

Model se k této rychlosti přibližuje s časovou konstantou $\tau=2{,}5\ \mathrm{s}$:

$$
\dot v=\mathrm{clamp}\left(\frac{v_{target}-v}{\tau},-4,4\right).
$$

Tento údaj je pouze energetický odhad stoupání nebo klesání; poloha vrtulníku se v prostoru nesimuluje.

### Směrová dynamika a tlumení

Součet aerodynamických a rotorových momentů před tlumením je

$$
Q_{rotors+wind}=Q_{mr}+Q_{tr}+Q_{wind}.
$$

Zbytkové aerodynamické tlumení trupu a stabilizačních ploch je aproximováno lineárním a kvadratickým členem:

$$
Q_{damping}=-c_1\omega-c_2\omega|\omega|,
$$

kde $c_1=1\,200\ \mathrm{N\,m\,s/rad}$ a $c_2=1\,000\ \mathrm{N\,m\,s^2/rad^2}$. Celkový moment a úhlové zrychlení jsou

$$
Q_{net}=Q_{mr}+Q_{tr}+Q_{wind}+Q_{damping},
\qquad
\dot\omega=\frac{Q_{net}}{I_z}.
$$

Stav se integruje explicitním Eulerovým krokem $\Delta t=1/120\ \mathrm{s}$:

$$
\omega_{k+1}=\omega_k+\dot\omega_k\Delta t,
$$

$$
\psi_{k+1}=\psi_k+\omega_{k+1}\Delta t.
$$

Ovladač **Angular Momentum** tedy fyzikálně představuje $I_z$, nikoliv moment hybnosti $L=I_z\omega$. Při změně hmotnosti se zachová zvolené rozložení hmoty pomocí vztahu

$$
I_{z,1}=I_{z,0}\frac{m_1}{m_0}.
$$

## Doporučené experimenty

1. **Rovnováha momentů:** začněte v bezvětří, spusťte simulaci a mírně změňte pedály. Porovnejte skutečný a potřebný tah.
2. **Vliv setrvačnosti:** opakujte stejnou změnu pedálů s minimální a maximální hodnotou **Angular Momentum**. Moment zůstane podobný, ale úhlové zrychlení se změní.
3. **Boční vítr:** nastavte vítr z 90° a poté z 270°. Sledujte obrácení momentu větru a změnu úhlů náběhu ocasního rotoru.
4. **Horko a výška:** porovnejte vis na hladině moře a v 4 000 m při vysoké teplotě. Sledujte hustotu, výkon, nosnost a limit SPUU-52.
5. **LTE:** při běžící simulaci zvětšujte pedálový úhel nebo nastavte nevýhodné proudění a sledujte pracovní bod v grafu za hranicí 12° a následný pokles tahu.
6. **OGE korekce:** při stejné hmotnosti porovnejte přední a zadní vítr. Sledujte změnu ekvivalentní nosnosti, potřebného výkonu a vertikální rychlosti.

## Omezení modelu

Simulace nezahrnuje:

- vliv země (IGE), pohyb vrtulníku v horizontální rovině ani změnu skutečné výšky;
- klonění, klopení, mávání listů, kuželovitost a gyroskopické jevy;
- dynamické odtržení proudění, dynamiku vírového prstence ani *settling with power*;
- úplný model LTE, interferenci víru hlavního rotoru s ocasním rotorem ani detailní stabilitu ocasních ploch;
- dynamiku motorů a převodovky, regulaci otáček, ztráty pohonu, palivo nebo pokles rotorových otáček;
- turbulence, poryvy, střih větru, terén a překážky;
- přesnou aerodynamiku konkrétního typu vrtulníku nebo CFD.

Pevné otáčky, empirické korekce a kalibrační ztráty jsou vědomým kompromisem, který udržuje model srozumitelný a výpočetně lehký.

## Technické provedení

- jeden samostatný HTML soubor s vloženými styly, SVG a JavaScriptem;
- bez frameworku, balíčkovacího systému a externích knihoven;
- vykreslování přes `requestAnimationFrame`;
- fyzika s pevným krokem 1/120 s a omezeným doháněním po zpožděném snímku;
- numerické hledání trimu, tahu hlavního rotoru a indukované rychlosti ocasního rotoru;
- responzivní rozhraní ovladatelné myší, dotykem i klávesnicí;
- všechny výpočty a data zůstávají v prohlížeči uživatele.

Podrobný produktový a technický návrh je v souboru [`spec.md`](spec.md).

## Zdroj OGE korekce

Korekce vlivu větru vychází z digitalizovaných hodnot uvedených ve specifikaci projektu pro Mi-8MTV-5-1. Doplňující popis přechodu z axiálního do šikmého obtékání je odvozen z veřejně dostupného [aerodynamického manuálu Mi-8MTV2](https://www.digitalcombatsimulator.ru/upload/iblock/458/DCS-Mi-8MTV2_FlightManual_RU.pdf). Ostatní parametry slouží jako kalibrační hodnoty tohoto výukového modelu a nemají představovat schválená provozní data konkrétního stroje.
