# Plantilla «Cafetería y brunch» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **cálido**.
Todo en castellano de España, frases cortas, sin jerga. Brief de diseño completo en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = marrón café, acento = mostaza, fondo = crema, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`… Los derivados (`--oscuro` espresso del pie y la galería, `--claro`, `--suave`, `--crema`, `--tinta-acento` para el texto sobre mostaza, `--acento-legible`) se calculan con `color-mix` en `src/styles/global.css`.
- **Tipografías y aspecto general**: `src/styles/global.css` (redondeada del sistema muy pesada para títulos —`ui-rounded`, «Arial Rounded MT Bold», con respaldo a la sans del sistema—, sans del sistema para texto, botones píldora `.btn`/`.btn-sec`/`.btn--mostaza`, bandas `.banda--crema|clara|suave|cafe|oscura|mostaza`, festón de toldo `.feston`, mitades a sangre `.mitades`). Fuentes del sistema: no añadas fuentes externas.
- **Bandas**: `src/components/ui/Banda.astro` pinta una sección de borde a borde con el contenido en `.contenedor` (90 rem, 16 px de margen en móvil). Las mitades foto/texto (`.mitades`, `.mitad-texto`, `.mitad-foto`) dejan la foto tocando el borde de la ventana y alinean el texto con el contenedor.
- **Imágenes**: en `public/`. Fotos en `public/fotos/` (se generan a partir de `fotos.json`); si una foto de `/fotos/` falta, `Imagen.astro` muestra `/placeholders/<mismo nombre>.svg`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Personas: siempre `/placeholders/persona.svg`, nunca caras generadas.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = nombre en texto con un punto mostaza.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis). El pie enseña el nombre enorme, el horario, la dirección, el contacto, el menú y las redes.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`.
- `hero` → `secciones/hero.astro`: portada partida 50/50 (mostaza con título enorme | foto a sangre con sello redondo que gira) y cinta corrida con los `items`.
- `franja` → `secciones/franja.astro`: cabeza + fotos de `galeria` de borde a borde, con el pie de `items` en la misma posición.
- `carta` → `secciones/carta.astro`: banda café; bloque del brunch (`imagen` a sangre + `menu_dia` sobre mostaza) y `platos` por categoría.
- `sobre` → `secciones/sobre.astro`: texto + foto a sangre a la derecha; `declaracion` y valores (`items`).
- `galeria` → `secciones/galeria.astro`: cabeza espresso con botón a Instagram y cuadrados de borde a borde.
- `horario` → `secciones/horario.astro`: banda mostaza con las horas en cifras enormes y la dirección.
- `opiniones` → `secciones/opiniones.astro`: banda café, la primera opinión como cita gigante.
- `encargos` → `secciones/encargos.astro`: foto a sangre a la izquierda, pasos numerados y botón de WhatsApp.
- `preguntas` → `secciones/preguntas.astro`: acordeón `details/summary`; sin preguntas no se pinta.
- `contacto` → `secciones/contacto.astro`: mitad café con las vías de contacto y mitad crema con el formulario.
- `texto` → `secciones/texto.astro`: apartado genérico (`tipo: texto`), con foto a sangre si lleva `imagen`.

## Campos propios de esta plantilla (además del esquema común)
- `hero`: `cta` y `cta_secundario` (sin `cta` el botón llama; sin `cta_secundario`, «Cómo llegar» al mapa); `items` = detalles cortos (solo `titulo`) en la cinta corrida y en el sello.
- `franja`: `galeria` (rutas de las fotos, de borde a borde) e `items` [{titulo, texto}] = el pie de cada foto en el mismo orden (una ficha con `imagen` usa la suya). Hasta 4 fotos por fila.
- `carta.platos` [{nombre, texto, precio, categoria, destacado}]: se agrupan por `categoria` en el orden en que aparecen. `precio` SIEMPRE como cadena (`"4,80 €"`); vacío = sin etiqueta de precio. `destacado: true` pone la marca (`carta.marca_destacado`, por defecto «Favorito de la casa»).
- `carta.menu_dia` {titulo, precio, texto}: el brunch o desayuno cerrado, sobre mostaza; `texto` con una línea por plato (`|` en YAML). Sin `titulo` ni `texto`, no aparece. `carta.imagen`: foto a sangre junto al brunch.
- `sobre`: `texto` largo (párrafos separados por una línea en blanco), `imagen` vertical, `declaracion` (frase corta en grande) e `items` (valores: `titulo` + `texto`).
- `galeria`: `galeria` (6 fotos = una fila en escritorio; 4 u 8 = filas de 4) y `cta` (sin él, el botón va a `redes.instagram`).
- `horario.horario` [{dia, horas}]: sin él, se usa `contacto.horario`. Las horas con «Cerrado» salen apagadas.
- `opiniones.testimonios` [{texto, autor, nota}]: `nota` opcional (de dónde viene). Sin opiniones, la sección no se pinta. Sin estrellas ni notas.
- `encargos`: `texto`, `imagen`, `items` (pasos), `cta` (normalmente WhatsApp; sin él, el WhatsApp o el teléfono de contacto), `cta_secundario` y `nota`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. La cabecera es siempre sólida: no depende del orden.
3. **Cambiar textos, platos, precios, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Para agrupar platos usa `categoria`; para varios datos, una cadena. Máximo 24 elementos por lista.
5. **Nunca inventes** precios, cifras ni opiniones: si el cliente no los da, déjalos vacíos (los componentes lo soportan).
6. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`, con bandas (`.banda .banda--mostaza`…) como `src/pages/aviso-legal.astro`; enlázala en `site.yaml → menu`.
7. **Apartado nuevo**: añade `secciones.<id>` en `site.yaml` con `tipo:` = `texto`, `carta`, `galeria`, `franja`, `encargos`… (el diseño que quiera reutilizar). `src/pages/index.astro` lo recoge solo; no lo toques.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el de la cabecera), bandas a todo el ancho, 16 px de margen lateral del texto, botones de 44 px de alto como mínimo, sin scroll horizontal en móvil. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): ninguna.
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/<ruta>/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
