#Forgalom generátor
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

##Throughput Shaping Timer
A szabályozható forgalom generálást a JMeter Throughput Shaping Timer Plugin-jével oldottam meg. A plugin segítségével könnyen beállíthatjuk a kívánt másodpercenkénti kérések számát.

##Felhasználók szimulálása
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
