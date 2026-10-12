# landing-sg-sst-refresh

Reposicionamiento de la landing de Lina Fernanda Castillo hacia SG-SST: encabezado, "Sobre mí", servicios,
proceso formal, testimonios por caso y visibilidad bilingüe. Un solo archivo: `index.html` (sitio estático,
sin build ni tests; servidor local `python -m http.server 8080`).

## Specs

S1 · Nav (logo): nombre `Lina F. Castillo`; `<small>` = `Abogada - Especialista SG-SST`.

S2 · Hero, eyebrow (reemplaza "Asesoría Legal Profesional"): `Asesoría Legal Integral & SG-SST`.
El `<h1>` no cambia.

S3 · Hero, párrafo principal (`p.lead`), verbatim:
`Soy Lina Fernanda Castillo, abogada especialista en Seguridad y Salud en el Trabajo (SG-SST). Le acompaño a tomar decisiones legales seguras, con explicaciones claras, visión preventiva y una estrategia diseñada a su medida. Atención disponible en español e inglés.`

S4 · Hero, métricas (3, reemplazan 100%/24h/Online):
`100%` + `Atención personalizada` · `Bilingüe` + `Servicios en Español e Inglés` · `Online & Presencial` + `Asesoría flexible`.

S5 · Fotografías: los dos bloques (hero `.portrait` y "Sobre mí" `.about-media`) usan `img/lina-retrato.jpg`
(el retrato con gafas, 959x1024). `img/lina-oficina.jpg` queda sin uso.

S6 · "Mi compromiso" (`blockquote`), verbatim con la corrección gramatical `tranquilidad`:
`Mi prioridad es lograr una buena concertación y conciliación antes de acudir a un proceso judicial. Prevenir el conflicto protege la tranquilidad y el patrimonio de mis clientes.`
La cita `— LINA FERNANDA CASTILLO` no cambia.

S7 · Servicios: se agrega la tarjeta SG-SST **primera** en la retícula y se **elimina** "Derecho de Familia".
Títulos: `Sistema de Gestión de Seguridad y Salud en el Trabajo (SG-SST - PYMES)`.
Texto: `Diseño, implementación, auditoría y adecuación normativa del SG-SST para PYMES y microempresas. Garantizamos el cumplimiento de la norma colombiana, previniendo sanciones laborales y protegiendo el bienestar de su equipo de trabajo.`
No se agregan tarjetas de Cobro de Cartera ni de Organización Contractual.

S8 · "Cómo trabajo" (4 pasos, títulos y textos verbatim):
`01. Diagnóstico Inicial y Consulta` — `Evaluación analítica y confidencial de su caso para identificar riesgos, alcances normativos y las alternativas legales de solución.`
`02. Análisis Jurídico y Documental` — `Revisión detallada de antecedentes, contratos, títulos valores o normatividad aplicable, estableciendo las bases sólidas de la actuación.`
`03. Estrategia y Solución Concertada` — `Diseño de una hoja de ruta clara priorizando la conciliación y el acuerdo extrajudicial. Presupuesto y tiempos transparentes desde el primer momento.`
`04. Representación y Acompañamiento Continuo` — `Gestión legal directa, oportuna y transparente hasta la resolución satisfactoria de su caso, con informes periódicos del avance.`

S9 · Testimonios (3, con etiqueta de caso + estrellas + cita + atribución):
`Especialización en SG-SST` — `La Dra. Lina estructuró e implementó el Sistema de Gestión de Seguridad y Salud en el Trabajo (SG-SST) de nuestra empresa con absoluta rigurosidad normativa. Su conocimiento técnico y legal nos dio la tranquilidad de estar 100% protegidos y al día con el Ministerio del Trabajo.` — `Carlos M.` · `Gerente General / Implementación SG-SST`
`Cobro de Cartera (Factura, Pagaré, Letra de Cambio)` — `Excelente gestión en la recuperación de cartera morosa respaldada en facturas y pagarés. Gracias a su negociación persuasiva y estratégica, logramos el cobro efectivo sin llegar a un proceso judicial largo.` — `Active Media` · `Cobro de Cartera`
`Organización Contractual para Empleadores` — `Acompañó a nuestra compañía en la auditoría y reestructuración de todos los contratos de trabajo de nuestro personal. Su asesoría nos permitió organizar la relación contractual con los empleados de forma transparente, previniendo contingencias laborales.` — `Roberto S.` · `Director de Gestión Humana / Asesoría Corporativa`

