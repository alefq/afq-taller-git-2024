# POO-09 — Cómo se arman los grupos

**Navegación:** [Enunciado](ejercicio-poo-09-apis-cruzadas-2026-11-16.md) · Grupos · [Ejemplo UNO](ejercicio-poo-09-ejemplo-uno-2026-11-16.md)

La entrega y la nota son **individuales**. El grupo sirve para acordar a quién se consulta. A1 es *su* servicio. A2 y A3 son los dos compañeros cuyas APIs consulta.

El grupo habitual es de **tres** personas, **mismo juego** (Minecraft con Minecraft, CS2 con CS2). En un trío cada uno consulta a los otros dos.

```text
Ana consulta a Bruno y a Carla, y publica un escenario
Bruno consulta a Carla y a Ana, y publica un escenario
Carla consulta a Ana y a Bruno, y publica un escenario
```

Ana es A1 de su entrega. Bruno y Carla son su A2 y su A3.

Se agrupa por juego. El tamaño sale del **número de trabajos de ese juego**, no de un cupo fijo del curso.

| Resto al armar tríos | Qué se hace |
|---|---|
| 0 | Sólo tríos. |
| 2 | Un dúo. Cada integrante consulta al compañero y a un OpenAPI de un trío del **mismo** juego. |
| 1 | Esa persona se suma a un trío y el grupo queda de **cuatro**. En un grupo de cuatro, cada uno consulta a **dos** compañeros del grupo y lo documenta. Cada servicio del grupo lo consulta al menos un compañero. |

Ejemplo. Si un juego tiene 14 trabajos: cuatro tríos y un dúo. Si tiene 13: cuatro tríos y una persona que se suma a un trío (grupo de cuatro). Si tiene 18: seis tríos.

Un alumno no entrega este challenge sin grupo.

**Qué hace el dúo.** Siguen haciendo falta **dos servicios ajenos** por persona. Entre Ana y Bruno, el dúo, sólo hay un compañero. El segundo servicio lo piden a alguien de un **trío del mismo juego**. Esa persona ya tiene su round robin; les deja usar su OpenAPI.

Ejemplo. Ana y Bruno hacen Minecraft. Diego, Elena y Fabio son un trío de Minecraft. Diego acepta que el dúo consulte su API.

```text
Ana consulta a Bruno y a Diego, y publica un escenario
Bruno consulta a Ana y a Diego, y publica un escenario
Diego sigue consultando sólo a Elena y a Fabio
```

Ana y Bruno anotan en el README las tres URLs y, en una frase cada una, las reglas que usaron. Diego anota: «Mi OpenAPI también lo consultan Ana y Bruno.» El round robin de Diego, Elena y Fabio no cambia. En el dúo, A3 es ese OpenAPI del trío.

---

**Cátedra:** ale.feltes@uc.edu.py · @alefeltes
