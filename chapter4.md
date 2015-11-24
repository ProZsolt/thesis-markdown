Automatikus skálázás algoritmusok
=================================

Skálázó algoritmusokat általánosságban két csoportba sorolhatjuk. Egy algoritmus lehet reaktív, mely a rendszer egy valamilyen állapotára reagál, például érzékelik, hogy kevés az erőforrás, akkor allokál újabbakat . A proaktív algoritmusok ezzel szemben előrre próbálják jelezni a rendszer elkövetkezendő állapotát, hogy az erőforrások rendelkezésre álljon amikor később szügség lesz rájuk.

Ütemterv alapú
--------------
Számításba veszi a forgalom napszakok szerinti változását. Az az erőforrás allokáció mauálisan van beprogramozva a napszaktól függően. Például a délutáni időszakban nagyobb forgalom várható ezért ilyenkor több erőforrásra van szükség, míg az éjszaka folyamán kissebb a forgalom ezért ilyenkor kevesebb erőforrásra van szügség, mint az átlag. Nem tud reagálni a forgalomba bekövetkező váratlan változásokra.

Szabály alapú
-------------
A legtöbb szolgáltató ezt használja. Ehhez az egyszerű megközelítéshez általában két szabályt kell megfogalmazni, hogy mikor skálázzunk fel, illetve mikor skálázzunk le. A felhasználónak valamilyen metrika szerinti feltételt kell megfogalmaznia. Például, ha az átlagos processzor kihasználtság nagyobb mint 70%. Ha a feltétel teljesült, akkor automatikusan triggerelődik az előrre definiált skálázási akció. Pédául elindít egy újabb virtuális szervert. A szabály alapú automatikus skálázó algoritmusokat, reaktív algoritmusok közé sorolhatjuk.

Idősor elemzés
--------------
A idősor elemzésnél bizonyos metrikákat, például az átlagos processzor kihasználtságot, vagy a beérkező terhelést megadott időközönként mintavételezzük. Az eredmény egy idősor lesz ami tartalmazza az elmúlt n megfigyelés sorozatát. A automatikus sálázás problémája két részre bontható az elkövetkezendő metrika előrejelzése, illetve az ebből következő döntéshozás. Az idősor elemzés csak az első felére tudjuk alkalmazni, a másodikra használatunk például egyszrű szabálya alapú skálázást.
A idősor elemzésnek két célja van, előrre jelezni a jövő beli értéket az elmúlt megfigyelések alapján, illetve mintákat felismerni, melyből extrapolálható a jövőbeli érték.

Módszerek

* Átlag
  * Mozgó átlag
  * Súlyzott mozgó átlag
  * Exponenciális simítás
* Autó-regresszió
* Autó-regressziós mozgó átlag
* Gépi tanulás

Minták

* Minta felismerés
* Jelfeldolgozó technikákat
* Auto-korreláció

Szabályozás elmélet
-------------------
A szabályozó rendszereknek három fajtála van open loop, feedback and feed-forward

### Nyílt
Csak a rendszer jelenlegi állapotát és a rendszerről alkotott modelt. Nem használ visszacsatolást, hogy a rendszer elérte a kívánt végeredmént

### Visszacsatolt
Figyelik a rendszer kimenetét, és korrigálják az eltérést a kívánt céltól.
Fixed gain controllers
Adaptive control
Reconfiguring control
Model predictive control

### Előrrecsatolt
Megjósolják a rendszer viselkedését, a róla alkotott modell alapján, és megelőzik a hibát mielőtt bekövetkezne.

Megerősítéses tanulás
----------------
A megerősítéses tanulás egy automatikus döntéshozó algoritmus, amelyet alkalmazhatunk automatikus skálázásra. A döntéshozó (ágens), a tapasztalataiból (próbálgatás) tanulja meg hogy melyik a legjobb művelet amit végre kell hajtania a környezete bármely állapotában, az által, hogy maximalizálni próbálja az érte kapott jutalmat. A mi esetünkben az autmatikus skálázó az ágens, aki kapcsolatban van a skálázandó alkalmazással (környezet). Dönteni fog hogy adjon, illetve elvegyen erőforrásokat az alkalmazástól (művelet), a jelenlegi terheléstől, teljesítménytől és egyéb változóktól (állapot) függően, úgy hogy minimalizálja az alkalmazás válaszidejét vagy egyébb változóit (jutalom).

Sorbanállás-elmélet
-------------------
A sorbanállás-elmélet különböző folyamatok eseményeivel kapcsolatos várakozási sorokat, sorbanállási időket a kiszolgálásra, és ezek összefüggéseit tárgyalja az alkalmazott matematikai eszközeivel. A sorbanállási elméletben becslési modellt alkotnak a sorbanállás hosszáról és időtartartamáról, és a kiszolgálás sikerességéről. Az egyszerű csomóponti sorbanállásokat a Kendall-féle jelöléssel jellemeznek A/B/C/K/N/D formában, ahol A írja le a beérkezési időközt, B a munka nagyságát (kiszolgálási idő), és C a kiszolgálók számát, K a rendszer kapacitását vagy a sor hosszát, N az igényforrás számossága, D a kiszolgálás elve vagy a fontossági sorrend.
A mi esetünket megfeleltethetjük egy egyszerű csomóponti sorbanállásnk, úgy hogy egy sor megy a terhelés elosztóhoz, ami elosztja a kéréseket a virtuális szerverek felé.
