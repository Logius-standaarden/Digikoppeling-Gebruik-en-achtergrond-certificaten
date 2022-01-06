# Ontwerp aspecten Digikoppeling adapter

## Vragen

Dit hoofdstuk geeft antwoord op de volgende vragen met betrekking tot certificaten voor Digikoppeling:

1. Wat zijn de consequenties van het authenticeren en autoriseren met certificaten op organisatorisch niveau?
1. Welke organisaties kunnen een OIN krijgen?
1. Moet ik dezelfde of verschillende certificaten gebruiken voor servicerequester en serviceprovider?
1. Moet ik dezelfde of verschillende certificaten gebruiken voor WUS en ebMS2?
1. Wat moet ik doen als ik al een certificaat heb?

## Achtergrond

Het document “Digikoppeling Identificatie en Authenticatie” beschrijft de afspraken over gestandaardiseerde authenticatie volgens Digikoppeling standaarden. Een onderdeel van deze afspraken is dat authenticatie plaatsvindt op het niveau van organisaties. Dit heeft consequenties voor het certificaat dat organisaties gebruiken:

- Certificaten voor het gebruik van Digikoppeling worden beschikbaar gesteld aan organisaties en niet aan personen.
- Digikoppeling identificeert organisaties aan de hand van het OIN. Zie Digikoppeling Identificatie en Authenticatie.
- Voor de unieke identificatie en authenticatie van deze organisaties wordt het OIN opgenomen in een PKIoverheid certificaat in het zogenaamde Subject.serialNumber-veld door de TSP.<sup>10</sup>

<sup>10</sup>: Indien er sprake is van een twintig-cijferig nummer is dit altijd het OIN.

Een belangrijke overweging is of voor verschillende doelen ook verschillende certificaten gebruikt worden of dat deze doelen in hetzelfde certificaat worden gecombineerd. Keuzes hierbij zijn de combinatie van:

- Verschillende servicerequesters (dus clients in TLS-omgeving).
- Verschillende serviceproviders (dus servers in TLS-omgeving) zoals basisregistraties en andere gegevensbronnen.
- Servicerequesterrol en serviceproviderrol van een organisatie.
- Certificaten voor authenticatie, signing en/of encryptie.
- Gebruik voor WUS-omgeving en/of ebMS2-omgeving.

Combinatie van verschillende doelen in hetzelfde certificaat is efficiënt aangezien minder certificaten hoeven te worden aangeschaft en periodiek vernieuwd. Dat scheelt in kosten en inspanning. Combinatie van certificaten heeft ook een nadeel. Soms moeten hetzelfde certificaat en de bijbehorende privésleutel op meerdere servers (in zogenaamde keystores) opgeslagen worden. Het is dan lastiger om vast te stellen of er misbruik van een certificaat heeft plaatsgevonden. Daarom wordt sterk afgeraden om hetzelfde certificaat op verschillende servers toe te passen. Als deze servers een gemeenschappelijke keystore gebruiken geldt het bezwaar niet.

Voor gebruik van certificaten voor Digikoppeling is het toegestaan om certificaten te combineren voor alle genoemde doelen. Verder scheiden van certificaten per server wordt sterk aanbevolen, maar is niet vereist.

Vaak spelen ook technische inrichtingsaspecten een rol. Voor gebruik ten behoeve van server-authenticatie dient een Common Name (CN)<sup>11</sup> te zijn opgenomen in het certificaat. Combinatie is technisch daarom alleen mogelijk voor zover de TLS-afhandeling in dit verband plaatsvindt op dezelfde (proxy)server met dezelfde CN.

<sup>11</sup>: Hostname of Fully Qualified Name (FQN).

## Stappen

Allereerst dient een organisatie te kiezen voor welke doelen certificaten gecombineerd dan wel gescheiden worden (zie voorgaande paragraaf). Het advies hierbij is om elke server een eigen certificaat te geven zodat er normaliter geen hergebruik van het Digikoppeling certificaat plaatsvindt.

Het volgende hoofdstuk beschrijft stapsgewijs hoe men een OIN en een PKIoverheid certificaat kan verkrijgen.

