# 🌺 Hawái 2026 — un viaje planeado con IA

> Planeación completa de un viaje familiar a **Oʻahu** (17 → 22 de agosto de 2026, 5 adultos),
> hecha en conjunto con un asistente de IA: desde comparar islas hasta cerrar el itinerario día por día.
>
> **The whole trip was planned with an AI assistant.** This repo is the artifact of that process —
> research, comparisons, a voting app for the family, and the final day-by-day plan.
> All personal data has been replaced with placeholders (see [Privacidad](#-privacidad)).

**Sitio:** https://juadolfob.github.io/hawai-islas/

---

## Qué es esto

No es un blog de viaje. Es el **rastro de trabajo** de planear unas vacaciones en familia
usando IA como copiloto — con los datos, las comparaciones y las decisiones que quedaron por escrito.

Empezó con una pregunta simple (*¿a qué isla vamos?*) y terminó en un itinerario cerrado,
con reservas hechas, presupuesto verificado y una app de votación para que los cinco opinaran.

## Cómo se hizo

**1. Investigación → datos estructurados.**
En vez de notas sueltas, todo se fue volcando a YAML: islas, hoteles, tours, precios,
ventanas de reserva, traslapes entre actividades. Un solo archivo como fuente de verdad
([`data/itinerario_hawai_2026.yaml`](data/itinerario_hawai_2026.yaml), ~1,700 líneas).

**2. Datos → sitio.**
De ese YAML salieron las páginas HTML: comparación de islas, catálogo de atracciones,
comparación de hospedaje e itinerario visual. Todo autocontenido — se abren sin servidor.

**3. Decisiones en familia.**
El problema real no era encontrar cosas que hacer, era **elegir entre demasiadas**.
Se armó un sistema de votación con estrellas sobre 115 actividades: cada quien elegía
"quién soy" y calificaba. Los votos vivían en una Realtime Database para que se
sincronizaran en vivo entre los cinco.

**4. Depuración por traslape.**
La parte más útil y menos obvia: detectar que muchas actividades **ya venían incluidas**
en otras. El Circle Island Tour traía Diamond Head, Halona Blowhole, Makapuʻu, Dole y
Sunset Beach; el Toa Lūʻau incluía la entrada a Waimea Valley. Ir marcando esos traslapes
evitó pagar dos veces por lo mismo y liberó días completos.

**5. Bitácora.**
Durante el viaje se registró lo que realmente pasó
([`docs/bitacora.md`](docs/bitacora.md)) — contra lo que estaba planeado.

## Qué hay aquí

| Archivo | Qué es |
| --- | --- |
| [`index.html`](index.html) | Comparación de islas — la portada |
| [`atracciones.html`](atracciones.html) | Catálogo de atracciones y tours, con votación por estrellas |
| [`comparacion_hospedaje.html`](comparacion_hospedaje.html) | Comparación de hoteles |
| [`itinerario_render_hawai.html`](itinerario_render_hawai.html) | Itinerario visual |
| `data/` | Las fuentes en YAML |
| `docs/` | Notas de trabajo, estado del plan y bitácora |
| `img/` · `audio/` | Recursos del sitio |

> Las rutas `img/` y `audio/` no se deben mover: los `.html` las referencian directamente.

## La votación, congelada

Los votos vivían en una base de datos en tiempo real para que la familia votara desde
sus teléfonos y se vieran los cambios al instante. Terminado el viaje, la base se apagó
y **los resultados finales quedaron incrustados directamente en el HTML**.

La interfaz sigue funcionando: puedes elegir quién eres y votar, pero ahora se guarda
solo en tu navegador (`localStorage`). Sin backend, sin llaves, sin nada que mantener.

## 🔒 Privacidad

Este repo fue privado durante la planeación porque contenía datos reales.
Antes de hacerlo público **se reemplazó toda la información personal**:

- Nombres → roles genéricos (`Papá`, `Mamá`, `Hijo 1`, `Hijo 2`, `Hijo 3`)
- Códigos de reservación, PNRs y números de confirmación → `XXXXXX`
- Correos, teléfonos, fechas de nacimiento y números de lealtad → placeholders
- Se eliminaron los PDFs de confirmación y el reporte de pago
- Se eliminó la configuración de la base de datos

El historial de git se reescribió desde cero, porque borrar los archivos no basta:
los datos siguen siendo recuperables en commits anteriores.

Los precios, horarios, rutas y opiniones sobre lugares son reales — esa parte es
justamente lo que puede servirle a alguien más.

## Si te sirve para tu propio viaje

Lo aprovechable sin cambiar nada: la comparación entre islas, el catálogo de
atracciones con precios y calificaciones, la comparación de hoteles en Waikīkī,
y sobre todo el **análisis de traslapes** — qué tours se pisan entre sí y qué
ya viene incluido en cuál.
