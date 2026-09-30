# Rúbrica de ejercicios — Lenguaje de Programación 3 (CYT646)

**Slug:** `rubrica-ejercicios-lp3-2026`  
**Vigencia:** segundo semestre de 2026, a partir del 30 de septiembre  
**Uso:** corrección en sala y calificación de los ejercicios de programación orientada a objetos, salvo que un enunciado declare otra escala.

Esta rúbrica es **general**. Cada ejercicio puntualiza el dominio (por ejemplo Minecraft o Counter-Strike 2) y las puertas HTTP, si las pide. Los ocho criterios se mantienen.

**Escala por criterio:** 0 = no se observa · 1 = parcial · 2 = cumple · 3 = sólido (el estudiante explica el diseño y este aguanta un cambio).

Ocho criterios × 3 puntos = **24** como máximo. Orientación: 0–11 insuficiente · 12–16 en proceso · 17–20 cumple · 21–24 destacado.

Pregunta de anclaje: *¿puede otra clase, u otra capa, dejar el objeto en un estado imposible?*

---

## 1. Entrega y arranque (0–3)

El repositorio existe, es público cuando el enunciado lo pide, y el proyecto se ejecuta como indica la consigna (por ejemplo `./mvnw spring-boot:run`). Lo generado por el compilador no se versiona. Falta de README o de licencia, si el enunciado los exige, baja el puntaje.

## 2. Organización en paquetes (0–3)

Las clases viven en paquetes cuyo nombre coincide con las carpetas. El dominio permanece separado de la entrada HTTP o de las demostraciones. Un compañero puede ubicar una clase sin preguntar.

## 3. Ocultamiento e invariantes (0–3)

El estado cambia por mensajes y constructores, no por asignación directa desde fuera. Las reglas del dominio (vida, munición u otras que fije el enunciado) se sostienen también ante valores borde.

## 4. Herencia y clases hijas (0–3)

Existe una relación «es un». Si el enunciado pide un método abstracto, la clase base lo declara y **dos clases hijas** independientes lo implementan. El código que usa el modelo trata a las clases hijas como el tipo padre; no arma el comportamiento con `if` o `switch` según el nombre de la clase.

## 5. Constructores y sobrecarga (0–3)

El objeto nace válido. La clase hija invoca al constructor del padre cuando corresponde. Si el enunciado pide sobrecarga, hay más de una firma y cada una deja el objeto en un estado legal.

## 6. Comportamiento observable (0–3)

Se cumple lo que el enunciado pide ver funcionar: una demostración, una prueba o, cuando hay API REST (interfaz HTTP), el `IndexController`, la construcción con parámetros de la URL y el JSON (*JavaScript Object Notation*) de las clases hijas. La capa de entrada no es dueña de las reglas del dominio.

## 7. Git (0–3)

El historial se puede leer. Los mensajes dicen qué cambió y por qué. Hay ramas o un pull request cuando el enunciado los pide. No hay un único commit que mezcle todo el trabajo.

## 8. Documentación y defensa (0–3)

El README o el diagrama pedido (por ejemplo Mermaid) coincide con el código. En Classroom se adjunta el archivo que pida el enunciado (Markdown, PDF o Word), con **especificaciones**, no con un transcript de chat. El estudiante explica, en pocas frases, qué quedó encapsulado.

---

## Cómo aplicarla en sala (cinco a siete minutos)

El revisor abre la entrega, ejecuta lo que el enunciado indica y mira la clase base junto con las clases hijas. Formula una pregunta de diseño. No se puntúa el aspecto visual de Spring ni un tutorial copiado: se puntúa si el dominio aguanta y si otra persona puede usar el resultado.

## Registro rápido

| Alumno | 1 Entrega | 2 Paquetes | 3 Ocult. | 4 Herencia | 5 Ctor | 6 Observable | 7 Git | 8 Docs | Total | Nota |
|---|---|---|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |  | /24 |  |

Ejercicio (slug): ________  
Dominio: ________  
Repo: ________