S10 · Servicio bilingüe visible: franja fija arriba del nav con
`🌐 Legal Services Available in English & Spanish` + `Atención Legal Bilingüe`; y la línea
`Servicios de asesoría legal integral disponibles en español e inglés.` en la sección de contacto y en el footer.

## Tasks

T1 — S1-S6, S10: franja superior, offset del nav, hero (eyebrow, lead, métricas), nav logo, "Sobre mí"
(imagen + compromiso), nota bilingüe en contacto y footer. Route: inline. Estado: **cerrada**. retícula de servicios (alta SG-SST + baja Derecho de Familia), pasos formales, testimonios por caso.
Route: inline. Estado: **cerrada**.
T3 — Verificación. Route: inline (Node + `html.parser` + Edge headless vía CDP). Estado: **cerrada** con evidencia:
44/44 aserciones de S1-S10 sobre la página servida en `:8080` (y 10 aserciones negativas del copy retirado);
parseo sin tags sin cerrar ni errores de anidado; inventario 6 servicios / 4 pasos / 3 testimonios /
2 usos de `lina-retrato.jpg` / 2 notas bilingües; capturas headless de hero, `#sobre-mi`, `#servicios`,
`#proceso`, `#testimonios`, `#contacto` y móvil 420px con layout correcto.

Commits: T1–T8 y su verificación entraron en un solo work unit sobre `index.html` — `27d6f85` en la rama
`feat/landing-sg-sst-refresh` (el markup y el CSS de la misma página no se pueden separar sin dejar commits
intermedios rotos). Los documentos de `odd/` van en el commit siguiente.

T4 — S9 (reabre): la atribución del testimonio de Cobro de Cartera pasa a la empresa Active Media.
Route: inline. Estado: **cerrada** — respuesta del usuario: "La reseña la hizo Active Media". S9 actualizada:
autor `Active Media`, avatar `AM`, descriptor `Cobro de Cartera`; sale el nombre de Andrea G.

T6 — S9 (defecto reportado por el usuario): los tres bloques de autor de los testimonios deben quedar al
mismo nivel. Route: inline. Estado: **cerrada** — `.t-card` en flex column, cita con `flex:1` y descriptor con
`min-height:2lh` (reserva dos líneas) para que los tres bloques midan lo mismo. Medido con CDP:
avatares 808/808/808, nombres 795/795/795, descriptores 820/820/820, altura de bloque 69/69/69.

T7 — L8 (reevaluación integral del frontend): repaso visual/UX/estructura de toda la página.
Route: inline. Estado: **cerrada** con evidencia:
75/75 aserciones de S1-S10 sobre la página servida en `:8080` (incluye S7 verbatim y 15 negativas del copy
retirado); `overflow-x = 0` en 320/375/420/768/1024/1280/1440/1920; franja bilingüe de 34px en todos los
anchos; ningún anclaje tapado por la franja + nav; `:focus-visible` comprobado con Tab real (outline 2px
solid; el `outline-offset` se ve animado porque `.btn{transition:.3s}` transiciona todo); T6 sigue en pie
(tarjetas de testimonios 471/471/471 px y autores a la misma altura en 1024/1280/1440/1920).

Dos defectos reales encontrados **durante** esta verificación y arreglados en el mismo lugar:

- **D1 · etiquetas de contacto partidas (320 y 420px)**: `overflow-wrap:anywhere` en `.info-list` alcanzaba
tambien a los `<small>`, así que «CORREO» salía «CORRE / O» y «HORARIO» salía «HORAR / IO». Arreglo:
`white-space:nowrap` en `.info-list small` (los valores siguen partiendo donde haga falta: el correo a 320px
ocupa 3 lines y no desborda).
- **D2 · menú móvil tapando «Sobre mí» a 320px**: el panel era `position:fixed` con un offset fijo de 104px
que daba por sentado un nav de 93px; a 320px el `<small>` del logo envuelve a dos lines y el nav mide 110px
(fin del nav en 144px), así que el primer enlace quedaba detrás. Además, al scrollear el nav con
`backdrop-filter` pasa a ser bloque contenedor de descendientes `fixed`, y el panel saltaba 34px según el
estado de scroll. Arreglo sin número mágico: `position:absolute;top:100%;left:4%;right:4%` (el `nav` ya es
`position:fixed`, así que es el ancestro posicionado) → el panel queda pegado al borde inferior del nav en
todos los anchos y en los dos estados de scroll (medido: `menuTop == navBottom` en 320/375/420/768, arriba y
con scroll; ningún enlace tapado ni fuera del viewport).

