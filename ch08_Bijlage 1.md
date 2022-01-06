# Bijlage 1: Bestandsformaten voor certificaten

De volgende bestandsformaten worden gebruikt voor uitwisseling van sleutels en/of certificaten:

|||
|---|---|
| p7b   | De Cryptographic Message Syntax standaard (PKCS \#7) wordt gebruikt voor uitwisseling van certificaten en hogere orde certificaten uit de hiërarchie waarmee dit certificaat is ondertekend (en op hun beurt de bovengelegen certificaten zijn ondertekend). Bestanden in dit formaat hebben vaak de extensie .p7b en soms .p7c. Hetzelfde formaat wordt gebruikt voor CRL's.   |
| p10   | De Certification Request Standard (PKCS \#10) wordt gebruikt voor aanvraag van een door een TSP ondertekend certificaat en aangeduid als Certificate Signing Request (CSR). Het CSR bevat daartoe informatie die in het certificaat opgenomen moet worden waaronder de publieke sleutel. Bestanden in dit formaat hebben vaak de extensie .p10.   |
| p12   | Het Personal Information Exchange formaat (PKCS \#12) wordt gebruikt voor uitwisseling van certificaten en de bijbehorende privésleutel. Als de privésleutel ook in het bestand is opgenomen, is het gebruikelijk (en hoogstnoodzakelijk) om dit bestand met een wachtwoord te beveiligen. Bestanden in dit formaat hebben vaak de extentie .p12 of .pfx.   |
| cer (BER of DER) | De Basic Encoding Rules (BER) en de Distinguished Encoding Rules (DER) zijn beide een platform-onafhankelijke manier om certificaten weer te geven (encoding) ten behoeve van uitwisseling. DER-encoding heeft de voorkeur. Bestanden in dit formaat hebben vaak de extensie .cer. .der-encoded bestanden hebben soms ook de extensie .der. Bestanden bevatten soms meer dan één certificaat. |
| cer (base64)   | Base64 is een een platform-onafhankelijke manier om certificaten weer te geven (encoding); base64 is ontwikkeld ten behoeve van uitwisseling over internet middels Secure/Multipurpose Internet Mail Extensions (S/MIME). Bestanden in dit formaat hebben vaak de extentie .cer of .pem. Een .pem bestand kan soms ook een privésleutel bevatten (dit wordt afgeraden).   |

Bij gebruik in het kader van Digikoppeling zullen deze formaten vaak (maar niet uitsluitend) als volgt toegepast worden:

- aanvraag van een certificaat: .p10;
- ontvangst van het ondertekende certificaat: .p7b of .cer of .ber;
- export van de privésleutel en certificaat voor backup; .p12.

