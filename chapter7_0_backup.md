# Desing overview
Szakdolgozatom sororán egy olyan mérési környezetet alakítottam ki, ami teljesen moduláris, így később, ha módosítani kellene, például más IaaS szolgáltatót szeretnénk használni, vagy más metrika gyűjtési módszert alkalmazni, vagy a későbbiekben bemutatott különböző algoritmusokat szeretnénk használni, akkor csak a adott modult kell kicserélni, illetve maximum minimális változtatásokat eszközölni az alkalmazás többi részén.
Az általm készült rendszer a 4 részből áll, ahogy azt az ábrán láthatjuk.

##Forgalom generátor
Cél az volt, hogy a valóságban előforduló forgalomfajtákat (menyről részletesebben a 7. fejezetben írtam) generáljunk és ezzel terheljük meg a rendszerünket. A piacon több fajta forgalomgenerátor található, mind a maga előnyeivel és hátrányaival.
Kiválasztásnál a fő szempontok a következők voltak:

* Szabályozhatható forgalom generálás
* Könnyen kezelhető interfész
* Cross-platform
* Több fajta kérés küldése(GET, POST)
* Pluginezhető, ha a későbbiekben új dolgot szeretnénk hozzáadni
* Open source
* Futatható master, több slave módban

Választásom a JMeterre eset mivel ez teljesen lefedi az általam tartott igényeket.

###Throughput Shaping Timer
A szabályozható forgalom generálást a JMeter Throughput Shaping Timer Plugin-jével oldottam meg. A plugin segítségével könnyen beállíthatjuk a kívánt másodpercenkénti kérések számát.

###Felhasználók szimulálása
Fontos, hogy ne csak statikus forgalmat generáljunk, például az index oldalnak az egymás utáni letöltését. Olyan forgalmat szeretnénk generálni, mintha valós felhasználók használnák az oldalt, cikkeket olvasnának, tartalmat szerkesztenének, postokra kommentelnének. Igy nem csak a statikus oldal kiszolgálást teszteljük, hanem az adatbázisba írást, olvasást is. 
Első választásom a JMeterhez írt Selenium WebDriver-re eset, melyel valós felhasználók böngészését lehet modellezni Markov-láncok segítségével. Sajnos hamar kiderült, hogy az én esetemben alkalmatlan a feladatra, mivel nagyon sok erőforrást igényel, szimulált felhasználóként körülbelül egy processzormagot, amely több ezer felhasználót figyelembe véve nem lehetséges a kivitelezése, csak igen költséges infrastruktúra segítségével.
Majd sokat foglalkoztam saját teszt írásával, de ezel csak a WordPress funkcionalitásának csak egy kis részét tudtam vele szimulálni, nem volt benne süti kezelés, így nem tudtam tesztelni a bejelentkezett felhasználók viselkedését. Fejlesztés közben rátaláltam Shmuel Krakower által írt WordPress JMeter Template-t mely orvosolta ezeket a hiányosságokat, és remek eszköznek ígérkezett az oldal teszteléséhez.
A felhasználóval a következő funkciók vannak szimulálva:

* Főoldal megtekintése
* Bejelentkezés
* Blog bejegyzés megtekintése
* Blog bejegyzés írása
* Komment írása egy bejegyzéshez
* Keresés a weblapon

##IaaS infrastruktúra
Az általam használt infrastruktúrát egy CoudFormation template-tel építettem fel, így könnyen tudtam felépíteni és lebontani a stack-emet.
Az infrasruktúra a következő részekből áll:

###Load Balancer
Load balancernek az egyszerűség kedvéért az amazon beépített Elastic Load Balancerét használtam. Ez round robin segítségével osztja szét a forgalmat a kiszolgáló szerverek között. 
CloudWatch segítségével kinyerhető belőle a fontosabb metrikák, melyeket skálázás során fel tudunk használni, úgy mint:

* Egészséges hosztok száma
* Nem egészséges hosztok száma
* Beérkezett kérések szám
* Késleltetés
* Kiszolgálásra váró sor hossza
* Túlcsordult kérések száma

Ezen kívül figyeli a szerverek állapotát, és ha egy valamiért meghibásodna újat indít helyette.

###App server
A CloudFormationban írt LaunchConfiguration-el építem fel a szervert egy ubuntu 14.4-es AMI-t hasznáva alapul, mely gondoskodik róla hogy felkerüljön az alapvető LAMP stack(Apache, MySQL, PHP), majd erre felkerül a WordPress.
Ezen kívül felkerül minden szerverre egy collectd démon, melyről a monitorozásnál fogok részletesebben ismertetni.

###Auto Scaling group
A skálázásra az Amazon Auto Scaling group-ját használtam, mely könnyűvé teszi a ki- és beskálázást. API segítségével megadhatjuk neki, hogy mennyi futó szerverre van szükségünk és automatikusan elindítja a szükséges mennyiséget a LaunchConfiguration segítségével, vagy leállítja a feleslegesen futó szervereket.

###RDS adatbázis
Az amazon MySQL adatbázis szervere, mely leveszi a terhet a vállunkról, hogy magunknak keljen menedzselni egy szerverre telepített MySQL adatbázist, így megkímél minket az esetleges biztonsági frissítések telepítésétől, és egyébb karbantatrási munkálatoktól.

##Monitor

Eza a modul felelős a különböző metrikák begyüjtéséért, tárolásáért és hogy egy interfacet biztosítson a lekérdezésre.


##Graphite
Graphite[@graphite] egy idősor adatok tárolására és megjelenítésére készült alkalmazás.

Három a részből áll:

* carbon - Egy Twisted[@twisted] démon figyel a beérkező idősor adatokra
* whisper - Egy egyszrű adatbázis könyvtár az idősor adatok tárolására
* graphite webapp - Egy Django[@django] web applikáció, ami a grafikonokat rendereli Cairo[@cairo] segítségével


###CloudWatch és collectd


Monitorozásra először a Amazon CloudWatch szolgáltatását használtam, de ez a 5 percenkénti mintavételezési ideje miatt nem bizonyult elég nagy felbontásúnak.


Az szerverek monitorozására a szerverekre telepített collectd démont használok.
Monitorozásra Graphite-ot használok, ahol aggregálva jelenik meg minden metrika. Ennek kettős szeretpe

###StatsD


##Scaler


##Erőforrás kontroller
Ez felelős a Scaler-által ígényelt erőforrások lefoglalásáért. Interfaceként szolgál az IaaS infrastruktúra felé, esetleges IaaS szolgáltató váltásnál elég ezt lecserélni.
A modul a következő fukncionalitásokat tudja:

* `scale_up`: A jelenlegi kapacitást megnöveli X egységgel, alapértelmezetten egyel
* `scale_down`: A jelenlegi kapacitást lecsökkenti X egységgel, alapértelmezetten egyel
* `set_capacity`: A kapacitást beállítja X egységre

Jelenlegi megvalósításnál a kontroller AWS SDK segítségével, méretezi a Auto Scaling group-ban található szerverek számát.