Observación abierta, **no** tocada (decisión del usuario): el hero mide 1088px de alto, así que a 1440x900 y
1280x800 las tres métricas quedan 110px por debajo del pliegue (a 1440x1000, 10px). Viene del propio copy
aprobado (S3 en 5 lines + métricas S4) más las 24px extra de padding que la franja bilingüe agregó arriba.
Opciones acotadas: dar más ancho a la columna del `h1` en ≥1200px (pasa de 4 a 3 lines, ahorra ~90px) o
ajustar el `clamp()` del `h1`; ninguna se aplicó.

T8 — L11 (defecto reportado por el usuario): «quienes hacen la reseña no están iguales, en distintos
niveles, tamaños». Route: inline. Estado: **cerrada** — reproducido y medido con `cdp-talign.mjs` en 20
anchos antes de tocar. Tres causas concurrentes:

- **D3 · avatares elípticos (todos los anchos)**: `.t-author .av` no tenía `flex-shrink:0`, así que el
flexbox lo aplastaba a 28–38px de ancho manteniendo 42 de alto (a 1024 quedaba 29x42). Arreglo:
`flex-shrink:0` → círculos siempre 42x42.
- **D4 · banda 961–1049 (3 columnas angostas)**: el rótulo «Cobro de Cartera (Factura, Pagaré, Letra de
Cambio)» mide 452px en una línea y el contenido de tarjeta ahí es de 225px → envolvía a 3 líneas contra la
reserva de 2 (`min-height:2lh`) → estrellas y citas 19px más abajo en las tarjetas 2 y 3; y con el avatar
ya fijo en 42px, el descriptor «Director de Gestión Humana / Asesoría Corporativa» también pasaba a 3 líneas
(bloque de autor 91px vs 69px).
- **D5 · banda 601–960 (2 columnas con 3 tarjetas)**: 2 arriba + 1 huérfana abajo, con alturas distintas
(471/471/445 a 768) — la lectura directa de «distintos niveles, tamaños».

Arreglo (en `index.html`): `flex-shrink:0` en `.av`; `.t-grid` pasa a mobile-first (1 columna base) con
`@media(min-width:1080px){.t-grid{grid-template-columns:repeat(3,1fr)}}` — 1080 es el umbral medido a partir
del cual rótulo largo y descriptor entran en 2 líneas; y se retiró la banda de 2 columnas para testimonios
(servicios y proceso siguen en 2 columnas ≤960). Se probó y descartó una regla de banda `min-height:3lh`:
obligaba a reservar 3 líneas también al descriptor y desalineaba los autores de vuelta.

Evidencia: alineación medida en 16 anchos — ≤1079 apilado sin comparación lateral; ≥1080 alturas,
`authorRel`, `smallL`, `topicL` y `quoteL` iguales, avatar 42x42 y bloque de autor 69px en los tres; capturas
de `#testimonios` a 768/1024/1440 revisadas (a 1440 el corte feo «SG- / SST» desapareció: la línea ahora
corta antes de SG-SST); batería completa después del cambio: 75/75 aserciones, overflow 0 en 8 anchos, menú
móvil sin enlaces tapados en 4 anchos y 2 estados de scroll.

Nota menor: a ≤~340px el descriptor de la tarjeta 3 ocupa 3 líneas (apilado, sin vecina contra la que
desalinearse; sin recorte).

## Log

L8 (pedido del usuario, verbatim): "Reevalúa el frontend completamente, hay ciertos detalles que un poco
mal. usa la skill de impeccable si es necesario." → la skill `impeccable` NO existe en este entorno
(registro `.atl/skill-registry.md` y búsqueda en `~/.pi`, `~/.config/opencode/skills`, `~/.claude/skills`:
sin coincidencias), así que el repaso se hizo a mano. Ver T7.

L11 (pedido del usuario, verbatim): "mira donde que quienes hacen la reseña, no están iguales, se encuentra
en distinto niveles, tamaños." → T8 (avatares elípticos, banda 961–1049 desalineada, huérfana 2+1 en 601–960).

L10 (verificación de T7, 2026-10-12): la pasada quedó verificada y con dos arreglos propios (D1 etiquetas de
contacto partidas; D2 menú móvil tapando «Sobre mí» a 320px). Ver detalle y evidencia en T7. La skill
`impeccable` sigue sin existir en el entorno: el repaso se hizo a mano.

