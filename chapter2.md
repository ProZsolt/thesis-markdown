#Cloud computing alapfogalmak

Ennek a fejezetnek a célja, hogy mielőtt rátérnék a szakdolgozatom lényegi részét adó feladat tárgyalására, egy átfogó képet adjak az informatika ezen ágáról.

##Mi a cloud computing?

A elmúlt évek során a cloud computing egy új irányvonal lett az informatika fejlődésében, modern létének köszönhetően folyamatosan fejlődik és alakul.
A tradicionális vállalati rendszerek igen bonyolultak és költségesek. Az eszközök (szoftver és hardver) mennyisége és sokfélesége miatt külön szakértői csapatokat igényelnek, akik installálják, tesztelik, futtatják, frissítik a rendszer egyes elemeit. A cloud computing leveszi ezt a terhet a vállalatokról, úgy hogy nem kell ezeket lokálisan menedzselni, hanem ezen feladatokat egy szakértelemmel rendelkező külső cégre bízza, amely ezen túl felelős értük. [@Salesforce]
A cloud computing mostanára inkább buzzword lett, mintsem konkrét definíció, köszönhetően a bőséges marketingnek az IT iparban. A különböző vállalatoknak mind meg van a saját, egyedi definíciója rá.
Az Amazon (aki elsők között nyújtott cloud szolgáltatást ) szerint a cloud computing igény szerinti IT erőforrások és applikációk elérése az interneten keresztül. Annyit fizetsz amennyit használsz árazással.[@AmazonCloud]
A témában releváns publikációkban és cikkekben található rengeteg felületes, ellentmondásos megfogalmazás épp ezért én a ipari szabvány definícióját irom le, melyet a National Institute of Standards and Technology fogalmazott meg.

##NIST definíció
A cloud computing egy modell, amely lehetővé tesz egy mindenütt jelenlevő, kényelmes, igény szerinti hálózati hozzáférést, hogy egy konfigurálható, megosztott számítási erőforrás poolból (pl. hálózatok, szerverek, háttértárolók, alkalmazások és szolgáltatások), gyorsan le lehessen foglalni és felszabadítani erőforrásokat minimális menedzselési erőfeszítéssel vagy a szolgáltatói interakcióval.[@NIST]

##A felhő modell öt alapvető jellegzetessége

### Igény szerinti önkiszolgáló
A fogyasztó egyoldalúan rendelkezik számítástechnikai erőforrásokról, mint például a processzor idő és hálózati tároló, automatikusan anélkül, hogy emberi beavatkozásra lenne szükség az egyes szolgáltatóknál.

### Széles hálózati hozzáférés
A szolgáltatások hálózaton keresztül hozzáférhetőek, olyan protokollon keresztül melyet rengeteg eszköz (pl. munkaállomás, laptop, mobiltelefon, tablet) támogat.

### Erőforrás pooling
A szolgáltató számítástechnikai erőforrásait (pl. processzor kapacitás, memória, háttér tároló) összevonják úgy, hogy egyszerre több felhasználót tudjon kiszolgálni több bérlő (multi-tenant) modellben. A különböző fizikai és virtuális erőforrások dinamikusan hozzárendelhetők és újraoszthatók a fogyasztói kereslet függvényében. A fogyasztó általában nem tudja befolyásolni a biztosított erőforrásoknak a pontos helyét, csak egy magasabb absztrakciós szinten (pl. ország, város, vagy adatközpont).

### Gyors elaszticitás
Az erőforrásokat gyorsan le lehet foglalni és felszabadítani. A felhasználó szempontjából a hozzáférhető erőforrások poolja végtelennek tűnhet, akármikor, akármekkora mennyiségben foglalhat belőle le.

### Mért szolgáltatás
Az erőforrások használata nagy részletességgel monitorozandó, mely megkönnyíti az erőforrások automatikus és optimális használatát. A felhasznált erőforrások mennyiségének mind a felhasználó, mind szolgáltató felé átláthatónak kell lennie.

##Cloud rendszerek szolgáltatás szerinti csoportosítása

<div id="IPSaaS">
![Cloud rendszerek szolgáltatás szerinti csoportosítása\label{IPSaas}[@IPSaaS]](img/IPSaas.png)
</div>

