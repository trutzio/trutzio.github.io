---
title: Spring Boot mit GraalVM
tags:
    - Spring Boot
    - GraalVM
    - Docker
    - Serverless
    - Packeto Buildpacks
---

Möchtest Du deine Spring Boot Anwendung deutlich schneller starten als bisher? Das Zauberwort dafür lautet [GraalVM](https://www.graalvm.org/). Das GraalVM JDK kompiliert deine Spring Boot Anwendung in eine direkt ausführbare Datei, die keine Java Runtime mehr benötigt. Deine Anwendung wird zwar dadurch vom Betriebsystem indem sie ausgeführt wird abhängig, sie startet dann aber auch deutlich schneller.

## Zusammenfassung

Mit dem Befehl

```bash
mvn spring-boot:build-image -Pnative
```

lassen sich sehr schnell dockerisierte, native Spring Boot 3 Anwendungen bauen. Vorausgesetzt wird aber für den Bau eine Docker Installation.

## Beispiel

In diesem Artikel wird ein trivialer Spring Boot REST Service als native Anwendung innerhalb eines Docker Containers gebaut. Es wird keine GraalVM Installation benötigt, da eine dockerisierte Version von GraalVM verwendet wird. Spring Boot 3 und eine Docker Installation werden vorausgesetzt.

Erstelle mit Hilfe von [Spring Initializr](https://start.spring.io/)  eine minimale Spring Boot Anwendung und füge als Abhängigkeiten (Dependencies):
- Spring Web und
- GraalVM Native Support
 
![](/assets/images/spring-boot-graalvm-1.jpg)

ein. Drücke auf den Knopf "GENERATE", speichere die heruntergeladene zip Datei und importiere das Spring Boot Projekt aus der zip Datei in deine Entwicklungsumgebung.

Ich arbeite mit der [Spring Tool Suite](https://spring.io/tools) als Entwicklungsumgebung, so dass ich direkt über die IDE das obige Spring Boot Projekt erzeugen kann.

![](/assets/images/spring-boot-graalvm-2.jpg)

Damit wir etwas zum Testen haben, wird nun ein sehr, sehr einfacher "Hello world!" REST Service in die Spring Boot Anwendung eingebaut.

```java
@SpringBootApplication
@RestController
public class TestGraalvmApplication {

	public static void main(String[] args { 
		SpringApplication.run(TestGraalvmApplication.class, args);
	}

	@GetMapping("/")
	String hello() {
		return "Hello world!";
	}
}
```

Die gerade erzeugte minimale Spring Boot Anwendung benötigt ca. eine Sekunde um hochzufahren und liefert auf `https://localhost:8080` einfach nur den String "Hello world!" zurück.

![](/assets/images/spring-boot-graalvm-3.jpg)

Nachdem wir nun eine Spring Boot Anwendung mit einem minimalen REST Service gebaut haben, wollen wir diese Anwendung dockerisieren. Dies ist dank Spring Boot 3 Unterstützung extrem einfach. Mit dem Befehl

```bash
mvn spring-boot:build-image
```

wir die Anwendung gebaut und gleichzeitig in ein Docker Image verpackt. Damit aber der obige Befehl funktioniert, muss Docker lokal installiert und hochgefahren sein. Wie man in dem Log des obigen Befehls sieht, werden [Packeto Buildpacks](https://paketo.io/docs/concepts/buildpacks/) für den Bau des Docker Images verwendet. Nachdem der obige Befehl erfolgreich ausgeführt wurde, siehst Du mit `docker images`, dass unsere minimale Spring Boot Anwendung auch als Docker Image vorliegt.

Wenn Du unsere dockerisierte Spring Boot Anwendung mit dem Befehl

```bash
docker run --rm test-graalvm:0.0.1-SNAPSHOT
```

startest, siehst Du, dass die Startzeit weiterhin bei ca. einer Sekunde geblieben ist. Die dockerisierte Spring Boot Anwendung ist eine normale Java Anwendung geblieben, die eine Java VM benötigt.

![](/assets/images/spring-boot-graalvm-4.jpg)

Um eine **native Spring Boot Anwendung** zu bauen, muss der obige Maven Befehl lediglich um das Profil `native` ergänzt werden. 

```bash
mvn spring-boot:build-image -Pnative
```

Der Bau der Anwendung dauer jetzt erheblich länger und ist rechenzeitintensiver. Das Ergebnis nach ca. 1.5 Minuten (auf meinem Rechner) ist ein Docker Image, das unsere Spring Boot Anwendung als native Anwendung enthält. Wenn wir nun diese starten mit

```bash
docker run --rm test-graalvm:0.0.1-SNAPSHOT
```

dann ist sie nach ca. 0.026 Sekunden hochgefahren, also erheblich schneller als unsere Anwendung in der normalen Java Variante.

## Fazit

- mit der neuen Spring Boot 3 Version lassen sich extrem einfach native Spring Boot Anwendungen bauen, die innerhalb eines Docker Containers laufen,
- die Startzeit von nativen Anwendungen (GraalVM) ist erheblich kleiner als von normalen Java Anwendungen, die unter einer Java VM laufen und dadurch für [Serverless Szenarien](https://en.wikipedia.org/wiki/Serverless_computing) sehr interessant

## Links
- [Spring Boot Docs: GraalVM Native Image Support](https://docs.spring.io/spring-boot/docs/current/reference/html/native-image.html)