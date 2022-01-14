# Bestellen certificaat

## Vragen

Dit hoofdstuk geeft antwoord op de volgende vragen met betrekking tot certificaten voor Digikoppeling:

1. Wat heb ik nodig voordat ik een certificaat kan bestellen?
1. Bij wie kan ik een certificaat bestellen?
1. Wie genereert het sleutelpaar en waarom geeft PKIoverheid de voorkeur aan generatie door de aanvrager?
1. Wat zijn de formaten voor het opslaan van certificaten?

## Achtergrond

Er zijn twee manieren om een sleutelpaar van een certificaat aan te maken: zelf genereren of dit door de Trust Service Provider (TSP) laten doen. Als het sleutelpaar zelf aangemaakt wordt, blijft de primaire sleutel achter op de server en zal alleen de publieke sleutel aan de TSP verzonden worden. De TSP stuurt dan een door hem ondertekend certificaat terug waarin de publieke sleutel is opgenomen. Dit is de meest veilige oplossing aangezien de vertrouwelijke privésleutel nooit de gebruikersorganisatie (of zelfs de server waarop deze gebruikt gaat worden) verlaat.

Als de TSP het sleutelpaar aanmaakt, zal de TSP samen met het certificaat (en de daarin opgenomen publieke sleutel) een vertrouwelijke privésleutel opsturen. Deze sleutel wordt via een wachtwoord beveiligd. Dit is een minder veilige oplossing aangezien de privésleutel uitgewisseld wordt. PKIoverheid adviseert daarom om zelf een sleutelpaar te genereren, wat in het kader van Digikoppeling met klem wordt benadrukt. In het verdere document gaan we ervan uit dat een organisatie zelf het sleutelpaar genereert.

## Stappen

De procesgang voor het aansluiten op Digikoppeling is beschreven in het document “Leeswijzer aansluitprocedure gebruik Digikoppeling”. Deze maakt onderdeel uit van de aanvraagprocedure Digikoppeling die u vindt https://www.logius.nl/diensten/digikoppeling/aanvragen. Het bestellen van certificaten vormt hiervan een onderdeel. Om certificaten te kunnen bestellen, moet de organisatie een identificerend nummer hebben: het OIN. Dit nummer wordt verkregen bij de beheerorganisatie van Digikoppeling volgens de procedure die is beschreven op de website van Logius.

Bestellen van een certificaat vindt plaats bij een door PKIoverheid aangewezen TSP die certificaten op commerciële basis verstrekt. Logius houdt op haar website een lijst met goedgekeurde TSP's bij die een PKIoverheid certificaat kunnen leveren<sup>12</sup>. Op deze website staat ook achtergrondinformatie over certificaten en hun werking. Belangrijk aandachtspunt hierbij is dat de eerste keer een aantal extra handelingen (bijvoorbeeld een bezoek aan de notaris of GWK) voorafgaat aan het daadwerkelijk bestellen van het certificaat. De website van Logius en het stelselhandboek bieden een heldere beschrijving van het bestellen en de daarbij betrokken TSP's.

<sup>12</sup>: [https://www.logius.nl/pkioverheid/](https://www.logius.nl/pkioverheid/) bevat specifieke informatie over het aanschaffen van een certificaat.

De websites van de TSP's bevatten formulieren voor de aanvraag van certificaten. In het bestelproces en leveringsproces voor certificaten is het nodig om informatie zoals sleutels en certificaten uit te wisselen. Hiervoor bestaan verschillende bestandsformaten. Deze zijn beschreven in “Bestandsformaten voor certificaten“ in bijlage 1.

Om op deze wijze een certificaat te bestellen moet u eerst een Certificate Signing Request (CSR) maken op de server waarop u het certificaat wilt installeren. Dit CSR bevat naast de door u gegenereerde publieke sleutel ook gegevens die u in het certificaat wilt opnemen (zie hieronder). Vervolgens stuurt u dit CSR in p10 formaat op (afhankelijk van de TSP-procedure) per mail of op een fysieke drager per aangetekende post. Het aanmaken van een CSR verschilt per type server, maar er zijn veel leveranciers die hier handleidingen voor publiceren<sup>13</sup>. De privésleutel kunt u uit de keystore van uw server exporteren voor veilige back-up in een kluis; het p12 formaat is hiervoor geschikt (zie ook “Bestandsformaten voor certificaten“ in bijlage 1. Het volgende hoofdstuk beschrijft hoe u deze privésleutel zou moeten beveiligen.

<sup>13</sup>: Zie bijvoorbeeld https://www.verisign.com/en_US/website-presence/online/ssl-certificates/index.xhtml

Bij bestelling van het certificaat dient u de volgende onderdelen te specificeren:

- Country Name (C): twee letterige landcode C=NL.
- State or Province (S): PKIoverheid raadt het gebruik van dit veld af.
- Locality or City (L): PKIoverheid raadt het gebruik van dit veld af; indien gebruikt hier de vestigingsplaats van de organisatie opnemen. Bijvoorbeeld: L=Den Haag.
- Organisation (O): Volledige naam van de organisatie overeenkomstig gegevens in basisregistratie of formeel document. Bijvoorbeeld: O=Stichting ICTU.
- Organisational Unit (OU): Optionele naam van een organisatieonderdeel. Bijvoorbeeld: OU=Digikoppeling
- Common Name (CN): Dit is de FQN van de server (Host + Domain Name). Bijvoorbeeld: [www.logius.nl/digikoppeling/](http://www.logius.nl/digikoppeling/)
- OrganisatieIdentificatieNummer (OIN): Nummer dat is uitgegeven door de beheerorganisatie van Digikoppeling. Hoewel PKIoverheid in haar Programma van Eisen dit nummer als optioneel vermeldt is het verplicht in de context van Digikoppeling. Bijvoorbeeld: OIN=00000001123456789000. Dit nummer wordt vermeld op het aanvraagformulier.
- Key usage: In certificaten voor Digikoppeling moeten het digital Signature en keyEncipherment bit uit de key usage zijn opgenomen en zijn aangemerkt als essentieel. Geen ander key usage mag hiermee worden gecombineerd. Deze gegevens zijn standaard voor een Digikoppeling certificaat en kan men niet opnemen in het CSR of de aanvraag.
- Extended key usage: In certificaten voor Digikoppeling wordt afgeraden om dit veld toe te passen<sup>14</sup>. Deze gegevens zijn daarom standaard voor een Digikoppeling certificaat en kan men niet opnemen in het CSR of de aanvraag.

<sup>14</sup>: Interoperabiliteit met sterk verouderde Java-tooling kan vereisen dat de “extended key usage”-bits TLSwwwServerAuthentication en/of TLSwwwClientAuthentication opgenomen worden.

Het programma van Eisen deel 3b van PKIoverheid bevat een uitgebreider overzicht van velden die (deels optioneel) in een certificaat voor kunnen komen. Zie [www.logius.nl/pkioverheid](http://www.logius.nl/pkioverheid), zoekterm “deel 3b”.

Het door de TSP ondertekende certificaat ontvangt u meestal in een .p7b formaat of een .cer formaat (zie ook “Bestandsformaten voor certificaten“). Veranderen van informatie in het certificaat is niet mogelijk behalve door een nieuw certificaat aan te vragen. Het volgende hoofdstuk beschrijft hoe u dit certificaat kunt installeren.