###Software as a Service
Az a képesség biztosított, hogy a felhasználó használja a szolgáltató applikációját egy felhő infrastruktúrán. A szolgáltatás elérhető különböző klienseken keresztül, mint például a webböngésző. A felhasználó nem menedzseli vagy felügyelheti a program alatt futó felhő infrastruktúrát, beleértve az operációs rendszert, a hálózatot, szervereket vagy a tárhelyet, eltekintve néhány felhasználó függő alkalmazásspecifikus konfigurációs beállítástól.[@NIST]
Jelenleg a legelterjedtebb ilyen szolgáltatás a Google Apps, mely magában foglalja a levelező kliensét(GMail), naptár szolgáltatását (Calendar), és irodai programcsomagját(Docs, Spreadsheet, Slides) és még néhány egyéb alkalmazást. Ezek az alkalmazások ingyen hozzáférhetőek a nagyközönség számára, de a vállalatok privát használatra előfizethetnek, mellyel leválthatják a klasszikus asztali számítógépre telepített irodai szoftvereiket.
Ezen kívül még nagyon sok szolgáltatás van, melyek az asztali számítógépeinket szinte vékonykliensé egyszerűsítik. Például a zenei szolgáltatást nyújtó Spotify, a CRM szolgáltatást nyújtó Salesforce, vagy a Microsoft Office 365 szolgáltatása.

###Platform as a Service
Az a képesség biztosított, hogy a felhasználó telepítheti az általa írt, vagy más forrásból szerzett alkalmazást a felhő infrastruktúrára, a szolgáltató által biztosított programozási nyelvek, könyvtárak, szolgáltatások és eszközök segítségével. A felhasználó nem menedzseli vagy felügyelheti a program alatt futó felhő infrastruktúrát, beleértve az operációs rendszert, a hálózatot, szervereket vagy a tárhelyet, de az ő irányítása alatt állnak a telepített applikációk és konfigurációs beállításai az alkalmazás hoszting környezetnek.[@NIST]
Ilyen szolgáltatást nyújt a Google App Engine ahol Java, Python, PHP és Go fejlesztőkörnyezeteket kapunk, vagy a Heroku amely Ruby, Python, Java, Scala, Cloture és Node.js programjainkat futtathatjuk könnyedén. Esetleg az ennél specifikusabb szolgáltatással rendelkező Acquia, ahol a php-re épülő Drupal-t hosztolhatunk könnyedén, minden egyébb fejlesztő környezet beállításából adódó gond nélkül.

###Infrastructure  as a Service
A képesség biztosított, hogy a felhasználó rendelkezhet a processzor idő, a háttértár, a hálózat és egyéb alapvető számítási erőforrás felett, melyre bármilyen szoftvert telepíthet, amely magában foglalja az operációs rendszert a programnyelvek futtatási környezetét és egyéb alkalmazásokat.[@NIST]
Ez a szolgáltatás a fentebb említett két szolgáltatás(Saas, Paas) alapja, ennél a szolgáltatásnál a felhasználó gyakorlatilag virtuális szervereket bérel, melyek paramétereit (processzor teljesítmény, memória, háttértár) maga adja meg. Ilyen szolgátatást nyújt a Amazon Web Services, a Rackspace és még néhány szólgáltató melyeket a következő fejezetben mutatok be részletesen.

##Cloud rendszerek szervezés szerinti csoportosítása

###Private cloud
A felhő infrastruktúrát azért tartják fent, hogy kizárólagos rendelkezésére álljon egy szervezetnek, mely állhat több kisebb felhasználóból (pl. szervezet rész). Tulajdonosa, üzemeltetője lehet a szervezet, vagy egy harmadik fél, vagy e kettő kombinációja. Helyileg lehet a szervezet területén, vagy máshol is.[@NIST]

###Community cloud
A felhő infrastruktúrát azért tartják fent, hogy kizárólagos rendelkezésére álljon egy felhasználókból álló specifikus közöségnek, mely olyan szervezetekből jött létre, amelyek ugyanazokat az elveket (célt, biztonsági előírást, eljárásmódot) tartják fontosnak. Tulajdonosa, üzemeltetője lehet egy vagy több a közöségben lévő szervezet, vagy egy harmadik fél, vagy e kettő kombinációja. Helyileg lehet a szervezet területén, vagy máshol is.[@NIST]

###Public cloud
A felhő infrastruktúrát azért tartják fent, hogy a mindenki számára rendelkezésre álljon. Tulajdonosa, üzemeltetője lehet üzleti vállalkozás, akadémiai vagy kormányzati szervezet, vagy ezek valamilyen kombinációja. Helyileg a szolgáltató területén létezik.[@NIST]

###Hibrid cloud
A felhő infrastruktúra két vagy több különböző felhő infrastruktúrából (private, community, vagy public) áll, melyek különálló egyedek maradnak, de összeköti őket egy sztenderdizált, vagy egyedi technológia, ami lehetővé teszi az alkalmazások hordozhatóságát. (pl. cloud bursting a felhők közötti terheléselosztásra).[@NIST]
