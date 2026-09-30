# Rúbrica de ejercicios — Lenguaje de Programación 3 (CYT646)

**Slug:** `rubrica-ejercicios-lp3-2026`  
**Vigencia:** segundo semestre de 2026, a partir del 30 de septiembre  
**Uso:** corrección en sala y calificación de los ejercicios de programación orientada a objetos. Si un enunciado trae otra escala, se usa esa.  
**Enunciado vigente:** [ejercicio-poo-06-revision-paquetes-constructores-2026-09-30.md](ejercicio-poo-06-revision-paquetes-constructores-2026-09-30.md)

Es la misma rúbrica para todos. El enunciado dice el dominio —Minecraft o Counter-Strike 2, por ejemplo— y qué servicios REST hay que ver. Los ocho criterios no cambian.

**Escala por criterio:** 0 = no se ve · 1 = a medias · 2 = cumple · 3 = sólido (se puede explicar el diseño y el diseño aguanta un cambio).

Ocho criterios × 3 puntos = **24** como máximo. Orientación: 0–11 insuficiente · 12–16 en proceso · 17–20 cumple · 21–24 destacado.

Pregunta de anclaje: *¿puede otra clase, u otra capa, dejar el objeto en un estado imposible?*

---

## Entregables

Para corregir hacen falta cuatro piezas. El enunciado puede fijar el nombre de un archivo; el contenido es este.

1. **Enlace exacto al commit de la solución.** Una URL de GitHub que apunta a un *commit* concreto, con el hash completo: `https://github.com/<usuario>/<repositorio>/commit/<hash>`. Ahí está el código que se califica.

2. **README al día.** Lo que pida el enunciado (licencia, diagrama Mermaid u otra cosa) y un apartado que cuente los cambios de **sobrecarga** y de **sobreescritura**: qué se agregó, en qué clases, y cómo se distingue una de la otra.

3. **Bitácora de asistencia de inteligencia artificial (IA).** Un `BITACORA.md` en la raíz del repositorio o en `docs/`, con tres datos:
   - la **marca** del asistente o agente (ChatGPT, Claude, Grok, Copilot, Cursor, OpenCode…);
   - el **modelo exacto** del *large language model* (LLM, modelo de lenguaje de gran tamaño), como lo muestra la herramienta (`gpt-4o`, `claude-sonnet-4.5`, `grok-4`…);
   - un **resumen de los prompts**, en frases propias.

   Si no usaste IA, anotalo en la bitácora.

4. **Especificaciones en Classroom.** Un archivo Markdown (`.md`), PDF o Word (`.docx`) con objetivo, consignas y forma de probarlo, aplicadas al dominio de cada uno. En la misma entrega va el enlace al commit.

El código está en el repositorio público que indique el enunciado. Si hay Spring Boot, el servicio arranca con el comando de la consigna (`./mvnw spring-boot:run` en este taller).

---

## 1. Entrega y arranque (0–3)

Hay repositorio, público si el enunciado lo pide, y el proyecto corre. Lo que genera el compilador queda fuera de Git. La entrega trae el **enlace exacto al commit**. README, licencia y bitácora, cuando el enunciado los pide, entran en este puntaje. De los tres puntos, **uno** es por puntualidad: llega en la fecha de Classroom.

## 2. Organización en paquetes (0–3)

Las clases viven en paquetes cuyo nombre coincide con las carpetas. Si el enunciado apunta a un template, las carpetas siguen ese árbol. El dominio queda aparte de la entrada HTTP. Un compañero encuentra una clase sin preguntar.

## 3. Ocultamiento e invariantes (0–3)

El estado cambia por mensajes y constructores, no por asignación directa desde fuera. Las reglas del dominio —vida, munición u otras que fije el enunciado— se sostienen también ante valores borde.

## 4. Herencia, clases hijas y sobreescritura (0–3)

Hay una relación «es un». Si el enunciado pide un método abstracto, la clase base lo declara y **dos clases hijas** independientes lo **sobreescriben**: misma firma, implementación propia. Quien usa el modelo habla con el tipo padre; el comportamiento queda en las clases hijas.

## 5. Constructores y sobrecarga (0–3)

Se construye una nueva instancia con **constructores simples y sobrecargados**. Cada firma deja el objeto en un estado legal. La clase hija llama al constructor del padre cuando corresponde. Si el enunciado pide además la sobrecarga de un mensaje del dominio, hay más de una lista de argumentos para la misma acción.

## 6. Comportamiento observable (0–3)

Se ve funcionar lo que pide el enunciado: una demostración, una prueba o, cuando hay API REST, el `IndexController`, la construcción con parámetros de la URL y el JSON (*JavaScript Object Notation*) de las clases hijas. La capa de entrada deja las reglas en el dominio.

## 7. Git (0–3)

El historial es legible. Los mensajes explican qué aporta (o elimina y por qué) el cambio. El commit enlazado es el de la solución que se revisa. Hay ramas o un pull request cuando el enunciado los pide. Se organiza el trabajo en commits separados en el que cada uno soluciona o una funcionalidad específica o una parte estable de funcionamiento.

## 8. Documentación y defensa (0–3)

El README coincide con el código, trae el diagrama pedido y **explica la sobrecarga y la sobreescritura**. La bitácora cuenta con qué asistente y qué modelo se trabajó, y resume los prompts. También vale escribir que no se usó IA. Classroom tiene las especificaciones y el enlace al commit. En la defensa, en pocas frases, se entiende qué quedó encapsulado.

---

## Cómo aplicarla en sala (cinco a siete minutos)

Se debe poder abrir el enlace al commit, leer el README y la bitácora. En cinco a siete minutos se ejecuta lo que pide el enunciado y se miran la clase base y las clases hijas. Una pregunta de diseño. Cuenta si el dominio aguanta y si otra persona puede usar el resultado.

## Registro rápido

| Alumno | 1 Entrega | 2 Paquetes | 3 Ocult. | 4 Herencia | 5 Ctor | 6 Observable | 7 Git | 8 Docs | Total | Nota |
|---|---|---|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |  | /24 |  |

Ejercicio (slug): ________  
Dominio: ________  
Repo: ________  
Commit: ________  
Bitácora: ________
