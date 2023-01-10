---
title: Erstes Projekt mit Spring Initializr
tags:
    - Spring Boot
    - Initializr
    - Spring Boot Starter
---

In dieser Lektion werden wir ein erstes, sehr einfaches Spring Boot Projekt mit [Spring Initializr](https://start.spring.io/) erzeugen.

Du kann Spring Initializr auf zwei unterschiedliche Arten verwenden:
- als Web Anwendung unter https://start.spring.io/ oder
- direkt über die IDE deiner Wahl, also [Eclipse](https://www.eclipse.org/), [Spring Tools 4](https://spring.io/tools), [IntelliJ](https://www.jetbrains.com/idea/) oder [Visual Studio Code](https://code.visualstudio.com/).

Mit Spring Tool 4 ist die Verwendung von Spring Initializr besonders einfach, da keine zusätzliche Plug-ins installiert werden müssen. Ich werde deshalb im folgenden die Spring Tools 4 IDE verwenden.

Innerhalb der Spring Tools IDE erzeuge ein neues Projekt über den "Spring Starter Project" Wizzard.

![[/assets/images/spring-boot-grundlagen-001.jpg]]

Dieser Wizzard erzeugt ein Spring Boot Projekt innerhalb deiner IDE. Ein Spring Boot Projekt ist zunächst ein ganz normales Java Projekt, das entweder [[Maven]] oder [[Gradle]] als Build System verwendet. Maven ist in Unternehmensumfeld sehr verbreitet, deshalb verwende ich es auch in dieser Lektion.

Auf der ersten Seite des Wizzards wird
- die Java Version und das sogenannte Packaging des neuen Projektes angegeben, lasse hier bitte das Packaging auf "Jar und ändere es nicht auf War",
- es wird die Id des neuen Projektes angegeben, in Form einer GroupId und ArtifactId
- und es wird die Version des neu zu erzeugenden Projektes angegeben, hier empfehle ich Dir die Versionsnummer mit "-SNAPSHOT" enden zu lassen.

![[/assets/images/spring-boot-grundlagen-002.jpg]]

Auf der nächsten Seite des IDE Wizzards wird die Version von Spring Boot angegen, die Du verwenden möchtest. Bei der Erstellung dieses Videos war 3.0.1 die aktuellste stabile Version von Spring Boot.

In der Liste unter der Versionsnummer kannst Du die Frameworks angegeben, die Du als Abhängigkeiten in Deinem neuen Projekt haben möchtest. Ich wähle hier nur "Spring Web", da ich im folgenden einen REST Service aufbauen möchte.

![[/assets/images/spring-boot-grundlagen-003.jpg]]

Auf der letzten Seite des IDE Wizzards siehst Du eine URL in der Deine vorherigen Angaben als URL Parameter zusammengefasst sind. Diese URL könntest Du auch direkt im Browser verwenden um das Spring Boot Projekt herunter zu laden. Dies wollen wir nicht, da über die Spring Tools das Projekt direkt in der IDE angelegt wird.

Nach einem Click auf "Finish" wird wie gewünscht ein neues Spring Boot Projekt in Deiner IDE angelegt. Die vorhin angegebene ArtifactId wird als Projektname verwendet.

Die `pom.xml` Datei in dem gerade neu erzeugtem Projekt enthält das "Spring Web" Anhängigkeit, die ich vorhin im IDE Wizzard eingetragen habe.

![[/assets/images/spring-boot-grundlagen-004.jpg]]

In der Terminologie von Spring Boot werden die Abhängigkeiten als "starter" bezeichnet. Also ich habe vorhin in der IDE den Web Starter, auch `starter-web` als Anhängigkeit hinzugefügt.

Der `starter-test` wird standardmässig hinzugefügt, da das Schreiben von Unit Tests als Best Practice gilt. Der Test Starter enthält [[JUnit 5]] und [[Mockito]] als transitive Abhängigkeiten.

Der Ordner `src/main/java` enthält schon eine triviale Spring Boot Anwendung, die direkt gestartet werden kann. In dem Verzeichnis `src/test/java` befindet sich schon ein leerer JUnit Test.

Die Datei `application.properties` enthält die Konfiguration des Spring Boot Projektes, wobei diese auch in einer `application.yml` Datei gespeichert werden könnte. Bei Verwendung von [Spring Boot Profilen](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.profiles), können profilspezifische Konfigurationen in `application-{profile}.yml` gespeichert werden, mehr dazu auch unter [Profile Specific Files](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config.files.profile-specific). Profile werden hier nicht weiter behandelt.

