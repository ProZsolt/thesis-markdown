#Keretrendszer
Szeretném bemutatni a z eszközöket, amelyeket a feladatom megoldása során használtam.

##AWS


###Instance tipusok
Jelenleg az Amazon termékpalettáján jelenleg 39 féle instce típust találhatunk meg.[@EC2I] Mindenki megtalálhatja a maga feladatának megfelelő felépítésűt. A feladat mekönnyítése érdekében az Amazon 6 kategóriába rendezi a virtuális gépeket.

* Általános felhasználású T2,M3,M4
* Számítás optimalizált C3, C4
* Memória optimalizált R3
* GPU optimalizált G2
* I/O optimalizált I2
* háttértár optimalizát D2

Szakdolgozatom írása során ésn az amazon költséghatékony árazású általános felhasználásra szánt virtuális gépeit használtam.

-------------- --------------- --------- --------- ------
Instnce típus  Virtuális CPU   Memória   Tárhely   Ár
-------------- --------------- --------- --------- ------ 
t2.micro       1               1         8         0.013

t2.small       1               2         8         0.026

t2.medium      2               4         8         0.052

t2.large       2               8         8         0.104
-------------- --------------- --------- --------- ------ 

###IAM

###AMI

###ELB

###Autoscaling group

##Wordpress
A Wordpress egy nyílt forráskódú weboldal készítő eszköz PHP-ben írva. A világ egyik legnépszerűbb tartalomkezelő rendszere.

##JMeter
JMeter egy nyílt forráskódú terheléstesztelő szoftver Java-ban írva. Rengeteg plugin-nel, mellyel könnyedén alkalmassá válik szinte minden feladatra. 

##Ruby
A scaler implementációjára a Ruby programozási nyelvet választottam. A projekt méretét tekintve, és hogy csak egyedül dolgozom rajta, célom volt hogy a kódom írása során az egyszerűségre[@KISS] törekedjek, és hogy ahol lehet a könyvtárak támogatására hagyatkozzak.

##Graphite
Graphite[@graphite] egy idősor adatok tárolására és megjelenítésére készült alkalmazás.

Három a részből áll:

* carbon - Egy Twisted[@twisted] démon figyel a beérkező idősor adatokra
* whisper - Egy egyszrű adatbázis könyvtár az idősor adatok tárolására
* graphite webapp - Egy Django[@django] web applikáció, ami a grafikonokat rendereli Cairo[@cairo] segítségével

###Collectd
Collectd egy démon mely rendszer teljesítményének statisztikáit gyüjti és biztosítja a mechanizmust, hogy ezeket akár többféleképpen is eltárolhassuk, például a Graphite adatbázisába.

###Statsd
Az Etsy által készítet hálózati démon mely node.js alapokon fut. Figyeli a UDP-n és TCP-n beérkező statisztikákat, majd agregálva továbbküldi őket egy vagy több backend szolgáltatásnak (pl.: Graphite).
