# FOSS4G.NO 2017

## Postgres fast track
### big data - small computers
Lars Opsahl
NIBIO

The reasons to like postgres:

* great support
    * Both commercial and online
    * Great documentation
    * Good response(compared with oracle metalink for example)
* FLexibility: Can you program it, you can do it in postgres.
* Produce data to clients in the database

### Big data for me may be small data for you

Big data should handle XXXX inserts pr. second?
375
10000
1 mill
20 mill

What is the limit for your system? You should test for performance.

What does 300 000 000 000 decimal numbers mean? 2044. This is the data you'll be finished when your system handles 375 inserts/sec.

Client test tools. Scripts. copy(postgres), cat, split, sed, time... Easy to do, document, test.

### Bad server side setup

PSQL function: Data on CSV files --> Input table --> Final table

Server should use temporary table for input. Remove indexes. From 310 000 inserts to 800 000 inserts/sec. To go further:

Drop foreign key constraints: to 1 200 000.

Use unlogged table: from 1 200 000 to 8 000 000.
Non partitioned table problem. Subtables. Partitioning helps a  lot. Index separate tables. Jump directly to one table.

23 000 000 decimal numbers inserted per second.

### Summing up.
Partitioning on year and month.

Client fixes, server fixes, partitioned using master, performance drop. Partitioned direct tables, removed keys. Scales pretty well.

Can you use data without indexes? Thats why you use partitioning.

Postgres and PostGIS performs very well.

Data on CSV tables --> Final table

Good performance > more possibilties.
300 billion observations in 3 hours. With this possibility, we can upload relevant data on demand, without too much disk space.

Partition data based on geometry. Achieve the same as with year and month.  Problems: Simple feature problems: Distribute borders, same data, same points, in different tables. Postgis topology achieves the solution to this: Scattered data with partitioned tables, get the performance. The real problem is, again, disk space.


## "QGIS - og beregning av overvann m. m."

Jobber for NORKART. Analyser på FME og QGIS. Beregnet overvann for kommuner.

På kartet ser vi flomsonene. Hvor vannet renner. Vannansamlinger. Sårbare bygg. Det er overvann i denne sammenhengen.

Beregnet for 2100 hvordan kommunen ser ut med +3 meter.

http://drift.kortinfo.net/Map.aspx?Site=Middelfart&Page=Borgerside
Brukes som aktsomhetskart, på kommuneplannivå.

NVE flomsone WMS.
Overflatemodell kartverket WMS. Egentlig en fjellskyggemodell med bygninger og vegetasjon.
NVE årsnedbør.

Hva finnes av laserdata?  http://høydata.no laserinnsyn.

Når vi laster ned laserdata fra nettet, må vi inkorporere byggdata. Løfte terrengmodellen i 3d, der vi har byggmodellen. De er flatt 10meter. Dermed går ikke vannveiene gjennom bygninger.

QA: Hvor gamle er data? Spriker datoene for mye?

Bruker fill sinks på digital overflatemodell for å beregne hvor vannansamlinger skjer. Filtrerer på størrelse på område. Fargelegger etter dybde.

Hvor stort er volumet i vannansamlingene, og dermed hvor mye vann, hvor lang tid det tar å ansamle. Får et relativt tidsperspektiv med i beregningene

SAGA-modul



Midlertidig aktsomhetskart. Vise en mulig trussel.



## Jørgen Lundquist - Trikken Oslo

Kjører trikk.

Ruter har en åpen data API. Gjør anrop, får tilbake som json.  Når trikken skal komme og når den skal gå. Trafikklederne har inngang rett inn i datasystemene. Som fører er man bare interessert i når trikken en selv skal ha kommer.

Laget et web-basert verktøy.

Når trikken må vente pga kjøring på enkeltspor, bruker man sikringsvakt. Hvem slippes igjennom. Da bruker de mitt verktøy.

Laget verktøy for førere som laster over sine vakter rett over i Google kalender. Førere kan planlegge bedre, se når de har fri.

Veien videre: Google har et åpent API. Kan man koble ruter med det?

Takk.

## Verktøy og løsninger for effektiv tilgang og analyse av oseanografiske data

Morten Hansen - Nansen Senter

Geo-SPaaS muliggjør raskere utvikling og testing av vitenskapelige algoritmer, som kan bli operasjonell i server-systemer. Nansen Cloud tilbyr forskere verktøy og data i skyen som kan bli tilbudt via NetCDE API

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

Relatert til åpne data. Kroneksempelet er OpenStreetMap. Begynner å bli veldig bra. En rekke kilder inn. Tracker med GPS. Tracer satelittbilder. ESRI, Bing, Mapbox. Legger inn åpningstider osv. Mikser inn offentlige geografiske data. Jobber med å få inn N50-data, allerede lagt inn adressedataene. Dataene her har en åpen lisens

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
NOFA: Store: PostGIS. Process: PostGIS, R, GrassGIS, Python.
Publishing: R, shiny, QGIS, Lizmap   --> web

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
