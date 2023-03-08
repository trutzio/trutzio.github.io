---
title: Erstes Projekt mit Spring Initializr
tags:
    - Spring Boot
    - Initializr
    - Spring Boot Starter
---

In dieser Lektion wird ein erstes, sehr einfaches Spring Boot Projekt von Grund auf mit [Spring Initializer](https://start.spring.io/) erstellt.

Spring Initializr kann auf zwei verschiedene Arten verwendet werden:
1. als Webanwendung unter https://start.spring.io/ oder
2. direkt über die IDE der Wahl, z.B. [Eclipse](https://www.eclipse.org/), [Spring Tools 4](https://spring.io/tools), [IntelliJ](https://www.jetbrains.com/idea/) oder [Visual Studio Code](https://code.visualstudio.com/).

Mit der IDE "Spring Tools 4" ist die Verwendung von Spring Initializr besonders einfach, da keine zusätzlichen Plugins installiert werden müssen. Im Folgenden wird daher die Spring Tools 4 IDE verwendet.

Ein neues Spring Boot Projekt wird am besten mit dem "Spring Starter Project" Wizard erstellt.

![](/assets/images/spring-boot-grundlagen-001.jpg)

Ein Spring Boot Projekt ist zunächst ein ganz normales Java Projekt, das entweder [[Maven]] oder [[Gradle]] als Build System verwendet. Maven ist in Unternehmen weit verbreitet und wird daher im Folgenden verwendet.

Auf der ersten Seite des Wizards werden das Build System (Maven oder Gradle) und die Maven GAV Koordinaten (Group/Artefact/Version)  des neuen Projekts eingegeben. Als Package wird "Jar" und nicht "War" gewählt.

![](/assets/images/spring-boot-grundlagen-002.jpg)

Auf der nächsten Seite des Wizard wird die Version von Spring Boot angegeben, die in dem Projekt verwendet wird.

In der Liste unter der Spring Boot Versionsnummer werden die Frameworks angegeben, von denen das Spring Boot Projekt abhängig ist. Als Abhängigkeit wird nur "Spring Web" ausgewählt, da im Folgenden ein REST Service erstellt werden soll.

![](/assets/images/spring-boot-grundlagen-003.jpg)

Nach einem Klick auf "Finish" wird wie gewünscht ein neues Spring Boot Projekt in der IDE erstellt. Als Projektname wird die zuvor angegebene ArtifactId verwendet.

## Abhängigkeiten (Dependecies)

Die Datei `pom.xml` im neu erstellten Projekt enthält die Abhängigkeit "Spring Web", die ich zuvor im IDE Wizard eingetragen habe.

![](/assets/images/spring-boot-grundlagen-004.jpg)

In der Spring Boot Terminologie werden die Abhängigkeiten "Starter" genannt. Die zuvor im Wizard angegebene Abhängigkeit "Spring Web" erscheint daher in der Datei `pom.xml` als Abhängigkeit `starter-web`.

Die Abhängigkeit `starter-test` wird standardmäßig hinzugefügt, da das Schreiben von Unit-Tests in Spring Boot als Best Practice angesehen wird. Der Test Starter enthält automatisch [[JUnit 5]] und [[Mockito]] als transitive Abhängigkeiten, um die Erstellung von JUnit 5 Tests zu erleichtern.

Das Verzeichnis `src/main/java` enthält bereits eine triviale Spring Boot Anwendung, die direkt gestartet werden kann. Im Verzeichnis `src/test/java` befindet sich bereits ein leerer JUnit-Test.

Die Datei `application.properties` enthält die Konfiguration des Spring Boot Projektes, wobei diese auch in einer `application.yml` Datei gespeichert werden könnte.

Das neu erstellte Projekt kann entweder über das "Boot Dashboard" oder direkt über die Methode `main` der Java-Klasse `SpringBootGrundlagenApplication` gestartet werden.
![](/assets/images/spring-boot-grundlagen-005.jpg)
![](/assets/images/spring-boot-grundlagen-006.jpg)

Beide Anwendungsstartmethoden sind gleichberechtigt. Der Start der obigen Spring Boot Anwendung startet im Hintergrund einen Tomcat Web Application Server. Auf diese Web-Anwendung kann nun mit dem Browser deiner Wahl zugegriffen werden.

![](/assets/images/spring-boot-grundlagen-007.jpg)

Im Webbrowser wird zunächst ein Fehler angezeigt, da die Anwendung noch leer ist.

Das Fazit dieser Lektion ist, dass mit wenigen Klicks eine Spring Boot Anwendung von Grund auf erstellt werden kann, um mit der Erstellung einer Webanwendung oder eines REST Service zu beginnen.