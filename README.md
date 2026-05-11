# Projekt Dziennik Elektroniczny

## OVERVIEW
Projekt full-stack stworzony przy użyciu następujących technologii:
 - Frontend: React.JS
 - Backend: Java(Springboot) + Maven
 - Baza Danych: PostgreSQL
 - Containerization: Docker, Docker Compose

## PREREQUISITES
Przed uruchomieniem projektu należy upewnić się, że są zainstalowane odpowiednie wersje:
 - Java 21.0.9+
 - PostgreSQL 16.11
 - Maven 3.9.4
 - SpringBoot 4.0.0
 - React 19.2.3+
 - Docker
 - Docker Compose
 - Node.JS v.20

## Instalacja

1. Klonowanie repozytorium
```
git clone https://github.com/ZwhsmD/School-E-Registry
```

2. Instalowanie zależności

Backend:
```
mvn clean install
```

Frontend:
```
cd ./frontend
npm install
```

# Konfiguracja

Należy dodać swoją nazwę użytkownika i hasło do konta PostgreSQL w dwóch plikach

1. pap_project/src/main/resources/application.properties

```
...
spring.datasource.url=jdbc:postgresql:/db:5432/dziennikElektronicznyDB
spring.datasource.username={username}
spring.datasource.password={password}
spring.datasource.driver-class-name=org.postgresql.Driver
...
```

2. docker-compose.yml
```
...
backend:
    build: .
    ports:
      - "8080:8080"
    extra_hosts:
      - "host.docker.internal:host-gateway"
    environment:
      - CORS_ALLOWED_ORIGINS=http://localhost:3000
      - SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/dziennikElektroncznyDB
      - SPRING_DATASOURCE_USERNAME={username}
      - SPRING_DATASOURCE_PASSWORD={password}
      - SPRING_PROFILES_ACTIVE=default
...
```


# Uruchomienie projektu lokalnie

## Frontend:
```
cd ./frontend
npm start
```

Frontend będzie dostępny pod
http://localhost:3000/

## Baza danych:
```
psql -U {username} -d dziennikElektronicznyDB
```

By uruchomić bazę danych należy mieć konto postgres i zastąpić {username} swoją nazwą użytkownika.
W terminalu pojawi się pytanie o hasło do konta w PostgreSQL, które należy podać.

## Backend:
```
./mvn clean spring-boot:run
```

# Uruchomienie Projektu poprzez Dockera

Projekt posiada plik docker-compose.yaml, który zarządza frontendem, backendem i bazą danych

```
docker-compose up -d
```

Aplikacja będzie dostępna pod adresem
http://localhost:3000/

By zatrzymać kontenery należy użyć komendę
```
docker-compose down
```

# Dostęp do aplikacji

Port Backend: http://localhost:8080
Port Frontend: http://localhost:3000
Port PostgreSQL: 5432

# Baza danych - skrypty
1. Wprowadzenie gotowych danych do bazy
```
docker exec -i db psql -U sstanlej -d dziennikElektronicznyDB < src\main\resources\insert.sql
```

2. Uruchomienie testów jednostkowych
```
docker exec -i db psql -U sstanlej -d dziennikElektronicznyDB < src\test\resources\tests.sql
```

3. Czyszczenie bazy danych
```
docker-compose down -v
```

4. Uruchomienie bazy danych
```
docker-compose up -d --build
```
