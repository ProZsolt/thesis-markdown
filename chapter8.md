# Desing overview
Szakdolgozatom sororán egy olyan mérési környezetet alakítottam ki, ami teljesen moduláris, így később, ha módosítani kellene, például más IaaS szolgáltatót szeretnénk használni, vagy más metrika gyűjtési módszert alkalmazni, esetleg a későbbiekben bemutatott különböző algoritmusokat szeretnénk használni, akkor csak a adott modult kell kicserélni, illetve maximum minimális változtatásokat eszközölni az alkalmazás többi részén.
Az általam készült rendszer a 5 részből áll, ahogy azt az ábrán láthatjuk.

[KÉP]

##IaaS infrastruktúra
IaaS szolgáltatónál megvalósított infrastruktúra, mely tartalmaz egy két rétegű infrastruktúrát. Egy skálázható alkalmazási réteget, előtte egy load balancer-t és mögötte egy adatbázis réteget.
Az Amazon Web Service-n történő konkrét megvalósításról a 10. fejezetben írok bővebben.

###WordPress
Az alkalmazási rétegben a WordPress tartalomkezelő rendszert fogom skálázni.
A WordPress egy nyílt forráskódú weboldal készítő eszköz PHP-ben írva. A világ egyik legnépszerűbb tartalomkezelő rendszere.

##Forgalom generátor
A forgalom generátor feladata, hogy a valóságban előforduló forgalomfajtákkal (melyről részletesebben a 7. fejezetben írtam) terhelje meg a rendszert, hogy a rendszernek erre adott válaszát mérni tudjuk.
A JMeter-el történő konkrét megvalósításról a 10. fejezetben írok bővebben.

##Monitor

Ez a modul felelős a különböző metrikák begyütéséért, tárolásáért és egy interfészt biztosít a lekérdezésre. Tervezésnél fontosnak tartottam, hogy ezeket a metrikákat minél több helyről tudjam összegyűjteni.
A Graphite-al történő konkrét megvalósításról a 10. fejezetben írok bővebben.

##Skálázó
A mérési környezet lényegét adó modul, mely felelős a Monitor által begyűjtött metrikákból eldönteni, hogy a rendszert milyen állapotra kell hozni, igényel-e még erőforrásokat, vagy jelenleg túl sok kihasználatlan erőforrás van lefoglalva. Majd amikor döntésre jutott az Erőforrás kontroller segítségével érvényre juttatni a döntést.

##Erőforrás kontroller
Ez felelős a Scaler-által ígényelt erőforrások lefoglalásáért. Interfaceként szolgál az IaaS infrastruktúra felé, esetleges IaaS szolgáltató váltásnál elég ezt lecserélni.
A modul a következő fukncionalitásokat tudja:

* `scale_up`: A jelenlegi kapacitást megnöveli X egységgel, alapértelmezetten egyel
* `scale_down`: A jelenlegi kapacitást lecsökkenti X egységgel, alapértelmezetten egyel
* `set_capacity`: A kapacitást beállítja X egységre

Jelenlegi megvalósításnál a kontroller AWS SDK segítségével méretezi a Auto Scaling group-ban található szerverek számát.
