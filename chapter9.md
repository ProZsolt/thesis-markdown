#Forgalom generátor
Ez a fejezet mutatja be a különböző terhelés generátor alkalmazásoknak az előnyeit és a hátrányait, majd ezután bemutatom az általam kiválasztott eszköz segítségével hogyan valósul meg a terhelés generálás.

##Terhelés generátorok
Több tucat terhelés generátor található a piacon, de a legtöbb nem felel meg az igényeinknek. Alábbiakban bemutatom az 4 leggyakrabban használt terhelés generátort.[@BlazeMeter]

###The Ginder
Grinder egy ingyenes Java alapú BSD licence alatt elérhető terhelés generátor.  Paco Gomez fejlesztette és Philip Aston tartja karban. Két részből áll, The Grinder Console-ból, ami egy GUI alkalmazás, mely a különböző Grinder Agent-eket írányítja, és monitorozza valós időben, valamint IDE-ként is funkcionál a tesztek elkészítéséhez, és a Grinder Agent-ből, ami egy headless terhelés generátor

Főbb funkcók:

* TCP proxy, mellyel tárolni tudjuk a teszt során zajló hálózati forgalom adatait
* Elosztott tesztek, amelyek a Grinder Agent-ek növekedésével skálázódnak.
* Java API-ra épülő Python és Closure szkriptek a teszt esetek készítéséhez
* Könnyű paraméterezhetőség, mely magába foglalja az automata tesztgenerálást, és biztosítja hogy hozzáférhessünk külső fájlokhoz és adatbázisokhoz
* Több protokol támogatása

###Gatling
Gatling szintén egy ingyenes és nyílt forráskódú terhelés tesztelő alkalmazás. Elsődlegesen Stephane Landelle fejleszti és tartja karban. Gatlingnek egy egyszerű GUI-ja van, mely csak a teszt eredményeit hivatott megjeleníteni. A teszteket egy könnyen megtanulható domain specifikus nyelvben írhatjuk.

Főbb funkcók:

* HTTP rekorder
* Egy egyszerűen megtanulható domain specifikus nyelv a tesztek írásához
* Scala alapú
* Magasab terhelés generálás asszinkron, nem blokkolo megközelítés használatával
* HTTPS protokol támogatása
* Átfogó informatív értékelés

###Tsung
Tsunk egy Erlang alapú nyílt forráskódú terhelés tesztelő alkalmazás. Nicolas Niclausse készítette 2001-ben hogy tesztelje a Jabber(XMPP) chat alkalmazást. 2003-ban már képes volt HTTP protokollon futtatott tesztekre is. Ma már egy teljes értékű teljesítmény ?ez kell ide kétszer? teljesítmény tesztelő szoftverré nőtte ki magát.
Nem rendelkezik grafikus felülettel.
Főbb funkciók:

* Elosztott felépítés
* Az alapjául szolgáló többszálúságra tervezett Erlang nyelvnek köszönhetően rengeteg felhasználót tud kis erőforrással szimulálni
* Több protokoll támogatása
* Beépített, könnyen olvasható teszt jelentés, mely futás alatt is könnyen elérhető és megjeleníthető
* Külső adatforrások, adatvezérelt teszteléshez.

###JMeter
JMeter egy Java nyelven írodott nyílt forráskódú, teljes értékű asztali alkalmazás. Apache Software Foundation készítette 2001-ben. Moduláris struktúrájú, egy core szoftver kiegészítve rengeteg pluginnal. A legtöbb protokol implementálva van pluginként.

Főbb funkcók:

* Kereszt platformos. Minden operációs rendszeren fut amin van Java
* Skálázható. Ha nagyobb terhelésre van szügségünk, mint amire egy gép képes, akkor egy master irányíthat több távoli alkalmazást
* Sok protokollt támogat alapértelmezetten.
* Sok beépített és külső eszköz a teszt eredményeinek analizására és megjelenítésére.
* Plugin-olható, melyek segítségével szinte minden feladatot képes ellátni.

##Forgalom generátor megvalósítása
Az eszköz kiválasztásnál a fő szempontok a következők voltak:

* Szabályozhatható forgalom generálás
* Könnyen kezelhető interfész
* Cross-platform
* Több fajta kérés küldése(GET, POST)
* Pluginezhető, ha a későbbiekben új dolgot szeretnénk hozzáadni
* Open source
* Futtatható master, több slave módban

Választásom a JMeterre eset mivel ez teljesen lefedi az általam támasztott igényeket.

###Throughput Shaping Timer
Cél az volt, hogy a valóságban előforduló forgalomfajtákat (menyről részletesebben a 7. fejezetben írtam) generáljunk és ezzel terheljük meg a rendszerünket.
A szabályozható forgalom generálást a JMeter Throughput Shaping Timer Plugin-jével oldottam meg. A plugin segítségével könnyen beállíthatjuk a kívánt másodpercenkénti kérések számát.

###Felhasználók szimulálása
Fontos, hogy ne csak statikus forgalmat generáljunk, például az index oldalnak az egymás utáni letöltését. Olyan forgalmat szeretnénk generálni, mintha valós felhasználók használnák az oldalt, cikkeket olvasnának, tartalmat szerkesztenének, postokra kommentelnének. Így nem csak a statikus oldal kiszolgálást teszteljük, hanem az adatbázisba írást, olvasást is.
Első választásom a JMeterhez írt Selenium WebDriver-re eset, melyel valós felhasználók böngészését lehet modellezni Markov-láncok segítségével. Sajnos hamar kiderült, hogy az én esetemben alkalmatlan a feladatra, mivel nagyon sok erőforrást igényel, szimulált felhasználóként körülbelül egy processzormagot, így több ezer felhasználót figyelembe véve nem lehetséges a kivitelezése, csak igen költséges infrastruktúra segítségével.
Majd sokat foglalkoztam saját teszt írásával, de ennek segítségével a WordPress funkcionalitásának csak egy kis részét tudtam szimulálni, nem volt benne süti kezelés, így nem tudtam tesztelni a bejelentkezett felhasználók viselkedését. Fejlesztés közben rátaláltam Shmuel Krakower által írt WordPress JMeter Template-re, mely orvosolta ezeket a hiányosságokat, és remek eszköznek ígérkezett az oldal teszteléséhez.
A felhasználóval a következő funkciók vannak szimulálva:

* Főoldal megtekintése
* Bejelentkezés
* Blog bejegyzés megtekintése
* Blog bejegyzés írása
* Komment írása egy bejegyzéshez
* Keresés a weblapon
