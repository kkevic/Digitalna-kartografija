---
layout: default
title: Matematicka osnova karte
nav_order: 2
parent: Uvod
---
# Izrada matematičke osnove karte 

Na ovim vježbama student će se upoznati sa zadanim područjem za izradu karte u sitnom mjerilu.
Na temelju oblika i pružanja zadanog teritorija, student će odabrati najpovoljniju kartografsku projekciju, definirati njezine parametre, te na osnovu toga konstruirati mrežu meridijana i paralela odgovarajuće gustoće, kao i pravokutni unutarnji okvir karte. 

## Ishodi učenja
Po završetku  ovih vježbi student će moći:
- > kritički razmotriti te samostalno odabrati, definirati i pridružiti koordinatni sustav najpovoljnije kartografske projekcije za prikaz dodijeljenog dijela svijeta
- >	primijeniti alate za konstruiranje unutarnjeg okvira i kartografske mreže za zadano područje u najpovoljnijoj kartografskoj projekciji.

## Koncepti koji će se upotrijebiti na vježbama
Izrada matematičke osnove karte (sitnog mjerila) uključuje: (1) određivanje mjerila karte, (2) izbor najpovoljnije kartografske projekcije, (3) oblikovanje kartografske mreže i (4) kompoziciju karte. Kompozicija karte podrazumijeva određivanje granica područja preslikavanja i smještaj područja unutar okvira karte te razmještaj naziva, mjerila i tumača znakova karte. Potonje će se obraditi u narednim vježbama kada karta bude dopunjena sadržajem.

![matem_osnova](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/Mat%20osnova%20grafike_path.svg)

## Koraci u izradi matematičke osnove karte

**1. Izbor kartografske projekcije**

Svaki student treba samostalno odabrati najpovoljniju kartografsku projekciju za zadano područje. Najpovoljnija projekcija je ona koja, prema određenom matematičkom kriteriju, ima najmanje ukupne deformacije u usporedbi s drugim projekcijama na promatranom području. Detaljnije informacije o faktorima koji utječu na izbor projekcije za izradu geografskih karata u mjerilu 1:1 000 000 i sitnijem mogu se pronaći u skripti Kartografske projekcije (Frančula, 2004), u poglavlju *Izbor projekcije*.

>**1.1 Određivanje vrijednosti parametara projekcije**

Za odabranu kartografsku projekciju potrebno je odrediti parametre na temelju veličine i položaja zadanog područja.

>**1.2 Definiranje koordinatnog sustava izabrane kartografske projekcije**

