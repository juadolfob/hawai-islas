# 🤖 Cómo planeamos el viaje con IA

Resumen puntual del método. Seis días en Oʻahu, cinco personas, planeado y ejecutado conversando con Claude.

---

## 1. Una sola fuente de verdad

- Todo vive en **`data/itinerario_hawai_2026.yaml`**: vuelos, hospedaje, segmentos por día, catálogo de atracciones, reservas, riesgos, pendientes.
- El sitio se genera a partir de ahí. Nada se edita en dos lugares.
- Se editó con `ruamel.yaml` para no perder los comentarios.

## 2. Investigación delegada

- Se le pidió a la IA que catalogara **las 43 atracciones del pase Go City** con calificación, número de reseñas, precio sin pase y si requerían reservación aparte.
- Lo mismo con hoteles, islas y tours de Viator.
- Resultado: comparar deja de ser abrir 30 pestañas y se vuelve ordenar una tabla.

## 3. Decidir con métricas, no con opiniones

- El número clave: **el pase costó ~$1,040 ÷ 4 cupos = ~$260 por cupo.**
- Regla que salió de ahí: **si una atracción cuesta menos de $50, no vale un cupo** — se compra por fuera.
- Descartó de golpe museos de $16, clases de yoga de $23 y rentas baratas que se veían tentadoras.

## 4. Votación familiar en vivo

- **`atracciones.html`** + una **Realtime Database** (durante la planeación).
- Cada quien entra desde su teléfono, elige quién es, y califica con estrellas.
- Los votos se sincronizan al instante — todos ven las preferencias de todos.
- Sin login, sin cuentas, sin app. Solo un link.
- **Hoy la base está apagada:** los resultados finales quedaron incrustados en el HTML y la votación se guarda solo en el navegador.
- Ordenable por precio, calificación o **demanda** (qué tan rápido se agota).

## 5. Análisis de traslape

- Se extrajo el itinerario **real** de cada tour reservado y se cruzó contra el catálogo.
- Ejemplo: el tour de Circle Island ya incluía Halona Blowhole, Sunset Beach, Dole Plantation y el almuerzo de camarones — cuatro candidatas que estaban listadas por separado.
- Las redundantes se atenuaron en gris **con la razón escrita encima**, no se borraron.
- Efecto: dejas de reconsiderar lo mismo cada vez que abres la lista.

## 6. Estado visible en todo momento

Sistema de insignias por CSS sobre cada tarjeta:

| Estado | Significado |
| --- | --- |
| 🟢 Verde | Incluida en el pase / reservada |
| 🔵 Azul | Acceso libre, no requiere pase |
| 🟡 Amarillo | Incluida pero barata — no gastes cupo |
| ⚪ Gris | Descartada, con la razón |
| 🔴 Rojo | Traslape muy alto con algo ya reservado |

## 7. Asistencia en vivo durante el viaje

Lo que más valor dio no fue la planeación previa:

- **Rutas con cronómetro** — comparar H-2 vs H-3 vs costera y decir cuál ruta costaba la cascada.
- **Cálculos de "¿nos da tiempo?"** — 45 minutos antes del check-in del lūʻau, con el sendero a 20-30 min por lado: no daba.
- **Recuperar información de correos** — el link del waiver de Kualoa enterrado en un mensaje del operador, media hora antes de que importara.
- **Detectar errores en reservas** — el quinto número de pase registrado era el número de orden, no una tarjeta. Habría costado el precio completo del tour.
- **Verificar en vez de suponer** — horarios de apertura, ventanas de reservación, si un lugar acepta walk-ins. Casi siempre había un detalle que cambiaba la decisión.

## 8. Bitácora separada del plan

- **`docs/ESTADO_ACTUAL.md`** = el plan.
- **`docs/bitacora.md`** = lo que realmente pasó.
- Mantenerlos separados evita que el plan se reescriba con la memoria de lo que salió, y deja ver dónde falló la estimación.

---

## Errores que cometimos

- **Reservamos el lūʻau dos veces** (Viator + directo). Se canceló a tiempo y el directo salió $172 más barato.
- **Subestimamos los check-ins.** 45 minutos antes, obligatorio, sin reembolso si llegas tarde. Aplica a casi todo.
- **Sobreplaneamos el día 2.** Terminó siendo un día partido donde cada quien hizo lo suyo — y fue el favorito de todos.
- **El repositorio estuvo público por error** con datos personales dentro. De ahí viene la sanitización.

## Lo que repetiríamos

- El YAML como fuente única.
- La votación en vivo — cambia la discusión de negociación a consenso.
- Atenuar en gris con la razón visible, en vez de borrar.
- Preguntarle a la IA **"¿nos da tiempo?"** antes de cada decisión con reloj.
