# Biología, Hábitos y Control de Plagas de Granos Almacenados — Serviplagas

Capacitación web para técnicos de Serviplagas y personal de bodegas de granos.
Misma estructura que
[capacitacion-insectos-xilofagos](https://github.com/Servi-plagas/capacitacion-insectos-xilofagos):
un solo `index.html` sin dependencias de build, pensado para usarse desde el celular.

Contenido extraído de *Informe de capacitación: Biología, Hábitos y Control de las Plagas de
Granos Almacenados* (Serviplagas), en español sencillo y sin nombres científicos.

## Cómo funciona

1. **8 módulos** con poco texto y frases cortas: se explica la lógica (por qué se infesta el
   grano, cómo reconocer cada plaga, cómo inspeccionar y cómo se controla), no la terminología.
2. **Quiz de 8 preguntas** (una por módulo). Se aprueba con **6/8**.
   Antes de enviar, el técnico escribe su **nombre completo real**: se exigen al menos dos
   palabras, solo letras, y se convierte a formato título (`juan pablo pérez` → `Juan Pablo Pérez`).
   Las opciones se barajan en cada intento.
3. Al enviar el quiz se manda un correo automático a `informes.serviplagas@gmail.com` con el
   nombre, el puntaje y el detalle de cada respuesta (vía [FormSubmit](https://formsubmit.co),
   sin backend). La pantalla de resultados muestra si el envío salió bien y, si falla, ofrece un
   botón para reintentar.
4. Si aprueba, el técnico descarga un **certificado PDF** con logo, nombre, puntaje y fecha.
   Al generarlo se envía un segundo correo de confirmación. Si no aprueba, puede repasar los
   módulos y volver a presentar el quiz.

## Módulos e ilustraciones

Cada módulo abre con una **ilustración vectorial animada (SVG en línea)** que apoya el texto sin
repetirlo. Están escritas dentro de `index.html`, pesan pocos KB y funcionan sin conexión.

| Módulo | Qué muestra la animación |
|---|---|
| 1. ¿Por qué cuidar los granos? | Costales de arroz, trigo y maíz; aparecen gorgojos, se sale el grano y el medidor de calidad baja |
| 2. ¿Por dónde llega la plaga? | Camión que llega con el grano, polilla que entra por la ventana e insectos escondidos en residuos y grietas |
| 3. El gorgojo | Cuatro granos cortados: huevo → larva por dentro → adulto que sale → grano vacío, en «4 a 6 semanas» |
| 4. La polilla | Polilla volando, larva que deja hilos de seda y polvo fino, y trampa de feromonas que atrae adultos |
| 5. El escarabajo | Estiba con costales; debajo, polvo y grano partido con escarabajos y larva; una lupa recorre el rincón |
| 6. Inspección y monitoreo | Línea de tiempo con tres momentos (al recibir, durante, antes del lote nuevo) que se marcan con chulo |
| 7. Métodos de control | Tres paneles: físico (escoba, malla, humedad), químico (bodega sellada con gas y señal de peligro) y biológico (avispa y hongos) |
| 8. Programa integrado | Rueda de siete pasos que se encienden en orden: prevenir, detectar, identificar, corregir, controlar, verificar, documentar |

Los insectos se dibujan una sola vez (`<symbol id="ic-weevil">`, `ic-moth`, `ic-beetle`, `ic-larva`,
al principio del `<body>`) y se reutilizan con `<use>`. Las animaciones son CSS (clases `anim-*`)
y **se desactivan solas** si el dispositivo pide menos movimiento (`prefers-reduced-motion`).

`logo.png` viene del repositorio de xilófagos. El logo del certificado va **embebido en base64**
dentro de `index.html`, así que el PDF sale con logo incluso sin conexión.

## Publicar en GitHub Pages

> El documento fuente (`.docx`) está en `.gitignore`: solo se publica el sitio.

```bash
git add index.html logo.png README.md .gitignore
git commit -m "Capacitación: Plagas de Granos Almacenados"
git branch -M main
git remote add origin https://github.com/Servi-plagas/capacitacion-granos-almacenados.git
git push -u origin main
```

Luego en GitHub: **Settings → Pages → Source: `main` / `root` → Save**.

La app queda en `https://servi-plagas.github.io/capacitacion-granos-almacenados/`.

## Cambiar el correo de destino

Una sola línea en `index.html`:

```js
const NOTIFY_EMAIL = 'informes.serviplagas@gmail.com';
```

> Este correo ya está activado en FormSubmit por las otras capacitaciones.
> Si se cambia por uno nuevo, FormSubmit envía un correo de activación la
> primera vez que hay que confirmar.

## Ajustar el quiz

En `index.html`:

- `QUIZ_BANK` — las preguntas. `answer` es el índice de la opción correcta
  **antes** de barajar.
- `passingScore` — mínimo para aprobar (actualmente `6`).
- `totalQuestions` — debe coincidir con el número de preguntas.
