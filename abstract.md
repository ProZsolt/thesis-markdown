Kivonat {.unnumbered}
=======

A felhő infrastruktúra legnagyobb előnye a hagyományos saját infrastruktúrával szemben hogy Infrastucture as a Service (IaaS) modell tetszés szerint foglalhatunk le és szabadíthatunk fel virtuális szervereket látszólag korlátlan mennyiségben, így ideális esetben mindig annyi erőforrásért fizetünk, amennyit ha ténylegesen kihasználunk. Az aktuális terheléshez szükséges erőforrások mennyiségének megállapítása egy nem triviális probléma. Az utóbbi években számos automatikus skálázást megvalósító algoritmus, illetve vezérlés került ismertetésre a szakirodalomban.

Ezen szakdolgozat során bemutatom a különböző problémákat melyek felmerülnek a dinamikus erőforrás allokáció során. A szakdolgozatom elején bemutatom a különböző automatikus skálázási algoritmusokat, valamint a valóságban megjelenő terhelési mintákat, majd összeállítom az automatikus skálázási algoritmusoknak egy minőségi modelljét.

Az automatikus skálázás algoritmusok benchmarkolását lehetővé tévő keretrendszert az Amazon Web Services infrastruktúráján valósítottam meg, melyen egy Wordpress alkalmazást skálázok. 


Abstract {.unnumbered}
========

The cloud infrastructure's main advantage against own infrasucture is that in the Infrastucture as a Service (IaaS) model we can provision and de provision virtual machines as needed in seemingly infinite quantity. Ideally we pay only for the resources that we actually use. Calculating the resource needed for the actual load is a non trivial problem. In the last few years many automatic scaling algorithm publicated.

This thesis i will show the different issues that arise in the dinamic resource provisioning. In the first part I present the different scaling algorithms, and the load patterns that appear in the real world. Afther that I create the quality model of the automatic scaling algorithms.

The automatic scaling algorithm benchmarking framework was implemented on the Amazon Web Services infrastructure, where I scale a Worldpress application.
