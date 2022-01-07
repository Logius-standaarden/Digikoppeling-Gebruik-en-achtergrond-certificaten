# Inleiding

## Doel en doelgroep

Dit document beschrijft de wijze waarop, binnen de context van

Digikoppeling, met certificaten wordt omgegaan. Inhoudelijk voorziet het in de detaillering van de architectuur voor identificatie, authenticatie en autorisatie. Bovendien geeft het uitleg over de gebruikelijke werkwijze bij het toepassen van certificaten. Meer informatie over certificaten is te vinden op de website: [www.pkioverheid.nl](http://www.pkioverheid.nl) en cert.pkioverheid.nl.

Onderstaande tabel geeft de doelgroep van dit document weer.

| Afkorting | Rol | Taak| Doelgroep? |
|---|---|---|---|
| [MT]   | Management   | Bevoegdheid om namens organisatie (strategische) besluiten te nemen.   | **Nee**   |
| [PL]   | Projectleiding   | Verzorgen van de aansturing van projecten.   | **Nee**   |
| [A&D]   | Analyseren & ontwerpen (design) | Analyseren en ontwerpen van oplossings-richtingen. Het verbinden van Business aan de IT.   | **Ja**   |
| [OT&B]   | Ontwikkelen, testen en beheer   | Ontwikkelt, bouwt en configureert de techniek conform specificaties. Zorgen voor beheer na ingebruikname.  | **Ja**   |

## Digikoppeling standaarden

Dit document is een onderdeel van de Digikoppeling standaard.

![Overzicht van de onderdelen van de Digikoppeling Standaard, de standaard is onderverdeeld in normatieve en ondersteunende onderdelen](media/DK_Specificatie_structuur.svg "Opbouw documentatie Digikoppeling")


<details>
    <summary> Tekstalternatief </summary>
<h2>Digikoppeling</h2>
<p>Logius beheert Digikoppeling. De standaard bestaat uit beheermodel, een overzicht van actuele documentatie en de Digikoppeling architectuur. De architectuur omvat documentatie over identificatie en authorisatie, beveiligingsstandaarden en de koppelvlak standaarden. De koppelvlak standaarden bestaat uit API, WUS (SOAP) en ebMS standaarden met daarnaast een standaard voor grote berichten. Onderstaande documenten vormen samen de Digikoppeling standaard.</p>
<h3>Normatieve documenten</h3>
<ul>
  <li>
    <a href="https://publicatie.centrumvoorstandaarden.nl/dk/actueel/">Digikoppeling Overzicht Actuele Documentatie en voorschriften</a>
  </li>
    <li>
    <a href="https://publicatie.centrumvoorstandaarden.nl/dk/architectuur">Digikoppeling Architectuur</a> Dit is de huidige versie.
  </li>
  <ul>
    <li>
      <a href="https://publicatie.centrumvoorstandaarden.nl/dk/beveilig/">Digikoppeling Beveiligingsstandaarden en voorschriften</a>
    </li>
    <li>
      <a href="https://publicatie.centrumvoorstandaarden.nl/dk/idauth/">Digikoppeling Identificatie en Authenticatie</a>
    </li>
    <li>Koppelvlakstandaarden:</li>
    <ul>
      <li>
        <a href="https://publicatie.centrumvoorstandaarden.nl/dk/ebms/">Digikoppeling Koppelvlakstandaard ebMS2</a>
      </li>
      <li>
        <a href="https://publicatie.centrumvoorstandaarden.nl/dk/wus/">Digikoppeling Koppelvlakstandaard WUS</a>
      </li>
      <li>
        <a href="https://publicatie.centrumvoorstandaarden.nl/dk/gb/">Digikoppeling Koppelvlakstandaard Grote Berichten</a>
      </li>
    </ul>
  </ul>
  <li>
    <a href="https://publicatie.centrumvoorstandaarden.nl/dk/beheer/">Digikoppeling Beheermodel</a>
  </li>
</ul>
<h3>Ondersteunende documenten (niet normatief)</h3>
<ul>
  <li>
    <a href="https://publicatie.centrumvoorstandaarden.nl/dk/watisdk/">Wat is Digikoppeling?</a>
  </li>
  <li>
    <a href="https://publicatie.centrumvoorstandaarden.nl/dk/bpebms">Digikoppeling Best Practices ebMS2</a>
  </li>
  <li>
    <a href="https://publicatie.centrumvoorstandaarden.nl/dk/bpwus">Digikoppeling Best Practices WUS</a>
  </li>
  <li>
    <a href="https://publicatie.centrumvoorstandaarden.nl/dk/bpgb">Digikoppeling Best Practices Grote Berichten</a>
  </li>
  <li>
    <a href="https://publicatie.centrumvoorstandaarden.nl/dk/gbachtcert/">Digikoppeling Gebruik en Achtergronden Certificaten</a>
  </li>
  </ul>

</details>


## Achtergrond

Een belangrijk aspect voor beveiliging van Digikoppeling is de juiste identificatie, authenticatie en autorisatie van organisaties. Voor Digikoppeling is daarbij gekozen om certificaten toe te passen die voldoen aan de eisen van PKIoverheid<sup>1</sup>. Het juist toepassen van deze certificaten is essentieel voor een goede beveiliging. Helaas is dit toepassen ook complex. Digikoppeling heeft daarom aanvullend aan de door PKIoverheid gestelde eisen een aantal afspraken gemaakt die enerzijds de beveiliging conform PKIoverheid garanderen en anderzijds de complexiteit beheersbaar maken<sup>2</sup>. De praktische toepassing van deze afspraken is uitgewerkt in dit document. Het bevat daarvoor:

<sup>1</sup>: Zie [http://www.logius.nl/pkioverheid](http://www.logius.nl/pkioverheid)

<sup>2</sup>: Zie het document “Digikoppeling Identificatie en Authenticatie”

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

- Uitleg over PKIoverheid (hoofdstuk 2)

- Ontwerpen van de aansluiting op Digikoppeling met een Digikoppeling adapter (hoofdstuk 3).

- Bestellen van een certificaat (hoofdstuk 4).

- Ontvangst en installatie van het certificaat (hoofdstuk 5).

- Distributie van het certificaat (hoofdstuk 6).

- Gebruik van het certificaat (hoofdstuk 7).

De volgende hoofdstukken gaan hier per processtap op in. Elk hoofdstuk begint met de opsomming van een aantal vragen die duidelijk maken op welke informatiebehoefte het hoofdstuk antwoord geeft. Daarna volgt belangrijke achtergrondinformatie. Het hoofdstuk sluit af met een beschrijving van de benodigde activiteiten voor deze proces stap.

In bijlagen is de volgende aanvullende informatie opgenomen:

- Informatie over bestandsformaten waarin sleutels en/of certificaten uitgewisseld kunnen worden (Bijlage 1).

- Richtlijnen voor een veilig wachtwoord (Bijlage 2)

- Gegevens die in een certificaat opgenomen kunnen worden opgenomen (Bijlage 3)

## Referenties

| **Overige standaarden**   | **Referentie**   |
|---|---|
| PKIoverheid “Programma van Eisen” | [[PKI Policy]], www.logius.nl/pkioverheid/ |

