# Ejercicio POO-06 — Revisión, paquetes, constructores y sobrecarga

**Slug:** `ejercicio-poo-06-revision-paquetes-constructores-2026-09-30`  
**Fecha:** 30 de septiembre de 2026  
**Asignatura:** Lenguaje de Programación 3 (CYT646)  
**Rúbrica:** `RUBRICA-ejercicios-lp3-2026.md` (misma carpeta)  
**Guía de Git ya publicada:** [github.com/alefq/afq-taller-git-2024](https://github.com/alefq/afq-taller-git-2024)

---

## Vocabulario de los dos dominios

Este ejercicio retoma el modelado que cada estudiante eligió en las clases del 2 y del 3 de septiembre. No es necesario haber jugado los títulos: basta con entender de qué se habla.

**Minecraft** es un juego de bloques y criaturas. Una *entidad* es cualquier ser o cosa que existe en el mundo: el jugador, un animal o un monstruo. Un *mob* es una criatura que no es el jugador. El **Creeper** es el mob verde que se acerca y explota.

**Counter-Strike 2** (CS2) es un juego de disparos táctico por equipos. El inventario del jugador está formado por **armas**. El **AWP** (*Arctic Warfare Police*) es el rifle francotirador más conocido de ese juego: dispara un proyectil de gran daño y recarga con lentitud. Las demás familias —rifle de asalto, pistola, granada— se distinguen por el alcance y por el efecto.

**JSON** (*JavaScript Object Notation*) es el texto estructurado que una API REST (interfaz de programas por HTTP) devuelve al navegador o a Insomnia. Un **controller** es la puerta HTTP: recibe el pedido, habla con los objetos del dominio y responde; no es el dueño de las reglas del juego.

---

## Objetivo

El estudiante publica un servicio HTTP propio, construido con Spring Boot, que versiona el modelado de Minecraft o de Counter-Strike 2. En esa API se aplican herencia, sobreescritura, ocultamiento de la información, paquetes con sentido semántico, constructores que dejan el objeto válido y, al menos, una sobrecarga.

Al terminar, otra persona debe poder clonar el repositorio, arrancar el servicio y usarlo por la web, sin abrir un `main()` en el entorno de desarrollo.

---

## Contexto

Cada estudiante ya creó en GitHub un repositorio público (`INICIALES-taller-git-2026`) con README y licencia Apache 2.0, y colocó dentro un proyecto Spring Boot generado en [start.spring.io](https://start.spring.io) (Maven, Java 21, Spring Web). Las clases del diagrama de septiembre deben vivir en ese proyecto, deben compilar y deben quedar registradas en un historial Git legible.

Este enunciado no sustituye la guía de Git del taller. Completa la práctica con la revisión en sala y con el endurecimiento del diseño: paquetes, constructores y sobrecarga.

---

## Consignas

El estudiante elige **un** dominio —Minecraft o Counter-Strike 2— y trabaja sobre **sus** clases, no sobre un ejemplo genérico tomado de internet.

1. El estudiante **organiza** las clases en paquetes que coinciden con las carpetas. El dominio (`minecraft` o `cs2`) permanece separado de `web`. La clase `*Application` del starter no se borra ni se llena de lógica del juego.

2. El estudiante **incorpora** al proyecto el modelado previo, **corrige** los errores de compilación y **registra** esos cambios con `git add`, `git commit` y `git push`. El ejercicio de Git no consiste en rellenar el README al inicio.

3. El estudiante **declara** en la clase base un método abstracto cuyo nombre expresa un comportamiento que todas las clases hijas deben saber responder y que el padre no puede implementar, porque cada tipo se comporta de forma distinta. **Implementa** ese método en **dos clases hijas** independientes.

4. El estudiante **expone** dos puertas HTTP: un `IndexController` en `GET /`, que solo confirma que el servicio está vivo, y un controller que **construye** una instancia del dominio con parámetros de la URL. Esos valores alimentan el constructor o un método de fábrica. Si un valor viola una regla, la **clase** la rechaza; el controller no corrige el estado a mano.

5. El estudiante **responde**, en JSON, el resultado de pedirle el mensaje abstracto a **cada** clase hija. El controller trata ambas como el tipo padre. No arma el texto con una cadena de `if` según el nombre de la clase.

6. El estudiante **asegura** que el objeto nazca válido. La clase hija invoca al constructor del padre (`super`). Si existe más de una forma de construir, cada firma deja el objeto en un estado legal. Quien escribe al menos un constructor deja de recibir el constructor vacío que el compilador regalaba.

7. El estudiante **sobrecarga** al menos un constructor o un mensaje del dominio: la misma acción, otra lista de argumentos y otro contexto. Por ejemplo, disparar sin más datos frente a disparar indicando una distancia.

8. El estudiante **incluye** en el README el diagrama Mermaid de las clases del 2 y del 3 de septiembre, alineado con el código que hay en `src/`.

---

## Qué se entrega

El código queda en GitHub y el servicio arranca con `./mvnw spring-boot:run`. En Classroom se adjunta **un** archivo Markdown (`.md`), PDF o Word (`.docx`) con las **especificaciones de este ejercicio** aplicadas al dominio propio: objetivo, consignas y forma de probarlo. No se entrega un transcript de chat con un agente. El usuario de GitHub se informa en el chat del curso.

---

## Cómo se prueba

El revisor abre el README (licencia y Mermaid), arranca el Spring Boot y llama a `GET /`. A continuación prueba el endpoint que construye desde la URL y el JSON de las dos clases hijas. Abre la clase base y las dos clases hijas (método abstracto, visibilidad, constructor). Pregunta: *¿qué ocurre si el controller asigna a mano la vida o la munición?*

---

## Calificación

Se aplica la rúbrica general de la carpeta (`RUBRICA-ejercicios-lp3-2026.md`): ocho criterios de 0 a 3, máximo **24** puntos.

---

**Cátedra:** ale.feltes@uc.edu.py · @alefeltes
