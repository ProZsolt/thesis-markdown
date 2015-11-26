#Terhelési minták
Ahhoz, hogy meg tudjuk vizsgálni az egyes algoritmusok minőségét, szükséges megérteni, hogy az oldalunkra látogatók milyen rendszerességgel érkeznek. Ezért lentebb ismertetem a valóságban előforduló terhelési minták csoportosítását.[@mao_auto-scaling_2011]
[KÉP]

##Stabil
Amikor egy kiszolgálóhoz folyamatosan érkeznek be a kérések, nem változik nagyon a terhelés. Ilyen a terhelése például egy monitorozó rendszereknek, melyre mindig hasonló mennyiségű kérés érkezik.

##Növekvő
Erről akkor beszélünk, amikor a terhelés egyre növekvő tendenciát mutat. Ilyen egy híroldal vagy egy videómegosztó oldal terhelése. Amint egy friss hírt jelenik meg az oldalon, egyre több kérés érkezik az oldal felé, annak megfelelően ahogy az adott hír egyre népszerűbb lesz és egyre többen hivatkoznak rá, mint forrás.

##Ciklus
Ciklikusnak nevezzük azokat a terhelési mintákat amelyet egy online üzlet produkál. Reggeltől egyre több kérés érkezik a kiszolgálóhoz egészen estig, amikor ismét csökkenni kezd. De beszélhetünk éves ciklusról is, amikor karácsony közeledtével megnő a kereslet az ajándékozási láz miatt.

##Ki és be
Ilyen terhelési mintáról akkor beszélünk, amikor csak ritkán érkezik terhelés a rendszerre, például batch feldolgozásnál. Ekkor a rendszert rövid ideig használják, majd utána szinte ki lehet kapcsolni, vagy nagyon minimális erőforrással lehet üzemeltetni. Ilyen lehet a terhelés mintája például az online videokódoló rendszereknek, melyeket időnként használnak renderelésre, de a kérés lefutása után nem jut rá nagy terhelés.

##Slashdot effect
A növekvő terhelési minta egy végletének is lehet értelmezni, amikor egy oldal hirtelen, órák, vagy akár percek alatt hihetetlen nagyon népszerű lesz és egyre többen és többen akarják elérni. A nem ekkora terhelésre tervezett oldalak pillanatok alatt elérhetetlenné válhatnak, még akkor is, ha terveztek bele valamilyen skálázódást, csak ahhoz emberi beavatkozásra lenne szügség, ami ennyi idő alatt nem lehetséges.[@killalea_building_2008]
