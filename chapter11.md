#Monitor

Ez a modul felelős a különböző metrikák begyüjtéséért, tárolásáért és hogy egy interfacet biztosítson a lekérdezésre.


##Graphite
Graphite[@graphite] egy idősor adatok tárolására és megjelenítésére készült alkalmazás.

Három a részből áll:

* carbon - Egy Twisted[@twisted] démon figyel a beérkező idősor adatokra
* whisper - Egy egyszrű adatbázis könyvtár az idősor adatok tárolására
* graphite webapp - Egy Django[@django] web applikáció, ami a grafikonokat rendereli Cairo[@cairo] segítségével


##CloudWatch és collectd


Monitorozásra először a Amazon CloudWatch szolgáltatását használtam, de ez a 5 percenkénti mintavételezési ideje miatt nem bizonyult elég nagy felbontásúnak.


A szerverek monitorozására a szerverekre telepített collectd démont használom.
Monitorozásra Graphite-ot használok, ahol aggregálva jelenik meg minden metrika. Ennek kettős szerepe...???

Collectd egy démon, mely a rendszer teljesítményének statisztikáit gyüjti és biztosítja a mechanizmust, hogy ezeket akár többféleképpen is eltárolhassuk, például a Graphite adatbázisába.

##Statsd
Az Etsy által készítet hálózati démon mely node.js alapokon fut. Figyeli a UDP-n és TCP-n beérkező statisztikákat, majd agregálva továbbküldi őket egy vagy több backend szolgáltatásnak (pl.: Graphite).

