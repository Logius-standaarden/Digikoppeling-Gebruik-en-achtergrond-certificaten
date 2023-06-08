# Achtergrond PKIoverheid certificaten

## PKIoverheid

De Nederlandse overheid heeft een eigen Public Key Infrastructure ingericht waarmee de veiligheid van digitale diensten in Nederland kan worden geborgd door middel van het uitgeven (en intrekken) van digitale certificaten.

De certificaat autoriteit (CA) borgt de integriteit en authenticiteit van het certificaat en staat in voor de identiteit van de certificaateigenaar.

De certificatie dienstverleners (TSPs<sup>3</sup>) verstrekken PKIoverheid certificaten (onder de root of stamcertificaat van de Staat der Nederlanden) conform de eisen van PKIoverheid en vallen onder toezicht van Logius als Policy Authority (PA). De PA beheert het Programma van Eisen (het normenkader) en Certification Practice Statements. De PA bepaalt de toetreding van TSPs tot het stelsel en houdt toezicht op de TSPs.<sup>4</sup>

<sup>3</sup>: Trust Service Providers (TSPs) is de engelse term voor certificatie dienstverleners. De afkorting TSPs wordt in dit document gebruikt voor beide begrippen. TSP’s werden eerder CSP genoemd, Certificate Service Provider.

<sup>4</sup>: https://www.logius.nl/diensten/pkioverheid

Kenmerken PKIoverheid<sup>5</sup>:

