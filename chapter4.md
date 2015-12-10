#Skálázási módszerek

##Erőforrás allokáció
Egy rendszer tervezésénél fel kell készülnünk a beérkező forgalom terhelésére, erre több módszer is létezik, melyeket itt mutatok be.[@srirama_deliverable_2010]

###Maximumra tervezés
A várható terhelés maximumára tervezzük a rendszerünket és ennek megfelelően foglaljuk le az erőforrásainkat, így minden beérkező igényt ki tudunk elégíteni. Hátránya, hogy az idő nagy részében az erőforrásaink kihasználatlanok, így a nem használt erőforrásainkért feleslegesen fizetünk.

###Átlagra tervezés
A várható átlagos terhelésre tervezzük a rendszerünket és ennek megfelelően foglaljuk le az erőforrásokat, így kissebb lesz az üzemeltetési költségünk, Ekkor az idő nagy részében ki tudjuk szolgálni a felhasználóinkat, de egy esetleges nagyobb igény esetén nem tudjuk kiszolgálni az összes felhasználót.

###Dinamikus erőforrás allokáció
Mindig az igénynek megfelelő erőforrást foglalunk le, így az üzemeltetési költségeink az optimális szintet tarthatóak és az összes hozzánk érkezett kérést ki tudjuk szolgálni. Ehhez a módszerhez már nem elég a tervezési fázisban eldönteni a rendszer kapacitását, folyamatosan figyelni kell az igényeket, és ennek megfelelően változtatni a rendszer állapotát. Ennek a problémának a megoldására a következő fejezetben ismertetek néhány algoritmust, melyek leveszik a terhet a vállunkról.

##Főbb skálázási típusok
Amikor skálázásról beszélünk két féle skálázási módszert különböztetünk meg[@hwang_cloud_2015][@whatScalability]

###Scaling up
Ekkor újabb erőforrásokat adunk egyazon logikai egységhez, például több memóriát vagy nagyobb processzor teljesítményt.
Virtuális gépeknél mindezt gyorsan és könnyen megtehetjük minden különösebb erőfeszítés nélkül, egy két kattintással, vagy pár sor kóddal.
Előnye, hogy nem kell új gépet menedzselni és a gépek közötti kommunikációt megoldani, illetve az estleges szoftver licencekből is kevesebb kell. Hátránya hogy az esetleges rendszerhiba esetén egy nagyobb kapacitás esik ki a rendszerünkből.

###Scaling out
Ilyenkor ahelyett, hogy megnövelnénk az egyik logikai egységünk teljesítményét, egy újabb logikai egységet adunk a már létező mellé. Egy ilyen rendszer sokkal jobban bírja a terhelést és nagyobb hibatűréssel rendelkezik, viszont az egyre növekvő számú gépparkunk több és több adminisztrációs feladatot ró ránk.