Potrebno je definirati korisnički koordinatni sustav, *Custom CRS (Coordinate Reference System)*, sa svim potrebnim parametrima za odabranu kartografsku projekciju. Kao primjer koristit će se uspravna konformna konusna projekcija s referentnim elipsoidom WGS84, jednom standardnom paralelom koja prolazi sredinom područja preslikavanja i srednjim meridijanom područja preslikavanja. Projekcija se definira pomoću sintakse [PROJ](https://proj.org/en/9.5/)-a, koja se koristi unutar QGIS-a za preciznu transformaciju koordinata između različitih kartografskih projekcija i referentnih sustava.

![UserDefinedCRS](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/UserDefinedCRS.png)

*Primjer definicije korisničkog koordinatnog sustava Lambertove konformne konusne projekcije s jednom standardnom paralelom pomoću sintakse PROJ-a.*

>**1.3 Određivanje mjerila**

Općenito, pri izradi karte mogu se javiti dva slučaja za određivanje mjerila: (1) mjerilo je unaprijed definirano ili (2) mjerilo je uvjetovano veličinom papira.

U zadatku na vježbama ***mjerilo karte uvjetovano je veličinom papira*** – formatom papira A4. Vrijednost mjerila moguće je odrediti nakon uspostavljanja veze između veličine područja za izradu karte (u ravnini kartografske projekcije) i veličine papira.

Mjerilo je moguće odrediti korištenjem modula QGIS-a Print *Layout*. Mjerilo je potrebno odabrati tako da bude zaokruženo na smislenu cjelobrojnu vrijednost.

**2. Konstruiranje kartografske mreže u koordinatnom sustavu uspravne ekvidistantne cilindrične projekcije (x=λ, y=φ) – Lat/Lon pseudoprojekcija**

Budući da je predefinirana kartografska projekcija QGIS-a [Lat/Lon EPSG: 4326](https://epsg.io/4326), ekvidistantna cilindrična projekcija s ravninskim koordinatama koje odgovaraju geografskoj širini i dužini, kartografska mreža u toj projekciji može se jednostavno iscrtati alatima dostupnima unutar QGIS-a. 

Optimalna gustoća linija kartografske mreže određuje se prema:

- > Optimalna gustoća mreže u mjerilu karte je približno 5 cm.
- > Na ekvatoru je 1° približno 110 km.
- > Ako je npr. mjerilo karte 1:1 000 000 tada je 5 cm na karti 50 km u prirodi, odnosno približno 0,5°.

Kako prilikom transformacije mreže u izabranu projekciju ne bi došlo do gubitka koordinatnih linija (uslijed moguće promjene oblika mreže, npr. kod konusnih projekcija) potrebno je konstruirati kartografsku mrežu (zadane gustoće) koja je **šira** od zadanog područja.

Za iscrtavanje kartografske mreže, koja je sa svake strane šira od granica zadanog područja, može se koristiti alat *Create Grid* iz trake s alatima *Vector* > *Research Tools*.

![Create grid](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/1_1_Create%20Grid%20Window.PNG)

*Primjer zadavanja parametara za iscrtavanje linijske mreže meridijana i paralela koja 
obuhvaća šire područje u odnosu na dano područje.*

*(Unos: Grid type: linija, Grid extent: minimalna i maksimalna vrijednost geografske duljine i širine granice područja uvećana za nekoliko sa svake strane granice područja, horizontal/vertical spacing: 
u ovisnosti o mjerilu određena gustoća mreže.)*

**Napomena:** Voditi računa da mreža bude centrirana u odnosu na područje za koje se karta izrađuje (širina obuhvata (*extent*) mreže u odnosu na izračunatu gustoću mreže).

**3. Progušćivanje geometrije**

Meridijani i paralele u ravnini većine kartografskih projekcija nisu ravne već zakrivljene linije. Budući da su okvir područja i kartografska mreža u QGIS-u predstavljeni kao linijski tipovi sa samo dvije lomne točke (početnom i krajnjom), transformacija tih linija u ravninu izabrane kartografske projekcije neće omogućiti prikaz zakrivljenih linija. Stoga je potrebno progustiti geometrije kartografske mreže i okvira područja prije reprojiciranja u odabranu kartografsku projekciju.

Progustiti geometriju dodavanjem lomnih točaka moguće je primjenom alata: *Vector* > *Geometry Tools* > *Densify by count*. Dobivene slojeve potrebno je spremiti u vanjsku datoteku shapefile u koordinatnom sustavu uspravne ekvidistantne cilindrične projekcije (x=λ, y=φ), EPSG: 4326.

![Densify by count](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/Densify%20by%20count.png)

*Primjer dodavanja lomnih točaka okviru*

*(Input layer: sloj granice područja, Vertices to add: proizvoljan)*

![Progusceno rezultat](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/Progusceno.png)

*Prikaz iscrtane šire kartografske mreže s dodanim lomnim točkama*

**4. Reprojiciranje**

Transformacija *On the fly* u koordinatni sustav kartografske projekcije izabrane kao najpovoljnije za prikaz područja može dati uvid u uspješnu realizaciju prethodnih koraka. Međutim, transformacija *On the fly* ne mijenja koordinatni sustav pridružen vektorskim slojevima; ona samo vizualno prilagođava slojeve izabranoj projekciji. Zbog toga je potrebno slojeve progušćene geometrije mreže i okvira područja spremiti u vanjsku datoteku shapefile u koordinatnom sustavu odabrane kartografske projekcije. 

**5. Određivanje pravokutnog unutarnjeg okvira karte u izabranoj kartografskoj projekciji**

Granica područja, koja je prvotno bila pravokutna, može izgubiti taj oblik nakon transformacije u izabranu projekciju. Stoga je važno iz dobivenog oblika odrediti pravokutni okvir koji će predstavljati unutarnji okvir buduće karte. Taj okvir će služiti kao osnovna referenca u kompoziciji elemenata karte, osiguravajući da se svi prikazi i sadržaji unutar karte pravilno uklapaju u zadani prostor.

![Extract layer extent](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/Layer%20extent.png)

*Određivanje pravokutnog unutarnjeg okvira karte.*

Dobiveni okvir potrebno je spremiti u vanjsku datoteku shapefile u koordinatnom sustavu izabrane kartografske projekcije.

**Napomena:** Unutarnji okvir karte možda će biti potrebno dodatno modificirati, ovisno o kompoziciji karte i smještaju izvanokvirnog sadržaja karte. Takva prilagodba omogućit će optimalno raspoređivanje sadržaja karte i osigurati da svi elementi karte budu jasno vidljivi.

**6. Izrezivanje šire mreže meridijana i paralela na unutarnji okvir karte**

Mreža, koja je prekrivala šire područje od zadanog, odrezana je na unutarnji okvir karte. U tom slučaju, sloj unutarnjeg okvira poslužio je kao granica za izrezivanje koordinatne mreže. 

![Rezanje mreže meridijana i paralela](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/Intersection_okvir.png)

*Izrezivanje šire mreže meridijana i paralela na unutarnji okvir karte primjenom naredbe Intersection*

![Parametri za intersection](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/Intersection_alat.png)

*Primjer izbora parametara za presjek slojeva mreže i okvira*

*(Input layer: sloj koji se reže, Overlay layer: sloj po kojem se reže)*

Dobiveni sloj potrebno je spremiti u vanjsku datoteku shapefile u koordinatnom sustavu izabrane kartografske projekcije.

**7. Rezultat vježbi**

Konačan rezultat na ovim vježbama uključuje mrežu meridijana i paralela, kao i pravokutni unutarnji okvir karte. Ti elementi zajedno čine osnovu za daljnje postupke u izradi karte.

![Rezultat vježbi](https://github.com/kkevic/Digitalna-kartografija/blob/main/Sadrzaj/Slike/1_Rezultat%20matematicke%20osnove.png)

*Primjer dobivenog rezultata: unutarnji okvir karte s iscrtanom mrežom meridijana i paralela u odabranoj najpovoljnijoj projekciji*

### Literatura

Frančula, N. (2004): [Kartografske projekcije](https://www.bib.irb.hr/croris-redir/), interna skripta na Geodetskom fakultetu Sveučilišta u Zagrebu
