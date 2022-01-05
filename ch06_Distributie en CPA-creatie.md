# Distributie en CPA-creatie

## Vragen

Dit hoofdstuk geeft antwoord op de volgende vragen met betrekking tot certificaten voor Digikoppeling:

1. Op welke wijze kan ik anderen mijn certificaat ter beschikking stellen t.b.v. authenticatie en hoe verkrijg ik certificaten van anderen?
1. Wat is de rol van het serviceregister bij distributie van certificaten?
1. Wat is de rol van een CPA bij distributie van certificaten?

## Achtergrond

Identificatie van organisaties vindt voor Digikoppeling plaats aan de hand van het OIN dat is opgenomen in het certificaat. Het certificaat zelf (dat ook een uniek identificatienummer heeft) wordt niet rechtstreeks voor identificatie gebruikt; dit verloopt altijd via het OIN uit het certificaat. Nieuwe (of extra) certificaten voor dezelfde organisatie hebben altijd hetzelfde OIN nummer (maar een ander certificaatnummer). Zolang het certificaat geldig is (ondertekend door de TSP, geldigheidsdatum nog niet verstreken en niet ingetrokken) kunnen organisaties ervan uitgaan dat dit OIN correct is.

Basisregistraties en gegevensbronnen met vertrouwelijke gegevens autoriseren toegang tot hun gegevens aan de hand van het OIN in het certificaat.

Het is daarom nodig om uw OIN vooraf aan organisaties ter beschikking te stellen. Distributie van certificaten is afhankelijk van het profiel vaak niet nodig voor Digikoppeling op basis van WUS. Bij Digikoppeling op basis van ebMS2 worden certificaten echter ook opgenomen in de CPA's die organisaties uitwisselen.

## Stappen

Uitwisseling van certificaten is vaak nodig voor gebruik binnen Digikoppeling verband.

Voor het maken van CPA's kunnen organisaties gebruikmaken van het Digikoppeling CPA register.

