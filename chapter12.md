#Skálázó

Ez a része a programonank teljesen moduláris, minvel lényege, hogy minél több skálázisi algoritmust egyszerűen ki lehessen próbálni.

##Ruby
A scaler implementációjára a Ruby programozási nyelvet választottam. A projekt méretét tekintve, és hogy csak egyedül dolgozom rajta, célom volt, hogy a kódom írása során az egyszerűségre[@KISS] törekedjek, és hogy ahol lehet a könyvtárak támogatására hagyatkozzak.

##Általános felépítése
A skálázáshoz szükséges metrikákat a Graphite HTTP API-ján keresztül kérjük le.[@GraphiteAPI] Az API az eredményeket JSON formátumban adja vissza. Erre épülve készítettem egy Monitor osztályt, mely a lekérdezéseket kényelmesebbé teszi, úgy hogy könnyen paraméterezhetőek a függvényei és a  metrikákat egy könnyen használható struktúban adja vissza.

A kálázási algoritmus végeredményét, hogy kell-e ki- vagy beskálázni az Erőforrás Controller megfelelő függvényeinek hivogatásával jutathatjuk érvényre.

##Automatikus skálázási algoritmusok
Kiválasztottam egy reaktív és egy prediktív algoritmust, melyek implementálásával és a mérés eredményeinek összehasonlításával demonstrálom a rendszer működését.
Mindkét algoritmus működéséhez szügséges, hogy hozzáférjenek a következő metrikákhoz:

* avgCPU[t] - A virtuális gépek átlagos processzor kihasználtsága t időpillanatban.
* numVM - Aktuálisan futó virtuális gépek száma

###Szabály alapú skálázás
A legtöbb IaaS cloud szolgáltató alapjában véve ezt használja alapértelmezetten mivel relatívan egyszerű az implementálása és felhasználói szempontból egyszerű a paraméterezése.
A következő paramétereket fogadja az algoritmus:

* thrUp - A köszöb mely fölött felfele skálázunk (pl.: 70%-os processzor kihasználtság)
* vUp - Ennyi másodpercig kell teljesülnia a fentebbi thrUp küszöbnek.
* inUp - A felskálázás lecsengésének ideje másodpercben, eddig nem végzünk újabb skálázást, ha felskálázás történt.
* thrDown - A köszöb mely fölött lefele skálázunk (pl.: 50%-os processzor kihasználtság)
* vDown - Ennyi másodpercig kell teljesülnia a fentebbi thrDown küszöbnek.
* inDown - A leskálázás lecsengésének ideje másodpercben, eddig nem végzünk újabb skálázást, ha leskálázás történt.

Implementálása a következő algoritmus szerint történt:

\begin{align*}
&\text{ha avgCPU[t] > thrUp vUp másodpercen keresztül, akkor}\\
&\hspace{1cm}numVM = numVM + 1\\
&\hspace{1cm}\text{ne csinálj semmit inUp másodpercig}\\
&\\
&\text{ha avgCPU[t] < thrDown vDown másodpercen keresztül, akkor}\\
&\hspace{1cm}numVM = numVM - 1\\
&\hspace{1cm}\text{ne csinálj semmit inDown másodpercig}\\
\end{align*}



###Exponenciális simítás segítségével történő előrejelzés
Exponenciális simitás segítségével megjósolhatjuk a rendszer következő állapotást


##Skálázási algoritmusok összehasonlítása
A rendszerem tesztelésére előállítottam a mestersége terhelést a JMeter segítségével.

<div id="muterheles">
![Mesterséges terhelés\label{muterheles}](img/muterheles.png)
</div>


----------------------
Metrika                
----------------------
Késleltetés

Üzemeltetési költség

Elérhetőség