<sup>5</sup>: [Hoe werkt PKIoverheid?](https://www.logius.nl/diensten/pkioverheid/hoe-werkt-het)

- Exclusief keurmerk van de Staat der Nederlanden.

- Gebaseerd op Nederlandse wet- en regelgeving en Europese standaarden.

- Beheer van de standaard door de Rijksoverheid.

- Regie van incidenten of calamiteiten door de Rijksoverheid.

- Actief toezicht op de certificatiedienstverleners door de Rijksoverheid.

- Mogelijkheid om een rechtsgeldige elektronische handtekening te zetten.

- Eén digitaal certificaat voor meerdere voorzieningen.

### Stamcertificaat

De Staat der Nederlanden heeft een eigen stamcertificaat die de basis vormt voor het vertrouwen van de onderliggende certificaten.

Binnen de PKI voor de overheid zijn op vier niveaus verschillende typen certificaten gedefinieerd, te weten:

- Stamcertificaat;
- Domeincertificaat;
- TSP certificaat;
- Eindgebruikercertificaat.

Voor machine to machine verkeer (en dus ook voor Digikoppeling) wordt gebruik gemaakt van het Staat der Nederlanden Private Root CA G1 stamcertificaat.
(Voor webauthenticatie wordt vanaf 1-1-2021 gebruik gemaakt van het stamcertificaat Staat der Nederlanden EV Root CA, Dit stamcertificaat wordt niet gebruikt voor Digikoppeling<sup>6</sup>)


Het Public Root G3 en de Private Root G1 Stamcertificaten maken gebruik van SHA-256.

<sup>6</sup>:Zie de Digikoppeling Beveiligingsvoorschriften en richtlijnen voor de specifieke eisen en evt. uitzonderingen.
### Certificaat hiërarchieën

Op dit moment zijn er meerdere certificaathiërarchieën PKIoverheid. Na verloop van tijd zijn steeds sterkere algoritmes of andere functionaliteiten nodig om de betrouwbaarheid van certificaten te kunnen garanderen. Alle certificaten binnen eenzelfde hiërarchie zijn gebaseerd op hetzelfde algoritme. De oudste hiërarchie is gebaseerd op het SHA1-algoritme; de nieuwere hiërarchieën op SHA256. De EV-hiërarchie is speciaal ingericht om alleen certificaten voor Extended Validation uit te geven.<sup>7</sup>



Om foutmeldingen te voorkomen bij machine-to-machine communicatie, moet de gehele certificaatketen van eindgebruikerscertificaat tot aan het stamcertificaat gevalideerd kunnen worden. Deze hiërarchieën zijn te raadplegen op de website van PKIoverheid<sup>8</sup>.

<sup>7</sup>: https://www.logius.nl/standaarden/pkioverheid/certificaten/
<sup>8</sup>: Idem

### TSPs

Een Certificatie dienstverlener (Trust Service Provider oftewel TSP) verstrekt een PKIoverheid certificaat aan de aanvrager op basis van een aanvraag die voldoet aan de voorwaarden, een identiteitscontrole en controle van het Handelsregister.

### Persoonsgebonden certificaten

Een certificaat kan worden verstrekt ter identificatie en authenticatie van een persoon, een organisatie of een apparaat. Persoonsgebonden certificaten kunnen b.v. worden gebruikt om documenten te ondertekenen of om iemand te kunnen authenticeren.

### Server (service) certificaten

Digikoppeling vereist het gebruik van server (of service) certificaten voor de beveiliging van endpoints van webservices. Voor het signen en versleutelen van berichten wordt aanbevolen om een apart certificaat te gebruiken.

### Private services servercertificaten

Een PKIoverheid services servercertificaat is een Private Root certificaat en geschikt voor de beveiliging van verkeer tussen systemen.

Een Private Root certificaat is 3 jaar <sup>9</sup> geldig. Dit type certificaat is niet aangemeld bij softwareleveranciers en wordt door browsers niet automatisch vertrouwd. Dit is echter geen belemmering als het certificaat gebruikt wordt voor berichtenverkeer tussen systemen.

<sup>9</sup>: Laatste raadpleging februari 2020

**Raadpleeg [Digikoppeling Beveiligingsstandaarden en voorschriften] voor de eisen m.b.t certificaten.**

### Generaties en naamgeving

Er zit een maximumlengte aan de geldigheidsduur van een Root CA-certificaat. In het geval van PKIoverheid is dat 12 à 15 jaar. De periode waarin een Root CA-certificaat geldig is wordt een generatie genoemd. De generaties worden opvolgend genummerd, vandaar dat we spreken over G1,G2 en G3.  Zo’n nieuwe generatie is vaak ook een moment om de te gebruiken crypto-algoritmen nog eens kritisch te bekijken en –indien nodig- te vernieuwen. Bijvoorbeeld overschakeling naar een langere sleutellengte en sterker hashing alghoritme. Bij de Private Root ‘leven’ we in de 1e generatie, vandaar de naam Private Root G1. Deze generatie loopt tot 14 november 2028.

## Toepassingen

Een PKIoverheid-certificaat wordt gebruikt bij:

- beveiliging van websites
- authenticatie (van servers en/of personen)
- rechtsgeldige elektronische handtekeningen
- versleuteling van elektronische berichten

Zie https://www.logius.nl/diensten/pkioverheid voor meer informatie.

### Hoe werkt PKI in Digikoppeling?

PKI beveiliging werkt met PKI sleutelparen: elke partij beschikt altijd over een publieke sleutel en een private sleutel. De private sleutel is geheim en mag nooit worden gedeeld met een ander. De publieke sleutel wordt gedeeld met andere uitwisselingspartners. Zowel de verzender als de ontvanger beschikken over een eigen PKI sleutelpaar; zij wisselen hun publieke sleutels met elkaar uit.

Digikoppeling schrijft voor dat het transport kanaal (internet of diginetwerk) wordt beveiligd via tweezijdig TLS. Beide partijen wisselen hun publieke sleutels uit en zetten hiermee een tweezijdig versleutelde TLS verbinding op. Dit document geeft uitleg over hoe dit werkt en wat hiervoor nodig is.

Daarnaast geeft de Digikoppeling standaard de mogelijkheid de inhoud van het bericht te versleutelen of te ondertekenen (of allebei):

- De verzender gebruikt zijn private (of geheime) sleutel om een bericht of bericht inhoud te ondertekenen.
- De verzender gebruikt de publieke of openbare sleutel van de ontvanger om het bericht of bericht inhoud te versleutelen (encryptie). De ontvanger gebruikt zijn eigen private sleutel om het bericht te ontcijferen. Dit heet asymmetrische encryptie.

Digikoppeling onderkent de profielen *signed*, en *signed en encrypted* die zowel voor WUS als ebMS2 zijn uitgewerkt.



<aside class="note" title="REST API">
<p>Zie het [[Digikoppeling REST API profiel]] voor de ondersteuning van signing en encryptie voor REST API's</p>
</aside>
