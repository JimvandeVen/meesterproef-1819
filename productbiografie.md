# Product Biografie

![dashboard](./img/dashboard.png)

## Inhoud
- [Inleding](#inleiding)
- [Week I](#week-i)
- [Week II](#week-ii)
- [Week III](#Week-iii)
- [Week IV](#Week-iv)
- [Week V](#Week-v)
- [Leerdoelen](#leerdoelen)
- [Mijn rubric](#mijn-rubric)

## Inleiding

In dit document, de productbiografie, ga ik per week door het project heen. Ik zal elke week een korte beschrijving geven van wat we hebben gedaan. Met daarbij de verschillende schetsen, itteraties en uitwerkingen. Aan deze onderdelen zijn features verbonden die ik naast een aantal leerdoelen zal leggen. Per feature/leerdoel zal ik kijken welke rubric erbij past en dit onderbouwen.

## Week I
*27-5*

- Briefing Project
- Onderzoek huidige situatie en prioriteiten
- Onderzoek huidige tech stack

In deze week hebben wij ons plan om het platform te herontwerpen bij de opdrachtgever neergelegd in een presentatie met onze bevindingen.
Hierop kregen wij een positieve reactie van de klant.
De klant komt zelf meer van de technische kant en heeft zelf geen goed beeld van wat UX is en door deze meeting werd de waarde daarvan duidelijker en stemde hij in met het alternatieve plan.

Deze week zijn wij bezig gegaan samen met de UX-ers om onderzoek te doen naar het ALICE project en hoe het platform daar in past.

Marcel en ik zijn ook bezig geweest met het uitzoeken van de tech stack die de ICT-ers gekozen hadden voor de front-end van het platform.
Met het onderzoek merkte wij dat het voor ons een moeilijke stack zou zijn om op verder te werken door de keuze van talen en frameworks.
Door deze conclusie hebben wij besloten een eigen proof of concept demo te maken met onze eigen stack en zijn gaan uitzoeken wat hiervoor het beste was.

- opdracht
- onze oplossing
- features
- leerdoelen per feature
- rubric per feature
- uitleg per rubric

## Week II
*03-06*

- Onderzoek Alice project shifters
- Eerste iteratie tech stack
- Eerste demo pagina's
- Heroverweging eerste stack
- Keuze design system(Material design)


Deze week stond ook nog in het thema van onderzoek doen. We hebben contact gezocht met zoveel mogelijk mensen die bij CERN hebben gewerkt aan het ALICE project via linkedin en ander platformen om zo zoveel mogelijk gebruikers input mee te kunnen nemen.
Ook werden deze week de eerste wireframes opgeleverd door de UX-designers en zijn wij begonnen met het opzetten van een tech stack

#### Eerste stack
De eerste stack die wij samengesteld hebben bestond uit:

##### Server
- Node js with Express framework
	- Multer
	- body-parser
- Sessions
- Templating engine (hbs)
- Websockets socket io

##### Client
- Websockets (socket io)
- D3
- Material design

We hebben deze keuze gemaakt omdat het bestond uit voor ons bekende packages en frameworks.
Voor de server hadden we een basic express server met handlebars als templating engine en websockets voor realstime data distributie naar de Client.

Op de client hadden wij websockets voor het verwerken van realtime data en D3 voor het visualiseren van data op het dashboard.

Na overleg met onze UX-designers hebben wij besloten Material design te gebruiken als design system binnen het platform. Deze keuze is tot stand gekomen door de aard van het project. Het jiskefet project is een project dat een wisselende samenstelling heeft van teams die er aan werken, voornamelijk bestaand uit ICT studenten. Door de wisselende opstelling binnen het project is het wel belangrijk dat er consistentie en houvast is met een duidelijke documentatie voor de volgende teams.
Het zelf bouwen van een design system viel niet binnen onze scope van het project en daardoor hebben wij gekeken naar een bestaand design system met goede documentatie dat herkenbaar is voor gebruikers.
Ook is visuele identiteit niet heel belangrijk binnen dit platform, maar usabillity en herkenbaarheid is wel een belangrijke factor.


Na het uitwerken van het eerste prototype voor het project merkte wij dat deze stack misschien niet de beste keuze was voor het platform dat wij willen bouwen.
Dit lag eraan dat de flow van data etc. binnen handlebars en het schrijven van helper functies vrij omslachtig was voor de schaal van het project en hebben wij besloten om de volgende week de stack opnieuw door te denken.

## Week III
*10-06*

- Evaluatie eerste wireframes
- Onderzoek nieuwe Stack
- Keuze nieuwe Stack
- Uitwerken proof of concept demo

In deze week kwamen er meer designs en wireframes binnen van onze UX-designers om uit te werken.

Na de conclusie van de vorige week over de tech stack zijn wij op zoek gegaan naar een andere setup die toepasselijk was voor het platform.
Redelijk snel kwamen wij tot de conclusie dat het werken met een component based framework het beste zou werken voor het samenstellen van het systeem.
Marcel kwam met de MERN stack dat staat voor:
- Mongo
- Express
- React
- Node

Deze stack bevat bijna alle delen die nodig waren binnen ons platform, maar deze stack is deprecated en er wordt daarvoor tegenwoordig vaak doorverwezen naar NEXT.js wat een package is dat Express, Node en React combineert voor server-side gerenderde React applicaties.

De nieuwe stack bestaat uit:
#### Server
- Next.js
- Socket.io

#### Client
- React
- React-dom
- Socket.io
- D3
- Material design als design system

Na het samenstellen van de stack hebben wij gekeken naar een userflow die wij wilde uitwerken voor het proof of concept prototype van jiskefet en hebben wij de pagina's verdeeld om uit te werken. Marcel heeft zich gefocust op het dashboard en ik ben bezig gegaan met de overview pagina's van de logs en runs en de flow van data door de components en applicatie

Deze week ben ik veel bezig geweest met het uizoeken van de flow van data tussen components en states binnen react en hoe ik dat kon beinvloeden. Dit bleek een vrij tijdrovend process te zijn met een hoge learningcurve, maar met gebruik van de documentatie goed uit te zoeken.

Nu het process van development echt begon te lopen kwam er een pijnpunt aan het licht waar wij zelf geen invloed op hebben. Bij het team van ICT blijken er constant problemen te onstaan met de API waardoor de flow van data niet betrouwbaar is. Bijna op dagelijkse basis begeeft de API en de data is niet compleet, hierdoor hebben wij de knoop doorgehakt en heeft Marcel een eigen API geschreven om een stabiele flow van data te hebben binnen de applicatie.

## Week IV
*17-06*

- User tests
- Doorontwikkelen prototype
- Documentatie

Deze week zij onze UX-desigers bezig gegaan met het testen van de wireframes met OA. eye-tracking om het design te valideren.

Op dinsdag hebben wij een call gehad met CERN en het team dat daar deze week zat om het project te bespreken. Bij de presentatie van het nieuwe ontwerp kwamen positieve reacties over het design, maar ook nog wat vragen en opmerkingen over bepaalde manieren waarop informatie weergegeven werd.

Voor het development zijn wij verder gegaan met de userflow verder uit te werken binnen het prototype en hebben wij nogmaals aangekaart bij de klant dat het niet betrouwbaar zijn van de API ons werk moeilijker maakt.

Tegen het einde van deze week waren de meeste functionaliteiten rond en kwam de focus op het samenvoegen van de verschillende delen van de applicatie.

## Week V
*24-06*
# Meesterproef 2019 @cmda-minor-web · 2018-2019

In de Meesterproef ga je toepassen wat je in de Minor Webdev hebt geleerd. 
Voor de Meesterproef krijg je een opdracht van een echte opdrachtgever. 
Je gaat leren hoe je je geleerde kennis en skils kan gebruiken om een oplossing voor een probleem te ontwerpen. Testen, maken, evalueren
, testen, maken ...
Je kan kiezen uit verschillende projecten. Hier ga je 5 weken aan werken

Coaches: Joost Faber, Laurens Aarnoudse, Vasilis van Gemert, Janno Kapritsias en Koop Reynders.

## Werkwijze

Voor de Meesterproef geef je met een eerste en tweede keuze aan welk project je graag wil doen. Daarna wordt door de coaches een indeling gemaakt.  

In de eerste week krijg je een briefing bij de opdrachtgever en schrijf je een debriefing. 
Dat is de opdracht en de doelstellingen in eigen woorden beschreven. 
Daarna ga je iedere week een proof-of-concept bespreken met je opdrachtgever. 
In week 5 presenteer je het eindresultaat tijdens een expositie. 
Hiervoor moet je ook een passende presentatie maken.

Elke week zijn er 2 coachingsmomenten gepland. 
Op vrijdag ga je naar de opdrachtgever om je vorderingen te bespreken.

- Maandag/Dinsdag - Debriefing met een van de coaches.
- Woensdag/Donderdag - Code review met een van de coaches.
- Vrijdag - Bespreking met de opdrachtgever.


## Criteria en beoordeling

[WAFS Rubric](https://docs.google.com/spreadsheets/d/e/2PACX-1vTjZGWGPC_RMvTMry8YW5XOM79GEIdgS7I5JlOe6OeeOUdmv7ok1s9jQhzojNE4AsyzgL-jJCbRj1LN/pubhtml?gid=0&single=true)

[Performance Matters Rubric](https://docs.google.com/spreadsheets/d/e/2PACX-1vTO-pc2UMvpT0pUjt6NJeckc5N9E7QvCxEfVJW1JjuM0m_9MM8ra05J0s6br486Rocz5JVMhAX_C37_/pubhtml?gid=0&single=true)

[REal Time Web Rubric](https://docs.google.com/spreadsheets/d/e/2PACX-1vSd1I4ma8R5mtVMyrbp6PA2qEInWiOialK9Fr2orD3afUBqOyvTg_JaQZ6-P4YGURI-eA7PoHT8TRge/pubhtml)

[Mijn rubric](https://docs.google.com/spreadsheets/d/1GgvnGCYsqH6agW-4KcxYMsjE5_POe2UOi12ONM4nYsM/edit?usp=sharing)


### Design rationale
In de Design rationale schrijf je de debriefing, de probleem-definitie, toon je de oplossing en schrijf je een uitleg van de code. 
De Design rationale is een verantwoording van je ontwerp.

### Product biografie
In het eindproject doorloop je een iteratief proces. 
Elke week bespreek je met je opdrachtgever je vorderingen en ideeen. 
In de Product biografie hou je stap voor stap bij wat je allemaal hebt gedaan. 
Je schrijft over het proces, de werkwijze en de planning. 
Ook schetsen, testen, uitprobeersels en inspiratie zijn deel van de Product biografie.

### Reflectie op eigen niveau
Aan de hand van de vakrubrics reflecteer je systematisch op je werk. 
In een aantal gesprekken met een coach _reviewen_ we de code van je project. 
Dit doen we op basis van de rubrics van de verschillende vakken. 
Zo krijg je een goed beeld van je eigen niveau, mogelijke aandachtspunten en/of aspecten van het design-proces waar je je nog op kan verbeteren.

### Een blije klant
Voor de klant maak je een (werkend) prototype. Gericht op een bepaalde gebruikersgroep, geschikt voor verschillende apparaten, met echte data, én een goede UX. 
Jeweettoch. 
Een blije klant is een goede klant. 
Soms ontkom je er niet aan dat je een beetje eigenwijs moet doen. 
Dan doe je juist niet wat de klant wil en probeer je de opdrachtgever te overtuigen met een proof-of-concept. 
En soms kan het voorkomen dat het proces niet helemaal soepel loopt. 
Dat hoort erbij en daar leer je van.
Aan het eind van het project vragen we de klant feedback op het geleverde werk... 
