# Ejercicio POO-09 — Challenge de APIs cruzadas

**Slug:** `ejercicio-poo-09-apis-cruzadas-2026-11-16`  
**Fecha:** 16 de noviembre de 2026  
**Asignatura:** Lenguaje de Programación 3 (CYT646)  
**Enunciado anterior:** [ejercicio-poo-08-crud-h2-insomnia-2026-10-28.md](ejercicio-poo-08-crud-h2-insomnia-2026-10-28.md)  
**Formato de entregables:** [RUBRICA-ejercicios-lp3-2026.md](RUBRICA-ejercicios-lp3-2026.md) (commit, README, bitácora, especificaciones en Classroom)  
**Guía de Git:** [github.com/alefq/afq-taller-git-2024](https://github.com/alefq/afq-taller-git-2024)

**Navegación:** Enunciado · [Grupos](ejercicio-poo-09-grupos-2026-11-16.md) · [Ejemplo UNO](ejercicio-poo-09-ejemplo-uno-2026-11-16.md)

**Entrega individual. Nota individual.** Cada estudiante entrega **su** repositorio, con **su** escenario y **su** commit. El trío o el dúo sirve para acordar a quién se consulta. En Classroom, POO-08 era individual; este ítem también se califica por persona.

**Este ítem de Classroom vale 15 puntos.** Doce son este challenge. Tres son la corrección de POO-08. Esa parte **no** se vuelve a mirar con la rúbrica de 24.

**Defensa oral.** Es **otro** ejercicio de Classroom, **10 puntos**.

---

## Vocabulario

**OpenAPI** (antes Swagger) es un documento en JSON o YAML que describe la API: rutas, verbos, cuerpos, códigos de error. Quien consume necesita la URL de ese documento y que el servicio esté vivo.

**Cliente HTTP** es el código de *su* proyecto que habla con el servicio de un compañero. Cómo se implementa (cliente nativo, *starter* de Spring u otra librería) lo investigan ustedes.

**A1, A2 y A3.** A1 es *su* servicio (el que orquesta el escenario). A2 y A3 son los dos compañeros cuyas APIs consulta. En un dúo, A3 es el OpenAPI de un trío del mismo juego.

**Round robin.** Cada estudiante consume **dos APIs de compañeros** y publica **un** escenario propio que usa las validaciones de esas dos. El servicio propio no cuenta como uno de los dos consumos. Cómo se arman tríos, dúos y el resto 1 está en [Grupos](ejercicio-poo-09-grupos-2026-11-16.md). La forma del escenario (otro juego) está en [Ejemplo UNO](ejercicio-poo-09-ejemplo-uno-2026-11-16.md).

---

## Los 3 puntos de corrección de POO-08

No hay una segunda pasada con la rúbrica de 24. El enlace al documento de corrección está en el comentario privado del ítem POO-08 en Classroom.

| Situación | Los 3 puntos |
|---|---|
| La corrección no trae observaciones ni descuentos (puntaje completo, 24 de 24) | 3, en forma automática. README: «POO-08 con puntaje completo.» |
| Tiene observaciones o descuentos | 3 si está **todo** cerrado (README: cada ítem y cómo se cerró). Si queda alguno, 0. |
| Entregó POO-08 y no tiene el documento | 3 si el servicio de POO-08 está completo y anda: CRUD, simulación y los errores de las dos reglas. README: «No tengo el documento de corrección.» |
| No entregó POO-08 | 0. El challenge de 12 se puede hacer igual, con grupo. |

---

## Objetivo

En **su** repositorio, cada estudiante:

1. Cierra las observaciones de POO-08 si las hay (tabla de los 3 puntos) y publica el **OpenAPI** de su API, de modo que un compañero lo abra en el navegador o lo importe en Insomnia.
2. En un **grupo** acordado, consume **dos APIs ajenas** (A2 y A3) usando sólo ese documento OpenAPI y las reglas escritas.
3. Expone **un endpoint propio de escenario**: un pedido REST que tiene que pasar por las validaciones de ambos compañeros. Si las dos aceptan, **persiste la jugada** en su H2. Si una API rechaza, la base queda igual y el cliente ve de quién fue el rechazo.
4. Deja en `insomnia/` o `docs/insomnia/` la colección, y en el README el mapa del grupo.

El escenario es **posible en el juego** que el grupo eligió. Combina hechos que las dos reglas ajenas cuidan.

---

## Qué hay que pensar

Estas preguntas se responden en el README, con los nombres de **su** grupo y **sus** reglas. El enunciado no nombra clases, rutas ni librerías concretas.

**OpenAPI.** ¿Dónde vive su documento? ¿Qué operaciones de la simulación o de las reglas aparecen ahí, con descripción suficiente para que un extraño las invoque?

**Grupo.** ¿Quiénes son A1 (su servicio), A2 y A3? Si es un dúo, ¿quién comparte el segundo OpenAPI y de qué juego es? ¿Qué reglas publicó cada API que van a consultar, en una frase, con enlace al README o al OpenAPI del compañero?

**Escenario.** ¿Qué hecho del juego necesita **las dos** validaciones ajenas para ser legal? ¿Qué se ve en *su* base después de un escenario exitoso? ¿Qué queda igual si A2 acepta y A3 rechaza?

**Cliente.** ¿Cómo configura las URLs de A2 y A3 (propiedades, variables de entorno)?

**Errores.** ¿Propaga el código y el cuerpo que mandó el compañero, o los traduce a *su* jerarquía de excepciones? ¿El handler propio distingue «falló la API de A2» de «falló la de A3»?

**Límite.** El código fuente del compañero no se clona para copiar reglas. Si el OpenAPI no alcanza, se le pide al autor que complete el documento, no que pase una clase Java.

---

## Consignas

1. **Observaciones y OpenAPI propio.** Las observaciones de POO-08 se cierran según la tabla de los 3 puntos. Esta entrega **no** se vuelve a calificar con la rúbrica de 24. El servicio publica un documento OpenAPI 3. Investiguen cómo se habilita en Spring Boot. Las dos reglas y la simulación tienen que poder entenderse desde ese documento. Un compañero lo importa sin pedir el `.java`.

2. **Grupo y round robin.** Por defecto, tres repositorios del mismo juego. En el README de cada uno hay una tabla con nombres, rol (A1 / A2 / A3), URL base, URL del OpenAPI y las dos reglas del dueño, en una frase. El resto 2 o 1 se resuelve en [Grupos](ejercicio-poo-09-grupos-2026-11-16.md). La forma del escenario está en [Ejemplo UNO](ejercicio-poo-09-ejemplo-uno-2026-11-16.md).

3. **Dos clientes.** En *su* proyecto hay llamadas HTTP a A2 y a A3. Las URLs se configuran (propiedades o variables de entorno). El primer contacto con cada API es leer o importar el OpenAPI.

4. **Endpoint de escenario.** Un recurso REST *suyo* (nombre y verbo los eligen) que:
   - consulta a A2 y a A3 en un orden que justifiquen;
   - declara el escenario exitoso si **ambas** validaciones ajenas lo permiten;
   - **persiste la jugada** en *su* H2 cuando el escenario es exitoso (un `GET` posterior la muestra);
   - si una API ajena rechaza, deja su H2 igual que antes y atribuye el error.

5. **Insomnia.** Colección en `insomnia/` o `docs/insomnia/`: entorno o variables para las tres bases; pedido al OpenAPI propio; pedido al escenario feliz; un pedido que provoca el rechazo de A2 y otro el de A3. README con el orden (quién tiene que estar arriba primero). Conviene dejar **respuestas de ejemplo** exportadas (camino feliz y cada rechazo), para la corrección si un compañero no está en línea.

6. **Bitácora y commits.** `BITACORA.md` al día. Commits que separen: correcciones de POO-08; publicación de OpenAPI; clientes hacia A2 y A3; escenario; colección Insomnia.

El grupo puede correr en tres puertos de la misma máquina o en notebooks de la sala. El README dice cómo clonar y arrancar **los tres** commits.

---

## Si un compañero está apagado en la corrección

La cátedra puede clonar los tres commits del README y arrancarlos.

- Si el commit de A2 o A3 **no arranca**, esa persona pierde en OpenAPI y en escenario de **su** entrega. A1 no pierde esos 12 si su cliente está en el código, el README trae las URLs y la colección de Insomnia trae las respuestas de ejemplo del feliz y de cada rechazo.
- Si A2 nunca publicó OpenAPI, A2 pierde su criterio 1. A1 muestra el intento y lo que sí pudo probar con A3.
- A1 documenta en el README qué hizo cuando A2 o A3 no respondían (reintento, mensaje al compañero, respuestas guardadas).

---

## Cómo se prueba (sobre el commit)

Esta prueba alimenta los **15 puntos** de este ítem. La defensa oral es otro ejercicio.

1. README: si POO-08 tuvo puntaje completo (24 de 24), los 3 puntos ya están. Si había observaciones o descuentos, están **todos** cerrados.
2. Abrir los OpenAPI de A1, A2 y A3. Se entienden las reglas sin abrir el código.
3. Arrancar A1 (su servicio), A2 y A3 (los dos compañeros).
4. En A1, el escenario feliz: A2 y A3 aceptan y un `GET` en A1 muestra la jugada guardada.
5. Un caso en que A2 rechaza: el H2 de A1 queda igual; se ve de quién fue el rechazo.
6. Un caso en que A3 rechaza, simétrico.

Pregunta de anclaje: *si el compañero cambia el nombre de una ruta, ¿alcanza con actualizar lo que dice el OpenAPI, o había código copiado de su dominio?*

---

## Calificación de este ítem (15 puntos)

Sólo estos 15. La rúbrica de 24 de POO-08 **no** se aplica. La defensa oral es otro ítem.

**Corrección de POO-08 (3 puntos).** Puntaje completo (24 de 24): 3 en forma automática. Con observaciones o descuentos: 3 si está **todo** cerrado; 0 si queda algo. Sin documento: 3 si POO-08 está completo y anda (CRUD, simulación y los errores de las dos reglas). Sin entrega previa de POO-08: 0.

**Este challenge (12 puntos).** Cuatro criterios, 0 a 3 cada uno.

| # | Criterio | 3 puntos cuando… |
|---|---|---|
| 1 | OpenAPI | El documento propio describe CRUD, simulación y errores de las dos reglas. Un extraño puede invocarlo. |
| 2 | Round robin | El README muestra el mapa A1, A2 y A3. En un trío, los tres anotan las mismas tres URLs. El OpenAPI de un trío también lo puede usar un dúo. |
| 3 | Consumo | Hay llamadas reales a A2 y a A3, configuradas, leídas desde el OpenAPI. |
| 4 | Escenario persistido | Un endpoint propio combina ambas validaciones. El éxito **se guarda** en H2 y se vuelve a leer. El rechazo se atribuye y deja la base igual. Insomnia está en `insomnia/` o `docs/insomnia/` y cubre el feliz y un rechazo por compañero. |

Suma de este ítem: **15** (12 + 3). Orientación: 0–6 insuficiente · 7–10 en proceso · 11–13 cumple · 14–15 destacado.

**Entrega tardía.** El retraso se mide desde la fecha y hora del ítem en Classroom. El descuento sigue la sucesión de Fibonacci. Se resta de los 15. El descuento máximo es de 13 puntos. Con 50 horas o más de retraso, el trabajo no se corrige. La nota no baja de 0.

| Retraso | Descuento |
|---|---|
| Más de 0 y menos de 5 horas | 1 punto |
| De 5 a 10 horas (inclusive) | 2 puntos |
| Más de 10 y menos de 20 horas | 3 puntos |
| De 20 a 30 horas (inclusive) | 5 puntos |
| Más de 30 y hasta 40 horas | 8 puntos |
| Más de 40 y menos de 50 horas | 13 puntos |
| 50 horas o más | no se corrige |

---

## Qué se entrega

Las cuatro piezas del apartado «Entregables» de la rúbrica general, aplicadas a este challenge.

1. Enlace exacto al **commit** de la solución (observaciones cerradas si las había, escenario y clientes).
2. README: POO-08 con puntaje completo, o cada ítem cerrado, o que no hay documento; mapa A1/A2/A3, reglas citadas, URL de cada OpenAPI, cómo arrancar los tres servicios.
3. Bitácora de IA (BITACORA.md).
4. En Classroom: un archivo **Markdown (.md), PDF o Word (.docx)** con este enunciado aplicado a **su** entrega (quiénes son A1, A2 y A3; cuál es el escenario en una frase; cómo probarlo) y el enlace al commit.

El servicio arranca con `./mvnw spring-boot:run`.

---

**Cátedra:** ale.feltes@uc.edu.py · @alefeltes
