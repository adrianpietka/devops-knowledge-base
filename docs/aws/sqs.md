# SQS - Amazon Simple Queue Service

## Typy kolejek

### Standard

- wiadomość dostarczana przynajmniej jeden raz, ale może być więcej razy
- nie ma porządkowania wiadomości
- obługuje prawie nieograniczoną liczbę transkacji na sekundę dla SendMessage / ReceiveMessage / DeleteMessage
- przydatne gdy niezbędna jest wysoka przepustowość

### FIFO

- przetwarzanie wiadomości dokładnie jeden raz
- pierwszy wchodzi, pierwszy wychodzi - zachowana jest kolejność wiadomości
- 3000 komunikatów na sekundę
- przydatne gdy kolejność wiadomości jest ważna lub gdy nie mogą pojawić się duplikaty wiadomości

## Nazewnictwo

- FIFO musi kończyć się na ".fifo"
- max 80 znaków
- alphanumeric, hyphens (-) oraz underscores (_)
 
## Konfiguracja

### Visibility timeout

- czas przez jaki wiadomość po odebraniu z kolejku nie jest widoczna dla innych odbiorców wiadomości
- rozpoczyna się gdy Amazon SQS zwróci wiadomość
- jeśli w tym czasie wiadomość nie zostanie przetworzona i usunięta przez konsumenta, wraca ona na kolejke
- jeśli wiadomość ma zostać odebrana dokładnie raz, konsument musi ją usunąć w czasie trwania limitu
- domyślnie 30 sekund dla wszystkich wiadomości w kolejce

### Message retention period

- czas życia wiadomości na kolejce, która nie jest usuwana
- po przekroczeniu zdefiniowanego czasu wiadomość jest automatycznie usuwana
- domyślnie 4 dni
- okres może wynosić od 60 sek do 14 dni

### Delivery delay

- opóźnienie pierwszego dostarczenia wiadomości na kolejke
- wiadomości nie są widoczne dla konsumentów przed upłynięciem ustawionego czasu
- domyślnie 0, maksymalnie 15 minut
- kolejka standardowa - zmiana tej wartości nie wpływa na wiadomości na kolejce
- kolejka FIFO - zmiana tej wartości wpływa na wiadomości w kolejce

### Maximum message size

- maksymalny rozmiar wiadomości na kolejce
- rozmiar wiadomości w zakresie 1 bajt - 256 kb
- w JAVIE istnieje `amazon-sqs-java-extended-client-lib`, która przechowuje większe wiadomości w Amazon S3

### Receive message wait time

- czas przez który podczas odpytanie kolejki będzie czekać na udostępnienie jakiejś wiadomości (np. kolejka może być pusta, ale w przeciągu tego czasu pojawi się nowa wiadomość)
- domyślnie 0, maksymalnie 20 sek
- długie odpytywanie pomaga obniżyć koszty korzystania z usługi, eliminująć liczbę pustych odpowiedzi (gdy nie ma wiadomości)
- jeśli zbierze się maksymalna liczba wiadomości, natychmiast są one zwracane, nie czekając na upłynięcie czasu odpowiedzi

## Access Policy

TODO

## Dead-letter queue

- kolejka wiadomości których nie można przetworzyć np. z powodu błednego komunikatu, danych w niej zawartych czy problemów w komunikacji z systemem zewnętrznym
- przydatne w celu debugowania, dlaczego danej wiadomości nie udało się przetworzyć
- należy wybrać jedną z utworzonych kolejek lub podać ARN
- Maximum receives
  - ile razy maksymalnie może wystąpić błąd konsumpcji danej wiadomości
  - od 1 do 1000
  - po przekroczeniu ustawionego limitu, wiadomość wpada na kolejkę dead-letter

## Wiadomość

- Wysyłka
  - Message body
    - wymagane
  - Message group ID
    - wymagane
    - określa grupę wiadomości na kolejce
  - Message deduplication ID
    - wymagane
    - token do deduplikacji wiadomości w interwale deduplikacji
  - Message attributes
    - opcjonalnie
- Odbieranie
  - Message ID
    - nadawany automatycznie, podczas dodawania wiadomości na kolejke

## Typowe problemy

- Błędnie skonfigurowany limit czasowy
- Brak Dead Leater Queue
- https://lumigo.io/blog/sqs-and-lambda-the-missing-guide-on-failure-modes/
- https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html
