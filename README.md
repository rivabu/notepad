# Notepad: Simple Spring Boot App  

This simple application is used for demo purposes. It exposes the `actuator` endpoints as well as the `/notes` endpoint, which creates a note when it gets a `POST` request.

## Usage

The Notepad stores the notes in a MySQL instance, so it expects the MySQL database to be up and running. The bellow command starts a MySQL container with a newly created database `notepad` in it. It also sets up the mysql root password as `root`.

`$ docker run -d --name mysql -e MYSQL_DATABASE=notepad -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 mysql:5.7`

Now, clone this repository and go into the notepad directory:

`$ git clone https://github.com/rivabu/notepad.git`
`$ cd notepad`

Once you succesfully cloned the repository, start the application the jar artifact:

`$ mvn clean install`

Wait for the unit and integration tests to run and the artifact to be generated. Eventually it will be stored in the `target/` directory.

Now, start the application:

`$ java -jar $(ls target/*.jar)`

Check that the application is up and running hitting the actuator `/health` endpoint:

`$ ls -l`

Create a new note:

`
$ curl -H "Content-Type: application/json" -X POST -d '{"title":"Kubernetes","content":"Best container orchestration tool ever"}' http://localhost:8081/notes


## Features

- `Flyway` to manage database migrations.
- `maven-surefire-plugin` to run only unit tests with `mvn test`.
- `maven-failsafe-plugin` to run unit and integrations tests with `mvn verify`.
- 1 simple unit test, 2 integrations tests (a api test to ensure that the JSON returned by the endpoint is correct) and a database test (saves a note and ensures that it was successfuly persisted in MySQL).
- `maven-release-plugin` to release new application versions in GitHub.

## Flyway
- nieuwe versie gemaakt V2__rients test
- flyway-- hash conflict gemaakt, hoe opruimen? niet gelukt: docker image verwijderd en opnieuw aangemaakt, app opnieuw gestart, dan werkt het wel


## Docker
- $docker run: maak nieuwe container, heel eventueel het image op van de docker repo
- $docker ps: geeft lijst met images die draaien
- $docker stop /mysql: stop container
- $docker rm /mysql: verwijder container
- $docker start selenium-hub //let op de dash!
- $docker start chrome
- $docker start mysql: start container
- $docker images: lijst met aanwezige images
- $docker rmi mysql: remove images sql
- $docker container ls -a: alle containers ook die niet runnen

##kitematic

- handige tool om runnende containers te bekijken

## run selenium tests
- mvn verify -Dacceptance.notepad.url=http://192.168.0.32:8081 -Dselenium.browser=chrome -Pacceptance-tests

docker container run -d --name selenium-hub -p 4444:4444 selenium/hub:3.4.0

 -Dspring-profiles-active=acceptance-tests -Dacceptance.notepad.url=http://192.168.0.22:8081 -Dselenium.browser=chrome
 
#chrome
 
docker pull selenium/node-chromedocker pull selenium/node-chrome-debug

docker container run -d --name node-chrome-debug -e HUB_PORT_4444_TCP_ADDR=selenium-hub -e HUB_PORT_4444_TCP_PORT=4444 --link selenium-hub:selenium-hub selenium/node-chrome-debug
docker container run -d --name node-chrome -e HUB_PORT_4444_TCP_ADDR=selenium-hub -e HUB_PORT_4444_TCP_PORT=4444 --link selenium-hub:selenium-hub selenium/node-chrome

in kitemac stel de port van chrome-debug in: 5900 -> 5901
op de MAC download VNC viewer. 
open deze op localhost:5901, het password is 'secret'. Nu zie je de remote desktop van chrome.

als je de selenium-test runt, zie je de browser.

handige URL: https://www.dev2qa.com/setup-selenium-grid-with-docker/

## issues

1. het nemen van screenshots gaat fout, het is een keer gelukt om een screenshot binnen te krijgen, maar niet nadat de test 
gefaald is. Dan wordt direct de connectie naar de browser gesloten.

2. mijn ipadres van mijn laptop wijzigt regelmatig. Dan moet het ip-adres in de pom.xml gewijzigd worden.

3. soms is een een poort conflict met karma. Beide draaien op 8081

## poorten

mysql: 3306 ()
webserver: 8081 (http://localhost:8081/)
selenium-hub: 4444 (http://localhost:4444/grid/console)

## artificatory

https://www.jfrog.com/confluence/display/RTF/Installing+with+Docker

docker pull docker.bintray.io/jfrog/artifactory-oss:latest

docker run --name artifactory -d -p 8082:8081 docker.bintray.io/jfrog/artifactory-oss:latest

http://localhost:8082

user deployer aangemaakt, password: password01
user admin: password: password

releasen:
mvn release:prepare
mvn release:clean
mvn release:perform

# github authentication

maak public key aan in ~/.ssh directory

ssh-keygen -t rsa -C "rientsvanburen@gmail.com"

importeer de inhoud van de public key in github

