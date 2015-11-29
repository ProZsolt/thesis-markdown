# Desing overview
Szakdolgozatom sororán egy olyan mérési környezetet alakítottam ki, ami teljesen moduláris, így később, ha módosítani kellene, például más IaaS szolgáltatót szeretnénk használni, vagy más metrika gyűjtési módszert alkalmazni, vagy a későbbiekben bemutatott különböző algoritmusokat szeretnénk használni, akkor csak a adott modult kell kicserélni, illetve maximum minimális változtatásokat eszközölni az alkalmazás többi részén.
Az általm készült rendszer a 5 részből áll, ahogy azt az ábrán láthatjuk.



##IaaS infrastruktúra


###WordPress
A Wordpress egy nyílt forráskódú weboldal készítő eszköz PHP-ben írva. A világ egyik legnépszerűbb tartalomkezelő rendszere.

##Forgalom generátor
Cél az volt, hogy a valóságban előforduló forgalomfajtákat (menyről részletesebben a 7. fejezetben írtam) generáljunk és ezzel terheljük meg a rendszerünket.

##Monitor

Eza a modul felelős a különböző metrikák begyüjtéséért, tárolásáért és hogy egy interfacet biztosítson a lekérdezésre.


##Scaler


##Erőforrás kontroller
Ez felelős a Scaler-által ígényelt erőforrások lefoglalásáért. Interfaceként szolgál az IaaS infrastruktúra felé, esetleges IaaS szolgáltató váltásnál elég ezt lecserélni.
A modul a következő fukncionalitásokat tudja:

* `scale_up`: A jelenlegi kapacitást megnöveli X egységgel, alapértelmezetten egyel
* `scale_down`: A jelenlegi kapacitást lecsökkenti X egységgel, alapértelmezetten egyel
* `set_capacity`: A kapacitást beállítja X egységre

Jelenlegi megvalósításnál a kontroller AWS SDK segítségével, méretezi a Auto Scaling group-ban található szerverek számát.
