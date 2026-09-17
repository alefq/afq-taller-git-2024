# Taller de Git y modelado orientado a objetos

**Asignatura:** Lenguaje de Programación 3 (CYT646)  
**Edición:** 2026

Hasta ahora el programa corría con un `main()` en *su* computadora. Esta práctica es el primer paso hacia algo que **otra persona puede usar**: una API HTTP (un servicio al que se le habla por la web, no haciendo clic en un `.java`).

El repositorio se **crea en GitHub** (con README y licencia Apache 2.0). Después se le pone adentro un **Spring Boot para API REST** generado en [start.spring.io](https://start.spring.io). Encima se versiona el modelado de Minecraft o Counter-Strike 2 (CS2) y se agregan controladores.

**La entrega de Git no es “rellenar el README” al inicio.** El README existe porque GitHub lo pide al crear el repo. Lo que se versiona primero son las clases. Al **final**, el mismo README debe mostrar el **diagrama Mermaid** de las clases del 2 y 3 de septiembre.

Pasar al chat del curso **el usuario de GitHub** antes de seguir.

---

## Parte A — Repo en GitHub, después Spring Boot

### A.1 Crear el repositorio en la web

En [github.com/new](https://github.com/new):

| Campo | Valor |
|---|---|
| Nombre | `INICIALES-taller-git-2026` (ejemplo: `af-taller-git-2026`) |
| Visibilidad | **Público** |
| README | **Sí** — marcar *Add a README file* |
| Licencia | **Apache License 2.0** |

Eso crea en la raíz un `README.md` (texto de portada del proyecto: en uno real irían tecnologías, cómo levantarlo, referencias) y un `LICENSE`. **Apache License 2.0** permite usar el contenido (incluso comercialmente), sin garantías; hay que acreditar a quien corresponda.

El README **no** es el ejercicio de POO. No se usa para “aprobar Git” escribiendo párrafos de más.

### A.2 Clonar (HTTPS)

En Linux o macOS: terminal. En Windows: **Git Bash**. Hasta la Parte G el remote es HTTPS. SSH va **después** de los controllers, y **solo en el host**.

```bash
git clone https://github.com/MI_USER_DE_GITHUB/INICIALES-taller-git-2026.git
cd INICIALES-taller-git-2026
```

### A.3 Identidad Git (una vez por máquina)

```bash
git config --global user.name "mi-usuario-de-Github"
git config --global user.email "mi-email-asociado-a-cuenta-de-github@email.com"
```

Más configuraciones: [wiki Git (Joko)](https://joko.miraheze.org/wiki/Git#Configuraciones).

### A.4 Meter el Spring Boot (API REST) *dentro* de ese clone

Abrir [start.spring.io](https://start.spring.io):

| Campo | Valor |
|---|---|
| Project | **Maven** |
| Language | Java |
| Spring Boot | 3.x (estable) |
| Group | `py.edu.uc.lp3` |
| Artifact | el **mismo** nombre del repo (`INICIALES-taller-git-2026`) |
| Packaging | Jar |
| Java | **21** |
| Dependencies | **Spring Web** (eso habilita la API REST) |

*Generate*, descomprimir. Copiar al clone (sin borrar `LICENSE` de GitHub): `pom.xml`, `mvnw`, `mvnw.cmd`, `.mvn/`, `src/`. El `.gitignore` del starter se une al del repo. El `README.md` de GitHub se deja; como mucho una línea de cómo arrancar (`./mvnw spring-boot:run`).

```bash
./mvnw spring-boot:run
```

Tiene que abrir en `http://localhost:8080`. Ctrl+C al terminar. Si no arranca, no se sigue.

No se borra la clase `*Application`. No se pega un tutorial entero de Spring.

Completar `.gitignore` con [gitignore.io](https://www.toptal.com/developers/gitignore) (`Java,IntelliJ,Maven`). No versionar `target/`, IDE ni la VM.

```bash
git status
git add -A
git status
git commit -m "chore: Spring Boot API REST desde start.spring.io"
git push
```

---

## Parte B — Subir el modelado previo (ejercicio de Git)

El ciclo `status` → `add` → `commit` → `push` se hace **con las clases del diagrama**, no editando el README.

### B.1 Copiar las clases

El starter dejó un paquete bajo `src/main/java/py/edu/uc/lp3/…`. **No se mueve** `*Application`. Al lado:

```text
src/main/java/py/edu/uc/lp3/
├── …/…Application.java
├── minecraft/     o     cs2/
└── web/           (los controllers van después)
```

Traer el modelado de POO-02 / POO-03. Ajustar `package` a las carpetas.

### B.2 Compilar y corregir

```bash
./mvnw -q compile
```

Suele fallar por `package` ≠ carpeta, `import` rotos, padre que no se copió, o Java ≠ 21 en el `pom.xml`. Corregir **el código**, no comentar la jerarquía. Hasta **BUILD SUCCESS**. Luego `./mvnw spring-boot:run`: tiene que levantar aunque aún no haya endpoints de dominio.

### B.3 Agregar, commit, push

```bash
git status
git add src/main/java/py/edu/uc/lp3/
git status
git commit -m "feat: modelado Minecraft|CS2 enganchado al Spring Boot"
git push
```

Más correcciones → **otro** commit (`fix: …`), no reescribir historia ya pusheada.

### B.4 Bitácora

```bash
git pull
git log
git checkout HASH    # primer commit (README+licencia) o el del Spring Boot
git checkout main
```

---

## Parte C — Colaboración

El repo del compañero también salió de GitHub (README + Apache 2.0) y tiene Spring Boot.

```bash
git clone https://github.com/USER_DEL_COMPAÑERO/INICIALES-taller-git-2026.git
cd INICIALES-taller-git-2026
git checkout -b INICIALES-contribucion-lp3
```

Ahí **no se toca el README**. Se agrega una especialización que no pise archivos, se compila, se arranca, `add` / `commit` / `push` de la rama, **Compare & pull request** a su `main`. El dueño revisa y mergea.

Pedido de cambio: el reviewer comenta; se corrige **código** en la **misma** rama y se pushea. El PR se actualiza solo.

---

## Parte D — Criterios del modelado

Tratar cualquier entidad o arma de forma uniforme **sin un `if` por cada tipo**.

1. **Ocultamiento.** El estado cambia por mensajes, no por asignación directa.
2. **Reglas en la clase.** Tras el constructor y cada mensaje, el objeto sigue válido.
3. **Herencia de comportamiento.** Si se sobreescribe, se decide si se llama al padre o se reemplaza.
4. **`private` por defecto.**

Pregunta del reviewer: *¿puedo dejar este objeto inválido desde otra clase o desde el controller?*

---

## Qué es un Controller (léase antes de programar)

Hasta ahora **ustedes** ejecutaban el programa. Un **controller** es la puerta por la que *otra persona o herramienta* (el navegador, Insomnia) le pide algo a su programa por HTTP: una dirección (`/`, `/api/…`) y a veces datos en la URL.

- El controller **no es el juego**. No calcula daño ni guarda munición. Recibe el pedido, **habla** con los objetos del dominio (constructores y métodos) y **devuelve una respuesta**.
- Esa respuesta, en una API REST, suele ser **JSON**: texto estructurado que una máquina lee. El navegador lo muestra; Insomnia también.
- Así aparecen “capas” sin magia: **entrada HTTP** (controller) / **reglas del dominio** (sus clases). Si para “hacer el endpoint” hay que abrir los campos `public`, la capa de reglas se rompió.

### `IndexController`

Es el portero de la casa: **`GET /`** (la raíz, `http://localhost:8080/`).

No construye Creeper ni AWP. Solo confirma que el servicio está vivo: quién lo hizo, si el dominio es Minecraft o CS2. Si esto no responde, el resto de la API no se prueba.

### El otro controller (construcción por URL)

Recibe parámetros en la query (`?nombre=…&vida=…`). Esos valores van al **constructor** (o fábrica) de **una** clase del modelo. Si el valor es ilegal, **la clase** lo rechaza; el controller no “arregla” el estado.

---

## Parte E — Los dos controllers

Cuando el modelado **compila y está commiteado**:

1. `IndexController` → `GET /` como arriba.
2. Un controller de construcción con parámetros de URL (`@RequestParam`), ruta a criterio, dominio propio.

Verificar compile + `spring-boot:run`, probar en el navegador o Insomnia, luego `add` / `commit` / `push` de las clases en `web` (o el paquete que usen). **No** hace falta pegar un tutorial de Spring: hace falta que se entienda *quién habla con quién*.

---

## Parte F — Método abstracto, dos hijas, JSON (paso final)

Aplicación práctica de **herencia**, **sobreescritura** y **ocultamiento**. No se copia un ejemplo de internet ni se pega código cocinado de un chat.

### Qué tiene que quedar andando

- En la **clase base** (la más general del dominio: entidad, arma, etc.) hay **un método abstracto**: un mensaje que *todas* las hijas deben saber responder, pero cuya *forma concreta* no la puede escribir el padre (cada tipo se comporta distinto).
- **Dos clases hijas independientes** (dos archivos, dos tipos reales del dominio) implementan ese método. Cada una informa *su* comportamiento. El estado sigue oculto: el método **no** es un getter disfrazado de todos los campos.
- Un **controller** (puede ser uno nuevo o ampliar el de la Parte E) responde **JSON** con el resultado de pedirle ese mensaje a **cada** hija. El controller trata a ambas como el **tipo padre**. No hay una ristra de `if (esCreeper)` / `if (esAWP)` para armar el texto: cada objeto informa el suyo.

Si el padre no era `abstract`, tendrá que serlo para poder declarar el método abstracto. Si solo había una hija, hay que crear la segunda.

### Cómo pedir ayuda a un agente (armar el prompt)

El agente no aprueba el práctico: **ustedes** tienen que poder explicar el diseño. Un prompt útil describe el *contrato*, no pide “regalame las clases”. Incluyan:

1. Contexto: Spring Boot 3, Java 21, paquete donde está *su* modelo (Minecraft o CS2), nombres **reales** de *su* clase base y de las dos hijas.
2. Pedido: método abstracto en la base cuyo nombre exprese un comportamiento común con realización distinta; implementación en las dos hijas; estado `private`; el controller pide el mensaje al tipo padre y arma un JSON con lo que cada una informó.
3. Restricciones: no abrir campos; no `if` por tipo en el controller para el texto del comportamiento; diff mínimo; no reescribir el resto del proyecto.
4. Cierre: “explicame en tres frases qué quedó encapsulado y por qué el padre no puede implementar ese método”.

Si la respuesta trae setters públicos para todo, un `switch` por nombre de clase, o un README en lugar de código, **no está lista**: se pide de nuevo con las restricciones, o se corrige a mano.

Verificar: compile, arranque, `GET /`, el endpoint de construcción, y el endpoint que lista/informa el comportamiento de las **dos** hijas. Luego commit.

---

## Parte F-bis — README: el diagrama Mermaid (paso final de documentación)

Cuando el código ya cumple la Parte F, el `README.md` de la raíz deja de ser solo la portada de GitHub. Debe **incluir el diagrama de clases en Mermaid** que armamos en las clases del **2 y 3 de septiembre** (POO-02 y POO-03): la jerarquía que cada quien eligió (Minecraft o CS2), actualizada si el método abstracto y la segunda hija cambiaron el diseño.

No es un ensayo ni un tutorial. Es el mismo modelo que ya dibujaron, escrito para que GitHub lo **dibuje** en la página del repo.

En el README, un bloque:

````markdown
```mermaid
classDiagram
  %% pegar aquí el diagrama de las clases del 2 y 3 de septiembre
```
````

Criterios:

- Se ve la clase base, las hijas y la relación de herencia (`<|--` en Mermaid).
- Coincide con lo que hay en `src/` (si agregaron la segunda hija o el método abstracto, el diagrama también).
- No hace falta documentar Spring, Git ni el controller en ese diagrama: solo el **dominio**.

Commit aparte, después de que el JSON de las dos hijas ya funciona:

```bash
git add README.md
git commit -m "docs: diagrama Mermaid del modelado (2 y 3 sep)"
git push
```

En el PR al compañero **no** se pisa su README para “ganar puntos”: el diagrama va en **su** repo.

---

## Parte G — SSH (después de los controllers, solo en el host)

La clave de GitHub se genera **en la máquina del desarrollador**. **No** en OpenCode ni en otra CLI de agente, ni en una VM/sandbox cuyo disco el agente lea.

Si el código se edita en Lubuntu / sandbox: el sync **host → runtime del agente** es SSH **desde el host**. El `git push` a GitHub sale del host. El agente no lleva `id_ed25519`.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Pública → GitHub → *SSH and GPG keys*. En el clone del **host**:

```bash
git remote set-url origin git@github.com:MI_USER_DE_GITHUB/INICIALES-taller-git-2026.git
git push
ssh -T git@github.com
```

---

## Descripción del PR (plantilla)

```markdown
## Dominio
Minecraft | CS2

## Qué se agrega
- Superclase y método abstracto: …
- Dos hijas y qué informa cada una: …
- GET /  → …
- GET (construcción por URL) → …
- GET (comportamientos) → JSON con las dos hijas
- README: diagrama Mermaid de las clases del 2 y 3 de septiembre

## Cómo probar
./mvnw -q compile
./mvnw spring-boot:run

## Revisión pedida
¿El controller usa el tipo padre o pregunta el tipo concreto?
¿Se puede romper el invariante desde el controller?
```

---

## Entrega en Classroom

Además del repositorio, se adjunta **un archivo** con las **especificaciones del ejercicio** (objetivo, consignas, criterios de aceptación, cómo probar). Formato: **Markdown (`.md`), PDF o Word (`.docx`)**. No se entrega un transcript de chat con un agente.

---

## Definition of Done

- [ ] Usuario de GitHub en el chat
- [ ] Repo **creado en GitHub** con README inicial y Apache License 2.0, público
- [ ] Spring Boot (Maven, Java 21, Spring Web) *dentro* de ese clone; `./mvnw spring-boot:run` funciona
- [ ] Modelado previo compilando; `add` / `commit` / `push` de **clases**, no del README
- [ ] `git log` y `checkout` de un hash, vuelta a `main`
- [ ] Rama y PR en el repo del compañero
- [ ] `IndexController` (`GET /`) y controller de construcción por URL
- [ ] Método abstracto en la base, dos hijas independientes, JSON con el comportamiento de cada una (sin `if` por tipo en el controller)
- [ ] `README.md` con el diagrama **Mermaid** de las clases del 2 y 3 de septiembre, alineado con el código
- [ ] Especificaciones del ejercicio **adjuntadas en Classroom** como un solo archivo **Markdown (`.md`), PDF o Word (`.docx`)** (no un transcript de chat)
- [ ] SSH **después**, en el **host**, no en el sandbox del agente

---

**Cátedra:** ale.feltes@uc.edu.py · @alefeltes
