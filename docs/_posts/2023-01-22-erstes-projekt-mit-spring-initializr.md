---
title: Erstes Projekt mit Spring Initializr
tags:
    - Spring Boot
    - Initializr
    - Spring Boot Starter
---

In dieser Lektion wird ein erstes, sehr einfaches Spring Boot Projekt mit [Spring Initializr](https://start.spring.io/) erstellt.

Spring Initializr kann auf zwei verschiedene Arten verwendet werden:
- als Web Anwendung unter https://start.spring.io/ oder
- direkt über die IDE deiner Wahl, also [Eclipse](https://www.eclipse.org/), [Spring Tools 4](https://spring.io/tools), [IntelliJ](https://www.jetbrains.com/idea/) oder [Visual Studio Code](https://code.visualstudio.com/).

Mit der Spring Tools 4 IDE ist die Verwendung von Spring Initializr besonders einfach, da keine zusätzlichen Plugins installiert werden müssen. Im Folgenden wird daher die IDE Spring Tools 4 verwendet.

Erstelle in der Spring Tools IDE ein neues Projekt mit dem "Spring Starter Project" Wizard.

![](/assets/images/spring-boot-grundlagen-001.jpg)

Ein Spring Boot Projekt ist zunächst ein ganz normales Java Projekt, das entweder  [[Maven]] oder [[Gradle]] als Build System verwendet. Maven ist in Unternehmen weit verbreitet, daher werde ich es in dieser Lektion verwenden.

Auf der ersten Seite des Wizards werden das Build System (Maven/Gradle) und die GAV (Group/Artefact/Version) Koordinaten des neuen Projekts eingegeben. Bitte wähle als Packaging "Jar" und ändere es nicht auf "War".

![](/assets/images/spring-boot-grundlagen-002.jpg)

Auf der nächsten Seite des Wizard wird die Version von Spring Boot angegeben, die du verwenden möchtest. Zum Zeitpunkt der Erstellung dieses Videos war 3.0.1 die aktuellste stabile Version von Spring Boot.

In der Liste unter der Versionsnummer kannst Du die Frameworks angeben, die Du als Abhängigkeiten in Deinem neuen Projekt haben möchtest. Ich wähle hier nur "Spring Web" aus, da ich im Folgenden einen REST-Service erstellen möchte.

![](/assets/images/spring-boot-grundlagen-003.jpg)

Auf der letzten Seite des IDE Wizards siehst Du eine URL, in der Deine bisherigen Angaben als URL-Parameter zusammengefasst sind. Du könntest diese URL auch direkt im Browser verwenden, um das Spring Boot Projekt herunterzuladen. Wir möchten dies nicht, da die Spring Tools das Projekt direkt in der IDE erstellen.

Nach einem Klick auf "Finish" wird wie gewünscht ein neues Spring Boot Projekt in der IDE erstellt. Als Projektname wird die zuvor angegebene ArtifactId verwendet.

Die Datei `pom.xml` in dem neu erstellten Projekt enthält die Abhängigkeit "Spring Web", die ich vorhin im IDE Wizard eingetragen habe.

![](/assets/images/spring-boot-grundlagen-004.jpg)

In der Spring Boot Terminologie werden die Abhängigkeiten "Starter" bezeichnet. So habe ich vorhin den Web Starter, auch `starter-web` genannt, als Abhängigkeit in der IDE hinzugefügt.

Der `starter-test` wird standardmäßig hinzugefügt, da das Schreiben von Unit-Tests als Best Practice angesehen wird. Der Test Starter enthält [[JUnit 5]] und [[Mockito]] als transitive Abhängigkeiten, so dass das Erstellen von JUnit 5 Tests leicht möglich ist.

Das Verzeichnis `src/main/java` enthält bereits eine triviale Spring Boot Anwendung, die direkt gestartet werden kann. Im Verzeichnis `src/test/java` befindet sich bereits ein leerer JUnit-Test.

Die Datei `application.properties` enthält die Konfiguration des Spring Boot Projektes, wobei diese auch in einer `application.yml` Datei gespeichert werden könnte.

Das neu erstellte Projekt kann entweder über das "Boot Dashboard" oder direkt über die Methode `main` der Java-Klasse `SpringBootGrundlagenApplication` gestartet werden.
![](/assets/images/spring-boot-grundlagen-005.jpg)
![](/assets/images/spring-boot-grundlagen-006.jpg)

Beide Anwendungsstartmethoden sind gleichberechtigt. Der Start der obigen Spring Boot Anwendung startet im Hintergrund einen Tomcat Web Application Server. Auf diese Web-Anwendung kann nun mit dem Browser deiner Wahl zugegriffen werden.

![](/assets/images/spring-boot-grundlagen-007.jpg)

Im Webbrowser wird zunächst ein Fehler angezeigt, da die Anwendung noch leer ist.

Das Fazit dieser Lektion ist, dass mit wenigen Klicks eine Spring Boot Anwendung von Grund auf erstellt werden kann, um mit der Erstellung einer Webanwendung oder eines REST Service zu beginnen.