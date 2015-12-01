#IaaS infrastruktúra
Az alábbi fejezetben először röviden bemutatom az Amazon Web Services általam használt szolgáltatásait, majd részletesen bemutatom az általam készített skálázható infrastruktúrát

##Amazon Web Services

###EC2 Instance tipusok
EC2 Instance-nak nevezzük az AWS virtuális szervereit.
Jelenleg az Amazon termékpalettáján 39 féle instance típust találhatunk meg.[@EC2I] Mindenki megtalálhatja a maga feladatának megfelelő felépítésűt. A feladat mekönnyítése érdekében az Amazon 6 kategóriába rendezi a virtuális gépeket.

* Általános felhasználású T2,M3,M4
* Számítás optimalizált C3, C4
* Memória optimalizált R3
* GPU optimalizált G2
* I/O optimalizált I2
* háttértár optimalizát D2

Szakdolgozatom írása során és az Amazon költséghatékony árazású általános felhasználásra szánt virtuális gépeit használtam.

-------------- --------------- --------- --------- ----------
Instnce típus  Virtuális CPU   Memória   Tárhely   Ár
-------------- --------------- --------- --------- ---------- 
t2.micro       1               1GB       8GB       0.013$/óra

t2.small       1               2GB       8GB       0.026$/óra

t2.medium      2               4GB       8GB       0.052$/óra

t2.large       2               8GB       8GB       0.104$/óra
-------------- --------------- --------- --------- ----------

###Identity and Access Management (IAM)
Segítségével könnyen és biztonságosan kontrollálhatjuk hozzáférést az AWS erőforrásokhoz és szolgáltatásokhoz. IAM-mel készíthetük és menedzselhetjük a felhasználókat és csoportokat, valamint szabályokat állíthatunk fel, hogy mihez férjenek hozzá és mihez ne.

###Amazon Machine Images (AMI)
Az Amazon Machine Images biztosítja az információkat, melyek szükségesek ahhoz, hogy el tudjuk indítani a EC2-es Instance-okat.
Következő dolgokat tartalmazza:

* Egy sablonját az alapértelmezett meghatónak, mely tartalmazhatja az operációs rendszert, az alkalmazás szervert és az alkalmazásokat.
* Indítási jogokat, mely tartalmazza melyik felhasználó használhatja új Instance indítására.
* És a block device mapping-ot, hogy melyik meghajtót csatoljuk fel az intance-ra, amikor elindítjuk. 

###Elastic Load Balancer(ELB)
Ez round robin segítségével osztja szét a forgalmat a hozzárendelt kiszolgáló szerverek között. Egyszerűen tudunk hozzáadni és elvenni szervereket.

###CloudFormation
Az AWS CloudFormation egy olyan eszközt ad a fejlesztők kezébe, mellyel egyszerűen lehet létrehozni és menedzselni az összefüggő AWS erőforrásokat.
Könnyen írhatunk sablonokat JSON formátumban, melyben leírjuk a szükséges erőforrásokat. Nem kel nekünk kitalálni a lefoglalás sorrendjét, az AWS lefoglalja a szükséges sorrendben. Az így lefoglalt erőforrásokat egyben kezelhetjük, módosíthatjuk, szüntethetjük meg. Az egyben kezelt erőforrásokat stack-nek nevezzük.

###LaunchConfiguration
A LaunchConfiguration tartalmaz minden szerverindításhoz kapcsolódó információt, úgy mint az instance típusa, az AMI-t, és tartalmazhat az első indításkor lefutó parancsokat, melyel alkalmazásokat telepíthetünk, illetve bekonfigurálhatjuk a szerverünket.

###Autoscaling group
Autoscaling segítségével könnyen skálázhatunk le és fel. Amikor létrehozunk egy ilyet, megadhatunk neki egy LaunchConfiguration-t, mely segítségével képes lesz új szerverek indítására. Segítségével egy egyszerű API hívás segítségével állíthatjuk be a futó szervereink számát, ha túl sok fut akkor leállít néhányat, ha kevés akkor meg újakat indít a beállított LaunchConfiguration segítségével. Hozzárendelhetünk egy vagy több Elastic Load Balancer-t mely segítségével eloszthatjuk rajta a forgalmat.

##Infrastruktúra megvalósítása
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
