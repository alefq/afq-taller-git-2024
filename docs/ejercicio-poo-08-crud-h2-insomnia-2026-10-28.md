# Ejercicio POO-08 — CRUD REST, H2, reglas de juego y excepciones

**Slug:** `ejercicio-poo-08-crud-h2-insomnia-2026-10-28`  
**Fecha:** 28 y 29 de octubre de 2026 (una misma unidad de clase)  
**Asignatura:** Lenguaje de Programación 3 (CYT646)  
**Rúbrica:** [RUBRICA-ejercicios-lp3-2026.md](RUBRICA-ejercicios-lp3-2026.md)  
**Enunciado anterior:** [ejercicio-poo-06-revision-paquetes-constructores-2026-09-30.md](ejercicio-poo-06-revision-paquetes-constructores-2026-09-30.md)  
**Guía de Git:** [github.com/alefq/afq-taller-git-2024](https://github.com/alefq/afq-taller-git-2024)

Este es el **trabajo práctico** de la segunda mitad del semestre. El servicio **guarda** el estado en una base **H2**. El cliente de prueba es una **colección de Insomnia** versionada en el repositorio. El CRUD de una entidad es el piso. Encima van **dos reglas de negocio del juego**, una **simulación** que las pone a andar, y una **jerarquía de excepciones** con un *handler* por tipo.

El enunciado plantea preguntas. Las respuestas salen de su modelo. No hay un árbol de clases «correcto» copiado de un tutorial de empleados ni de otro videojuego.

---

## Vocabulario

**CRUD** (*Create, Read, Update, Delete*) es el conjunto de cuatro operaciones sobre un **recurso**: crear, leer, actualizar y borrar. En una API REST esas operaciones se expresan con verbos HTTP sobre una URL que nombra el recurso, no la acción.

| Operación | Verbo HTTP típico | Recurso (ejemplo) | Código de éxito habitual |
|---|---|---|---|
| Crear | `POST` | la colección del recurso | 201 Created |
| Leer uno | `GET` | un ítem, con su identificador en la URL | 200 OK |
| Leer varios | `GET` | colección, con o sin filtro | 200 OK |
| Actualizar | `PUT` o `PATCH` | ítem | 200 OK |
| Borrar | `DELETE` | ítem | 204 No Content |

Si el ítem no está, **404**. Si el cuerpo rompe una regla del dominio, **400** (o el código que justifiquen en el README). El número de la URL es el identificador que asignó la persistencia, no un índice de una lista en el controller.

**H2** es un motor de base de datos relacional que corre **dentro** del proceso Java. En el taller alcanza con el perfil de desarrollo: el archivo (o la memoria) vive junto a la aplicación. Spring Boot lo conecta con `spring-boot-starter-data-jpa` y el driver de H2. **JPA** (*Java Persistence API*) describe cómo una clase se corresponde con una tabla. Un **repositorio** de Spring Data es, en la práctica, una **interfaz**: ustedes declaran los mensajes; el marco genera la implementación.

**Insomnia** es el cliente REST que ya usaron para `GET /`. Una **colección** agrupa pedidos (método, URL, encabezados, cuerpo JSON). Esa colección se exporta a un archivo y se sube al repositorio para que un compañero reproduzca las pruebas.

Las reglas del juego viven en las **clases del dominio**. El controller traduce HTTP. El repositorio traduce filas. Cuando una regla no se puede cumplir, el dominio **lanza una excepción**; el *handler* HTTP la convierte en JSON y en un código de estado.

**Excepción** es un objeto que interrumpe el flujo normal porque ocurrió algo que el método no puede resolver ahí. Una **jerarquía** de excepciones es una familia: una clase base del dominio y **al menos dos** clases hijas, cada una nombrada según la regla que falló. Un **handler** HTTP atiende **un tipo**. El cliente distingue a las hermanas por el cuerpo o por el código de estado. Cómo se declara eso en Spring es parte de lo que hay que investigar.

---

## Objetivo

Publicar un servicio HTTP con Spring Boot, sobre el modelado de **Minecraft** o de **Counter-Strike 2**, con:

1. persistencia en **H2** de **tres clases** de su modelado (una familia con padre y dos hijas, o tres clases que la simulación necesita y que ustedes justifiquen);
2. un **CRUD REST completo** sobre al menos una de esas familias;
3. **dos reglas de negocio** del juego, pensadas por el grupo, que permitan una **simulación** persistida:
   - en Minecraft, de **explosiones**;
   - en Counter-Strike 2, de **daño** o de **carga de munición**;
4. una **jerarquía de excepciones** del dominio (clase base y dos hijas) y un **handler por tipo**;
5. al menos un **protocolo** (`interface`) como en POO-07;
6. una **colección Insomnia** con el CRUD, la simulación en el caso feliz, y **un pedido por cada tipo de excepción** que el handler distingue.

Un compañero clona, arranca con `./mvnw spring-boot:run`, importa la colección y recorre crear → simular → ver el estado persistido → provocar cada error.

---

## Contexto

Siguen en `INICIALES-taller-git-2026`. El proyecto ya tiene Spring Web. Ahora entra **Spring Data JPA** y **H2**. Los paquetes del template se mantienen: dominio en `domain`, entrada HTTP en `rest.controller`. La persistencia merece su propio paquete (`repository` o el nombre que justifiquen): ahí viven **interfaces**, no la lógica del Creeper ni del AWP.

La pregunta de anclaje del semestre se mantiene: *¿puede otra clase, u otra capa, dejar el objeto en un estado imposible?* Ahora hay una capa más: la fila de la tabla. Si JPA expone un setter público que acepta munición negativa, el invariante se rompió igual que si el controller asignaba el campo.

---

## Qué hay que pensar (antes de copiar anotaciones)

Estas preguntas se responden en el README, en frases propias. El código tiene que ser coherente con esas respuestas.

**Recurso y verbo.** ¿Cuál es el sustantivo de su API? ¿La URL nombra al recurso y el verbo HTTP dice la operación?

**Identidad.** ¿Qué campo es la clave? ¿Quién la asigna? ¿El JSON de creación la lleva o la omite?

**Herencia y tablas.** JPA ofrece más de una forma de guardar una jerarquía. ¿Cuál eligieron y por qué, en **su** dominio? ¿Cómo se distingue el subtipo en el JSON?

**Interfaz y repositorio.** El repositorio de Spring Data es una interfaz. ¿Qué gana el controller al depender de ese tipo? Relacionen esto con el protocolo de POO-07.

**Protocolo del dominio.** Hay una `interface` **suya**, con el nombre que ya dibujaron o uno nuevo que justifiquen. ¿Qué endpoint la usa? ¿Puede hablar con instancias de familias distintas?

**Ocultamiento.** ¿Quién sostiene las reglas numéricas del juego? ¿Qué prueba de Insomnia muestra que un `POST` ilegal deja la base igual que antes?

**PUT y PATCH.** ¿Reemplazan el recurso entero o un subconjunto de campos? ¿Qué ocurre con un campo omitido?

**DELETE.** ¿Qué significa borrar en su modelo? ¿Ese verbo HTTP habla con un mensaje del dominio?

**Dos reglas.** ¿Qué dos hechos del juego cambian el estado de más de un objeto a la vez? ¿Cómo se llama el recurso HTTP de la simulación? ¿Un `GET` posterior muestra el resultado ya persistido?

**Excepciones.** ¿Cómo se llama cada clase de la jerarquía y por qué? ¿Un recurso inexistente y una regla de juego incumplida son tipos distintos? ¿Qué lleva el JSON de error?

---

## Inspiración (otros juegos; no se copian)

El práctico sigue en Minecraft o en CS2. Los títulos que siguen sirven para preguntarse qué cuenta como regla. Cada grupo inventa las suyas y las nombra con el vocabulario de **su** juego.

- *Pokémon*: un golpe depende del tipo; un estado impide seguir actuando. ¿Qué equivalente cabe en su simulación?
- *League of Legends*: una acción gasta un recurso y espera. ¿Qué se agota en la suya?
- *The Legend of Zelda* o *Fortnite*: hay un insumo que se consume y un tope. ¿Cuál es el insumo en su modelo?
- *Valorant*: a veces la misma acción tiene dos formas, o sólo es legal en un lugar. ¿Su simulación distingue contextos?
- *Super Mario* o *Stardew Valley*: una acción deja al personaje o al mundo en otro estado, o se acaba la energía del día. ¿Ese estado nuevo se guarda?

El README nombra las **dos reglas propias** en una frase cada una y dice qué tres clases participan. Si mencionan otro juego, es para explicar la idea.

---

## Consignas

Elegí **un** dominio —Minecraft o Counter-Strike 2— y trabajá sobre **tus** clases.

1. Dependencias y arranque: `spring-boot-starter-data-jpa`, driver H2, consola H2 habilitada en desarrollo. En `application.properties` (o YAML) se ve la URL de H2, el usuario y si `ddl-auto` crea el esquema. El README explica cada propiedad en una frase.

2. **Tres clases** de su modelado entran en el proyecto, compilando y persistidas cuando la simulación las necesita. En la familia principal, **dos clases hijas** independientes siguen siendo «es un» respecto del padre. El método abstracto de POO-06 **sigue existiendo** y se sobreescribe. Los constructores simples y sobrecargados siguen dejando el objeto legal. JPA necesita un constructor sin argumentos: investiguen cómo convive eso con el ocultamiento (pista: visibilidad del constructor vacío frente a los constructores de negocio).

3. Una **interfaz** de dominio (POO-07) con al menos un mensaje. Al menos **dos** clases, de **familias distintas** si el modelo lo permite, implementan esa interfaz. Un endpoint de lectura usa el tipo de la interfaz.

4. Un repositorio Spring Data para la clase base de la familia persistida. Los mensajes extra de consulta los inventan ustedes según el dominio. Se declaran en la **interfaz**; no se implementan a mano.

5. **CRUD REST** sobre la colección de esa familia:

   - `POST` crea y devuelve el recurso con su `id`.
   - `GET` de la colección lista lo persistido (no una lista armada en el método).
   - `GET` por `id` devuelve un ítem o 404.
   - `PUT` o `PATCH` actualiza y persiste.
   - `DELETE` quita el ítem (o lo marca, si esa es la regla) y responde el código que documentaron.

   El controller habla con el repositorio y con el dominio. El JSON tiene que poder **discriminar** el subtipo al crear y al listar. Investiguen cómo se hace en Jackson y justifiquen la elección.

6. Un servicio en `GET /` confirma que la aplicación vive.

7. **Dos reglas de negocio** del juego, como métodos del dominio. El controller las dispara; las reglas no se improvisan en la capa HTTP. Esas reglas alimentan **una simulación** expuesta por REST, que involucra las **tres clases** del modelado:

   - Minecraft: **explosiones**.
   - CS2: **daño** o **carga de munición**.

   El resultado se **persiste**. Un `GET` posterior muestra el estado después de simular. El README describe las dos reglas en lenguaje del juego, con los nombres de **sus** clases.

8. **Jerarquía de excepciones** del dominio: una clase base y **dos hijas**. Los nombres los elige el grupo. El dominio lanza la hija que corresponde. Hay **un handler HTTP por tipo**, de modo que el cliente distinga a las hermanas. Investiguen cómo se declara eso en Spring, y la diferencia entre excepción comprobada y no comprobada; justifiquen cuál usan.

9. Colección **Insomnia** en el repositorio (`insomnia/` o `docs/insomnia/`):

   - un entorno con la URL base del servicio;
   - un pedido por cada verbo del CRUD;
   - un `POST` que viola un invariante de construcción;
   - un `GET` o `DELETE` contra un `id` inexistente;
   - el pedido del endpoint que usa la **interfaz** de dominio;
   - la **simulación** en el caso que cumple las dos reglas;
   - **un pedido por cada hija** de la jerarquía de excepciones (el handler se ve distinto en el JSON o en el código HTTP).

   En el README: cómo importar la colección y el orden de ejecución (crear primero, copiar el `id`, simular, provocar errores).

10. Diagrama Mermaid al día: tres clases, interfaz, repositorio, controller, familia de excepciones. El README distingue **herencia**, **implementación de interfaz**, **uso del repositorio** y **jerarquía de excepciones**.

11. `BITACORA.md` con marca del asistente, modelo de LLM y resumen de prompts. Si no usaron IA, anótenlo.

12. Commits separados: dependencias y propiedades; entidades; repositorio; controller CRUD; reglas y simulación; excepciones y handlers; colección Insomnia; README. Cada mensaje dice qué aporta el cambio.

---

## Qué no hace falta (todavía)

No se pide autenticación, ni PostgreSQL en un servidor aparte, ni operaciones batch de cien registros, ni una jerarquía de mappers de integración.

---

## Qué se entrega

Las cuatro piezas de la rúbrica, más la colección.

1. Enlace exacto al **commit** de la solución.
2. README: arranque, propiedades H2, diagrama, las dos reglas en una frase cada una, respuestas a las preguntas de «Qué hay que pensar», cómo importar Insomnia.
3. Bitácora de IA.
4. En Classroom, especificaciones aplicadas a **su** dominio (objetivo, URLs, invariantes, cómo probar), con el enlace al commit.

El servicio arranca con `./mvnw spring-boot:run`.

---

## Cómo se prueba (cinco a diez minutos)

Se abre el commit. Se lee el README. Se arranca Spring Boot. Se importa la colección. Se recorre:

1. `GET /` — vivo.
2. `POST` válido — 201 y un `id`.
3. `GET` colección — el recurso aparece.
4. `GET` por `id` — coincide.
5. actualización — el campo cambia y **sigue** después de un `GET`.
6. `POST` ilegal — error y la colección **no** creció con basura.
7. `DELETE` — el `GET` posterior es 404 (o el estado que documentaron).
8. endpoint del protocolo — JSON con el mensaje de la interfaz.
9. simulación — el estado persistido cambió de un modo que se puede contar con las dos reglas.
10. cada excepción hija — el handler de ese tipo responde; el JSON (o el código HTTP) se distingue del de la hermana.

Consola H2: se puede abrir y **ver la tabla**. Una pregunta de anclaje: *si mañana cambiamos H2 por otra base, ¿qué archivos tocan y cuáles se quedan quietos?* Otra: *¿quién lanza la excepción, el controller o el objeto del juego?*

---

## Calificación

Rúbrica general: ocho criterios de 0 a 3, máximo **24**. En este práctico pesan especialmente:

- **2 Paquetes:** dominio, REST y repositorio separados.
- **3 Ocultamiento:** invariantes frente al JSON y frente a JPA.
- **4 Herencia:** familia persistida, sobreescritura y jerarquía de excepciones.
- **6 Observable:** CRUD, simulación con dos reglas, H2, handlers por tipo y colección Insomnia.

El criterio 6 pide ver **persistir de verdad** y **simular de verdad**: un `GET` después de un `POST` y después de la simulación; la tabla en H2; un error por cada tipo de excepción. La regla vive en un método del dominio; el controller la dispara.

---

**Cátedra:** ale.feltes@uc.edu.py · @alefeltes
