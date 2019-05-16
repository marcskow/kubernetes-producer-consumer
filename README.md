# Specyfikacja Projektu

### Temat
Mikroserwisowa aplikacja do rejestrowania danych samochodowych.

### Stos technologiczny
* Budowa serwisów: **Java, Maven**
* Konteneryzacja: **Docker**
* Orkiestracja: **Kubernetes**
* Infrastruktura: **AWS**
* Komunikacja: **REST, JSON**

### Opis
Projekt będzie polegał na komunikacji dwóch serwisów, z których jeden będzie nadawcą wiadomośći w formacie **JSON**, a drugi ich odbiorcą. Nadawca będzie symulował wysyłanie danych przez samochody znajdujące się w ruchu. Dane będą zawierały informacje na temat stanu samochodu, jego położenia, paliwa i innych parametrów.

Całość będzie stworzona w architekturze mikroserwisowej, z orkiestratorem w postaci **Kubernetesa**. Aplikacje będą budowane jako **obrazy Dockerowe** poprzez przygotowanie odpowiednich **Dockerfile**. Następnie stworzona zostanie konfiguracja Kubernetesa, w założeniu umożlwiająca w łatwy sposób zmianę ilości kontenerów - nadawców i kontenerów - odbiorców. 

Użycie Dockera i Kubernetesa umożlwi sprostanie wymaganiom skalowalności aplikacji, ułatwi też wdrożenie aplikacji na środowisko "produkcyjne" (będzie to środowisko demonstracyjne, ale proces wdrożenia w środowisku produkcyjnym byłby taki sam).

### Architektura
![Architecture](https://github.com/marcskow/kubernetes-producer-consumer/blob/master/resources/Entity%20Relationship%20Diagram.png)
