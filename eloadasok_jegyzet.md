> Kommunikáció Teams-en
> Moodle-n jegyzet
> [Hf portálon](hf.mit.bme.hu) - laborjelentkezés, leadandók stb. vagy moodle-ben van automatikus kiértékelés (de naponta 1-szer lehet leadni)
> 1 ZH - 12. héten pénteken
> Viga 60 pont, a jegy 60%-a
> Pluszfeladatok 20 iMsc-ért, 5-5 ZH és Vizsga
> 2.-tól kezdve a Laborok vagy jelenléti vagy online (7 labor van - ne akarjuk utolsó héten leadni)
>
> Zh sávok kedd 18-20, péntek 14-16

# Mesterséges intelligencia

## 1. EA
- *Bevezetés:* alkalmazások, fejlődése, mire jó
    - Az intelligenciához szükség van különböző komponensekre, ezekre sokféle modell van
    - MI megközelítések:
        - Emberi módon gondolkodó: neurális modellezés (ez nem feltétlenül racionális gondolkodás)
        - Emberi módon cselekvő: tudásábrázolás, következtetés, természetes nyelvű értés, tanulás (turing teszt)
        - Racionálisan gondolkodó
        - Racionálisan cselekvő

## 2. EA
- **Probléma megoldás kereséssel:**
    - Nem informált keresési módszer: a célt tudjuk, de nem tudjuk hogyan $\Rightarrow$ pl. DFS, BFS, Uniform-Cost search
    - Racionális ágens: úgy választ, hogy maximalizálja a várható hasznosságot
    - Reflex ágens: valami egyszerű érzékelésre reagál (bejárásnál: amíg van bogyó, addig menjen)
- Keresési fa vs állapottérgráf 
    - *azért végtelen a kvíznél a megoldás, mert kör van a gráfban*
    - DFS: azért nem feltétlenül optimális, mert nem mindig találja meg a magasabban lévő (kevesebb lépéses) azonos megoldást
    - Iteratívan mélyülő keresés: a BFS és DFS előnyeit együtt használja ki, mert a legmélyebb szint megnézése helyett a DFS majd megtalálja az ottani optimális értéket
    - UCS - Egyenletes költségű keresés: a legkisebb költségű csomópontot fejti ki
        - feltételezzük a pozitív éleket
- Útvonal keresések
    - ...
    - A*, ahol a H a heurisztikát jelüli, hogy milyen messze lehet kb a cél
        - f(n) = g(n) + h(n)
        - az elrontott dolognál az A heurisztikáját kéne megjavítani
        - meg kell nézni az összes más útvonalat is, aminek az f(n)-je kisebb, mint amivel a célba eljutottunk

## 3. EA
- Kérdések:
    - Melyik nem optimális? mélységi
    - Melyik hamis? B az iteratívan mélyülő keresés mindig ...
    - K3-at nem vettük
    - K4? 
        *A mohó keresés ha teljes akkor optimális is*
    - K5? heurisztika jó, ha nme becsüli fölé a célig a költségeket
    - K6-K7 nem volt
- Van egy példa a*-ra *(a dián elcsúszik, hogy a 260-nak annyinak is kéne maradnia, de 280 lett for some reason)*
- Tilitolinál a heuriszikák:
    - Manhattan távolság: hányat kell lépni jobbra / balra + fel/le, hogy a helyére kerüljön
        - Ez a heurisztika kicsit javít, de megéri sokat számolni érte?
    - Voltak a triviális heurisztikák...
- Gráf alapú keresés:
    - Ahol már jártunk az ki van fejtve, ezért ha megint odajutnánk azt nem kell kifejteni
    - A heurisztikánk ha jó, akkor mi rontja el az A*-ot?
        - nem elég, hogy mindig kevesebb a heurisztika költsége a valósnál
        - hanem az élköltségre is igaznak kell lennie, hogy $h(A) - h(C) \leq \text{valós költség}(A \to C)$
    - voltak pszeudo kódok
<!--új diasor-->
- Mi történik, ha vannak a keresésnél megkötések?
    - Pl. a térképszínezési probléma, n királynő probléma, sudoku
    - CSP problémák típusai: (Constraint Satisfaction Problem)
        - diszkrét változók - véges / végtelen tartománnyal
        - folytonos változók
    - kényszergráfok
    - az ilyen problémák általában kezdőállapotból egy cél állapotba eljutás olyan operátorokkal, amik megfelelnek a megkötésnek
        - keresési fában azonban ez túl sok állapot lenne, ha van n db változónk, akkor n!*d^n csomópontunk lesz
        - visszalépéses keresés: (backtrack)
            - először csinálunk valamit és ha az sérti bármelyik megkötést, akkor onnan visszalépünk és másik utat választunk
            - egyszerű megoldás, egyszerűbb problémáknál működhet jól, de néha nem *(lassan jön rá, hogy nincs megoldás, vagy néha sokat kell visszalépni ha rossz irányba indul el)*
            - egyáltalán honnan tudjuk, hogy melyik irányba menjünk, honnan induljunk?
                - ezen segíthetnek a heurisztikák
        - visszalépéses keresés + heurisztikák:
            - Szűrési heurisztikák: (hogyan szűrjük ki az útvonalakat)
                - előretekintő ellenőrzés (a jövőből kiszedjük azokat az opciókat, amik sértik a feltételt) $\Rightarrow$ jó ez az előre tekintés, de annyira mégse jó
                - élkonzisztencia: a kényszerek terjesztése kapcsolódó éleken - vagyis $X \to Y$ él akkor és csak akkor konzisztens, ha X minden x értékére létezik Y-nak valami megengedett y értéke $\Rightarrow$ ha X-ben elfogadok egy értéket, akkor Y-ban is lesz olyan érték amivel még megoldható a feladat $\Rightarrow$ sokkal messzebbre előre látunk a jövőben
                Az algoritmus neve AC-3
            - Sorrendezési: (melyik változót válasszuk ki)
                - legkevesebb fenmaradó réték (MRV) heurisztika: ahol a legkisebb számúak a megengedett változók (mert így lesz kevés elágazás)
                - fokszám heurisztika: ami a legtöbb szomszéddal kapcsolatban van (mert így ha erre nincs megoldás, akkor másra sem lesz)
            - Értékhozzárendelés:
                - legkevésbé korlátozó értéket: olyan értéket adjunk a változónak, ami a többi csomópont értékére a legtöbb választást hagyja
    - volt még szó a fák struktúrájára, ha kör van ezekben, akkor szétszedhetjük külön gárfokra és azoknak az értékeire kereshetünk külön megoldásokat

## 4. EA
- A probléma relaxációja: elhagyunk megkötéseket, megtartjuk a változókat
- Heurisztika elfogadható, ha soha nem becsüli felül a cél eléréséhez szükséges költséget
- h1 heurisztika dominálja h2-t, ha: h1 értéke mindig jobb, mint h2 értéke, de legalább akkora mint h2 (vagyis közelebb van a valós költséghez)
- adott változó értékének meghatározásához: a legkevésbé korlátozó érték heurisztika
- bináris korlát: 2 változó viszonyára ad korlátot
- Néztünk további példát a legkevesebb fennmaradó érték heurisztikára

