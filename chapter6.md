#Terhelési minták
Ahhoz meg tudjuk vizsgálni az egyes algoritmusok minőségét, szükséges megérteni, hogy az oldalunkra látogatók milyen rendszerességgel érkeznek. Ezért lentebb ismertetem a valóságban előforduló terhelési minták csoportosítását.[@mao_auto-scaling_2011]

##Stabil
Amikor egy kiszolgálóhoz folyamatosan érkeznek be a kérések, nem változik nagyon a terhelés. Ilyen a terhelése például egy monitorozó rendszereknek, melyre mindig hasonló mennyiségű kérés érkezik.

##Növekvő
Erről akkor beszélünk, amikor a terhelés egyre növekvő tendenciát mutat. Ilyen egy híroldal vagy videómegosztó oldal terhelése, ahogy egy hírt felraknak egyre több kérés érkezik az oldal felé, ahogy az hír egyre népszerűbb lesz és egyre többen hivatkoznak rá mint forrás.

##Ciklus
Ciklikusnak nevezzük a azokat a terhelési mintákat amelyet egy online üzlet produkál. Reggeltől egyre több kérés érkezik a kiszolgálóhoz egészen estig, amikor ismét csökkenni kezd. De beszélhetünk éves ciklusról is, amikor harácsony közeledtével megnő a kereslet az ajándékozási láz miatt.

##Ki és be
Ilyen terhelési mintákról amikor a terhelés csak ritkán érkezik terhelés, például batch feldolgozásnál. Ekkor a rendszert rövid ideig használják, majd utána szinte ki lehet kapcsolni, vagy nagyon minimális erőforrással lehet üzemeltetni. Ilyen lehet a terhelési mintája például az online videokódoló rendszereké, melyre időnként használnak renderelésre, de a kérés lefutása után nem jut rá nagy terhelés.

##Slashdot effect
A növekvő terhelési minta egy végletének is lehet értelmezni, amikor egy oldal hirtelen, órák, vagy akár percek alatt hihetetlen nagyon népszerű lesz és egyre többen és többen akarják elérni. A nem ekkora terhelésre tervezett oldalak pillanatok alatt elérhetetlenné válhatnak, még akkor is, ha terveztek bele valamilyen skálázódást, csak ahhoz emberi beavatkozásra lenne szügség, ami ennyi idő alatt nem lehetséges.[@killalea_building_2008]
