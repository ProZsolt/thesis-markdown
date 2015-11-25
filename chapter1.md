#Cloud computing alapfogalmak

Ennek a fejezetnek a célja, hogy mielőtt rátérnék a szakdolgozatom lényegi részét adó feladat tárgyalására, szeretnék egy átfogó képet adni az informatika ezen új ágáról.

##Mi a cloud computing?

A elmúlt években a cloud computing egy új irányvonal lett az informatika fejlődésében. Köszönhetően a modern létének folyamatosan fejlődik és alakul.
A tradicionális vállalati rendszerek igen bonyolultak és költségesek. Az eszközök (szoftver és hardver) mennyisége és sokfélesége miatt külön szakértői csapatokat igényelnek, akik installálják, tesztelik, futtatják, frissítik a rendszer egyes elemeit. A cloud computing leveszi ezt a terhet a vállalatokról, úgy hogy nem kell ezeket lokálisan menedzselni, hanem egy szakértelemmel rendelkező külső cégre bízza, aki ezen túl felelős érte. [@Salesforce]
A cloud computing mostanára inkább buzzword lett, mintsem konkrét definíció, köszönhetően a bőséges marketingnek az IT iparban. A különböző vállalatoknak mind meg van a maguk egyedi definíciója rá.
Az Amazon (aki elsők között nyújtott cloud szolgáltatást ) szerint a cloud computing igény szerinti IT erőforrások és applikációk elérése az interneten keresztül. Annyit fizetsz amennyit használsz árazással.[@AmazonCloud]
A témában releváns publikációkban és cikkekben található rengeteg felületes, ellentmondásos megfogalmazás épp ezért én a ipari szabvány definícióját irom le, melyet a National Institute of Standards and Technology fogalmazott meg.

##NIST definíció
Cloud computing egy modell, amely lehetővé teszi, egy  mindenütt jelenlevő, kényelmes, igény szerinti hálózati hozzáférést egy megosztott medence konfigurálható számítási erőforrások (pl. hálózatok, szerverek, háttértárolók, alkalmazások és szolgáltatások), gyorsan le lehet foglalni és felszabadítani minimális menedzselési erőfeszítéssel vagy a szolgáltatói interakcióval.[@NIST]

##A felhő modell öt alapvető jellegzetessége

### Igény szerinti önkiszolgáló
A fogyasztó egyoldalúan rendelkezik számítástechnikai erőforrásokról, mint például a processzor idő és hálózati tároló, automatikusan anélkül az emberi beavatkozásra lenne szükség az egyes szolgáltatóknál.

### Széles hálózati hozzáférés
A szolgáltatások hálózaton keresztül hozzáférhetőek, olyan protokollon keresztül melyet rengeteg eszköz (pl. munkaállomás, laptop, mobiltelefon, tablet) támogat.

### Erőforrás pooling
A szolgáltató számítástechnikai erőforrásait (pl. processzor kapacitás, memória, háttér tároló) összevonják, úgy hogy egyszerre több felhasználót tudjon kiszolgálni, több bérlő (multi-tenant) modellben. A különböző fizikai és virtuális erőforrások dinamikusan hozzárendelhetők és újraoszthatók a fogyasztói kereslet függvényében. A fogyasztó általában nem tudja befolyásolni a biztosított erőforrásoknak a pontos helyét, csak egy magasabb absztrakciós szinten (pl. ország, város, vagy adatközpont). 

### Gyors elaszticitás
Az erőforrásokat gyorsan le lehet foglalni és felszabadítani. A felhasználó szempontjából a hozzáférhető erőforrások poolja végtelennek tűnhet, akármikor, akármekkora mennyiségben foglalhat belőle le.

### Mért szolgáltatás
Az erőforrások használata nagy részletességgel monitorozandó, mely megkönnyíti az erőforrások automatikus és optimális használatát. Az erőforrások felhasználásának mennyiségének mind a felhasználó, mind szolgáltató felé átláthatónak kell lennie.

##Cloud rendszerek szolgáltatás szerinti csoportosítása

<div id="IPSaaS">
![Cloud rendszerek szolgáltatás szerinti csoportosítása\label{IPSaas}[@IPSaaS]](img/IPSaas.png)
</div>

###Software as a Service
Az a képesség biztosított, hogy a felhasználó használja a szolgáltató applikációját egy felhő infrastruktúrán. A szolgáltatás elérhető különböző klienseken keresztül, akár vékonykliensen, mint például a webböngésző, vagy egy programspecifikus API-n keresztül. A felhasználó nem menedzseli vagy felügyelheti a program alatt futó felhő infrastruktúrát, beleértve az operációs rendszert, a hálózatot, szervereket vagy a tárhelyet, eltekintve néhány felhasználó függő alkalmazásspecifikus konfigurációs beállítástól.[@NIST]

###Platform as a Service
Az a képesség biztosított, hogy a felhasználó telepítheti az általa írt, vagy más forrásból szerzet alkalmazást a felhő infrastruktúrára, a szolgáltató által biztosított programozási nyelvek, könyvtárak, szolgáltatások és eszközök segítségével. A felhasználó nem menedzseli vagy felügyelheti a program alatt futó felhő infrastruktúrát, beleértve az operációs rendszert, a hálózatot, szervereket vagy a tárhelyet, de az ő irányítása alatt állnak a telepített applikációk és konfigurációs beállításai az alkalmazás hoszting környezetnek.[@NIST]

###Infrastructure  as a Service
A képesség biztosított, hogy a felhasználó rendelkezhet a processzor idő, a háttértár, a hálózat és egyéb alapvető számítási erőforás felett, melyre bármilyen szoftvert telepíthet, mely magában foglalja az operációs rendszert a probramnyelvek futtatási környezetét és egyéb alaklmazásokat.[@NIST]

##Cloud rendszerek szervezés szerinti csoportosítása

###Private cloud
A felhő infrastruktúrát azért tartják fent, hogy kizárólagos rendelkezésére álljon egy szervezetnek, mely állhat több kisebb felhasználóból (pl. szervezet rész). Tulajdonosa, üzemeltetője lehet a szervezet, vagy egy harmadik fél, vagy e kettő kombinációja. Helyileg lehet a szervezet területén, vagy máshol is.[@NIST]

###Community cloud
A felhő infrastruktúrát azért tartják fent, hogy kizárólagos rendelkezésére egy felhasználókból álló specifikus közöségnek, mely olyan szervezetekből jöttek létre, amelyek ugyanazokat az elveket (célt, biztonsági előírást, eljárásmódot) tartják fontosnak. Tulajdonosa, üzemeltetője lehet egy vagy több a közöségben lévő szervezet, vagy egy harmadik fél, vagy e kettő kombinációja. Helyileg lehet a szervezet területén, vagy máshol is.[@NIST]

###Public cloud
A felhő infrastruktúrát azért tartják fent, hogy a mindenki számára rendelkezésre álljon. Tulajdonosa, üzemeltetője lehet üzleti vállalkozás, akadémiai vagy kormányzati szervezet, vagy ezek valamilyen kombinációja. Helyileg a szolgáltató területén létezik.[@NIST]
 
###Hibrid cloud
A felhő infrastruktúra két vagy több különböző felhő infrastruktúrából (private, community, vagy public) áll, melyek különálló egyedek maradnak, de összeköti őket egy sztenderdizált, vagy egyedi technológia, ami lehetővé teszi az alkalmazások hordozhatóságát. (pl. cloud bursting a felhők közötti terheléselosztásra).[@NIST]

