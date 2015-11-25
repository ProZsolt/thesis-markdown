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

###Software as a Service

###Platform as a Service

###Infrastructure  as a Service

##Cloud rendszerek szervezés szerinti csoportosítása

###Public cloud
###Private cloud
###Hibrid cloud
