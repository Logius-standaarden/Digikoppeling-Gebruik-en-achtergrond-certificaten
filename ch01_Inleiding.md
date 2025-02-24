# Inleiding

## Doel en doelgroep

Dit document beschrijft de wijze waarop, binnen de context van Digikoppeling, met certificaten wordt omgegaan. Inhoudelijk voorziet het in de detaillering van de architectuur voor identificatie, authenticatie en autorisatie. Bovendien geeft het uitleg over de gebruikelijke werkwijze bij het toepassen van certificaten. Meer informatie over certificaten is te vinden op de website: https://cert.pkioverheid.nl/.

Onderstaande tabel geeft de doelgroep van dit document weer.

| Afkorting | Rol | Taak| Doelgroep? |
|---|---|---|---|
| [MT]   | Management   | Bevoegdheid om namens organisatie (strategische) besluiten te nemen.   | **Nee**   |
| [PL]   | Projectleiding   | Verzorgen van de aansturing van projecten.   | **Nee**   |
| [A&D]   | Analyseren & ontwerpen (design) | Analyseren en ontwerpen van oplossings-richtingen. Het verbinden van Business aan de IT.   | **Ja**   |
| [OT&B]   | Ontwikkelen, testen en beheer   | Ontwikkelt, bouwt en configureert de techniek conform specificaties. Zorgen voor beheer na ingebruikname.  | **Ja**   |

## Digikoppeling standaarden

Dit document is een onderdeel van de Digikoppeling standaard.

<figure>
  <object data="https://logius-standaarden.github.io/publicatie/dk/actueel/media/DK_Specificatie_structuur.svg" type="image/svg+xml" id="infographic">Overzicht van de onderdelen van de Digikoppeling Standaard, de standaard is onderverdeeld in normatieve en ondersteunende onderdelen</object>
  <figcaption>Opbouw documentatie Digikoppeling</figcaption>
</figure>

<b>Legenda</b>


<table class="legendum">
    <thead>
        <tr>
            <th><strong>Kleur</strong></th>
            <th><strong>Soort Document</strong></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="green">Groen</td>
            <td>Standaard documentatie</td>
        </tr>
        <tr>
            <td class="grey">Grijs</td>
            <td>Ondersteunende documentatie</td>
        </tr>
    </tbody>
</table>


<b>Beheer</b>

- De standaarddocumenten (groen/vierkant aangegeven) vallen onder het beheer zoals geformaliseerd in het document [[[?DK-Beheermodel]]].

- De ondersteunende documentatie wordt onderhouden door Logius als de beheerder van de standaard (en afgestemd met stakeholders/ gebruikers).

- Alle goedgekeurde documenten zijn te vinden op de website van Logius, [www.logius.nl](https://www.logius.nl/onze-dienstverlening/domeinen/gegevensuitwisseling/digikoppeling).

## Achtergrond

Een belangrijk aspect voor beveiliging van Digikoppeling is de juiste identificatie, authenticatie en autorisatie van organisaties. Voor Digikoppeling is daarbij gekozen om certificaten toe te passen die voldoen aan de eisen van PKIoverheid<sup>1</sup>. Het juist toepassen van deze certificaten is essentieel voor een goede beveiliging. Helaas is dit toepassen ook complex. Digikoppeling heeft daarom aanvullend aan de door PKIoverheid gestelde eisen een aantal afspraken gemaakt die enerzijds de beveiliging conform PKIoverheid garanderen en anderzijds de complexiteit beheersbaar maken<sup>2</sup>. De praktische toepassing van deze afspraken is uitgewerkt in dit document. Het bevat daarvoor:

<sup>1</sup>: Zie [http://www.logius.nl/pkioverheid](http://www.logius.nl/pkioverheid)

<sup>2</sup>: Zie het document [Digikoppeling Identificatie en Authenticatie](https://gitdocumentatie.logius.nl/publicatie/dk/idauth/)

- een uitwerking van de consequenties van deze authenticatie-afspraken;

- voorstellen / best practices voor het gebruik van certificaten.

In document wordt duidelijk aangegeven of het een uitwerking betreft (die verplicht is vanuit deze afspraken) of een voorstel (waar men van af kan wijken).

## Omgang met certificaat

Certificaten zijn gebaseerd op sleutelparen waarvan het publieke deel in het certificaat is opgenomen en het privédeel door de certificaateigenaar geheim wordt gehouden. Beide delen passen op elkaar in de zin dat:

- ondertekening met de privésleutel via de publieke sleutel gecontroleerd kan worden;

- encryptie met de publieke sleutel alleen met de privésleutel ontcijferd kan worden.

De privésleutel vertegenwoordigt in de elektronische communicatie de eigenaar. Binnen de huidige Digikoppeling afspraken is dit een overheidsorganisatie. Overheidsorganisaties hebben veelal toegang tot (meerdere) basisregistraties en hebben vergaande rechten binnen de e-overheid. Het is daarom van het grootste belang om zeer vertrouwelijk om te gaan met een privésleutel behorend bij een certificaat en te voorkomen dat deze zoek raakt of in verkeerde handen belandt. Een dergelijke situatie leidt namelijk tot:

- toegang tot de e-overheidssystemen voor onbevoegden;

- het intrekken van een sleutel met het gevolg dat een organisatie niet kan deelnemen aan de e-overheid;

- de noodzaak tot het opnieuw genereren van het sleutelpaar en het aanvragen van een certificaat.

## Leeswijzer

Dit document is opgebouwd volgens een karakteristiek proces dat organisaties bij invoering van Digikoppeling doorlopen:

- [Uitleg over PKIoverheid](#achtergrond-pkioverheid-certificaten)

- [Ontwerpen van de aansluiting op Digikoppeling met een Digikoppeling adapter](#ontwerp-aspecten-digikoppeling-adapter)

- [Bestellen van een certificaat](#bestellen-certificaat)

- [Ontvangst en installatie van het certificaat](#installatie-certificaat)

- [Distributie van het certificaat](#distributie-en-cpa-creatie)

- [Gebruik van het certificaat](#gebruiksaspecten)

De volgende hoofdstukken gaan hier per processtap op in. Elk hoofdstuk begint met de opsomming van een aantal vragen die duidelijk maken op welke informatiebehoefte het hoofdstuk antwoord geeft. Daarna volgt belangrijke achtergrondinformatie. Het hoofdstuk sluit af met een beschrijving van de benodigde activiteiten voor deze proces stap.

In bijlagen is de volgende aanvullende informatie opgenomen:

- [Informatie over bestandsformaten waarin sleutels en/of certificaten uitgewisseld kunnen worden](#bijlage-1-bestandsformaten-voor-certificaten)

- [Richtlijnen voor een veilig wachtwoord](#bijlage-2-richtlijnen-voor-een-veilig-password)

- [Gegevens die in een certificaat opgenomen kunnen worden opgenomen](#bijlage-3-basisattributen-in-certificaat)

## Referenties

| **Overige standaarden**   | **Referentie**   |
|---|---|
| PKIoverheid “Programma van Eisen” | [[PKI Policy]], www.logius.nl/pkioverheid/ |

