#Scaler

Ez a része a programonank teljesen moduláris, minvel lényege, hogy minél több skálázisi algoritmust egyszerűen ki lehessen próbálni.

##Ruby
A scaler implementációjára a Ruby programozási nyelvet választottam. A projekt méretét tekintve, és hogy csak egyedül dolgozom rajta, célom volt, hogy a kódom írása során az egyszerűségre[@KISS] törekedjek, és hogy ahol lehet a könyvtárak támogatására hagyatkozzak.

##Általános felépítése
A skálázáshoz szükséges metrikákat a Graphite HTTP API-ján keresztül kérjük le.[@GraphiteAPI] Az API az eredményeket JSON formátumban adja vissza. Erre épülve készítettem egy Monitor osztályt, mely a lekérdezéseket kényelmesebbé teszi, úgy hogy könnyen paraméterezhetőek a függvényei és a  metrikákat egy könnyen használható struktúban adja vissza.

A kálázási algoritmus végeredményét, hogy kell-e ki- vagy beskálázni az Erőforrás Controller megfelelő függvényeinek hivogatásával jutathatjuk érvényre.

##Automatikus skálázási algoritmusok
A következőkben bemutatom néhány sálázási algoritmus konkrét megvalósítását.

###Szabály alapú


###ARIMA