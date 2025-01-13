---
layout: default
title: Izrada reljefa
nav_order: 3
parent: Uvod
---
# Izrada reljefa 

Na ovim vježbama student će odraditi predradnje nužne za izradu reljefa na karti temeljem podataka digitalnog modela reljefa (DMR). Nakon preuzimanja podataka, student će podatke transformirati u koordinatni sustav izabrane kartografske projekcije, prekontrolirati podacima hidrografije i izrezati na unutarnji okvir karte. Na preobrađene podataka digitalnog modela reljefa, student će primijeniti postupke filtriranja i računalnog sjenčanja. Dobiveni rezultati stvorit će dojam plastičnosti reljefa na karti: prikaz visina hipsometrijskom skalom boja i prikaz reljefnih oblika svjetlom i sjenom. 

**Napomena:**Za izradu ovih vježbi potrebno je imati odrađene prethodne vježbe – kreiran sloj pravokutnog unutarnjeg okvira karte. Ovi materijali prilagođeni su izradi reljefa u GIS alatu [GRASS GIS 7.8.7](https://grass.osgeo.org/download/windows/), te njegovoj vizualizaciji u [QGIS 3.26 Buenos Aires](https://blog.qgis.org/2022/06/24/qgis-3-26-buenos-aires-is-released/).

## Ishodi učenja
Po završetku  ovih vježbi student će moći:
- > procijeniti prikladnost izvornika i rasterskih podataka DMR-a za izradu reljefa karte,
- >	tumačiti dozvole i ograničenja nad preuzetim rasterskim podacima,
- > interpretirati koordinatni sustav preuzetih podataka u odnosu na izabranu najpovoljniju kartografsku projekciju,
- > koristiti alate GIS sustava GRASS GIS u predobradi rasterskih podataka DMR-a za izradu reljefa,
- > odrediti razinu detaljnosti rastera reljefa u odnosu na mjerilo karte,
- >	izabrati najpovoljnije parametre računalnog (analitičkog) sjenčanja reljefa za neko područje,
- > objasniti značaj boje i oblikovati prilagođenu hipsometrijsku skalu boja za prikazivanje visina reljefa.

## Koncepti koji će se upotrijebiti na vježbama
Prikazivanje oblika reljefa Zemlje je složen kartografski zadataka jer se radi o kontinuiranom trodimenzionalnom objektu. Prikazom treba prvo osigurati dovoljnu geometrijsku točnost, a zatim i što veću zornost, kako bi se lakše spoznavali trodimenzionalni objekti prikazani u dvodimenzionalnoj ravnini karte. Reljef je jedini skup podataka na karti koji se prikazuje rasterom. U ovisnosti o izvoru s kojeg se preuzimaju, rasterski podaci mogu biti u različitim formatima, različitog prostornog obuhvata, u različitim koordinatnim sustavima i slično. S obzirom na karakteristike karte (mjerilo, područje prikaza,…), podaci najčešće neće direktno odgovarati potrebama karte zbog čega je potrebno napraviti predobradu podataka. Na općegeografskim kartama srednjih i sitnijih mjerila reljef se često prikazuje hipsometrijskom skalom boja.

![izrada reljefa](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/Reljef.svg)

## Koraci u izradi matematičke osnove karte
