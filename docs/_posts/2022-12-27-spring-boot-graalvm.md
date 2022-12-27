---
title: Spring Boot mit GraalVM
tags:
    - Spring Boot
    - GraalVM
---

Möchtest Du eine Spring Boot Anwendung deutlich schneller starten als bisher? Das Zauberwort dafür lautet [GraalVM](https://www.graalvm.org/). Das GraalVM JDK kompiliert deine Spring Boot Anwendung in eine direkt ausführbare Datei, die keine Java Runtime mehr benötigt. Deine Anwendung wird zwar dadurch vom Betriebsystem abhängig indem sie ausgeführt wird, sie startet dann aber auch deutlich schneller.

In diesem Artikel wird ein trivialer Spring Boot REST Service als native Anwendung innerhalb eines Docker Containers ausgeführt. Es wird keine GraalVM Installation benötigt, da eine dockerisierte Version von GraalVM verwendet wird. Spring Boot 3 und eine Docker Installation werden vorausgesetzt.

Erstelle mit Hilfe von [Spring Initializr](https://start.spring.io/)  eine minimale Spring Boot Anwendung und füge als Abhängigkeiten (Dependencies):
- Spring Web und
- GraalVM Native Support
 
![](/assets/images/spring-boot-graalvm-1.jpg)

ein. Drücke auf den Knopf "GENERATE", speichere die heruntergeladene zip Datei und importiere das Spring Boot Projekt aus der zip Datei in deine Entwicklungsumgebung.

Ich arbeite mit der [Spring Tool Suite](https://spring.io/tools) als Entwicklungsumgebung, so dass ich direkt über die IDE das obige Spring Boot Projekt erzeugen kann.

![](/assets/images/spring-boot-graalvm-2.jpg)

Damit wir etwas zum Testen haben, wird nun ein "Hello world!" REST Service in die Spring Boot Anwendung eingebaut:

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

Die gerade erzeugte minimale Spring Boot Anwendung benötigt ca. eine Sekunde um hochzufahren und liefert auf `https://localhost:8080` einfach nur den String "Hello world!".

![](/assets/images/spring-boot-graalvm-3.jpg)

Nun haben wir eine Spring Boot Anwendung mit einem minimalen REST Service. Jetzt wollen wir diese Anwendung dockerisieren. Dies ist dank Spring Boot Unterstützung extrem einfach, mit dem Befehl auf der Kommandozeile:

```bash
mvn spring-boot:build-image
```

wir die Anwendung gebaut und gleichzeitig in ein Docker Image verpackt. Damit aber der obige Befehl funktioniert, muss Docker lokal installiert und hochgefahren sein.

## Links
- [Spring Boot Docs: GraalVM Native Image Support](https://docs.spring.io/spring-boot/docs/current/reference/html/native-image.html)