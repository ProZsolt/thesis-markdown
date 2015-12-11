#Skálázási algoritmusok minőségmodellje

##Felhő infrastruktúra minőségmodellje
Mielőtt belemennék a skálázási algoritmusok minőségének a vizsgálatába, először általánosságban beszélek a felhő infrastruktúra minőségi tényezőiről.
Alapvetően 3 csoportra bonthatjuk a minőséggel kapcsolatos metrikákat, ezek pedig: alapvető teljesítmény metrikák, felhő képességek és felhő termelékenység. [@hwang_cloud_2015]

###Alapvető teljesítmény metrikák
Ezek az alapvető metrikák nem csak a felhő infrastruktúrára jellemezőek, hanem a klasszikus szerverparkokon üzemeltettet párhuzamos, elosztott szolgáltatásokra is ugyanúgy vonatkoztathatóak. 

 * Futási idő: Az program futása alatt eltelt idő
 * Sebesség: Adott idő alatt elvégzett műveletek száma
 * Sebesség növekedés: Sebesség növekedés amit azzal érünk el, hogy egy újabb számítási egységet kapcsolunk a rendszerbe
 * Hatékonyság: Az elérhető teljesítmény maximumának százaléka
 * Skálázhatóság: A képesség, hogy az erőforrások skálázásával rendszerteljesítményt nyerjünk
 * Elaszticitás: A rendszer alkalmazkodóképessége az idővel változó terhelésre
 
###Felhő képességek
Ezek azok a mérőszámok, amelyek leírják egy felhő infrastruktúra hardver-, szoftver-, hálózati- és hibatűrő képességét az alábbiak szerint.

 * Késleltetés: A kérés elküldésétől az első válasz beérkezéséig eltelt idő.
 * Átengedő képesség: Átlagos kérések/műveletek/taszkok száma adott idő alatt.
 * Sávszélesség: Adatátviteli sebesség vagy I/O feldolgozási sebesség.
 * Háttértár kapacitás: Virtuális lemezek tárolókapacitása.
 * Szoftver eszközök: Szoftver hordozhatóság, API és SDk eszközök a felhőalkalmazások fejlesztéséhez.
 * Bigdata analizálás: Az a képesség, hogy kiderítsük a rejtett információkat, és megjósoljuk a jövőt.
 * Visszaállíthatóság: A visszaállíthatóság aránya vagy a képességge, hogy visszaáll az eredeti állapotába egy hiba vagy katasztrófa esetén.
 
###Felhő termelékenység
Ezek a szolgáltatással kapcsolatos metrikák, melyek megmutatják az adott infrastruktúrán nyújtott szolgáltatás minőséggel és árral kapcsolatos mutatóit.

 * Szolgáltatás minősége: A felhőszolgáltatással kapcsolatos elégedettség mértéke vagy egy benchmark teszt eredménye.
 * Energiaigény: A cloud computing rendszer energia fogyasztása
 * Üzemeltetési költség: A nyújtott felhőszolgáltatások (processzor teljesítmény, háttértár) adott időre eső költsége.
 * Szolgáltatási szint megállapodás / biztonság: A szolgáltatási szint megállapodásnak, a biztonsági-, titoktartási-, szerzői jogi szabályoknak való megfelelés
 * Elérhetőség: Az idő hány százalékában érhető el a rendszer.
 * Termelékenység: Egységnyi költségre vetített felhő szolgáltatás teljesítmény.
 
##Skálázási algoritmusok minőségmodellje
A fentebb általánosságban bemutattam a felhőhöz kapcsolódó metrikákat, alábbiakban részletesen fogok írni a skálázáshoz szorosan kapcsolódó minőségi jellemzőket.

###Késleltetés
Késleltetésen a kérés elküldésétől az első válasz beérkezéséig eltelt időt értjük.
Minél terheltebb a rendszerünk (minél nagyobb a processzor, memória kihasználtsága) annál lassabban tudja a rendszer a kéréseket kiszolgálni. Ez a felhasználó felé a szolgáltatás minőségének romlását eredményezi, mivel tovább kell várnia egy művelet végrehajtására.

###Elaszticitás
Elaszticitás a rendszer alkalmazkodóképessége az idővel változó terhelésre.


###Üzemeltetési költség
Üzemeltetési költségen a felhőszolgáltatások (processzor teljesítmény, háttértár) adott időre eső költségét értjük.
Minél több/nagyobb szervert futtatunk annál nagyobb az üzemeltetési költségünk, ezért törekedni kell arra, hogy ha a rendszeren nincsen terhelés, akkor ne használjunk feleslegesen erőforrásokat.

###Elérhetőség
Az elérhetőség azt mutatja, hogy a rendszer az idő hány százalékában ad választ a kéréseinkre.
A terhelés egészen addig nőhet, hogy a rendszer nem csak egyre hosszabb idő múlva ad választ, hanem egyáltalán nem tudja kiszolgálni a hozzá beérkezett kéréseinket, ekkor mondjuk, hogy a rendszer elérhetetlenné vált. Általában a szolgáltatási szint megállapodásban (röviden: SLA) van megadva egy érték, hogy a szolgáltatásnak az idő hány százalékában kell elérhetőnek lennie, ha ezt a szolgáltató megsérti, akkor a felhasználó jogosult kártalanítást kérni a szolgáltatótól.
