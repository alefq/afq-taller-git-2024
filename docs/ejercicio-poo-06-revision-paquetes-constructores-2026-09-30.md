# Ejercicio POO-06 — Revisión, paquetes, constructores y sobrecarga

**Slug:** `ejercicio-poo-06-revision-paquetes-constructores-2026-09-30`  
**Fecha:** 30 de septiembre de 2026  
**Asignatura:** Lenguaje de Programación 3 (CYT646)  
**Rúbrica:** [RUBRICA-ejercicios-lp3-2026.md](RUBRICA-ejercicios-lp3-2026.md)  
**Guía de Git ya publicada:** [github.com/alefq/afq-taller-git-2024](https://github.com/alefq/afq-taller-git-2024)  
**Template de paquetes:** [github.com/alefq/lp3-template-tp](https://github.com/alefq/lp3-template-tp/tree/main/src/main/java/py/edu/uc/lp3)

---

## Vocabulario de los dos dominios

Volvemos al modelado que elegiste el 2 y el 3 de septiembre. Si no jugaste esos títulos, igual podés seguir: con este glosario alcanza.

**Minecraft** es un juego de bloques y criaturas. Una *entidad* es cualquier ser o cosa que existe en el mundo: el jugador, un animal o un monstruo. Un *mob* es una criatura que no es el jugador. El **Creeper** es el mob verde que se acerca y explota.

**Counter-Strike 2** (CS2) es un juego de disparos táctico por equipos. El inventario del jugador está formado por **armas**. El **AWP** (*Arctic Warfare Police*) es el rifle francotirador más conocido de ese juego: dispara un proyectil de gran daño y recarga con lentitud. Las demás familias —rifle de asalto, pistola, granada— se distinguen por el alcance y por el efecto.

**JSON** (*JavaScript Object Notation*) es el texto estructurado que una API REST (interfaz de programas por HTTP) devuelve al navegador o a Insomnia. Un **controller** es un **servicio REST**: toma el pedido, habla con los objetos del dominio y responde. Las reglas del juego viven en las clases, no en el controller.

---

## Objetivo

La meta es publicar un servicio HTTP con Spring Boot, sobre tu modelado de Minecraft o de Counter-Strike 2. Ahí van herencia, **sobreescritura**, ocultamiento de la información, paquetes con sentido, constructores simples y sobrecargados, y **sobrecarga** de al menos un mensaje del dominio.

Cuando termines, un compañero tiene que poder clonar el repositorio, arrancar el servicio y usarlo por la web, sin abrir un `main()` en el entorno de desarrollo.

---

## Contexto

Siguiendo con el repositorio creado `INICIALES-taller-git-2026`, con README y licencia Apache 2.0. Adentro vive el Spring Boot armado desde [start.spring.io](https://start.spring.io) (Maven, Java 21, Spring Web). Las clases del diagrama de septiembre tienen que estar en ese proyecto, compilar, y verse en un historial Git que se pueda leer.

La guía de Git del taller sigue valiendo. Este enunciado suma la revisión en sala y aprieta el diseño: paquetes, constructores, sobrecarga y sobreescritura.

---

## Consignas

Elegí **un** dominio —Minecraft o Counter-Strike 2— y trabajá sobre **tus** clases.

Pedimos los dos mecanismos: **sobrecarga** (en la misma clase, el mismo nombre, otra lista de argumentos) y **sobreescritura** (la misma firma en la clase hija, con su propia implementación).

1. Las clases van en paquetes que coinciden con las carpetas. La organización sigue este template: https://github.com/alefq/lp3-template-tp/tree/main/src/main/java/py/edu/uc/lp3. El dominio queda en `domain`, los servicios REST en `rest.controller`. La clase `Application` sirve para arrancar; la lógica del juego va en otro lado.

2. El modelado de septiembre entra al proyecto. Si algo no compila, se corrige. Esos cambios se registran con `git add`, `git commit` y `git push`.

3. En la clase base, un método abstracto cuyo nombre diga qué tienen que saber hacer todas las clases hijas: algo que el padre no puede resolver, porque cada tipo responde distinto. **Sobreescritura:** dos clases hijas independientes implementan ese método, misma firma, cada una a su modo.

4. Dos **servicios REST**. Un `IndexController` en `GET /` confirma que el servicio está vivo. Otro controller construye una instancia del dominio con parámetros de la URL: esos valores alimentan el constructor o un método de fábrica. Si un valor rompe una regla, la clase lo rechaza y el controller informa el resultado.

5. En JSON, la respuesta de pedirle el mensaje abstracto a cada clase hija. El controller habla con ambas como si fueran el tipo padre. El texto sale del método sobreescrito.

6. Se construye una nueva instancia con **constructores simples y sobrecargados**. La clase hija llama a `super`. Cada firma deja el objeto en un estado legal.

7. Además, sobrecargá al menos un mensaje del dominio: la misma acción, otra lista de argumentos, otro contexto. Disparar sin más datos, o disparar indicando una distancia, es el ejemplo típico.

8. El README lleva el diagrama Mermaid de las clases del 2 y del 3 de septiembre, alineado con lo que hay en `src/`, y un apartado que explica qué cambió con la **sobrecarga** y con la **sobreescritura**: qué se agregó, en qué clases, y cómo se distingue una de la otra.

9. En el repositorio, un `BITACORA.md` (en la raíz o en `docs/`) con la marca del asistente o agente de inteligencia artificial (IA), el modelo exacto del *large language model* (LLM, modelo de lenguaje de gran tamaño) y un resumen de los prompts que usaste. Si no usaste ninguno, anotalo.

---

## Qué se entrega

Cuatro cosas, y el código en GitHub.

1. El **enlace exacto al commit** de la solución: `https://github.com/<usuario>/INICIALES-taller-git-2026/commit/<hash>`. Con esa URL se abre el código que se revisa. Pegalo en Classroom y, si podés, también en el README.

2. El **README** al día: licencia Apache 2.0, diagrama Mermaid alineado con `src/`, y el apartado de sobrecarga y sobreescritura.

3. La **bitácora** (`BITACORA.md`): marca del asistente o agente, modelo de LLM y resumen de prompts. Si no usaste IA, anotalo ahí.

4. En Classroom, **un** archivo Markdown (`.md`), PDF o Word (`.docx`) con las especificaciones de este ejercicio aplicadas a tu dominio: objetivo, consignas y cómo probarlo, más el enlace al commit. Tu usuario de GitHub va al chat del curso.

El servicio arranca con `./mvnw spring-boot:run`.

---

## Cómo se prueba

Se debe poder abrir el enlace al commit, leer el README y la bitácora. El README incluye licencia, Mermaid, sobrecarga y sobreescritura. Arranca Spring Boot, `GET /` responde, el servicio REST construye desde la URL y el JSON de las dos clases hijas está a la vista. Se ven la clase base y las dos clases hijas: método abstracto sobreescrito, visibilidad, constructores simples y sobrecargados. Una pregunta de anclaje: *¿qué ocurre si el controller asigna a mano la vida o la munición?*

---

## Calificación

Vale la rúbrica general de la carpeta ([RUBRICA-ejercicios-lp3-2026.md](RUBRICA-ejercicios-lp3-2026.md)): ocho criterios de 0 a 3, máximo **24** puntos. Estos entregables pesan sobre todo en los criterios 1, 5, 7 y 8.

---

**Cátedra:** ale.feltes@uc.edu.py · @alefeltes