#### Keresés ellenséges környezetben és játékok (adversarial search)
- Játékok típusai: 
    - determinisztikus/sztochasztikus
    - különböző játékosok száma
    - minden információhoz van-e hozzáférés, 
    - zéró összegű játék (ha az egyik csapat/játékos nyer, a másik veszít)
- Leíráshoz lehetőségek:
    - $S$ állapotok $s_0$ a kezdőállapot
    - $P = \set{1...N}$ játékos
    - $A$ cselekvéssel
    - $SxA \to S$ állapotátmenet függvénnyel
    - ... (a dián rajta van)
    - végállapot $V(s)$
- És akkor meg lehet oldani 1 ágens (résztvevő vagy hasonló) esetén, hogy megvizsgáluk, hogy melyik végállapotban érjük el a legtöbb pontot
- De ha 2 ágens van (Pac-man és szellemes példa)
    - Akkor a játékfa úgy néz ki, hogy minden páratlan sorban az egyik lép és minden másikban a másik
- Minmax megoldás:
    - Minimax értékek: a lényeg, hogy minimalizálni akarjuk az ellenfél pontjait és maximalizálni a sajátjaink
    - Vagyis akkor tudunk nyerni, ha a játékfát ki tudjuk fejteni a levelekig és azt kiértékelni
    - Ez a megoldás optimális egy racionális játékossal szemben, de nem mindig számíthatunk erre
    - A minmax hatékonysága olyan, mint a DFS-é, $O(b^m)$ (b - bábúk és m - mélység mellett)
        - De szükséges felderíteni a teljes játékfát?
        - Kis problémáknál lehet az a jó megoldás, hogy 3-4 lépést elgondolunk előre
- Alfa-béta implementáció:
    - Elindulunk úgy, hogy $\alpha=-\infty$ és $\beta=\infty$
    - Lemegyünk a fa aljáig, ahol ha min-é az utolsó lépés, akkor ő kiválasztja azt ami rosszabb nekünk $\Rightarrow \beta=\text{amit min választ, mert nem tudunk jobbat csinálni}$
    - Ezután fellépünk és max jön, viszont neki a min értéke lesz az, amit 1-el lentebbi szinten számolunk
        - És nem fejtjük ki, hogyha min alatt van a várható érték, amit kapni fogunk (mert ha van jobb alternatívánk, akkor nem éri meg a rosszabbal foglalkozni)
    - Mindig csak azt terjesztjük fölfelé, ami a keresés szempontjából releváns
    - Probléma: a legtöbb játéknál nem tudunk lemenni a levelekig, így kifejteni sem
    - De pl. sakknál már 8 mélységig keresünk és a táblán lévő bábúk értékeit használjuk becslésre, az már egész jó
- Véletlenek esetén:
    - Nem tudjuk biztosan az értékeket (pl. kockadobás), de mindeközben a maximum értékre törekszünk
    $\Rightarrow$ Expectimax
    - A változás, hogy minimum helyett várható értéket számolunk
- Kevert rétegű játéknál: ahol a környezet random, ott expectiminmax

## 5. EA
*(Minimax pacman akkor volt jó, amikor a szellem véletlenszerűen mozgott)*
*(Ezek azért nem algoritmusok, mert valójában racionális ágenseket tervezünk és ezek a megoldások adják a racionalitásuk)*

- A véletlent használó modelleknél honnan tudjuk, hogy milyen valószínű az egyes kimenetelek valószínűsége?
    - Vagy van egy informált szakértőnk
    - Vagy szimulálni kell a játékot
- Monte Carlo Tree Search (MCTS):
    - Veszünk mintákat, amik alapján becslünk nehezen számítható értékeket
    - Ötvözi a keresési fát a véletlenszerű kimenetekkel (jó GO AI-k)
    - 4 lépést használ:
        1. kiválasztás: eldönti mely állapotot bontjuk ki
        2. terjeszkedés: kibontja a fának azt a csomópontját, vagyis abban a csomópontban megvizsgáljuk, hogy mi történik ha onnan indul a játék
        3. szimuláció: (véletlen módon) lejátszuk az adott állapotból induló játékokat
        4. visszaterjesztés: a játék eredményét felfelé terjesztjük (a/b-vel azt jelöljük, hogy `a` játékot sikerült megynerni `b` darabból) és ahol a legnagyobb lesz az esélyünk azt választjuk a fában
        *egyébként a minta képen el van írva a középső fa 4/8 helyett 5/8 kellene*
        *(lépések: selection, expansion, simulation, backpropagation)* 
    - [Minta](vgarciasc.github.io/mcts-viz)
    - Fontos probléma (exploration - exploitation) felfedezés vs kizsákmányolás
        - Inkább nézzünk új útvonalakat megpróbálni? Vagy próbáljuk meg a jelenlegit minél jobban kifejteni?
        - Ezt kutatták, ahol a válasz:
            - Exploitation: $\frac{w_i}{n_i}$
            - Exploration: $c \cdot \sqrt{\frac{\ln(t)}{n_i}}$
            - Ahol:
                - $w_i$ a győzelmek száma az i. csomópontban
                - $n_i$ a meglátogatási száma az i. csomópontnak
                - $C$ felfedezési paraméter
                - $t_i$ az i. szüleinek meglátogatásának száma
            - "a képlet valójában mindegy, inkább a probléma a lényeg"

#### Hasznosságok
> Vannak hasznosságok, de sohasem definiáltuk, hogy az micsoda
> Pedig az a racionális, ami a legnagyobb várható hasznosság felé halad

- Ha worst-case-re tervezünk, mint a minmax-nál, akkor a magasabb értékeléseket szeretjük
    - De ha például a fa alján négyzetre emeljük a számokat, akkor az változtat? Nem, mert a minimax érzéktelen a monoton transzformációkkal szemben
    (hiszen a legnagyobb szám négyzete is a legnagyobb marad - ha pozitív értékeket használunk csak)
    Vagyis a transzformációk nem változtatnak a hasznosságán 
- A hasznosságok olyan függvények, amik a kimeneteleket képzik le valós számokra és leírják az ágens preferenciáit
    - Pl. nekem ha fagyik közül kell választani, akkor a tölcsér=0, 1 gombóc=1, 2 gombóc=2 pont, 
    de ha laktóz érzékeny lennék, akkor nem ehetnék fagyit $\Rightarrow$ tölcsér=0, 1 gombóc=-1, 2 gombóc=-2 pont,
- Tétel: bármely "racionális" preferencia összefoglalható hasznossági függvényként
- Miért a kimeneteleket preferáljuk, miért nem egy viselkedést?
    1. a kutatások ezt mutatták
    2. A hasznosságot ha meghatározzuk az kialakítja a megfelelő viselkedéseket $\Rightarrow$ fontosabb a kimenet, mint a viselkedés
