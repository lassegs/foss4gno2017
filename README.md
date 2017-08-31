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
