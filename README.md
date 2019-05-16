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

Użycie Dockera i Kubernetesa umożlwi sprostanie wymaganiom skalowalności aplikacji, ułatwi też wdrożenie aplikacji na środowisko "produkcyjne" (stworzone zostanie środowisko demonstracyjne, ale proces wdrożenia w środowisku produkcyjnym byłby taki sam).

Obrazy Dockerowe będą budowane i uploadowane do **Docker Registry**. Użyte zostanie publiczne repozytorium https://hub.docker.com/, ale mogłoby to być dowolne repozytorium np. Amazon Elastic Container Registry (ECR), lub registry lokalne.

Kubernetes będzie posiadał definicję kontenerów dockerowych które ma zainstalować w odpowiedniej liczbie instancji. Aplikacje nie będą znały swoich dokładnych adresów, wewnętrzna sieć będzie zarządzana przez Kubernetesa, za jego pomocą zostanie zaimplementowane service discovery, docelowo ma on również zarządzać przydzielaniem ruchu wychodzącego z producerów do odpowiednich konsumerów.

### Architektura
![Architecture](https://github.com/marcskow/kubernetes-producer-consumer/blob/master/resources/Entity%20Relationship%20Diagram.png)

### Kroki milowe
1. Przygotowanie aplikacji Producenta i Konsumera
2. Komunikacja konsumera z bazą danych MongoDB
3. Stworzenie skryptu budującego .jar (Maven lub Gradle)
4. Stworzenie Dockerfile
5. Stworzenie konfiguracji Kuberntesesa w formie pliku yaml
6. Deploy klustra na AWS (jako Amazon EKS)

### Dockerfile
```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
EXPOSE 8195
ADD build/libs/spring-bootstrap-consumer-1.0.jar consumer.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/consumer.jar"]
```
