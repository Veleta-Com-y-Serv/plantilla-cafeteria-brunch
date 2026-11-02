# Plantilla NoExpertise · Cafetería y brunch

Web cálida y a todo color para cafeterías, brunch, pastelerías, heladerías y panaderías, con carta y horario.

- Sectores: cafeteria, brunch, pasteleria, heladeria, panaderia. Estilo: cálido. Plan mínimo: gratis. Orden 220.
- Secciones: hero, franja, carta, sobre, galeria, horario, opiniones, encargos, preguntas, contacto (y `texto` para apartados nuevos).
- Diseño a ancho completo: portada partida 50/50 (mostaza con título enorme y foto a sangre con sello que gira), cinta corrida, franja de fotos de borde a borde, carta en banda café con el brunch sobre mostaza, foto a sangre en «Nosotros», galería tipo Instagram sin márgenes, horario en cifras enormes sobre mostaza, cita gigante, encargos con foto a sangre, contacto partido y pie espresso con festón de toldo. Tipografía redondeada muy pesada del sistema y botones píldora. Detalle en `DISEÑO.md`.
- Ejemplo: Café Almendro, cafetería ficticia en el Realejo de Granada.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD (`CafeOrCoffeeShop`) y preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; fotos a generar en `fotos.json` (13).

## Campos propios

| Sección | Campos |
|---|---|
| `hero` | `cta`, `cta_secundario`, `items` [{titulo}] (cinta corrida) |
| `franja` | `galeria` [rutas], `items` [{titulo, texto}] (pie de cada foto, por posición) |
| `carta` | `imagen`, `marca_destacado`, `menu_dia` {titulo, precio, texto}, `platos` [{nombre, texto, precio, categoria, destacado}] |
| `sobre` | `declaracion`, `texto`, `imagen`, `items` [{titulo, texto}], `cta` |
| `galeria` | `galeria` [rutas], `cta` |
| `horario` | `horario` [{dia, horas}] |
| `opiniones` | `testimonios` [{texto, autor, nota}] |
| `encargos` | `texto`, `imagen`, `items` [{titulo, texto}], `cta`, `cta_secundario`, `nota` |
| `preguntas` | `preguntas` [{pregunta, respuesta}] |

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.

## Páginas propias

- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