L9 (hallazgo de reconciliación, 2026-10-12): el texto de la tarjeta SG-SST en `index.html` NO es el de S7.
S7 pide: "Diseño, implementación, auditoría y adecuación normativa del SG-SST para PYMES y microempresas.
Garantizamos el cumplimiento de la norma colombiana, previniendo sanciones laborales y protegiendo el
bienestar de su equipo de trabajo." El archivo tiene: "...microempresas, con el cumplimiento de la norma
colombiana." → o se recortó en la pasada de T7 o T3 nunca comparó el texto completo. Requiere decisión del
usuario: restaurar S7 verbatim o enmendar S7.

L1 (pedido original, verbatim): ver `L1-pedido-original.md` — resumen exacto: 1) menú y hero (logo `Lina F. Castillo` /
`Abogada - Especialista SG-SST`, badge `Asesoría Legal Integral & SG-SST`, nuevo texto principal del hero con
especialización SG-SST y atención bilingüe, métricas `100%`/`Bilingüe`/`Online & Presencial`); 2) "Sobre mí" y
"Mi compromiso" (reemplazar la foto con lentes por el retrato oficial y nuevo texto de compromiso sobre
concertación y conciliación); 3) tarjeta adicional de servicios SG-SST para PYMES, con sugerencia de incluir
explícitamente Cobro de Cartera y Organización Contractual Empresarial; 4) redacción formal y corporativa de
"Cómo trabajo" en 4 pasos; 5) reemplazo de los tres testimonios por casos estructurados (SG-SST, Cobro de
Cartera, Organización Contractual); 6) mención global del servicio bilingüe (inglés) en barra superior/menú o
banner, y en footer y contacto. Aclaración final: "con la imagen me refiero a usar ambas donde sale con gafas".

L2 (respuestas del usuario, 4 preguntas): fotos → **ambas con gafas** (los dos bloques usan el retrato con
gafas); badge `Asesoría Legal Integral & SG-SST` → **eyebrow sobre el H1**; servicios → **"agrega SG-SST y de
primero y elimina la de 'derecho de familia'"**, sin tarjetas nuevas de Cobro de Cartera ni Organización
Contractual; mención bilingüe → **franja fina arriba del nav**.

L3 (decisiones del orquestador, para revisar): (a) S6 corrige `protege el tranquilidad` → `protege la
tranquilidad`; (b) se quita el `:` final de las etiquetas de caso en S9 (puntuación de lista, no de copy);
(c) se agrega `SG-SST (Seguridad y Salud en el Trabajo)` como primera opción del `<select>` "Área de interés"
del formulario, porque el servicio estrella no era capturable como lead — revertible en una línea;
(d) `Derecho de Familia` permanece en ese `<select>` (decisión de negocio, no de diseño);
(e) CSS: `.hero-stats` pasa a `flex-wrap` con tipografía menor y la franja superior desplaza el nav 34px
(hero a `9.5rem`, menú móvil a `104px`), más `scroll-margin-top:110px` en secciones por los anclajes.

L7 (defecto reportado por el usuario, verbatim): "Si te fijas la reseña del medio, no está al mismo nivel
 de las demás." → causa real: los tres bloques de autor no miden lo mismo (un descriptor de una línea contra
dos), así que alinearlos sólo por abajo (`margin-top:auto` o `flex:1` en la cita) no alcanzaba y dejaba el
testimonio del medio 26px más abajo. Solución: reservar dos líneas al descriptor (`display:block;
min-height:2lh`) y recién entonces el flex column los alinea por arriba y por abajo a la vez.

L6 (respuesta del usuario, verbatim): "La reseña la hizo Active Media" → S9 actualizada en consecuencia (T4 cerrada).

L5 (pedido del usuario, verbatim): "la reseña de Andrea G. relacionada al "cobro de cartera", cambiala por la empresa active Media." → afecta S9 (testimonio 2) y reabre T2 en su parte de atribución (T4).

L4 (cierre, 2026-10-12): verificación ejecutada — 44 aserciones de S1-S10 + 10 negativas contra la página
servida, `html.parser` sin errores de anidado, e inspección visual con Edge headless (CDP: `Emulation`,
reveal congelado en su estado final, `captureBeyondViewport`). Dos ajustes salieron de esa inspección:
(f) `.about-media img` pasa de `aspect-ratio:3/2; object-position:60% 30%` a `aspect-ratio:4/5;
object-position:50% 50%`: el retrato vertical cropeado a 3:2 dejaba la cara tapada por la tarjeta navy
superpuesta, que cubre el 45% inferior del bloque; (g) S7 quedó con 6 tarjetas (3×2) y el título largo de
SG-SST envuelve en 3 líneas sin romper la retícula. Ningún aspecto fuera del archivo `index.html` fue tocado.
