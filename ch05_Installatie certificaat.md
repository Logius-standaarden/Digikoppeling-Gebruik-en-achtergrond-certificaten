# Installatie certificaat

## Vragen

Dit hoofdstuk geeft antwoord op de volgende vragen met betrekking tot certificaten voor Digikoppeling:

1. Waarom is het belangrijk om de privésleutel van mijn certificaat te beveiligen?
1. Hoe moet ik de privésleutel van een certificaat opslaan?
1. Hoe beveilig ik de toegang tot deze sleutel?

## Achtergrond

Het programma van eisen<sup>15</sup> dat PKIoverheid aan TSP's oplegt bevat de verplichting aan TSP's om over de juiste beveiliging van sleutels door gebruikers te waken inclusief de mogelijkheid tot audit (zie kader).

<sup>15</sup>: Zie [[PKI Policy]], zoekterm “deel 3b”.

## Stappen

Zodra u een door de TSP ondertekend certificaat ontvangt kunt u dit installeren bij de privésleutel op uw server. Dit certificaat (met de daarin opgenomen publieke sleutel) is niet vertrouwelijk. De bijbehorende privésleutel daarentegen des te meer. Het is belangrijk om deze privésleutel goed te beveiligen. Immers: de privésleutel vertegenwoordigt in de elektronische communicatie de eigenaar en kan toegang tot (meerdere) basisregistraties en andere services geven (zie verder “Omgang met certificaat“).

Om de privésleutel behorend bij certificaten veilig op te slaan in een keystore is het noodzakelijk om veilige wachtwoorden te kiezen. Gebruik daarom een wachtwoord dat moeilijk te herleiden is (zie “Bijlage 2: Richtlijnen voor een veilig password“ voor een voorbeeld). Basisregistraties en andere gegevenshouders kunnen aanvullende maatregelen eisen vanuit de vertrouwelijkheid van de door hen beheerde gegevens en het gebruik van daarbij behorende certificaten<sup>16</sup>.

<sup>16</sup>: Een voorbeeld hiervoor vormt de zorg, waar men eisen stelt aan opslag van servercertificaten.

Het opslaan van een privésleutel van een certificaat in een keystore verschilt per systeem. Raadpleeg de documentatie van uw systeem voor de manier waarop dit moet plaatsvinden. Er zijn ook veel leveranciers die hier handleidingen voor publiceren. Probeer te allen tijde het kopiëren van privé-sleutels zo veel mogelijk tegen te gaan met fysieke, technische en procedurele maatregelen.