- Bizonytalan kimenetelekkel mit kezdjünk? Mit preferálunk, a biztosabbat vagy az értékesebbet?
    - Hogy tudjunk választani, be kell tartani bizonyos axiómákat:
        - Tranzitivitási axióma, ha A, B, C kimenetelekből az én értékelésem szerint: $A>B, B>C$, akkor $C \ngeq A$ *(különben nem tudok választani)*
        - Sorrendezhetőség: $(A > B) \lor (B > A) \lor (A \sim B)$, ha van egyik vagy másik preferenciám vagy semlegesek, akkor is tudok választani
        - Felcserélhetőség: $A \sim B \Rightarrow [p, A: 1-p, C] \sim [p, B; 1-p, C]$
            - vagyis ha egy nyeremény játékon A és B-nek is ugyanaz az esélye C-vel szemben, akkor a nyeremény játékok is semlegesek, ha A-t és B-t is ugyanannyira kedvelem
        - Monotonitás: $A > B \Rightarrow [p, A: 1-p, B] \geq [q, A; 1-p, B] \Leftrightarrow p \geq q$
        - Folytonosság: $A > B > C ...$ 
        <!--nem tudtam a diáról leírni =( és nincs fenn-->
    - Tétel: figyelembe véve a preferenciákat, amik kielégítik az axiómákat, ott létezik valós értékű U függvény, amelyre $U(A) \geq U(B) \leftrightarrow A \geq B$
    és $U([p_1,S_1;p_2,S_2;...,p_n,S_n]) = \sum_i p_i U(S_i)$
        - vagyis a nyeremény játék hasznossága a hasznosságok várható értéke lesz
    - Vagyis a megoldás a MEU (maximum expected utility) elv:
        - Azt kell kiválasztani, ami maximalizálja a várható hasznosságot
- *emberi hasznosságfüggvények:* 
    - pl. orvosoknál használt mikromort = egymiliomod a halál esélye, QALY = kockázatos döntések és az egészséges életévek aránya, ezek beavatkozás előtt fontos kérdések
    - halál nagyon kicsi esélye vs pénz $\Rightarrow$ kb 30$-nál lesz közönbös
    - EMV - expected monetary value
    - Az emberek általában kockázattűrők szerencsejátéknál, mert kevesebbet szeretnek fizetni, mint az EMV
        - Biztosítási díj: amit az ember hajlandó beáldozni arra, hogy a bizonytalanságot kiküszöböljék. Vagyis, ha 400-at fizetünk egy 500-as EMV-ért, akkor 100 lesz a biztosítási díj
- A hasznosság lehet több komponensű is, pl. ha 3 féle erőforrást kell begyűjteni a játékban, akkor azokat mind figyelembe kell venni
    - ez általában nem a 0 összértékű játékoknál jellemző, hannem ilyenkor mindenkinek saját hasznossági mutatója van. Ilyen esetekben adódhat versengő és kooperatív viselkedés is


## 6. EA
#### Logika
- Logika szerepe a komplex MI alkalmazásokban: logikai szabályalapú következtetés és beavatkozás
    - *Ha csak szabályokat használunk, akkor nem feltétlen csak akkor nyúl bele, amikor akarjuk. Ha mélytanulást használunk, akkor meg nem tudjuk, hogy biztosan beavatkozik-e $\Rightarrow$ ezeket érdemes lesz kombinálni*
- A logika egy tudásbázisból és egy következtető gépből áll
![](./img/2024-09-25-10-34-42.png)
    - Régebben szabályalapú szakértői rendszerek voltak, mostmár LLM-ek is szerepet játszanak
- Logikai következtetés fajtási:
    - Dedukció: ha $\to$ akkor (implikáció)
        - formálisan érvényes következtetés
        - feltételből jön a következtetés
        - ez a tudásátalakítás: megfigyelés alapján szabály
    - Indukció: `ha 1-re igaz, ha 2-re igaz, ... ha n-re igaz, akkor n+1-re is`
        - tapasztalat alapján következtetés
        - akkor lenne formálisan korrekt a következtetés, ha végtelen számú minta alapján tudunk következtetni (a valóságban nem tudunk n-t venni)
        - de hasznos általánosításra
    - Abdukció: `ha <tapasztalat> akkor <szabály>`
        - Ha több dolognak is ugyanaz a következménye, akkor ugyanaz lesz a tapasztalata, de abból a szabályt nem tudjuk kitalálni, max hipotézist felállítani
        *pl. ha mosolyog, akkor boldog... de az emberek nem csak ilyenkor mosolyognak, szóval ez nem egy jó abdukció*
        - Probléma: az oknak meg kéne előznie az okozatot
        - hasznos bizonyításra, de nem formális ez sem
- Következtetés:
    - Premissza: a feltételezés
    - Vannak közbenső eredmények
    - És n közbenső eredmény utána kijön a végső eredmény
- Az érvényes következtetés, ami az információkat felhasználja és ebből újat hoz létre. Az állítások átalakítása nem valódi következtetés ($A \lor B = B \lor A$)
- $TB |= \alpha$ (vonzatreláció), Tudásbázis és $\alpha$ mondat között akkor áll fell vonzatreláció, ha: $\alpha$ igaz minden világra ahol $TB$ is igaz
    - **A következtetés:** $\alpha$ kiszámítása TB mondatainak manipulálásával
        - A bizonyítás pedig a következtetési algoritmus lépéssorozata
- Fontos az interpretáció:
    - Egy mondat önmagában nem jelent semmit és lehet igaz/hamis környezettől függően
    - `Fut(Ágens1)`-et ha úgy értelmezzük, hogy:
        - Ágens1 egy személy, akkor a valóvilágban igaz a mondat, de digitális világban hammis
        - Ágens1 egy program, akkor a valóvilágban hamis a mondat, de digitális világban igaz
- Modell és világ:
    - Bármely világ, ahol 1 mondat igaz az lehet modell. *(Egy mondatnak számos modellje lehet)*
        - Minél többet állítunk, annál kevesebb modellünk lesz *(mert több feltételt nehezebb kielégíteni)*
    - Egy $\alpha$ vonzata $TB$-nek, akkor $TB$ modelljei mind modelljei $\alpha$-nak
    *(kinda triviális)*
        - Mert a modellhalmaz $|M(\alpha)| > |M(TB)| \qquad \text{ hiszen } \qquad M(TB) \subseteq M(\alpha)$
- Igazságtartó következtetés: csak igazságfüggvényekkel dolgozik (olyan függvények, amik csak a részeinek és logikai műveletek definíciójától függ, nem az interpretációtól)
    - Következtetési eljárás teljes: ha minden vonzatmondathoz talál bizonyítást (igaz ami bebizonyítható) $A |= B$-ból $A |- B$
    - Következtetési eljárás helyes: ha minden bizonyított mondat vonzatrelációban áll a tényekkel (amit bizonyított az igaz is) $A |- B$-ból $A |= B$
- Érvényes: minden világban minden értékkonfigurációban igaz $A \lor \lnot A$
- Kielégíthető: ha létezik olyan interpretáció, hogy valamely világban igaz
    - Ami érvényes az kielégíthető
- Kielégíthetetlen: ami nem kielégíthető (sohasem igaz $A \land \lnot A$)

- **Ítéletkalkulus:** nulladrend logika, amiről eddig beszéltünk
    - Egyszerű logikai operátorokat használunk
    - precedencia: $\lnot, \land, \lor, \to, \Leftrightarrow$
    - Szemantika: minden modell igaz/hamis értéket rendel minden ítéletszimbülumhoz
    - Az ítéletlogikai ekvivalenciák (32. dián)
        - Fontos állítások
        $TB |= \alpha$ akkor és csak akkor, ha $TB \to \alpha$ érvényes
        $TB |= \alpha$ akkor és csak akkor, ha $TB \land \lnot \alpha$ kielégíthetetlen

## 7. EA
> Közlemények: jó dolgok jönnek (IMSc my beloved)

*az óra ilyen kitérővel kezdődött, hogy a logika most hogyan találkozik az LLM-ekkel*

- Ítéletlogika következtetési mintái (hogyan elégítsünk ki egy tetszőleges állítást)
    - Modus poens: ha $A \to B$, akkor B legyen igaz
    *(ábramagyarázat a diákhoz: ha a felsőt tudjuk, akkor a vonal alattit beírhatjuk a tudásbázisunkba)*
    - And eliminálása: ha $A_1 \land ... \land A_n$, akkor $A_1, ..., A_n$ legyenek mind igazak
    - And bevezetése: ha $A_1, ..., A_n$ mind igazak, akkor $A_1 \land ... \land A_n$
    - Or bevezetése: $A_i = A_1 \lor ... \lor A_n$
    - Dupla negálás eliminálása: $\lnot \lnot A = A$
    - Elemi rezolúció: $A \lor B$ azt jelenti, hogy tudjuk, hogy $\lnot B$ akkor a tudásbázisunkba írjuk, hogy $A$
    - Rezolúció: $A \lor B$ azt jelenti, hogy $\lnot B  \lor G$, ha $A \lor G$ *(vagy ilyesmi)*
- Az ítéletlogika monoton: új mondatot mindig csak úgy vehetünk hozzá, hogy az eddigieket ne sértse. Vagyis az igaz mondatok száma csak nőni tud.
- ![](./img/2024-10-02-11-02-22.png)
- Az előrecsatolt / hátracsatolt következtetés lényege: építünk egy fát az állításokból és vagy az igaz megállapításokból előrefelé lépkedve bizonyítjuk a dolgokat, vagy a céltól visszafelé lépkedünk egészen addig, amíg elegendő igaz állítást nem találunk, hogy a cél levezethető legyen
- *Manapság már tanításnál nem ilyeneket használnánk, hanem megerősítéses tanulást, de pl. asszisztenseknél ez működik*
- TB alapján bizonyítás: 
    1. az ekvivalenciákat el kell hagyni mert $A \leftrightarrow B = (A \to B) \land (B \to A)$
    2. ...
    3. ... <!--sajnos nem tudtam leírni, de ez a szakasz a Q mondat bizonyítása TB alapján-->
    - A lényeg, hogy klózokká alakítsuk az állításokat (implikáció és egyéb dolgok elhagyása, csak $\land \lor \lnot$ marad)
    - Ezután ellenőrizzük hogy a feltételeink tudnak-e teljesülni
        - Ha pl. az a kérdés, hogy $R$ igaz-e? Akkor azt válaszoljuk meg, hogy $\lnot R$ feltételnél ellentmondásba kerül a tudásbázis, vagyis üreshalmaz a hozzátartozó világ
        - És ha ezt be tudom látni, akkor $R$ igaz, hiszen $\lnot R = \text{Hamis} \Rightarrow R = \text{Igaz}$
- De a világ nem olyan egyszerű, hogy mindent felírjunk klózokkal
    - Objektumok vannak és az objektumok kapcsolatait írjuk le, atomokkal, összetett mondatokkal stb.
    - Vannak kvantorok: $\forall, \exists$ 
    - Egyenlőség: `(term1 = term2)` igaz adott interpretáció mellett, akkor és csak akkor, ha `term1` és `term2` ugyanarra az objektumra vonatkoznak
        - pl. $\forall x \ \lnot szeret(x, Répa) = \lnot \exists x \ szeret(x, Répa)$
    - Ha 2 predikátumról nem jelentjük ki, hogy azonosak, akkor lehet más interpretációjuk. Pl. `gigászi(x) = hatalmas_leviatán(x)` csak akkor igaz, ha előtte deklarálom, hogy $\forall x \ \text{gigászi}(x) = \text{hatalmas_leviatán}(x)$. Hasonlóan egy objektumot is nevezhetek két módon, de csak akkor azonosak, ha kijelentem (pl. a cica és macska nem ugyanaz, amíg nem mondom)
- Predikátum kalkulus:
    - Teljes: minden igaz állítás belátható
    - A vonzat csak félig eldönthető: állítás hamis volta nem mutatható ki 
    (az ítéletkalkulusnál be lehet bizonyítani, hogy valami igaz/hamis, itt meg lehet hogy végtelen ciklusba kerülhetünk $\lnot \exists x : nem_az_univerzum_tagja(x)$, mert mindent be kell helyettesíteni)
    - A megoldásokhoz a következtetési lépéseket kibővíthetjük:
        - Modus ponens jelenlegi alakban, ha tudjuk, hogy $p(A)$ és a szabály, hogy $\forall x, p(x) \to q(x)$, akkor beírhatjuk a tudásbázisba, hogy $q(x)$
        - Eliminálni kell a kvantorokat, amik bizonyos esetekben elhagyhatók 
        <!--  ._.  -->
            - pl a létezik kvantor elhagyásánál a minden embernek létezik szíve-nél akkor hagyható el a létezik, ha kimondjuk, hogy minden embernek nem tetszőleges hanem saját hozzárendelt szíve van

## 8. EA
- Sok mindent tud az elsőrendű logika, de kellenek megkötések, hogy jól legyen használható
- Problémák:
    - Ha nincsen megkötés a feltételekre, akkor minden igaz állítás bebizonyítható, de a hamissága nem mutatható ki véges számú lépéssel
- A klóz formára hozás kiegészítő anyag, nekünk csak annyi kell, hogy az állításokat ezen végig futtassuk és utána használjuk valamiféle bizonyításra
- Rezolúciós bizonyítás: ha $TB + \lnot Q$ állítás egy üreshalmaz, akkor $\lnot Q$ hamis vagyis $Q$ igaz

##### Ontológiák
- Ontológia típusok:
    -  Az első rendű logika erős szemantikával rendelkezik, de a világot kevésbé írja le
    -  Középút: UML, RDF/S, aminek kevésbé erős a szemantikája, de a világot jobban leírja
    -  Taxonómiák: gyenge szemantika, erős leírás a világról
-  Bizonytalanság:
    -  Az első rendű logika nehezen kezeli a bizonytalanságokat

#### Valószínűségi modellezés
- Összetett eseménytér: (pl. Meleg/Hideg, Napos/Esős kombinációinak tudjuk a valószínűségét) együttes eloszlásukat nézzük
    - Ez kevés változónál könnyen kezelhető, de ha rengeteg van, sokféle értékkel, akkor a hozzá tartozó táblázatot nagyon sok idő létrehozni
        - Ráadásul nem minden változó összefüggő
    - A célunk egy összetett eloszlást létrehozni adott modellhez, optimálisan
        - Emlékezteteő: $P(a|b) = \frac{P(a, b)}{P(b)}$
        - Láncszabály: $P(x_1, x_2, x_3) = P(x_1)P(x_2 | x_1)P(x_3 | x_1, x_2)$
        - Bayes tétel: $P(x|y) = \frac{P(y|x)}{P(y)} \cdot P(x)$
            - Ez azért segít, mert egy megfigyelésből könnyebb hipotézist felállítani, mint hipotézisből a megfigyelés valószínűségét
            - Az a fektetett nyolcas fél az arányoságot jelenti
            - Ok okozati következtetetésnél: $P(\text{ok}|\text{okozat}) = \frac{P(\text{okozat}|\text{ok})}{P(\text{ok})} \cdot P(\text{okozat})$
        - Bayes tétel többszörös használata: Ha valaki szeretne elmerülni a valószínűségi hálókban, azoknak ez számít
            - $P(h|e, e') = \frac{P(e' | e,h)}{P(e'|e)} \cdot \frac{P(e|h)P(h)}{P(e)}$
            - az emberi következtetési modell kb így működik:
            $P(\text{Modell = m}| \text{Megfigyelés = adat}) = \frac{P(\text{Modell = m}| \text{Megfigyelés = adat}) \cdot P(\text{Modell = m})}{P(\text{Megfigyelés = adat})}$
        - Eddig ismételtük az összefüggő dolgokat, de mi van a függetlenekkel?
            -  Független, ha: $P(x, y) = P(x) \cdot P(y)$
            -  Feltételes függetlenség: X feltételesen független Y-tól ismert Z esetén
            $P(x, y|z) = P(x|z)P(y|z)$ aminek az átfogalmazása $P(x|y, z) = P(x|z)$
                -  Vagyis, ha $X \to Z \to Y$, és tudjuk Z-t, akkor mindegy, hogy Y van-e egyáltalán
-  Bayes háló:
    1. csomópontok: a valószínűségi változók
    2. irányított élek: Y-X-el összekötött, ha Y-nak közvetlen befolyása van X-re
    3. Minden csomópont  egy kis együttes eloszlás résztáblát jelöl (vagyis ő és a rá ható "szülők" egy táblában)
    4. A gráf DAG (nem tartalmaz irányított kört - mert akkor körbe függenének egymástól)
    ![](./img/2024-10-09-11-46-03.png)

## 9. EA
- A gráfban olyanok a szülők, mintha védőövet képeznének a változók körül
- Azért elég $5$ változónál $2^5 - 1$ méretű tábla, mert a $-1$ az valójában számolható a többiből, hiszen a peremeloszlás összege 1
- A képen a riasztásnál azért elég 4 sor, mert $P(R=0 | B, F)$ számítható $P(R | B, F)$-ből
- Néha előfordulhat, hogy ezzel a struktúrával nem sikerül nyerni semmit (mert minden szülő 1 gyerekhez tartozik)
- Markov-Takarója: egy adott csomópont szülői és gyerekei (a háló többi pontja nem befolyásolja ezt a pontot)
- Állítások:
    1. a háló egy együttes valószínűségi eloszlás leírása
    2. a háló a feltételes függetlenségről szóló állítások együttese
- Fel tudjuk bontani feltételes valószínűségek szorzatára
- FVT
- Háló megépítése:
    1. probléma változóinak meghatározása
    2. sorrend meghatározása
    3. Amíg maradt érintetlen változó: $X_i$-t válasszk ki és adjunk egy csomópontot a hálóhoz. Legyen a Szülők(X_i), a minimális halmaz amik hatnak X_i -re
    4. Definiáljuk X_i feltételes valószínűségi tábláját
- Lokálisan struktúrált rendszer
- Megéri-e új kapcsolatokat felvenni? Attól függ, ha valami ritka eset vagy túl nagy táblákat eredményezne, akkor nem feltétlen
    - Pontosabb lesz a háló, de komplexebb, ezért kérdéses
    - Ilyenkor a növekedés inkább lineáris, mint exponenciális
- Naív Bayes-hálók: kétféle csomópont létezik: ok/következmény, a következmények egymástól feltételesen függetlenek egymástól feltéve az okot (csak 1 szülő van, jóval egyszerűbb, mint a valóság, de egész pontos, gyerekek között nincs függőség)
    - Régen spam filterek működtek így: hogy pl. figyelembe vették a subject-et, linkeket és arra húztak valószínűségeket
- Valószínűségi hálók szemantikája:
    3. a háló oksági kapcsolatok együttese
    - Reichenbach's common cause principle: X, Y közötti korrelációnál vagy $X \to Y$ vagy $Y \to X$ vagy $Y \leftarrow * \rightarrow X$ (van egy vagy több közös ok), DE mi csak azt tudjuk leginkább mérni, hogy $X, Y$ asszociált-e
    *(ha már 3 változót vizsgálunk, akkor már van amit meg tudunk különböztetni: $X \rightarrow Y \leftarrow Z$-t a többitől)*
*(Következtetés valószínűségi hálókban diasor)*
- Következtetés felsorolással:
    - ha köztes lépések értékét nem ismerjük, akkor aszerint szummázni kell. Ha tudjuk hogy volt földrengés és János hívott, de nem tudjuk, hogy szól-e a riasztó, akkor R értéke helyére az Igazat és a hamisat is be kell szúrni, amikor számolunk
    - Mi történik, ha van olyan rész a kiszámításban, amire nekünk nincs szükségünk? Akkor azokat el lehet hagyni
- A következtetés komplexitása:
    - Kicsi problémáknál egyszerű, de nagyobb, több útvonalon következtethetőnél már nem hatékony (ilyenkor mást kell csinálni)
        - vagy közelítő számítást végzünk: sztochasztikusan - sorsolunk egy útvonalat, amivel ki tudjuk számolni a feltételes valószínűségét
        - vagy egyszerüsíteni kell a modellt

## 10. EA
(gyakorló feladatok teams-en 10.16)
- a megfigyelési ekvivalencia azt jelenti: hogy különböző oksági modelleknek lehet azonos függőségi térképe
    - $X \to Y \to Z \equiv X \leftarrow Y \leftarrow Z \equiv X \leftarrow Y \to Z$ 
        - Ezekről nem derül ki az ok-okozat, ugyanazokat a függőségeket fogják kiadni
- egyszeresen összekötött gráf struktúrával rendelkező Bayes hálóban létezik lineáris idő és tér komplexitású ...
- Bayes háló nem oksági kapcsolatokat reprezentál (csak képes rá), hanem eloszlást
- A bayes háló csomópontjai függenek a saját szüleiktől és saját gyerekeiktől, de a szüleik őseitől nem
- Az oksági kapcsolatok mindig asszociációs kapcsolatok is
- Példa feladat: *(2021 PPZH 6. feladatát néztük, de teams-en kinn van a feladat)*
- $P(X = \text{"x"} | A = \text{"y"})$, ha X függ még $B, C$-től is, akkor 
    - $\displaystyle P(X = \text{"x"} | A = \text{"y"}) = \alpha \sum_b \sum_c P(X = \text{"x"} | A = \text{"y"}, B, C)$
        - vagyis behelyettesítjük B és C helyére az összes lehetséges értékük
        - $\alpha$ normalizációs konstanst úgy számoltuk ki, hogy a feltétel helyére beillesztettük pont a másik értéket. Mert ez a háló kicsi volt, ezért lehetett sejteni, hogy 1, de nagyobb hálónál nem feltétlen van így
    - Várható hasznosság értéke: megszorozzuk a hasznossági értéket annak a valószínűségével, hogy az az eset előfordul és kiválasztjuk azt a döntést, aminél maximális a hasznosság $\Rightarrow$ ha így döntünk, akkor egy racionális döntési hálót kapunk
*(vissza váltás dia sorra)*
- Előző órán volt az a probléma, amit több útnál láttunk
    - Elutasító logika: csak azokat használuk, amik megfelelnek a lekérdezésnek
    - Valószínűségi súlyozás
        - P(Eső |vizesPázsit, Locsoó), ilyenkor a locsolóról tudjuk, hogy igaz, az esőt generálhatjuk, de mert tudjuk hogy vizes a pázsit, ezért beállítjuk annak az értékét is
        - P(VizesPázsit = igaz | Locsoló=igaz, Esik = igaz)
        - Van Markov Chain Monte Carlo mintavételezés is, de ezekbe nem nagyon mentünk bele

*(új diasor)*

### Maximális várható hasznosság
- Egylépéses MEU (max estimated usefullness) - ha minden változót ismerünk, akkor csak 1 lépéssel kiválasztjuk a maximumot
- Több lépésnél szekvenciális döntési probléma
    - a példán az volt a baj, hogy a robotunk csak 0.8 eséllyel lépett arra, mint amerre mi akartuk, hogy lépjen, de 0.1 volt az esélye, hogy rossz helyre lép
    - Megoldás: jutalmakat fogunk osztani bizonyos esetben
        - ha túl nagy a "negatív jutalom" akkor nem igazán érdekli, hogy csapdába lép, mert úgyis megbüntetik minden lépésért
        - ha túl nagy a pozitív jutalom a nem meghalásért, akkor nem lesz célba jutni szándéka
        - ha kicsit rossz minden lépés, akkor kockázatot is vállal azért, hogy célba érjen (ez nem a "tökéletes" megoldás, de talán a leginkább racionális)
    - "Leszámítolás": ha a cél elértéktelenedik idővel (ez azért jó, mert minél hamarabb érjük el, annál többet ér), de ez csak véges lépésnél jó
        - Ha végtelen esemény horizontunk van, akkor adhatunk a leszámításhoz egy felső jutalom küszöböt, ami a végtelen sorozat hasznosságát segít kiszámítani (dián a képlet)
        - Végesnél pedig $\pi*$ az a policy, ami maximalizálja a várható hasznossági értéket
        - s adott állapotból kiindulva, a akciót végrehajtva s' állapotot kapva T(s, a, s') a valószínűsége ennek U(s') a hasznossága
            - és ezeket megszorozva kapjuk az adott lépés haszosságát
        - Bellmann-egyensúlyi egyenlet ezt fejezi ki, de még $\gamma$ leszámítási tényező az idő telése szerint leértékeli a dolgokat
        - ennek az előnye, hogy a porszívónak nem kell az egész szobát feltérképezni, hanem elég jobbra-balra megnézni, hogy a következő lépése merre hasznosabb

## 11. EA
- Markov döntési folyamat
    - $S$ állapotok, $s_0$ kezdőállapot, $A$ cselekvések halmaza, 
    - $P(s'|s,a)$ / $T(s'|s,a)$ állapotátmenetek visznek minket át az állapotok között
    - $R(s, a, s')$ jutalom (reward), ami segít a motivációban
    - $\gamma$ leszámítolási tényező (discount)
- A versenyautós példán azt lehet látni, hogy melyik akció hatására milyen valószínűséggel kerülünk valamelyik állapotba és hogy ezért mennyi reward jár
    - gyakorlatilag egy keresési fa, ahol expectimax keresést lehet csinálni
    - de ha valóban ez lenne, akkor nem vennénk figyelembe, hogy a távoli jutalmak nem számítanak nekünk
    - az állapotok hasznosságára volt egy summa képlet
- A versenyautós játékfa megvalósítás örökké tartana, ráadásul az állapotok is folyamatosan ismétlődnek.
    - Megoldás értékiteráció:
    $U_0(s) = 0$-val indulunk $U_k(s)$ az adott iterációban jelzi a lépést
    - így kiszámolhatjuk újra meg újra, hogy n lépés után mi a legjobb
    - Viszont idővel egyre kevésbé lényeges, hogy érdemes-e folyamatosan frissíteni vagy már tudjuk az optimális néhány lépést és csak nagyobb kihagyásokkal is elég 
- A szakértőtől kapott adatokat érdemes kiértékelni
<!--idk man, telik az idő-->
- Megerősítéses tanulás:
    - Feltételezzünk egy Markov-döntési folyamatot
    - De nem fogjuk ismerni T-t vagy R-t
    - Ilyenkor online tanulással kell ezeket megtudni
- pl. vásható életkor
    - modellalapú: $E[A] \approx \sum_a \frac{num(a)}{N} \cdot a$ (vagyis megszámoljuk korosztályonként, hogy hány darab van)
    - modellmentes: $E[A] \approx \frac{1}{N} \sum_i a_i$ (ez az átlaga az összes ember életkorának)
        - akkor működik, ha megfelelőfekvenciával jelennek meg a minták
- Passzív megerősítéses tanulás: 
    - bemenet: rögzített eljárás mód
    - nem ismerjük T, R-t 
    - a cél az egyes állapotok hasznosságának kiszámítása $\pi$ eljárás módhoz 
    - Közvetlen kiértékelés: amit látunk azt leírjuk és visszafelé lépkedve kiszámoljuk a korábbi állapotok hasznosságát
        - Előny: könnyen kiszámítható, nem igényli T, R-t, végül kiszámítja a helyes átlagértékeket
        - Hátrány: elveszítünk egy csomó információt és annyira jó megoldást nem kapunnk
    - Időbeli különbség tanulás (IK):
        - a frissítésnél a régi és az új közti különbséget súlyozzuk egy $\alpha$-val 
    <!--itt elkezdenek kimaradni dolgok-->
    - Aktív megerősítéses tanulás:
        - nincs T, R
        - ki kell választani a cselekvéseket
        - cél: mi legyen az eljárás?
        - **Q tanulás:**
            - Nézzük meg, hogy a Q értékek hova konvergálnak, ami még akkor is optimális eljáráshoz vezet, ha szubotimálisan cselekszünk
    - Markov-döntési folyamat vs RL
- Felfedezés vs kizsákmányolást (exploration vs exploitation)
    - elkezdi keresni a jó utakat és ha megvan akkor elkezdi ezt használni
    - de ha van ennél jobb akkor jó lenne, ha megtalálná
    - Hogyan fedezzünk fel?
        - véletlenszerű akciók ($\epsilon$-mohó) egy kicsi valószínűséggel
            - felfedezi a teret, de nem tökéletes és később is túráznia kell
        - felfedezési függvények: fedezzen fel olyan területeket amelyek rosszaságát még nem állapították meg, utána hagyja abba a felfedezést
            - annyiban más pl. a Q tanulás, hogy $f$ függvénybe csomagoljuk a beágyazást
        <!---sajnos túl gyorsan tekerte a diát-->
    - Regret <!--én is így érzem-->
        - hogyan lehet a tanulást magát optimálisan csinálni?
        - mit tegyünk ha több millió állapotnak nem kéne mindegyikét letesztelni (pl. ha a pac-man-ben hiányzik 1 bogyó, mert már megettük az nem változtat sokat)
            - megoldás: bizonyos tulajdonságokkal jellemzünk állapotokat és utána ezeket használjuk súlyozva
                - pl. hogy milyen messze van a legközelebbi szellem (és nem az összes szellem helye)
                - ezeket a súlyokat meg kell szülni
                - Lineáris regresszióval
                - Közelítő Q-tanulás

## 12. EA
- békás példa a Q tanulásra, különböző helyekhez különböző akciók értékét nézzük
- legjobb eljárás meghatározása példa:
  $U(s) = R(s) + \gamma \underset{a'}{\max} \sum T(s, a, s') \cdot U(s')$
  A táblázatban a sorok s, az oszlopok s'-t jelölik, benne pedig az átlépés valószínűségét
    - és a hasznosságok összehasonlítása annyi volt, hogy az $s=3$ sorban az átlépések valószínűségét megszoroztuk az U(s') hasznosságértékkel és így ahol ez nagyobb volt, azt kellett választani (jelen esetben az $a_2$-es volt)
    - másik számolási mód, ahol állapot átmenethez van a jutalom megadva
- Megcsináltuk a Q-tanulás példát is
    - A kiindulási Q táblázatból 
        |     | a1  | a2  |
        | --- | --- | --- |
        | s1  | 0   | 0   |
        | s2  | 0   | 0   |
    - végig megyünk és updateljük:
        1. lépés:
            |     | a1  | a2  |
            | --- | --- | --- |
            | s1  | 5   | 0   |
            | s2  | 0   | 0   |
        2. lépés:
            |     | a1  | a2    |
            | --- | --- | ----- |
            | s1  | 5   | 0     |
            | s2  | 0   | -3.25 |
        3. lépés:
            |     | a1  | a2    |
            | --- | --- | ----- |
            | s1  | 5   | 6.25  |
            | s2  | 0   | -3.25 |
            - pl. itt a 6.25 úgy jött ki, hogy 
            $Q(a2, s1) = \alpha (R(s1) +  \alpha\underset{a'}{\max} - Q(a2, s1))$ vagy valami hasonló (gyorsan el lett tekerve) és $0 + \frac{1}{2} \cdot (10 + \frac{1}{2} \cdot 5 - 0) = 6.25$

### Felügyelt tanulás
- jó, mert általánoss problémákra lesz megoldás
- tanulás minták alapján
    - nincsenek előre kialakított szabályaink a feladatra, csak a minták
- Tanulás vs analitikus tervezés
    - analitikus tervezés: kellett szakértők segítsége, jó modell az adott problémára, a konkrét mechanizmust meg tervezni és algoritmusként implementálni
    - tanulás: megtervezni a tanulást és csak azt algoritmusként implementálni, az adatok relevanciája / struktúrája számít
- Gépi tanulás fontosabb fajtái:
    - Felügyelt tanulás: ahol ismerjük a bemenetet + az elvárt kimenetet
    - Megerősítéses tanulás: bizonyos értékeléseket kap adott akciónként (nem feltétlen minden lépés után)
    - Felügyelet nélküli tanulás: semmilyen információnk nincs a helyes kimenetről
    - Féligellenőrzött tanulás: egy résznél ismerjük az elvárt kimenetet, de nagy résznél nem 
- Felügyelt tanulás
    - $x$ bemenetre $h(x)$ hipotézisünk van, de azt szeretnénk hogy ez közelítse a valóságot: $f(x)$-et
    - a tanulás célja, hogy
    $h(x) = f(x)$ legyen ismert példákon és
    $h(x') \simeq f(x')$ ismeretlen példákon
- *Étteremben várás példa probléma*
    - Döüntési fák: elindulunk rajta, ha levélhez érünk, akkor kapunk eredményt
        - Szeretnénk általános, tömör fákat csinálni a mintából $\Rightarrow$ a fa gyökeréhez a kimenetet leginkább befolyásoló tényezőt kell vinni
        - akkor kell a fa építést abbahagyni, ha már mindent sikerült helyesen beosztani
        - de lehet eset a fa építésnél, amikor nem marad minta az egyik levélre. Ilyenkor a korábbi döntések alapján tudunk oda levelet tenni
        - baj lehet az is, hogy ha ugyanahhoz a bemenethez különböző kimenet tartozik. azt mondhatjuk, hogy zajos az adatunk. Ilyenkor lehet mondjuk többségi szavazást használni
        - akkor legjobb az attribútum, ha a mintákat tökéletesen szeparálja, nem kell belőle a fában tovább menni (csak levelekhez kapcsolódik $\Rightarrow$ egyértelmű döntés)
        - egy döntési fának az információtartalmát ki lehet értékelni. Azt szeretnénk elérni, hogy a fa fennmaradó részeinek entrópiáját megszámoljuk és a kiindulásét, akkor a kettő közti különbség legyen egy elég nagy szám

## 13. EA
nem voltam :(

## 14. EA
- Gépitanulás, ha vannak modelljeink, azoknak egyes paramétereit hogyan kéne hangolni
    - Lineáris regresszió
        - A bemenetek változó értékek (jellemző, feature)
        - Minden változónak van súlya 
        - Cél hogy valamiféle hibafüggvény szerint a legkisebb hibát eredményezze, így igazítjuk a változókat
        - Ahhoz hogy megtaláljuk a hibafüggvény szélsőértékét (minimumát) akkor a deriválás segítségével megtaláljuk a súlyfüggvény elmozdulását
        (az 1/2-ed a képleten csak azért van, hogy a négyzet deriválása után eltűnjön)
    - $\alpha$ paraméter mekkora bátorsággal változtassunk = learning rate
    - Lineáris osztályozó olyan mint a lineáris regresszió, csak a végén van valami függvény (activation függvény)
        - perceptronnak nevezzük, mert érzékelést jelöl
    - Bináris döntési szabály:
        - a minták pontok a térben 
        - minden súlyvektor egy hipersík
        - Az egyik oldal Y=+1, a másik Y=-1, a lénegy, hogy a pozitív minták a pozitív oldalon legyenek a negatívak a negatívon
        - Tanulás:
            1. kezdetben a súlyok nullák
            2. minta osztályozás a súly alapján (ha helyes, nincs változás)
            3. ha nem jó, akkor állítsa be a súlyvektort
        - Perceptronnál van sgn függvény és a + b bias
        - Persze csak akkor jó, ha binárisan szeparálható
        - Megjegyzés: több osztályos módon, több hipersíkkal, amiknek saját súlyvektoruk van, úgy el lehet választani
    - Perceptronok tulajdonságai:
        - elválaszthatóság - szeparabilitás: igaz, ha egyes paraméterek alapján a modell tökéletesen szeparálja a mintákat
        - konvergencia: ha a minta elválasztható, a perceptron végül konvergál (de ha nem, akkor nem lesz konvergens a megoldás - de nem lineárisan ettől még elválasztható)
    - Perceptron bajai:
        - ha nem elkülöníthetők: akkor "kidőlhet"
        - lehet hogy nem tökéletesen választja el (nem pont középre kerül, hanem lehet hogy valamelyiket épphogycsak elválasztja)
        - overfitting: a tanító adaton emelkedik a pontossága, de a teszt / validációson romlik
    -  Miért jobb ha valószínűségeket kapunk? mert az még valami információt adhat
    -  Az szeretnént, ha valami az egyik osztályba tartozik, akkor tartson 1 felé, különben 0 felé: sigmoid függvény erre jó $\phi(z)=\frac{1}{1+e^{-z}}$
-  Maximum likelihood becslés:
    -  ...
    -  Logisztikus regressziót (ami akkor van, hogyha szigmoidot teszünk a végére)
    -  Gyakorlatilag a soft max bináris esete és attól függően, hogy $e$-nek milyen együtthatója van, úgy kezd el egyre inkább hasonlítani más függvényekre
-  Hogyan tanuljunk?
    -  Maximum likelihood becslés
    -  Maximum feltételes likelihood becslés
- = többosztályos logisztikus regresszió
- Hill Climbing:
    - Az egyik legfontosabb keresés típus
    - Egy bizonyos környezetben keresünk
    - Vagyunk valahol, a szomszédrokól meg tudjuk mondani, hogy mi a lehetséges lépések állapota
    - Nem tudjuk, hogy mi a cél, csak keressük
    - Mohónál megállunk egy lokális szélsőértéken
    - Megoldások: szimulált lehűtés, több útvonalat keresünk
        - a szimulált lehűtés: hajlandóak vagyunk negatív lépéseket is megtenni, de ennek a hajlandóságát folyamatosan csökkentjük (hűtjük)
    - fölfelé menetnél több dimenzióban GradientAscent: nem egy súly szerint optimalizálunk, hanem ahány súly van, azt mind szeretnénk úgy változtatni, hogy a súlyra pozitívan hasson (optimalizáljuk a súlyt)
    - gradient descent: amikor a hibát akarjuk csökkenteni
- playground.tensorflow.org-on néztünk egy példát
<!--
- Történelem:
    - viszonylag korán előkerültek a perceptronok (de csalódtak, mert valamire jó valamire nem)
    - utána előkerült a sigmoid és a backprop is
    - utána a 2000-es években az SVM-ek vették át a vezető szerepet
    - 
-->
- Univerzális függvény approximációs réteg: 2 rétegű neurális háló elég mennyiségű neuronnal meg tud közelíteni egy folytonos függvényt bármely elvárt pontossággal 
    - túl általános: mennyi neuron? hány réteg? mennyi tanító minta? valójában ez nem minden
- Gradienst kiszámoljuk a hibában, de lefelé akarunk menni, ezért a learning rate előtt kivonás van
- Loss function-k különböző célokra:
    - MSE (mean squared error - négyzetes) - regressziónál
    - Crossentropy - bináris klasszifikáció
    - softmax / kategorikus keresztentrópia - több osztályos klasszifikáció
- Learning steps: forward pass - back propagation
    - visszafelé lépkedünnkk, az inputnál kicsit eltér mint a hidden layereken
- Volt a backpropagation képlet szépen levezetve, elég részletesen kifejtve 
    - igazából a következő fejlődési lépcsőt a történelemben ez érte el, hogy 1 lépéssel képesek voltunk javítani a hatékonyságot
    <!--- vizsgán kell tudni, hogy vannak tanítási, tesztelési adatok stb..-->
- majd beszélünk a gradiens eltűnésének problémájáról

## 15. EA
> papíron zh, még ennek az előadásnak az anyagából
> a moodle-be feltöltött anyagok / gyakorlatok segítik a felkészülést
> olyan mintha a tavalyi 2 zh anyagát együtt kéne tudni, kezdjünk készülni időben

- Döntések értékelése:
    - Bináris döntések értékelése:
        - True Positive, True Negative, False Positive (1. típusú hiba - false alarm), False Negative (2. típusú hiba - "elnézett támadás")
        - Konfúziós mátrixot lehet csinálni:
        | Döntés / Valóság | Beteg | Egészséges |
        | ---------------- | ----- | ---------- |
        | Beteg            | TP    | FP         |
        | Egészséges       | FN    | TN         |
        - Ebből csinálunk valami metrikát, építhetünk döntési fát, valószínűségi modellt stb.
    - Jósági mutatók: true positive rate és true negative rate
        - $TPR = \frac{TP}{P} = \frac{TP}{TP + FN}$
        - $TNR = \frac{TN}{N} = \frac{TN}{TN + FP}$
        - (Van még FPR - de ott ugye annak örülünk, ha az minél kisebb)
    - Positive predictive value, negative predictive value
        - eddig a valós adatokhoz viszonyítottunk, most meg a modell értékeléseihez viszonítunk
        - bizonyos területeken ezt használják precizitásként
        - $PPV = \frac{TP}{TP + FP}$
        - $NPV = \frac{TN}{TN + FN}$
    - Accuracy:
        - $ACC = \frac{TP+TN}{TP + TN + FP + FN} = \frac{TP + TN}{P + N}$
    - Miért kell ilyen sok metrika?
    Mert 1 nem feltétlen elég, gondolj bele hogyha mindent negatívnak osztályozunk akkor a TNR nagyon magas lesz, de valójában nem lesz helyes a döntés
    - Volt F1 Score is meg lett említve, meg hogy van egy csomó más metrika is (de nem kiemelve)
    - Az értékek súlyozása mindig helyzettől függ: azt szeretnénk, hogy több helyes beteget találjunk vagy azt hogy kevesebb potenciális beteg sétáljon az utcán ...
    - ROC: receiver operating characteristic
        - Van egy grafikon, aminek egyik tengelye a TPR másik FPR ott a középső lineáris egyenes az a véletlen osztályozó. Minél távolabb van ettől a vonaltól a modellünk görbélye különböző adatokon
        - Az ROC a görbe
        - AUC: Area Under Curve: a görbe alatti terület, amit maximalizálni akarunk
    - Vannak ennek is más reprezentációi, de van pl. Precision Recall Curve
    - A helyes döntésnek is van költsége:  hiszen a vizsgálatot el kell végezni, ahhoz hogy TN-t megállapítsuk ugyanúgy kell teszt
- a dián $N_t = N_\text{teljes} = N_\text{negatív} + N_\text{pozitív}$
    <!--I zoned out for a bit-->
- Döntés a kötség függvényében: a döntésünk nagy mértékben azon múlik, hogy jól becsüljük-e meg az egyes költségeket
    - Ha $C_{01}$ nagy, akkor attól tartunk hogy egész ms alakul ki 
    - ...
- ez a dia a zh anyagának a vége

---

- Konvolúció, mély tanulás nem lesz zh-ban, csak a legutóbbi alkalom
- Gyakorló példák elérhetők moodle-ben