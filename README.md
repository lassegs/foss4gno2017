# FOSS4G.NO 2017

![](http://i.imgur.com/jn1lNlX.jpg)

## Postgres fast track
### big data - small computers
Lars Opsahl
Norsk Institutt for Bioøkonomi

The reasons to like PostgreSQL

Great support
    * Both commercial and online
    * Great documentation
    * Good response(compared with oracle metalink for example)
* Flexibility: Can you program it, you can do it in postgres.
* Produce data to clients in the database

### Big data for me may be small data for you

![](http://i.imgur.com/3s8ZAm8.jpg)

Big data should handle XXXX inserts pr. second?
375?
10000?
1 mill?
20 mill?

What is the limit for your system? You should test for performance.

What does 300 000 000 000 decimal numbers mean? 2044. This is the data you'll be finished when your system handles 375 inserts/sec.

Client test tools. Scripts. copy(postgres), cat, split, sed, time... Easy to do, document, test.

### Bad server side setup

PSQL function: Data on CSV files --> Input table --> Final table

Server should use temporary table for input. Remove indexes. From 310 000 inserts to 800 000 inserts/sec. To go further:

Drop foreign key constraints: to 1 200 000.

Use unlogged table: from 1 200 000 to 8 000 000.

Non partitioned table problem. Subtables. Partitioning helps a  lot. Index data into separate tables. Jump directly to tables in queries.

23 000 000 decimal numbers inserted per second.

![](http://i.imgur.com/nadMKDs.jpg)

### Summing up.
Partitioned data on year and month.

Client fixes, server fixes, partitioned using master, performance drop. Partitioned direct tables, removed keys. Scales pretty well.

Can you use data without indexes? Thats why you use partitioning.

Postgres and PostGIS performs very well.

Data on CSV tables --> Final table

Good performance > more possibilties.
300 billion observations in 3 hours. With this possibility, we can upload relevant data on demand, without too much disk space.

Partition data based on geometry. Achieve the same as with year and month.  Problems: Simple feature problems: Distribute borders, same data, same points, in different tables. Postgis topology achieves the solution to this: Scattered data with partitioned tables, get the performance. The real problem is, again, disk space.

This kind of throughput eats SSDs.


![](http://i.imgur.com/AGFBDml.jpg)

## "QGIS - og beregning av overvann m. m."

Jobber for NORKART. Analyser på FME og QGIS. Beregnet overvann for kommuner.

På kartet ser vi flomsonene. Hvor vannet renner. Vannansamlinger. Sårbare bygg. Det er overvann i denne sammenhengen.

Beregnet for 2100 hvordan kommunen ser ut med +3 meter.

http://drift.kortinfo.net/Map.aspx?Site=Middelfart&Page=Borgerside
Brukes som aktsomhetskart, på kommuneplannivå.

NVE flomsone WMS.
Overflatemodell kartverket WMS. Egentlig en fjellskyggemodell med bygninger og vegetasjon.
NVE årsnedbør.


![](http://i.imgur.com/Rx7FoAa.jpg)

Hva finnes av laserdata?  http://høydata.no laserinnsyn.

Når vi laster ned laserdata fra nettet, må vi inkorporere byggdata. Løfte terrengmodellen i 3d, der vi har byggmodellen. De er flatt 10meter. Dermed går ikke vannveiene gjennom bygninger.

QA: Hvor gamle er data? Spriker datoene for mye?

Bruker fill sinks på digital overflatemodell for å beregne hvor vannansamlinger skjer. Filtrerer på størrelse på område. Fargelegger etter dybde.

Hvor stort er volumet i vannansamlingene, og dermed hvor mye vann, hvor lang tid det tar å ansamle. Får et relativt tidsperspektiv med i beregningene

SAGA-modul

Midlertidig aktsomhetskart. Vise en mulig trussel.



## Jørgen Lundquist - Trikken Oslo

Kjører trikk.

Ruter har en åpen data API. Gjør anrop, får tilbake data som  json.  Når trikken skal komme og når den skal gå. Trafikklederne har inngang rett inn i datasystemene. Som fører er man noen ganger bare interessert i når trikken en selv skal ha kommer.

Laget et web-basert verktøy for å se trikketider på mer tekniske måter, som passer for de ansatte i trikken.

Når trikken må vente pga kjøring på enkeltspor, bruker man sikringsvakt. Hvem slippes igjennom. Da bruker de mitt verktøy.

Laget verktøy for førere som laster over sine vakter rett over i Google kalender. Førere kan planlegge bedre, se når de har fri.

Veien videre: Google har et åpent API. Kan man koble ruter med det?

Takk.

## Verktøy og løsninger for effektiv tilgang og analyse av oseanografiske data

Morten Hansen - Nansen Senter

Geo-SPaaS muliggjør raskere utvikling og testing av vitenskapelige algoritmer, som kan bli operasjonell i server-systemer. Nansen Cloud tilbyr forskere verktøy og data i skyen som kan bli tilbudt via NetCDE API.

![](http://i.imgur.com/oIcOvEQ.jpg)
### New opportunities with Open Data and Standards

Policy change - publicly funded data is free and openly avaliable
New Standards

  * OpenDAP - Allows data streaming, thus "access to pixels instead of images"
  * INSPIRE, NetCDF-cf, NASA DIF, NASA GCMD keywords, etc.

Nansat is a scientist friendly Python toolbox for processing 2d satellite Earth observation data.

Django-Geo-SPaaS - a GeoDjango app for satellite data management.

### Geo-SPaaS Virtual Machines

Standardized virtual machines configured for given usage - e.g., in projects.
Vagrant configuration describes all software requirements, packages, operating system configuration, etc.

  * Works on Mac, Linux and Windows ++
  * Works on your local system with the tools you're familiar with - easily code in your fav text editor.

Standard configuration:
 * Python /IPython
 * NumPy
 * SciPy
 * GDAL
 * Nansat
 * Django-Geo-SPaaS

Nansat defines what a given variable is. GDAL and Nansat coupled gives clear knowledge about what the data is.

### Getting started

1. Open a terminal
2. git clone https://github.com/nansencenter/geo-spaas-vagrant
    * Contains vagrantfile with configs for local virtual machines.
3. vagrant up vm-name and vagrant provision vm-name

ESA GlobCurrent retrieving surface currents from satellites. Jupyter notebook example.|

### Summary and way forward
Challenges

* The amount of available data from satellites, in-situ measurements and models is big and increasing.
* Data storage is distributed - "moving processing to the data" is not straight forward.

The Geo-scientific platform as a service shall allow
 * EAsy access to distributed (external/independent) data catalogues.
 * Scientist oriented software tools for data analysi
 * Distributed data storage and access (Geo-SPaaS nodes)

Next step: An API connecting the nodes - to allow common access and data in a cloud.


## Barents Sea Marine Atlas

Endre Moen
Norsk Marint Datasenter - Havforskningsinstituttet

Cirka 700 ansatte.

BarMar inneholder data om fisk. Oseanografiske data. Aggregerte data, basert på rådata fra forskningstokt og fiskeri. Blir presentert i et rutenett på 25x25 km.

Brukere kan filtrere fisk lengde- og alders-intervaller, eller kjønn.

Hvor kommer dataene fra? Data-fangst fra forskningstokt og fiskeri fra Norge og Russland. Analyse av forskere, med gridding, aggregering, en slags interpolering. VIsualisering, aggregering på nytt. BarMar. Tilsammen blir det oversikt over økosystemene i barentshavet.

BarMar kan legges oppå hverandre. Sender spørring til GeoServer, lager SQL-spørring til PostGIS DB, får data tilbake, gjør til WMS, som sendes til klient.

På sikt er det et mål at våre data skal være tilgjengelig for nedlasting.
BarMar skal være brukervennlig og ikke gå på for detaljert nivå.

barmar.nodc.no/BarMar/barmar.html

### Veien videre
Laste ned datagrunnlag for kartene.
Flere datasett: Sild, makrell, blåkveite og saltholdighet, temperatur.

Bra på å svare på romlige spørsmål
Ikke bra på å svare på ikke-romlige spørsmål.

sjømil: http://www.imr.no/sjomil/index.html


BarMar
Laget med OpenLayers 3, Java, GeoServer og PostGIS.



## Utvikling med Open Source GIS i Statens Vegvesen

Thomas Levin - Statens Vegvesen

Noen tanker fra en FoU seksjon.

Kobling mellom geodata og trafikkflyt. Svært proprietær etat. Betalt utvikling hos leverandører, proprietære formater etc.. Begynt å ta tak i det, frigjør data.

### Utfordringer på lang sikringsvakt

Hovedmål
* Framkommelighet og regional utvikling
* Trafikksikkerhet
* Miljø
* Universell utforming

Blir målt og skal bli bedre. Håndtere større samfunnsendring og se konturene av selvkjørende kjøretøy og det grønne skiftet.

Fokus i dag ligger på miljøbetraktninger.

### Svare på enkle spørsmål

Hvor mye diesel bruker jeg over fjellet til Oslo
(produksjon i distriktene)

Det er sammenfall mellom miljø og bedriftsøkonomi for næringstransporten.
 - 1 kilo NOx, gir ingen mening, mens 1 liter diesel gjør det.
 - Det finnes mye data om transportene på vegene i Norge
 - EU-systemet produserer mye bra data i "papirform". Utslippsfaktorer f. x. Excelark, kolonner endrer seg, hver gang de oppdaterer.
 - SVV har en unik database med fagdata som er "flytende"

https://www.vegvesen.no/vegkart/vegkart - enkelt å bruker

NVDB har all fagdata.  Ruteberegning + offentlig API

EEA Guide book PDF + Excel . Bygger pythonkode, åpent bibliotek, for å interpolere dataene og gi ut i "flytende" form.
Legge inn data om kjøretøy, fra, til, last.
Inn i beregning, summerer til slutt.

Målet er at industrien og aktørene som kan gjøre endringene får dataen inn i seg. De skal inn i fagsystemene til aktørene. De som bygger flåtesystemer skal kunne gjøre utslippsberegninger på en planlagt transport.




### En oppskrift på lave kostnad
Om vi regner investering i kunnskap som nyttig.
Absolutt laveste kostnad er QGIS. Først må folk lære seg å bruke QGIS. Et entrypunkt. Begynner her.
Fagdata fra NVDB.
Ruteplanlegger.
Python som flufferkode.

### QGIS modul ble svaret

Trykke inn punkter i kartet. Så må man vente litt. Ruteforslag genereres av v ruteplan-tjeneste, sparer brukere fra å ha lokale vegnett.

![](http://i.imgur.com/NTOfCOG.jpg)


Gir tilbake ruteforslag: Laga sånn at de skal være ganske forskjellige, små avvik gir ikke forskjellige alternativer. Strategivalg: Hvilket dalføre.
Tast inn biltype og hvilke komponenter du vil beregne, og om du vil ha segment for segment, eller hele kurver.

Målet etterhvert er å berike de lagene du får med enda flere data fra NVDB.

Vi kjører open source utvikling!

https://github.com/NPRA/RoadEmissionCalculator

Vi har prosesser på gang for å videreutvikle våre backend tjenester til å gi et enda bedre grunnlag for utslippsberegninger.

Når vi bruker data finner vi også feil - det er en bra ting.

Hovedkilde:

www.vegvesen.no/data
https://github.com/LtGlahn
https://github.com/NPRA

Sysler også med open hardware og gjør bremsetester på blåis.



## Geoforum
Interesseorganisasjon for alle som jobber med geomatikk. Synliggjøring av geomatikere. Kompetanseheving blant medlemmer. Fagpolitisk virksomhet.  Inviteres til stortinget, ift. digital agenda. Cirka 2000 medlemmer. Medlemsfordeler er rabatter på kurs og konferanser, pluss stipender.


## Det åpne geodata-økosystemet

Atle Frenvik Sveen

Basert på en artikkel. http://www.kartogplan.no/Artikler/KP2-2017/Det%20aapne%20geodata%20oekosystemet.pdf

### Hva er åpne data?
Åpen lisens
tilgjengelig - kan godt ta betalt for å levere dataen.
Maskinlesbart - papirutskrift ikke lov.
Åpent format - minst ett open source bibliotek for å lese og behandle

### Farer?
* Tolkning - Mine data, fagdata, trenger ekspertise for å tolke. Veiledere
* Ondsinnet distribusjon - modifiserer dataen av idioti og onde hensikter og får feil data i omløp.
* Selektivitet - åpne enkelte deler av data for å fremme en sak.

Alle data kan ha feil og har bias osv.

### Åpne Geodata
Nei, ikke selskapet.

Åpne geodata er et subset av åpne data.

Is spatial special? Ja. Egne miljøer, forskjellig lovgivning, og forskjellige formater. Noen av disse tingene gjør det spesielt.

Vi har data.norge.no og data.kartverket.no. Vi liker å tro at vi er spesielle.

### Data fra det offentlige
32 - 174 millioner i mulig verdiskapning?

Global Open Data index er et prosjket som tracker status på åpning av data over hele verden. 4 av 15 kategorier er geografiske data.

Norge er helt grønt selvom FKB ikke er åpent.

To hovedbeveggrunner for å åpne data:

Kapitalistisk: Ved å åpne data åpner vi for verdiskapning
Sosialistisk: Ved å åpne data åpner vi regjering, styring, transparancy.

I USA er det den sosialistiske argumentasjonen som vektlegges.
I Europa er det den kapitalistiske beveggrunnen som er viktig.

### Innovation at gunpoint

> "Nå er det en måned siden Kartverket slapp gratisdata, hvor er resultatene?"
> Thomas Nrodtvedt, FAD (fritt etter hukommelsen)

> "Det å forvente at det sitter en haug nerder og hopper når staten sier "Hopp", som hiver seg over de nye dataene, er utopisk".
> Atle Frenvik Sveen

Kartverket er flinke. Hack4.no for eksempel er kjempebra. Fornuftig og må gjøres mer av.

### VGI

Relatert til åpne data. Kroneksempelet er OpenStreetMap. Begynner å bli veldig bra. En rekke kilder inn. Tracker med GPS. Tracer satellittbilder. ESRI, Bing, Mapbox. Legger inn åpningstider osv. Mikser inn offentlige geografiske data. Jobber med å få inn N50-data, allerede lagt inn adressedataene. Dataene her har en åpen lisens

Hva skjer når det skjer endringer i de offentlige dataene? Hvordan tracker du det? Vet ikke, finn ut og bli rik.

Kartverket rett i kartet-tjenesten har cirka det samme.

### Symbiose

En samvirkning mellom VGI og offentlige data. Eksempel fra NY som føllger med på alle endringer i OpenStreetMap. Når det har skjedd endringer i OSM, sendes det en mail til offentlig etat for å endre sine datasett.

### FOSS(4G)

Same same, but different.

RMS: Kode skal være åpent, ellers er det malware.

Ikke alle data bør være åpent, pga personvern og sånn. Men mye av inspirasjonen er hentet fra friprogbevegelsen. Kanskje open data er mer som open source.


### Hacker cartography

Bruker OS-verktøy med åpne data for å lage og bearbeide crowdsourced, vgi osv.

Mapnik er et godt eksempel. En kartrenderer. Laget for OpenStreetMap, men nå tatt av generelt.

Google, Microsoft, Facebook er blant de største bidragsyterne til friprog.

Samme for VGI. Mapbox har et stort team av folk som forbedrer OpenStreetMap.


### Fremtiden?

Profesjonallisering av de som publiserer sine data. Det å legge til rette for bruk av dataene, være til stede, ha tutorials, forklare hvordan det brukes.

Mer åpenhet, fanden vil ha fler. Flere data i det åpne.

Større krav fra brukere om regelmessige oppdateringsfrekvenser. Klarere lisenser (OpenStreetMap fra CC til ODbL).


## From the field to web and reports. Efficient data flows with QGIS and PostGIS.

Jakob Misch
http://nina.no/

### NOFA - Nordic Freshwater Atlas
* Data infrastructure for Freshwater species.
    * Collection
    * Analysis
    * Preservation
    * Presentation
    * Publication
* Long terminal
* Workflow efficient.

Everything open source from OSGeo projects. OSGeo projects are stable, and there in 5 years.

Input: QGIS, Lizmap, BASH, python.
NOFA: Store: PostGIS ( fish occurences, environmental factors). Process: PostGIS, R, GrassGIS, Python.
Publishing: R, shiny, QGIS, Lizmap   --> web
Share: QGIS, R, Python

### Darwin core
International standard for species occurrence data. Data structure. Defined terms. Controlled vocabulary. Metadata.

Researchers from all over the world collaborate with this.

A schema i Postgresql:
1. Location Location type, waterbody, county, municipality, elevation, geometry, ...
2. Event: location, remarks, recorded by, date, reliability, dataset, ...
3. Occurence: event, species, remarks, ....

### Additional data
Lakes 1.5 million in Norway, Swedn and Finland.
Catchments: 270 000 largest lakes.  Grass GIS is a powerfull, although resource hungry operation. Where the water comes from.
Rivers
Streets
Land cover
Climate
Terrain models
Administrative units

All are available in the system

### Visualisation and print plugins
QGIS plugin

Another option is QGIS server, Lizmap WMS, WFS.

R shiny, web applications using the R programming language.
https://shiny.vm.ntnu.no/users/andersfi/invafish/

### Insert and edit data
* Field data collection:
* QField (Android) - QGIS with less functions and another UI
* QGIS (Windows tablet) - full version
* IntraMaps Roam (Windows Tablet) - QGIS based.
* Lizmap (Web browser)
* OpenDataKit
* GeoShapes - Full platform with client and server
* ...

### Desktop: QGIS plugins
Motivation:

 * QGIS - PostGIS Layer
 * Scripts

Standard installation, with map canvas interaction. It's not released yet.

### Lizmap

http://tinyurl.com/Insertfish
Autmatically inserted into the postgres database.

### Analyze data

PostGIS processing. Most GIS functionality can be done directly in the database. Very fast, easy for the user. Postgres supports python as well as SQL.Create triggers, quality checks,

Also to calculate the distance to the closest road. How likely is it that humans tamper with the lake or not. Important for biologists. How close are different occurences? Linear in Postgres, river routing with pgRouting.

Server side

### R - Programming language
Predefined functions - process on the Server
Download data "views" - by species, by event.



## Copernicus-programmet og åpenhet

Anja Strømme - Norsk Romsenter

Om satellittdata og bruk i GIS-applikasjoner. Ny datakilde, satellittbilder er ikke nytt, åpenheten er det. Hvordan ser vi for oss dette blir brukt.

### Norsk Romsenter
Under næringsdepartementet. Forvalter norske rominteresser, også i ESA. Strategisk rådgiver og utreder for norsk forvaltning i romrelaterte saker. 40 ansatte på Skøyen i Oslo. Budsjett ca en milliard.

Hvorfor er rommet viktig for Norge? Vi ligger langt nord. Mange satellitter går i polare baner, og dekker Norge dermed veldig godt. Norge er et stort land og forvalter enorme havområder. Vi har ansvar for sikkerhet, is, search and rescue, fisk osv. Å bruke satellitter til den store overvåkinga, sende ut folk der det trengs. Vi har store behov, og er derfor også veldig store brukere av satellitter.

Vi har noen norske satellitter
AISSat-1 2010
AISSat-2 2014

Det ligger informasjon i disse dataene som har større bruksområde enn det som opprinnelig er tenkt.


### ESA JO program siden 70-tallet.
ESA Earth Observation Programme. Vi betaler kontingent og er med å bestemme hva de skal gjøre.

De meteorologiske innerst. Så er det Earth Explorers, til forskning. Copernicus-programmet tar suksessene herfra og skyter opp nye generasjoner med disse. Da kan vi begynne å planlegge ordentlig hva vi vil gjøre, fordi de er ikke bare 6 år og så faller ned, men vil være der operasjonelt over tid.

### Copernicus fra forskning til forvaltning.

Europes eye on earth.

* Dedikerte sentinel satellitter
* Tilgang til data fra andre satellitter
* Data fra bakken/droner/fly (in situ komponenten)
* 6 tjeenster

Vi er på vei inn i en ny tidsregning hvor langvarige, kontinuerlige, åplitelige og uniforme jordobservajsons dataserier vil øke og føre til en stor oppgang i produkter og tjenester.

Åpne data er sosialisme og kapitalisme. ja takk, begge deler. Det er ekstremt mye det kan brukes til. Vi trenger de dyktige innovatørene for å drive sosialismen videre og vica versa.

Volume of user downloads: 27.12 petabyte.

Sentinel 1 - SAR imaging. Radar. 100 minutter rundt jorda, 45 minutter fra hverandre. Weather, day night, interferometry
Sentinel 2 - Multi-spectral imaging. Land applications: urban, forest, agriculture.
Sentinel 3 - ocean and global land monitoring. Wide swatch ocean color, vegetation, sea/land surface temperature, altimetry
Sentinel 4 - Geostationary atmospheric

Sentinel-1 5x20 m hver 6 (1.-2.) dag. Radarbilder over hav og land. Ser endringer i ruhet på hav og land. Værfronter i hvor regnet har trykket ned havet. Kan brukes over land også. Snøtemperatur, hvor store snøkorn er, vanninnholdet. Blir det flom i år, hvordan skal vi forvalte vannmagasinene etc.

satellittbilder viser flomområder og kan se om veier står under vann.

Snøskred kan sees med Sentinel-1, siden snø som har ramla har annen ruhet. Search and rescue. Overvåking av rimfrost før snøskredkartlegging. Vi er ikke helt der ennå, men vi jobber mot det.


![](http://i.imgur.com/oY59Ieb.jpg)

Isen på Grønland i bevegelse måles.

Norwegian centre for deformation mapping (2016 ->)
Bruker infromasjon fra fasen i signal for å se om bakken har flyttet seg med millimeter. Operational + nationwide. Kommer til å legge ut dette for alle som frie og åpne data. Jordskred

Visualisering av setning og feil i jernbanen. Kan bestemme hvor man skal dra og fikse før det skjer feil.

Setning generelt er interessant for forsikringsbransjen.

### Sentinel 2 optisk satellitt.

KAn brukes til beskyttede områder, biodiversitet, land cover, skog helse, avskoging. Klima relatert endring i vegetasjon og isbreer. Innsjøer og elver. Pollenvarsel.

Har 12 farger. Kan kombinere bånd for å få forskjellige visualiseringer.

### https://satellittdata.no Den nye portalen for Copernicus data
Du gjør hva du vil med de dataene. Tjen penger, redd verden.

Bygger opp en nasjonal infrastruktur. Tilbyr data fra hele verden, som ferskvare.

200 terrabyte skiftes ut hver uke.

 satellittbilder fra Sentinel 2 over Norge hver femte dag. Mye skyer da.


### DHuS portalen

Bruker SAFE. Snap toolbox kan brukes. Kan lett hentes inn i QGIS

https://colhub.met.no  

NetCDF file format to ensure easier access to smaller dataset and added search functionality such as: area, band (sentinel 2), time, etc. Onthefly conversion to toher file formats and grids (GeoTIFF etc..). Enhanced scripting capabiliteis such as subscription and push. Tools for time-series and change detection. Later... Processing on demand "sandbox". Inclusion of future sentinels.

Innovasjon Norge call:
http://www.innovasjonnorge.no/satellittdata innen 15. september

### Kom på Hack4No i oktober
Vi er der, kommer for å hjelpe folk med å bruke satellittdata

## Hvor går grensen?

Alexander Salveson Nossum

Bordergo. Et prosjekt som kartverket kjører der Norkart er konsulenter og utviklerteam.

Problemstilling:
 * Eva og Erlend lurer på hvem som eier epletreet.
 * Lars landmåler skal måle opp eiendommer.

Er dette noe problem da? "Rev halve naboens uthus" Kan bli et problem, særlig når styrelederen kapper et hus i to.

Matrikkel - matrikkel m. (senlat. matricula "liste", diminutiv av matrix "livmor, grunnstamme") offentlig register over grunneiendommer.

Derfor ønsker Kartverket å se på nye metoder og utnytte ny teknologi for å løse dette.

Augmented reality - Google Tango. Se inn i fremtiden, utvikle en prototyp basert på AR på Tango-teknologien. Det sensasjonelle i den er en god del sensorer som ikke vanlig iPhones har. Den har dybdesensor, som en slags lasermåler, men optisk sensor. Du får punktskyer ut av den. Enklere å plassere virtuelle objekter inn i den ekte verden.

![](http://i.imgur.com/pFcz4F2.jpg)

Dette er fremtiden. Kan tas videre til landmålere i fremtiden som går rundt uten GPS-stang og går .

Video fra i dag tidlig i byen. Fungerer ganske bra.

Alt er ikke så enkelt. Drifting, at modellen beveger seg i rommet. Plassering i verdenskoordinater. Vi har geografiske koordinater, projisert. I AR har du AR-koordinatsystemet. GPS-nøyaktigheten er ganske dårlig i mobile enheter som er i dag. Høydemodell, man må ha en god høydemodell inn. Her har vi støtt på et reelt problem relatert til lukkede data. Laserpunktene er publisert. Men de dataene vi trengte var ikke åpne. Så vi måtte lage en annen tjeneste som konverterte de åpne dataene til data vi trengte.


Men vi fikser det meste. Rune Aasgard er en av de virkelig gode matteekspertene våre. Lagde en metode for å konvertere tango/AR-koordinater til UTM33N.

GPS-nøyaktighet er vanskelig å fikse. => Støtte for ekstern GPS. Mismatch mellom AR og GPSen i mobile enheter. Løst litt, ikke alt.

*Open sources i oktober på #HACK4NO*

Essensen i open source:

> If I have seen further than others, it is by standing upon the shoulders of giants. - Newton

### What's next?

> ...and, overnight, hundreds of millions of devices...

Apple kom på banen og lanserte sin egen sak. ARKit. Google legger ned Tango og starter ARCore 29. august. Dette kan komme til hundrevis av millioner av enheter.

Microsoft HoloLens og se på katter som flyr i rommet.

FOSS4G-NOR: The G in FOSS4G. Her ser vi nytten av fagfeltet vårt. Skjer mye fra gigantene. De dundrer inn på vårt fagfelt. Men helt motsatt egentlig. Det er vi som klarer å bringe inn de gode metodene inn i deres felt. Geodesi, projeksjonsformler, matematikken i dette, tas inn av de store. Geospatial er minst like viktig framover som det var i går.


## It's all about time series observations!

Massimiliano Cannata - Istituto science della Terra

I'm going to talk about a software that has been developed for many years in the southern part of Switzerland. Its for managing time series.

istSOS

![](http://i.imgur.com/DGa6KIa.jpg)
### Why do we need to monitor?
Better understand what is the reality and take better decisions. In our case everything started with working with civil protection, with a city close to a lake that flooded time after time. Together with the civil protection we built a system to produce almost in real time flooding maps, and forecasts for the next 6 to 12 hours.

Flooding is not instantanious, so we can predict.
This is a key aspect for wise decisions. Understand the situtation and timely react.
Completeness -> quality --> Availability --> Timeliness.

Simple, open, standard, powerful. Had experiences with proprietary software, stuck in lock in.

Watersheds can be international. We wanted to go standard, to make everything interoperable and interchangable.

istSOS is the software: http://www.istsos.org/
In the incubation process of OSGeo.

### Open architecture
Based on the principle of a Service Oriented Architecture (SOA) and the specification of Open Geospatial Consortium Sensor Web Enablement (OGC-SWE) initative

SOS user types and sequence. Data consumer can explore the data with GetCapabilites request, get info about the possibilites, the types of data etc. When you understand the data, you can do a DescribeSensor request, to find out what kind of sensor you are looking at. At the end you can perform an GetObservation request, when you want to access the data. You can perform filtering: give me all the data from the last 3 days. OR give me all the data for THIS area for precipitation.


istSOS service: istsoslib - database wherehouse  - configuration
Wa-service: walib
Interaction: Restful json - wainterface - SOS v1.0 XML.

With istSOS you get the standard and some extended features. We found out that the standard was not enough to manage the timeseries, so we added features.  

Authentication and authorization.

Data aggregation on the fly.

Time zone support, different coordniate systems, different time zones: ask in preferred time zones etc.

 Native quality index, everytime you store data, you have an associated quality index - tests to pass to get a higher quality score - both realtime and post-processing.

 mqtt integrated support - light and reliable - sends data from sensor to a data broker, and further to the data store.  

 Virtual procedure is some sensor for the user that really doesnt exist, but is based on predictions from other sensors.

 JSON, CSV formats for talking to multiple applications.

 GUI for asking and working with the data.

 Notification service.

 Widgets API so you can use this API to build javascript application in Android etc.

 In-situ fixed points and in-situ mobile points.

### Can you trust istSOS?

Configuration for service for Canton Ticino HydroMEt

* 549 registered stations
* 122 gb of data served
* 75 Mio served requests in 1 year
* 1 internal server error response (500)

Developed for 7 years.

![](http://i.imgur.com/KMqAxCF.jpg)

### Bottlenecks
getCapabilites vs big number of sensors.
Big concurrent users (>1000) vs server time-out
Very high frequency data vs Database insertion time.

## FOSS4G Boston oppsummering

Atle Frenvik Sveen


Den internasjonale konferansen går verden rundt. FOSS4G er den ledende teknologikonferansen for fagfeltet. Det er som å komme hjem. Gikk over 3 dager, 7 parallelle tracks, og workshops to dager før.

1100 deltakere. Norge på nummer 5, delt 4. plass med tyskland.

Paul Ramsay - PostGIS. The economics of open source. De tre økonomiene i spill. Oppmerksomhetsøkonomien. Pengeøkonomien. Gaveøkonomien. Hvordan samvirker de? Skjebnen til de små grunnleggende åpen kildekodebibliotekene vi bruker: GDAL, proj4 etc. De vedlikeholdes av kanskje en eller to personer. Her bør det gjøres noe. Ligner på Heartbleed i OpenSSL og Google/Faceboo.

![](http://i.imgur.com/1bnziut.jpg)

AI var stor trend om dagen. Eksperimentelt, får til noe, lovende resultater, ikke produksjonsklart.

Vektortiles. Begynner å modnes. Vi har tatt det ibruk. Erfaringer. T-rex, middleware for å generere vektortiles. Gjør det selv i node.
Native støtte for vektortiles i PostGIS.

Cesium og webnative med 3dtiles osv.

Sky og serverless. Rasterprosessering i lambda osv.

Richard Stallman, gud og far, leverte et show uten like. Det dreier seg ikke bare om fred frihet og alt gratis. Det er også en ideologi.  FOSS4G er mer businessorientert. Teknologikonferanse mer enn friprogkonferanse.

Fake maps: Hvordan kan du misbruke kart.

Litt sosialt: Gala-eventen var på akvariumet i Boston. Med PINGVINER!
