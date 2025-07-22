# BobApp

Clone project:

> git clone https://github.com/VAcheronPradelAlyssa/CI-CD.git

## Front-end 

Go inside folder the front folder:

> cd front

Install dependencies:

> npm install

Launch Front-end:

> npm run start;

### Docker

Build the container:

> docker build -t bobapp-front .  

Start the container:

> docker run -p 4020:4020 --name bobapp-front -d bobapp-front

## Back-end

Go inside folder the back folder:

> cd back

Install dependencies:

> mvn clean install

Launch Back-end:

>  mvn spring-boot:run

Launch the tests:

> mvn clean install

### Docker

Build the container:

> docker build -t bobapp-back .  

Start the container:

> docker run -p 8080:8080 --name bobapp-back -d bobapp-back

## Docker Compose

Pour lancer l'application complète (front + back) avec Docker Compose :

Build et démarrer tous les services:

> docker-compose up --build

Démarrer les services (si déjà buildés):

> docker-compose up

Arrêter tous les services:

> docker-compose down

L'application sera accessible sur :
- Front-end : http://localhost:4020
- Back-end API : http://localhost:8080 