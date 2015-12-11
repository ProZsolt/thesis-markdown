#Automatikus skálázás algoritmusok

Skálázó algoritmusokat általánosságban két csoportba sorolhatjuk. Egy algoritmus lehet reaktív, mely a rendszer egy valamilyen állapotára reagál, például érzékeli, hogy kevés az erőforrás, akkor allokál újabbakat . A proaktív algoritmusok ezzel szemben előrre próbálják jelezni a rendszer elkövetkezendő állapotát, hogy az erőforrások rendelkezésre álljanak, amikor később szükség lesz rájuk.[@lorido-botran_auto-scaling_2012]

##Ütemterv alapú
Számításba veszi a forgalom napszakok szerinti változását. Az erőforrás allokáció manuálisan van beprogramozva a napszaktól függően. Például a délutáni időszakban nagyobb forgalom várható, ezért ilyenkor több erőforrásra van szükség, míg az éjszaka folyamán kisebb a forgalom, ezért ilyenkor kevesebb erőforrásra van szükség, mint az átlag. Nem tud reagálni a forgalomba bekövetkező váratlan változásokra.

##Szabály alapú
A legtöbb szolgáltató ezt használja. Ehhez az egyszerű megközelítéshez általában két szabályt kell megfogalmazni, hogy mikor skálázzunk fel, illetve mikor skálázzunk le. A felhasználónak valamilyen metrika szerinti feltételt kell megfogalmaznia. Például, ha az átlagos processzor kihasználtság nagyobb mint 70%. Ha a feltétel teljesült, akkor automatikusan triggerelődik az előrre definiált skálázási akció: elindít egy újabb virtuális szervert. A szabály alapú automatikus skálázó algoritmusokat reaktív algoritmusok közé sorolhatjuk.

##Idősor elemzés
Az idősor elemzésnél bizonyos metrikákat, például az átlagos processzor kihasználtságot, vagy a beérkező terhelést megadott időközönként mintavételezzük. Az eredmény egy idősor lesz, ami tartalmazza az elmúlt n megfigyelés sorozatát. Az automatikus skálázás problémája két részre bontható: az elkövetkezendő metrika előrejelzésre, illetve az ebből következő döntéshozásra. Az idősor elemzést csak az első felére tudjuk alkalmazni, a másodikra használhatunk például egyszerű szabály alapú skálázást.
A idősor elemzésnek két célja van, előre jelezni a jövőbeli értéket ($y_{t+1}$) az elmúlt $\omega$ megfigyelés ($x_t, x_{t-1}, x_{t-2}, ..., x_{t-\omega+1}$) alapján, illetve mintákat felismerni, melyből extrapolálható a jövőbeli érték.

###Átlagoló módszerek
Ezek a módszerek használhatóak a zajok kiszűrésére és előrejelzésre. A jövőbeni érték úgy számolandó, hogy vesszük a súlyozott átlagát az előző n értéknek.

* Mozgó átlag: Az egyszerű mozgó átlag esetén vesszük a számtani közepét az előző n értéknek
* Súlyozott mozgó átlag: különböző súlyokat rendelünk az egyes megfigyeléseknek, tipikusan több súllyal vesszük számításba az újabb értékeket. 
* Exponenciális simítás: exponenciálisan csökkenő súlyokat rendelünk a mért értékekhez.
  
### Auto-regresszió 
Ebben az estben súlysó tényezőket ($a_{1}, a_{2}, a_{3}...$) úgy határozzuk meg, hogy kiszámítjuk a auto korrelációs együthatókat, és megoldunk a következő lineáris egyenletet: $\sum_{i=1}^{\omega}a_{i}R(i-j)=-R(j), for 1 \leq j \leq \omega$, ahol R a auto korrelációs együthatója az idősornak és $\omega$ a mintavételezett sor hossza. 

### Autó-regressziós mozgó átlag
Kombinálja az auto-egressziót és a mozgó átlagot. A jósolt kimenet $y_{t+1}$ az előző kimeneteken $y_{t-1}, y_{t-2}, y_{t-3}, ...$ és a bemeneteken $x_t, x_{t-1}, x_{t-2}, x_{t-2}, ...$ alapszik. Az általános formula: \begin{align}y_{t+1} = a_{1}y_{t-1} + a_{2}y_{t-2} + a_{3}y_{t-3} + ... + b_{0}x_{t} + b_{1}x_{t-1} + b_{2}x_{t-2} + ...\end{align}

##Szabályozás elmélet
A szabályozó rendszereknek három fajtála van, ezek az open loop, a feedback és a feed-forward

### Nyílt
Csak a rendszer jelenlegi állapotát és a rendszerről alkotott modellt ismeri. Nem használ visszacsatolást, hogy a rendszer elérte-e a kívánt végeredményt vagy nem.

### Visszacsatolt
Figyelik a rendszer kimenetét, és korrigálják a kívánt céltól való eltérést.

### Előrecsatolt
Megjósolják a rendszer viselkedését a róla alkotott modell alapján, és megelőzik a hibát mielőtt az bekövetkezne.

##Megerősítéses tanulás
A megerősítéses tanulás egy automatikus döntéshozó algoritmus, amelyet alkalmazhatunk automatikus skálázásra. A döntéshozó (ágens) a tapasztalataiból (próbálgatás) tanulja meg, hogy melyik a legjobb művelet, amit végre kell hajtania a környezete bármely állapotában azáltal, hogy maximalizálni próbálja az érte kapott jutalmat. A mi esetünkben az autmatikus skálázó az ágens, aki kapcsolatban van a skálázandó alkalmazással (környezet), dönteni fog hogy adjon, illetve elvegye-e erőforrásokat az alkalmazástól (művelet), a jelenlegi terheléstől, teljesítménytől és egyéb változóktól (állapot) függően úgy, hogy minimalizálja az alkalmazás válaszidejét vagy egyébb változóit (jutalom).

##Sorbanállás-elmélet
A sorbanállás-elmélet a különböző folyamatok eseményeivel kapcsolatos várakozási sorokat, a sorbanállási időket a kiszolgálásra és ezek összefüggéseit tárgyalja az alkalmazott matematikai eszközeivel. A sorbanállási elméletben becslési modellt alkotnak a sorbanállás hosszáról és időtartamáról, valamint a kiszolgálás sikerességéről. Az egyszerű csomóponti sorbanállásokat a Kendall-féle jelöléssel jellemezzük A/B/C/K/N/D formában, ahol A írja le a beérkezési időközt, B a munka nagyságát (kiszolgálási idő), C a kiszolgálók számát, K a rendszer kapacitását vagy a sor hosszát, N az igényforrás számosságát, D a kiszolgálás elvét vagy a fontossági sorrendet.
A mi esetünket megfeleltethetjük ezt egy egyszerű csomóponti sorbanállásnak úgy, hogy egy sor megy a terhelés elosztóhoz, ami elosztja a kéréseket a virtuális szerverek felé.
