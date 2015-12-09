#Monitor

Ez a modul felelős a különböző metrikák begyüjtéséért, tárolásáért és hogy egy interfacet biztosítson a lekérdezésre.


##Graphite
Graphite[@graphite] egy idősor adatok tárolására és megjelenítésére készült alkalmazás.

Három a részből áll:

* carbon - Egy Twisted[@twisted] démon figyel a beérkező idősor adatokra
* whisper - Egy egyszerű adatbázis könyvtár az idősor adatok tárolására
* graphite webapp - Egy Django[@django] web applikáció, ami a grafikonokat rendereli Cairo[@cairo] segítségével


##CloudWatch és Collectd

AWS felhasználók kényelmesen gyűjthetnek különböző metrikákat CloudWatch segítségével. Sajnálatos módon a CloudWatch több szempontból is limitálva van, úgy mint metrikák, konzisztencia, ár és a lekérdezés gyakorisága.
Javulás érhetünk el ezek terén, ha egy egyszerű és közkedvelt nyílt forráskódú alkalmazást, a Collectd-t használunk. Ez az alkalmazás beépítve tartalmaz rengeteg plugin, ami lehetővé teszi a teljesítmény metrikák kigyűjtését az operációs rendszerből, mely az EC2 instance-ban található. A konfigurációs fájl szerkesztésével beállíthatjuk, hogy mely plugin-t engedélyezzük, és a hogy milyen gyakorisággal gyüjtse a metrikákat, valamint hogy az összegyűjtött metrikákat, milyen formában továbbítsa.
Előnyei a Collectd-nek a CloudWatch-hoz képest:

* CloudWatch csak limitált számú monitorozási metrikát biztosít. Például semmilen memóriával kapcsolatos metrika nem érhető el. Ezzel szemben a Collecd rengeteg memóriahasználattal kapcsolatos metrikát biztosít , és ezen kívül, még részletesebb metrikát mutat a terhelésről, teljesítményről és a rendszer állapotáról.
* CloudWatch metrikái nem mindig állnak rendelkezésre konzisztensen, így lemaradhatunk fontos információkról.
* A CloudWatch ingyenesen biztosítja a metrikák öt percenkénti mintavételezését, illetve fizetős konstrukcióban az egy percenkéntit is, míg a Collecd a 10 másodpercenkénti mintavételezést is biztosítja bizonyos metrikáknál.

------------------------ ------------------------------- -------------------
                         Collectd                        CloudWatch
------------------------ ------------------------------- -------------------
Metrikák száma           több száz                       körülbelül 10

Konzisztencia            mindig                          általában

Költségek                ingyenes                        fizetős bizonyos
                                                         használat felett 
 
Lekérdezés gyakorisága   akár 10 másodpercenként         5 perc ingyenesen,
                                                         1 perc fizetősen

Fejleszthetőség          Bárki írhat hozzá kiegészítést  Nem bővíthető
------------------------ ------------------------------- -------------------

Table: A Collectd és a CloudWatch összehasonlítása

##Statsd
Az Etsy által készítet hálózati démon mely node.js alapokon fut. Figyeli a UDP-n és TCP-n beérkező statisztikákat, majd agregálva továbbküldi őket egy vagy több backend szolgáltatásnak (pl.: Graphite).

##Monitorozás megvalósítása
Monitorozásra Graphite-ot használok, ahol aggregálva jelenik meg minden metrika. Ennek kettős szerepe könnyen lehet vizualizálni az adatokat és a skálázás minőségét megállapítani, illetve a shálázó szoftver a Graphite HTTP API-ján keresztül képes minden szükséges információhoz hozzáférni.
A szerverek monitorozására először az Amazon beépített CloudWatch szolgáltatását próbáltam használni, de az 5 perces monitorozási idő miatt el kezdtem keresni az alternatívákat.
A szerverek monitorozására a szerverekre telepített Collectd démont használom. A processzor kihasználtságot, a memóriahasználatott, és az Apache adatait monitorozom fél perces gyakorisággal, és küldöm tovább a Graphite-nak, ami tárolja ezeket. Ezen kívül a skálázó alkalmazásból StatdD segítségével tudom eljutatni az információkat a Graphite-nak.
