# Gebruiksaspecten

## Vragen

Dit hoofdstuk geeft antwoord op de volgende vragen met betrekking tot certificaten voor Digikoppeling:

1. Hoe worden organisaties geautoriseerd?
1. Welke alternatieven heb ik om autorisatie in mijn applicatie te regelen?
1. Hoe vaak moet een certificaat vernieuwd worden?
1. Hoe controleer ik of een certificaat nog geldig is?
1. Hoe zorg ik dat ik met mijn certificaat kan testen?

## Achtergrond

Identificatie van organisaties vindt plaats aan de hand van het OIN. Authenticatie van dit OIN vindt plaats door te controleren of het certificaat waarin dit OIN is opgenomen ook geldig is. Autorisatie beperkt zich in beginsel tot organisatorisch niveau en maakt daarom gebruik van dit OIN<sup>17</sup>.

<sup>17</sup>: Een leidend principe van Digikoppeling is dat de overheidsorganisatie waar een persoon werkzaam is, verantwoordelijk is om deze persoon (medewerker) te authenticeren en juist te autoriseren voor deeltaken binnen de organisatie. Overheidsorganisaties onderling autoriseren (en authenticeren) elkaar vervolgens voor toegang tot bepaalde services op basis van de aan een organisatie toegewezen taak.

In specifieke gevallen kan autorisatie op een gedetailleerder niveau noodzakelijk zijn. Voor overheidsorganisaties is het bijvoorbeeld mogelijk om een subOIN aan te vragen.

Organisaties hebben daarom in hoofdlijnen de keuze uit de volgende opties voor autorisatie:

- *Iedereen autoriseren (na succesvolle authenticatie)*: Een dergelijke autorisatie kan in bijzondere situaties soms zinvol zijn. Het gaat hierbij om situaties waarbij elke overheidsorganisatie<sup>18</sup> dezelfde handelingen mag verrichten op een gegevensbron (of basisregistratie) of wanneer onjuiste handelingen beperkte consequenties hebben.
- *Autoriseren op OIN (na succesvolle autorisatie)*: Een dergelijke situatie is zinvol als organisaties niet dezelfde handelingen mogen verrichten omdat dit vergaande consequenties heeft voor de integriteit en vertrouwelijkheid. In deze situatie is het noodzakelijk dat de basisregistratie (of een andere service) een autorisatietabel met daarin OIN-nummers bijhoudt<sup>19</sup><sup> </sup><sup>20</sup>.
- Autoriseren op organisatieonderdeel:  
   Een dergelijke situatie kan nodig zijn vanuit een wettelijke verplichting aan de gegevenshouder om dit te doen. De gegevenshouder zal in dit geval van de communicatiepartners kunnen eisen dat zij een subOIN aanvragen om het specifieke organisatieonderdeel te onderscheiden.

<sup>18</sup>: Deze autorisatie is vaak te ruim. Het is namelijk mogelijk dat hackers een certificaat bedoeld voor medewerkers misbruiken om zich als Digikoppeling applicaties voor te doen. Dit komt doordat (afhankelijk van de TSP) ook persoonsgebonden PKIoverheid certificaten worden uitgegeven (zoals smartcards) die lijken op Digikoppeling certificaten. De technische achtergrond hiervan is dat een persoonsgebonden certificaat namelijk ook de key usage 'digitalSignature' heeft. Dit volstaat voor een TLS-client in Digikoppeling omgevingen. Sommige TSP's gebruiken bovendien dezelfde TSP-key voor signing van persoonsgebonden certificaten en server-certificaten zodat het verschil tussen de beide type certificaten nog moeilijker is vast te stellen.

<sup>19</sup>: Digikoppeling communicatiepartners wisselen het OIN uit ten behoeve van deze autorisatietabel.

<sup>20</sup>: zie het document : Digikoppeling Identificatie en Authenticatie.

