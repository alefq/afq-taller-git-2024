# Ejercicio POO-08 — CRUD REST, H2 e Insomnia

**Slug:** `ejercicio-poo-08-crud-h2-insomnia-2026-10-28`  
**Fecha:** 28 de octubre de 2026  
**Asignatura:** Lenguaje de Programación 3 (CYT646)  
**Rúbrica:** [RUBRICA-ejercicios-lp3-2026.md](RUBRICA-ejercicios-lp3-2026.md)  
**Enunciado anterior:** [ejercicio-poo-06-revision-paquetes-constructores-2026-09-30.md](ejercicio-poo-06-revision-paquetes-constructores-2026-09-30.md)  
**Guía de Git:** [github.com/alefq/afq-taller-git-2024](https://github.com/alefq/afq-taller-git-2024)

Este es el **trabajo práctico** de la segunda mitad del semestre. Sube la exigencia: el servicio deja de fabricar objetos en memoria para cada pedido y **guarda** el estado en una base **H2**. El cliente de prueba es una **colección de Insomnia** versionada en el repositorio.

El enunciado plantea preguntas. Las respuestas salen de su modelo, de la documentación de Spring Data y de lo que se discute en clase. No hay un único árbol de clases «correcto» copiado de un tutorial de empleados.

---

## Vocabulario

**CRUD** (*Create, Read, Update, Delete*) es el conjunto de cuatro operaciones sobre un **recurso**: crear, leer, actualizar y borrar. En una API REST esas operaciones se expresan con verbos HTTP sobre una URL que nombra el recurso, no la acción.

| Operación | Verbo HTTP típico | Recurso (ejemplo) | Código de éxito habitual |
|---|---|---|---|
| Crear | `POST` | colección, p. ej. `/api/mobs` | 201 Created |
| Leer uno | `GET` | ítem, p. ej. `/api/mobs/12` | 200 OK |
| Leer varios | `GET` | colección, con o sin filtro | 200 OK |
| Actualizar | `PUT` o `PATCH` | ítem | 200 OK |
| Borrar | `DELETE` | ítem | 204 No Content |

Si el ítem no está, **404**. Si el cuerpo rompe una regla del dominio, **400** (o el código que justifiquen en el README). El número de la URL es el identificador que asignó la persistencia, no un índice de una lista en el controller.

**H2** es un motor de base de datos relacional que corre **dentro** del proceso Java. En el taller alcanza con el perfil de desarrollo: el archivo (o la memoria) vive junto a la aplicación. Spring Boot lo conecta con `spring-boot-starter-data-jpa` y el driver de H2. **JPA** (*Java Persistence API*) describe cómo una clase se corresponde con una tabla. Un **repositorio** de Spring Data es, en la práctica, una **interfaz**: ustedes declaran los mensajes; el marco genera la implementación.

**Insomnia** es el cliente REST que ya usaron para `GET /`. Una **colección** agrupa pedidos (método, URL, encabezados, cuerpo JSON). Esa colección se exporta a un archivo y se sube al repositorio para que un compañero reproduzca las pruebas.

Las reglas del juego siguen viviendo en las **clases del dominio**. El controller traduce HTTP. El repositorio traduce filas. Ninguno de los dos asigna a mano la vida, la munición o el estado ilegal.

---

## Objetivo

Publicar un servicio HTTP con Spring Boot, sobre el modelado de **Minecraft** o de **Counter-Strike 2** que ya vienen trabajando, con:

1. persistencia en **H2** de al menos una familia con **herencia** (clase base y **dos** clases hijas);
2. un **CRUD REST completo** sobre esa familia;
3. al menos un **protocolo** (`interface`) que el servicio use para hablar con instancias de familias distintas, como en POO-07;
4. una **colección Insomnia** (o el export equivalente) en el repositorio, con un pedido por cada verbo del CRUD y un caso de error.

Un compañero clona, arranca con `./mvnw spring-boot:run`, importa la colección y recorre crear → leer → actualizar → borrar. Al reiniciar el proceso, lo que se guardó en el archivo H2 **sigue ahí** (si eligieron persistencia a archivo; si eligieron memoria, el README lo dice y explica la consecuencia).

---

## Contexto

Siguen en `INICIALES-taller-git-2026`. El proyecto ya tiene Spring Web. Ahora entra **Spring Data JPA** y **H2**. Los paquetes del template se mantienen: dominio en `domain`, entrada HTTP en `rest.controller`. La persistencia merece su propio paquete (`repository` o el nombre que justifiquen): ahí viven **interfaces**, no la lógica del Creeper ni del AWP.

La pregunta de anclaje del semestre se mantiene: *¿puede otra clase, u otra capa, dejar el objeto en un estado imposible?* Ahora hay una capa más: la fila de la tabla. Si JPA expone un setter público que acepta munición negativa, el invariante se rompió igual que si el controller asignaba el campo.

---

## Qué hay que pensar (antes de copiar anotaciones)

Estas preguntas se responden en el README, en frases propias. El código tiene que ser coherente con esas respuestas.

**Recurso y verbo.** ¿Cuál es el sustantivo de su API? ¿Por qué la URL nombra al mob o al arma, y el verbo HTTP dice qué hacer? ¿Qué ocurre si alguien pone `/api/crearCreeper`?

**Identidad.** ¿Qué campo es la clave? ¿La genera la base? ¿El JSON de creación lleva `id` o lo omite?

**Herencia y tablas.** JPA ofrece más de una forma de guardar una jerarquía (`SINGLE_TABLE`, `JOINED`, `TABLE_PER_CLASS`). ¿Cuál eligieron y por qué, en **su** dominio? ¿Dónde queda el discriminador, si lo hay? ¿Cómo se ve en el JSON que una instancia es Creeper y no Zombie (o AWP y no pistola)?

**Interfaz y repositorio.** El repositorio de Spring Data **es** una interfaz. ¿Qué gana el controller al depender de esa interfaz y no de una clase concreta de acceso a datos? Relacionen esto con el protocolo de POO-07: el servicio pide un mensaje; no necesita el apellido de la clase.

**Protocolo del dominio.** Además del repositorio, hay una `interface` **suya** (Explosivo, Recargable, Rastreable, o la que ya dibujaron). ¿Qué endpoint la usa? ¿El JSON de ese endpoint podría listar, en la misma colección, un Creeper y una dinamita, o un arma y un chaleco?

**Ocultamiento.** ¿Quién valida vida, daño o fecha? ¿El constructor, un método de dominio, una anotación de Bean Validation, las tres? ¿Qué prueba de Insomnia muestra que un `POST` con datos ilegales **no** deja una fila sucia?

**PUT y PATCH.** ¿Reemplazan el recurso entero o un subconjunto de campos? El README dice cuál eligieron y cómo se comporta un campo omitido.

**DELETE.** ¿Borrado físico o un estado «retirado» en el modelo? Si el dominio tiene un mensaje «romper» o «descartar», ¿el HTTP `DELETE` habla con ese mensaje?

---

## Consignas

Elegí **un** dominio —Minecraft o Counter-Strike 2— y trabajá sobre **tus** clases.

1. Dependencias y arranque: `spring-boot-starter-data-jpa`, driver H2, consola H2 habilitada en desarrollo. En `application.properties` (o YAML) se ve la URL de H2, el usuario y si `ddl-auto` crea el esquema. El README explica cada propiedad en una frase.

2. La clase base de la familia principal es persistible. **Dos clases hijas** independientes siguen siendo «es un» respecto del padre. El método abstracto de POO-06 **sigue existiendo** y se sobreescribe. Los constructores simples y sobrecargados siguen dejando el objeto legal. JPA necesita un constructor sin argumentos: investiguen cómo convive eso con el ocultamiento (pista: visibilidad del constructor vacío frente a los constructores de negocio).

3. Una **interfaz** de dominio (POO-07) con al menos un mensaje. Al menos **dos** clases, de **familias distintas** si el modelo lo permite, implementan esa interfaz. Un endpoint de lectura usa el tipo de la interfaz.

4. Un repositorio Spring Data para la clase base de la familia persistida. Los mensajes extra (`findBy…`) los inventan ustedes según el dominio: buscar mobs por bioma, armas por slot, etc. Esos métodos se declaran en la **interfaz**; no se implementan a mano.

5. **CRUD REST** sobre la colección de esa familia:

   - `POST` crea y devuelve el recurso con su `id`.
   - `GET` de la colección lista lo persistido (no una lista armada en el método).
   - `GET` por `id` devuelve un ítem o 404.
   - `PUT` o `PATCH` actualiza y persiste.
   - `DELETE` quita el ítem (o lo marca, si esa es la regla) y responde el código que documentaron.

   El controller habla con el repositorio y con el dominio. Si el cuerpo trae un tipo hijo, el JSON tiene que poder **discriminar** el subtipo (investiguen `@JsonTypeInfo` / un campo `tipo`, y expliquen la elección).

6. Un `IndexController` en `GET /` sigue confirmando que el servicio vive. Puede informar, en JSON, cuántos recursos hay persistidos.

7. Colección **Insomnia** en el repositorio (`insomnia/` o `docs/insomnia/`):

   - un entorno con la URL base (`http://localhost:8080` o la que usen);
   - un pedido por cada verbo del CRUD;
   - un `POST` que viola un invariante;
   - un `GET` o `DELETE` contra un `id` inexistente;
   - el pedido del endpoint que usa la **interfaz** de dominio.

   En el README: cómo importar la colección y el orden de ejecución (crear primero, copiar el `id`, seguir).

8. Diagrama Mermaid al día: familia, hijas, interfaz, repositorio, controller. El README distingue **herencia**, **implementación de interfaz** y **uso del repositorio**.

9. `BITACORA.md` con marca del asistente, modelo de LLM y resumen de prompts. Si no usaron IA, anótenlo.

10. Commits separados: dependencias y propiedades; entidades; repositorio; controller CRUD; colección Insomnia; README. Cada mensaje dice qué aporta el cambio.

---

## Qué no hace falta (todavía)

No se pide autenticación, ni PostgreSQL en un servidor aparte, ni operaciones batch de cien registros, ni una jerarquía de mappers de integración. Si aparece una excepción de dominio, un `@ControllerAdvice` suma; no reemplaza el CRUD ni el diagrama.

---

## Qué se entrega

Las cuatro piezas de la rúbrica, más la colección.

1. Enlace exacto al **commit** de la solución.
2. README: arranque, propiedades H2, diagrama, respuestas a las preguntas de «Qué hay que pensar», cómo importar Insomnia, sobrecarga y sobreescritura si cambiaron.
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

Consola H2: se puede abrir y **ver la tabla**. Una pregunta de anclaje: *si mañana cambiamos H2 por otra base, ¿qué archivos tocan y cuáles se quedan quietos?*

---

## Calificación

Rúbrica general: ocho criterios de 0 a 3, máximo **24**. En este práctico pesan especialmente:

- **2 Paquetes:** dominio, REST y repositorio separados.
- **3 Ocultamiento:** invariantes frente al JSON y frente a JPA.
- **4 Herencia:** familia persistida y sobreescritura.
- **6 Observable:** CRUD completo, H2 y colección Insomnia.

El criterio 6 pide ver **persistir de verdad**: un `GET` después de un `POST`, y la tabla en H2. Una lista creada dentro del método del controller **no** alcanza.

---

**Cátedra:** ale.feltes@uc.edu.py · @alefeltes
