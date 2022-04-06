# Region &amp; Availability Zone

## Region

- Region czyli miejsce w którym ulokowane są Data Center AWSa
- Region posiada AZ
- W założeniu każdy region od 2016 powinien posiadać minimum trzy AZ

## Availability Zone
	
- Niezależne od siebie lokalizacje w każdym regionie
- Pomagają zapewnić dostępność - tak aby usługi były wdrażane w różnych AZ, a gdy w jednym z nich się usługa przestaje być dostępna to inna strefa może obsłużyć żadanie
- Każda Availability Zona ma jedną lub więcej serwerowni (Data Center, niektóre nawet osiem)
- Każdy Data Center to 50-80 tysięcy fizycznych serwerów
- Każdy AZ redundantnie jest połączony z resztą AZ
- Transit Center - każdy AZ jest połączony do dwóch TC czyli lokalizacji zapewniających komunikację z pozostałymi regionami

## Linki

- [Infrastruktura AWS od środka](https://lukado.eu/Infrastruktura-AWS-od-srodka/)