In sommige gevallen kan het audit-proces vereenvoudigd worden met aanvullende identificatiegegevens. Bij dergelijke behoeften kunnen bijvoorbeeld afdelings- of persoonsgegevens als inhoud in een bericht opgenomen worden. Ook gegevens over authenticatie van afdelingen en personen kunnen, bijvoorbeeld in de vorm van certificaten, toegevoegd worden, maar spelen geen rol bij het Digikoppeling autorisatieproces.

Een geldig certificaat vormt binnen de overheid de basis voor vertrouwen op elektronisch gebied. Om risico van het gebruik van privésleutels door onbevoegden te beperken hebben certificaten een beperkte geldigheid (enkele jaren). Als dit vertrouwen tussentijds verloren gaat wordt het certificaat ingetrokken. Het is van groot belang dat de eigenaar van het certificaat een dergelijke situatie zo snel mogelijk meldt aan zijn TSP. Via een zogenaamde Certificate Revocation List (CRL) maken TSP's publiek kenbaar welke certificaten niet meer vertrouwd mogen worden. Het intrekken van een certificaat kan om verschillende redenen plaatsvinden:

- De privésleutel van het certificaat is niet meer beschikbaar:
  - Er is geen pending request aanwezig in de server bij installatie van het certificaat.
  - Er is sprake van een 'private key mismatch' bij installatie van het certificaat op de server.
  - De privésleutel is corrupt.
  - De privésleutel is verloren geraakt (bijvoorbeeld bij een server crash of upgrade).
  - Het wachtwoord van de privésleutel is vergeten.
- De privésleutel is gecompromitteerd.
- Bij installatie van het certificaat blijkt dat er een certificaat voor een onjuiste common name is aangevraagd.
- Informatie in het certificaat is niet meer juist (bijvoorbeeld wijziging van organisatienaam).

Ingetrokken certificaten waarvan de geldigheidsduur is verlopen worden niet meer in de CRL gepubliceerd.

TSP's kunnen informatie over ingetrokken certificaten in plaats van via een CRL ook via een onlinevoorziening opvraagbaar maken. Deze ondersteuning via het Online Certificate Status Protocol (OCSP) is voor TSP's niet verplicht (behalve voor EV certificaten)<sup>21</sup>. Indien beschikbaar biedt dit wel de mogelijkheid om elk certificaat direct online te verifiëren.

<sup>21</sup>: Zie voor detaileisen de Pkioverheid PVE deel 3: aanvullende eisen

## Stappen

Om de betrouwbaarheid van het certificaat te waarborgen is het nodig om dit regelmatig te vernieuwen. PKIoverheid eist van TSP's dat een certificaat maximaal vijf jaar geldig is maar in de praktijk geven TSP's certificaten uit die niet langer dan drie jaar geldig zijn. Vernieuwen van het certificaat zal moeten plaatsvinden ruim voordat dit verlopen is. Dit is vooral van belang als met meerdere organisaties samengewerkt wordt en met deze organisaties certificaten en CPA's (ebMS2) uitgewisseld worden.

PKIoverheid eist dat bij vernieuwing van het certificaat ook een nieuw sleutelpaar gegenereerd wordt.

Een certificaat is geldig als het aan de volgende drie eisen voldoet:

- De ondertekening van het certificaat berust op een geldige hiërarchie van certificaten afgeleid van het overheid stamcertificaat<sup>22</sup>.
- De geldigheidsduur van het certificaat is niet verstreken.
- Het certificaat is niet ingetrokken door de TSP.

<sup>22</sup>: Het stamcertificaat Staat der Nederlanden Root CA vindt u op https://cert.pkioverheid.nl/. Ingetrokken TSP-certificaten vindt u https://crl.pkioverheid.nl/.

