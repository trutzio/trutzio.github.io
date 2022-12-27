---
title: Spring Boot mit GraalVM
tags:
    - Spring Boot
    - GraalVM
---

Möchtest Du eine Spring Boot Anwendung deutlich schneller starten als bisher? Das Zauberwort dafür lautet [GraalVM](https://www.graalvm.org/). Das GraalVM JDK kompiliert deine Spring Boot Anwendung in eine direkt ausführbare Datei, die keine Java Runtime mehr benötigt. Deine Anwendung wird dadurch vom Betriebsystem abhängig indem sie ausgeführt wird, sie startet dann aber auch deutlich schneller.

In diesem Artikel wird ein trivialer Spring Boot REST Service als native Anwendung innerhalb eines Docker Containers ausgeführt. Es wird keine GraalVM Installation benötigt, da eine dockerisierte Version von GraalVM verwendet wird. Spring Boot 3 und eine Docker Installation werden vorausgesetzt.

## Links
- [Spring Boot Docs: GraalVM Native Image Support](https://docs.spring.io/spring-boot/docs/current/reference/html/native-image.html)