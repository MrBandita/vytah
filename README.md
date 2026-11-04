# 3IT KYME – Výtah (Simulátor)

Tento projekt řeší optimalizaci algoritmu pro řízení výtahu v 8patrové budově (dle zadání zadani.json). Cílem bylo výrazně snížit dobu čekání cestujících a optimalizovat ujetou dráha výtahu oproti původnímu „hloupému“ algoritmu.

**Autoři:** Jan Hruška & Dayan Batbold


## 1. V čem byl problém původního („panelákového“) výtahu?

* Fungoval jako hloupé taxi: jel pro jednoho člověka (či skupinku z jednoho patra), rozvezl je a po cestě nikoho dalšího nepřibral ani nevysadil.

* Důsledek: V ranní špičce vznikaly obří fronty v přízemí a lidé čekali na chodbách i přes 20 minut.


## 2. Jak funguje náš nový algoritmus (hlavní myšlenky)

1. Obousměrný sběr (SCAN / LOOK):
Výtah drží směr jízdy (nahoru/dolů) a cestou plynule vysazuje cestující a přibírá ty, kteří jedou stejným směrem (pokud je v kabině místo).

2. Expresní návrat při ranní špičce (Lobby Express):
Když se ráno u vchodu v přízemí nahromadí desítky lidí, výtah po vyložení v horních patrech neztrácí čas zbytečnými mezizastávkami pro jednotlivce, ale spěchá prázdný přímo do přízemí, aby maximalizoval přepravní kapacitu.

3. Ochrana proti vyhladovění nižších pater (Anti-Starvation):
Odpoledne jedou všichni shora dolů a kabina se často naplní v patrech 7 a 6. Lidé v patrech 1, 2 a 3 by tak byli ignorováni, protože kolem nich projíždí plný výtah. Algoritmus měří čas čekání – pokud někdo čeká příliš dlouho, výtah dostane přímou misi a jede cíleně zachránit nejdéle čekajícího člověka.

4. Předvídavé parkování:
Pokud zrovna nikdo nevolá, výtah nečeká na náhodném patře, ale sjede do přízemí, kde statisticky vzniká nejvíc požadavků.


## 3. Výsledky (porovnání statistik)

* Průměrný celkový čas klesl z 336 s na 211 s (každý člověk ušetřil v průměru přes 2 minuty, zlepšení o 37 %).

* Průměrné čekání kleslo z 313 s na 190 s (o 39 % méně čekání na chodbě).

* Nejdelší čekání (nejhorší případ) kleslo z 24 minut na ~14 minut (odstranění extrémů).

* Ujetá dráha klesla o 756 metrů (−26 %) – výtah lidi odvozil rychleji, ale najezdil o čtvrtinu méně metrů, čímž šetří energii a opotřebení.

> Místo pouhého vození lidí tam a zpět jsme zavedli plynulý obousměrný sběr s expresním sjížděním při ranní špičce a hlídáním maximální doby čekání, aby nikdo v budově nezostlal zapomenutý.


## 4. Matice odpovědnosti (Kdo co dělal)

| Oblast / Úkol | Jan Hruška | Dayan Batbold |
| :--- | :---: | :---: |
| Analýza zadání a chování fyziky | Hlavní řešitel | Podpora / Konzultace |
| Návrh logiky algoritmu (SCAN / LOOK) | Návrh a implementace | Testování okrajových stavů |
| Optimalizace špiček (Lobby Express & Anti-Starvation) | Implementace & vyladění | Optimalizace parametrů |
| Testování a ladění metrik | Hlavní ladění kódu | Ověření výsledků v simulátoru |
| Dokumentace a README | Zpracování textu | Revize a korektura |


## 5. Jak spustit simulaci

1. Stáhni nebo naklonuj toto repository.

2. Otevři soubor `vytah 2.html` ve webovém prohlížeči.

3. Přetáhni soubor `zadani.json` do připravené zóny na stránce nebo klikni na tlačítko pro výběr souboru.

4. Klikni na ▶ Spustit pro přehrání simulace.