Om na te gaan of het certificaat is ingetrokken (Engels: revoked) publiceren de TSP's een Certificate Revocation List (CRL). In deze lijst worden de serienummers van ingetrokken certificaten opgenomen. Het is daarom nodig dat de CRL op regelmatige basis geraadpleegd wordt (of indien beschikbaar het OCSP-alternatief). Aangezien er meerdere TSP's zijn aangewezen binnen het overheidsdomein zullen deze allemaal moeten worden geraadpleegd. PKIoverheid certificaten zijn onderdeel van een hiërarchie. Daarom moeten ook 'bovengelegen' CRL's worden geraadpleegd<sup>23</sup>.

<sup>23</sup>: Servers bieden standaard configuratieparameters voor een CRL. Niet altijd kan er naar meerdere CRL's verwezen worden. In dat geval kunnen automatische scripts helpen om meerdere CRL's samen te voegen.

Bij het gebruik van een CRL dient men erop te letten dat ook een CRL een bepaalde geldigheidsduur heeft. Voor het verlopen van de CRL dient er een nieuwe opgehaald te zijn. Bij het verzuim hiervan en het laten verlopen van de geldigheidsduur van de CRL worden alle certificaten van de betreffende TSP als ongeldig beschouwd<sup>24</sup>. Hoewel een CRL bruikbaar blijft tot de next update, is het verstandig om deze minimaal elke vier uur te verversen<sup>25</sup>. Basisregistraties (en andere gegevenshouders) kunnen voor hun domein specifieke eisen stellen.

<sup>24</sup>: Tevens kan het zijn dat de tooling die de CRL uitleest niet dynamisch de update van het CRLbestand registreert. Zo kan het zijn dat een webserver herstart moet worden voordat deze het nieuwe bestand inleest. Dit gedrag is afhankelijk van het gebruikte product. Het is daarom belangrijk dat dat goed getest wordt.

<sup>25</sup>: TSP's zijn verplicht om het intrekken van een certificaat uiterlijk vier uur na melding via de CRL te publiceren.

Bij het testen van applicaties is het van belang om certificaten te gebruiken waarvan de structuur overeenkomt met die van een PKIoverheid certificaat<sup>26</sup>. Pkioverheid kent een TEST hiërarchie voor dit doeleinde. Logius biedt daarnaast self signed testcertificaten om haar voorzieningen te kunnen testen.

<sup>26</sup>: Een belangrijk kenmerk van PKIoverheid certificaten is behalve het OIN voor Digikoppeling dat deze een vierlaagsstructuur hebben (stamcertificaat, domein, TSP en certificaathouder). Niet alle software kan standaard goed omgaan met een vierlaagsstructuur. Het is daarom belangrijk dat dit goed getest wordt.

Het is niet toegestaan om (keten)testsystemen uit te rusten met certificaten die zijn gegenereerd op basis van het overheid stamcertificaat; voor testen moet een testcertificaat gebruikt worden.

### TLS Offloading - CPA

Door het gebruik van TLS Offloading zijn er minder afhankelijkheden van certificaten in CPA’s. Daardoor kan de geldigheid van een CPA langer zijn dan de geldigheid van het certificaat.

### TLS offloading - WUS

Bij het gebruik van TLS Offloading, specifiek voor WUS (bevragingen), zijn er mogelijkheden om het OIN of andere kenmerken van het certificaat door te geven aan achterliggende applicaties. Dit kan nodig zijn voor het controleren van autorisaties.

Bij TLS-offloading is het mogelijk om het OIN (en andere certificaatgegevens) door te geven aan de achterliggende message-handler en de daarop aangesloten applicaties voor autorisatiedoeleinden.

*Voorbeeld voor Apache*

Er zijn voor een http-proxy o.b.v. Apache speciale mods om certificaat-gegevens door te geven aan de achterliggende messagehandler. Tussen Apache en Tomcat kun je werken met modSSL. Men krijgt dan overigens niet alleen het OIN maar alle certificaatgegevens. Met een kleine Java-app is het mogelijk de gegevens eruit te filteren en bijvoorbeeld toe te voegen aan het bericht dat de messagehandler via JMS doorgeeft aan de achterliggende applicatie.

