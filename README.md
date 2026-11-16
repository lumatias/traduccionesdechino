# Estudio Lu — estudiolu.com.ar

Sitio institucional (GitHub Pages) más las páginas de traducción pública de chino.

Páginas de traducción pública, estáticas, sin backend ni base de datos:

| Carpeta | Para quién | Qué hace |
|---|---|---|
| `traduccion-publica-chino/` | Público (indexable) | Landing bilingüe ES/中文. El formulario arma el pedido y lo abre en tu WhatsApp o correo. **No muestra precios.** |
| herramienta interna (fuera del repo) | Solo el traductor | Archivo local que genera el enlace del presupuesto y el mensaje de WhatsApp. No se publica. |
| `cotizacion/` | El cliente (enlace privado, `noindex`) | Presupuesto personalizado: detalle, total, entrega, validez, seña con Mercado Pago o alias, confirmación por WhatsApp, guardar en PDF. Todos los datos viajan en el enlace (`#…`), nada se guarda en el servidor. |

## Flujo

1. El cliente completa el formulario de la landing → te llega un mensaje estructurado por WhatsApp y adjunta el documento.
2. Abrís la herramienta interna en tu computadora, pegás el mensaje y apretás **Interpretar** (o cargás a mano). Ajustás precios, fecha y seña.
3. **Copiar mensaje** → lo pegás en el chat del cliente (o **Abrir WhatsApp del cliente** si cargaste su número).
4. El cliente abre su enlace, paga la seña por Mercado Pago o transferencia y confirma por WhatsApp.

## Publicar

1. Todo lo que está en `main` se publica solo en GitHub Pages (`estudiolu.com.ar`).
2. Las carpetas `traduccion-publica-chino/` y `cotizacion/` ya están enlazadas desde el menú.
3. La carpeta `interno/` está en `.gitignore` y nunca se sube.
4. Opcional: creá una imagen `og.jpg` (1200×630) en la misma carpeta para la vista
   previa en WhatsApp y redes, o cambiá la ruta en el JSON-LD y `og:image`.

## Cambiar precios y parámetros

Los precios viven **solo** en la herramienta interna (archivo local, bloque `CONFIG`):

| Clave | Qué controla | Valor inicial |
|---|---|---|
| `precios.personal / educacion / juridico` | Tu precio por foja (500 palabras) según tipo y dirección (`a_es` chino→español, `a_zh` español→chino). Se precarga al agregar un ítem; siempre podés pisarlo en la fila. | Arancel orientativo CTPCBA columna V, 1/9/2026 (reemplazalo por tus valores) |
| `legalizacion.simple / urgente` | Arancel CTPCBA por documento | $33.000 / $48.000 |
| `validezDias`, `entregaDiasHabiles` | Fechas que se precargan | 7 días / 4 días hábiles |
| `alias` | Alias o CBU que se precarga en cada presupuesto | vacío |
| `msg.es / msg.zh` | Plantilla del mensaje de WhatsApp al cliente | — |
| `publicBase` | URL pública de la página de presupuesto | `https://estudiolu.com.ar/cotizacion/` |
| `pin` | PIN para abrir la herramienta (solo disuasorio; la protección real es no publicar la URL) | vacío |

En `cotizacion/index.html` y `traduccion-publica-chino/index.html` el `CONFIG` solo tiene datos de contacto y la `matricula` (Tomo/Folio), que conviene completar en los dos.

Para el link de Mercado Pago: creá un "link de pago" por el monto de la seña desde la app de Mercado Pago y pegalo en el campo correspondiente; si lo dejás vacío, el presupuesto muestra solo el alias.

Fuentes de los valores iniciales:
- Aranceles: https://www.traductores.org.ar/matriculados/aranceles-orientativos/
- Legalizaciones: https://www.traductores.org.ar/publico/legalizaciones/

El CTPCBA actualiza aranceles unas tres veces al año (enero, mayo, septiembre).

## Idioma

- Por defecto español. Cambia a chino si el navegador del visitante está en chino,
  si la URL lleva `?lang=zh`, o si el visitante toca "中文" (se recuerda en el dispositivo).
- Para campañas dirigidas a la comunidad china, usá el enlace `…/traduccion-publica-chino/?lang=zh`.
- Los textos en chino están en el objeto `ZH` del script; los textos en español, en el HTML.

## SEO

- Título, descripción, canonical, Open Graph y datos estructurados (ProfessionalService + FAQPage) ya incluidos.
- Pendiente recomendado: perfil de Google Business Profile con la categoría "Traductor",
  y pedir reseñas a clientes que ya hicieron trámites.
