# Cafetería y brunch: brief de diseño

Plantilla `cafeteria-brunch` creada el 29/10/2026 a partir de `restaurante` con `php artisan plantillas:nueva` y
rediseñada entera (fila 6 del brief de la tanda «a ancho completo»). Este fichero se queda en el repo: es lo que lee
quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: cafeterías de barrio, sitios de brunch, pastelerías, heladerías y panaderías con obrador. Su cliente
  entra para ver la carta, saber si está abierto ahora y, el fin de semana, reservar el brunch o encargar una tarta.
- **Qué tiene que conseguir la web**: que se vea apetecible en un segundo y que el horario y la carta estén a mano;
  acciones: «Ver la carta», «Reservar brunch» (formulario o WhatsApp) y «Encargar por WhatsApp».
- **Tono y estilo** (`estilo: calido`): cálido, goloso y cercano. Sí: cartelería de cafetería de barrio, toldos,
  cartas de pizarra. No: la elegancia oscura de `restaurante` ni el «caja centrada con tarjetas blancas».
- **Ancho completo**: todas las secciones son bandas de borde a borde; fotos a sangre en mitades 50/50 y en franjas
  sin márgenes; contenido hasta 90 rem con 16 px de margen lateral en móvil.

## Concepto visual

- **Paleta de ejemplo**: primario `#5a3423` (marrón café), acento `#e0a526` (mostaza), fondo `#f6ecda` (crema),
  texto `#2a1b12`. Derivados con `color-mix`: espresso `--oscuro` (pie, cinta y cabeza de la galería), `--claro`,
  `--suave` (mostaza muy clara), `--tinta-acento` (texto sobre mostaza) y `--acento-legible` (mostaza oscurecida
  para textos sobre crema). Aguanta que el cliente cambie los cuatro.
- **Tipografía**: redondeada del sistema muy pesada (800/900) para títulos (`ui-rounded`, «SF Pro Rounded»,
  «Arial Rounded MT Bold», con respaldo a la sans del sistema), títulos de 2,75 rem en móvil y hasta 7 rem en la
  portada en escritorio; texto en la sans del sistema. Antetítulos en mayúsculas espaciadas con una raya mostaza.
- **Forma**: botones píldora; círculos mostaza para números, iconos y el «+» de las preguntas; **festón de toldo**
  (semicírculos del color de la banda asomando sobre la anterior) en la carta, el horario y el pie; sello redondo
  con el nombre en círculo que gira sobre la foto de portada; cinta corrida con los detalles del negocio.
- **Ritmo de bandas**: portada mostaza|foto → cinta espresso → franja crema con fotos a sangre → carta café →
  nosotros crema|foto → galería espresso + cuadrados → horario mostaza → opiniones café → encargos foto|claro →
  preguntas mostaza suave → contacto café|crema → pie espresso.

## Apartados (en orden)

1. `hero`: portada partida 50/50 (min. 92svh en escritorio). Título enorme, párrafo, dos botones; `items` en la cinta.
2. `franja` («El local»): fotos de `galeria` de borde a borde (barra, mesa, obrador) con el pie de `items` encima.
3. `carta`: banda café tipo pizarra; brunch del finde (`menu_dia`) sobre mostaza junto a una foto a sangre; `platos`
   por `categoria` con el nombre de la categoría a la izquierda (fijo al bajar) y los platos en 1-3 columnas con el
   precio en píldora mostaza y la marca «Favorito de la casa».
4. `sobre` («Nosotros»): texto con `declaracion` y valores numerados; foto a sangre a la derecha.
5. `galeria` («Fotos»): tipo Instagram, cuadrados sin márgenes (6 en fila en escritorio) y botón a Instagram.
6. `horario`: banda mostaza con las horas en cifras enormes, dirección y «Cómo llegar».
7. `opiniones`: banda café, la primera opinión como cita gigante y las demás en columnas.
8. `encargos`: tartas y bandejas; foto a sangre a la izquierda, pasos numerados, WhatsApp y nota.
9. `preguntas`: título a la izquierda y acordeón a la derecha.
10. `contacto`: partido a sangre (vías de contacto en café | formulario en crema).

## Fotos (`fotos.json`, 13)

Portada (mesa de mármol junto a la ventana con flat white y tostada), barra con máquina de espresso y vitrina,
desayuno completo cenital, obrador con cookies, brunch de fin de semana, interior de la cafetería en una casa
granadina, tarta por encargo y seis cuadradas para la galería. Luz de mañana cálida, tonos crema-mostaza-café,
sin texto legible, sin logotipos, sin personas.

## Qué no hacer

- Volver a la caja centrada estrecha con tarjetas blancas o al hero oscuro a pantalla completa de `restaurante`.
- Fuentes externas, dependencias nuevas o JavaScript más allá del de la cabecera.
- Precios, cifras u opiniones fijos en los componentes: todo sale de `site.yaml` y los componentes pintan bien vacíos.
