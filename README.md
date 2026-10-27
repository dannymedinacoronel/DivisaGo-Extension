# Divisa&Go

Divisa&Go es una extensión de Chrome para convertir divisas desde un popup compacto bajo el icono de la barra superior. Permite buscar monedas por país, nombre o código, consultar tasas de referencia, comparar cuatro fuentes pequeñas y copiar el resultado con un clic.

## Funciones

- Catálogo dinámico de monedas con cotización disponible, banderas y nombres localizados. Las monedas se distinguen por país y código ISO; por ejemplo, USD es el dólar estadounidense y CAD el canadiense.
- Búsqueda sin distinguir mayúsculas ni tildes. Escribe un país, un nombre de moneda o un código como `CAD`.
- Monedas favoritas: marca la estrella junto a una moneda en el selector y aparecerá en accesos rápidos en la parte superior de ambos selectores. La lista se guarda localmente en Chrome.
- Conversión cruzada entre cualquier par cubierto por la fuente principal. El cálculo se hace en el dispositivo y el importe se guarda temporalmente en la sesión del navegador para recuperarlo si se cierra el popup.
- Conversión de una divisa a sí misma disponible incluso sin conexión, porque no requiere consultar tipos de cambio.
- Cuatro tarjetas compactas para el par seleccionado: BCE, Wise, Xe y TradingView. Cada referencia es independiente y puede no estar disponible para ciertos pares.
- Selector de idioma al abrir el popup: español, inglés, portugués, francés, alemán e italiano. La elección se guarda en el almacenamiento local de Chrome y se restaura automáticamente en siguientes aperturas.
- Si el popup se cierra, el importe, las monedas elegidas, el tema y el idioma de la sesión se restauran al volver a abrirlo. Estos datos temporales se borran al cerrar Chrome.
- Actualización manual de las referencias y actualización periódica de Wise, Xe y TradingView.
- Copia del resultado al pulsar el recuadro de conversión.
- Temas Rosa, Día y Noche. La selección no se guarda y se restablece al recargar el popup.
- Popup anclado al icono de la extensión en la barra superior; no abre una pestaña ni una ventana aparte. Se cierra al hacer clic fuera de él.

## Instalación y actualización

1. Ve a **[Releases](../../releases/latest)** y descarga `divisa-and-go-1.5.0.zip`.
2. Descomprime el ZIP en una carpeta que no vayas a borrar (Chrome la lee desde ahí).
3. Abre `chrome://extensions` y activa **Modo de desarrollador**.
4. Selecciona **Cargar descomprimida** y elige la carpeta descomprimida.
5. Pulsa el icono de Divisa&Go para abrir el popup debajo del icono.

Para actualizar, descarga el ZIP del último Release, sustituye la carpeta y pulsa el botón de recarga de Divisa&Go en `chrome://extensions`.

Al abrir el popup por primera vez, elige uno de los seis idiomas disponibles y pulsa **Continuar**. Divisa&Go recuerda el idioma en el almacenamiento local de Chrome; puedes cambiarlo desde el selector de la cabecera.

## Capturas

| | |
|---|---|
| ![Convertir](docs/capturas/captura-1-convertir-1280x800.png) | ![Calculadora](docs/capturas/captura-2-calculadora-1280x800.png) |
| ![Evolución](docs/capturas/captura-3-evolucion-1280x800.png) | ![Comparar fuentes](docs/capturas/captura-4-comparar-1280x800.png) |
| ![Cripto](docs/capturas/captura-5-cripto-1280x800.png) | ![Temas](docs/capturas/captura-7-temas-1280x800.png) |

## Tipos de cambio y referencias

### Conversión principal: Frankfurter

La conversión principal obtiene los tipos diarios de la API abierta de [Frankfurter](https://frankfurter.dev/), que recopila referencias de bancos centrales y otras fuentes oficiales. Divisa&Go solicita tasas con base en el euro dentro de un intervalo reciente que termina en la fecha UTC actual; así puede elegir la última observación válida aunque la API también publique fechas futuras. El par elegido se calcula localmente. La fecha de referencia se muestra junto al cambio. Si las dos monedas tienen fechas de observación distintas, se muestran las fechas correspondientes.

La consulta de tipos se cancela si no responde en 15 segundos, para que el panel no se quede cargando indefinidamente; puedes volver a intentarlo con el botón de actualización.

Si Frankfurter no responde o no ofrece una tasa para el par seleccionado, Divisa&Go usa la primera referencia reciente disponible en este orden: BCE, Wise, Xe y TradingView. La fuente utilizada aparece en pequeño junto al resultado y la tasa de referencia debajo; las tarjetas de las demás fuentes siguen mostrando sus propias referencias. Si ninguna alternativa está disponible, pero Frankfurter ya había devuelto tasas durante esta sesión, se conserva esa referencia en memoria y se identifica como última tasa recibida. Wise, Xe y TradingView son referencias indicativas y pueden no estar disponibles temporalmente.

El catálogo se adapta a las monedas disponibles en las respuestas del servicio y a los países asociados a cada código. La cobertura puede cambiar y no incluye necesariamente todas las monedas que existen. Si no hay una tasa reciente para el par ni una referencia alternativa disponible, el conversor lo marca como no disponible en lugar de inventar el dato. La API está disponible en [api.frankfurter.dev](https://api.frankfurter.dev/v2/rates?base=EUR).

Frankfurter es un agregador abierto, no un banco central. Sus tasas son referencias diarias y no cotizaciones en tiempo real, precios de compra garantizados ni necesariamente el importe final de una transferencia. La fiabilidad y fecha dependen de las instituciones proveedoras. Consulta la lista de [fuentes y proveedores de Frankfurter](https://frankfurter.dev/providers/).

### Tarjetas de referencia

Las cuatro tarjetas consultan el mismo par de monedas y muestran el resultado para una unidad. Si falta el tipo principal, también pueden servir como respaldo siguiendo el orden BCE, Wise, Xe y TradingView; la aplicación identifica junto a la conversión cuál está usando:

| Fuente | Cómo se obtiene | Fecha y disponibilidad |
| --- | --- | --- |
| Banco Central Europeo (BCE) | API pública oficial del [BCE](https://data.ecb.europa.eu/), tasas de referencia diarias frente al euro; Divisa&Go calcula el cruce. | Muestra la fecha oficial. Solo funciona cuando el BCE publica las dos monedas del par; su cobertura es menor que la del conversor. |
| Wise | Lectura de la página pública de conversión de [Wise](https://wise.com/). | Se muestra la hora de consulta de la página; no garantiza que la tasa se actualizara en ese instante. |
| Xe | Lectura de la página pública del conversor de [Xe](https://www.xe.com/). | Se muestra la hora de consulta y, cuando aparece, la hora de referencia publicada por Xe. |
| TradingView | Lectura de la página pública del par de [TradingView](https://www.tradingview.com/). | Se muestra la hora de consulta. La disponibilidad o el retraso pueden depender del instrumento y de su proveedor de datos. |

Las tarjetas de Wise, Xe y TradingView se consultan al cambiar el par, cada cinco minutos y al pulsar el botón de actualización. Sus páginas pueden cambiar, limitar solicitudes o no publicar la tasa esperada; por eso una tarjeta puede quedar temporalmente sin datos. Las lecturas de estas páginas públicas no son integraciones oficiales y sus tasas son indicativas: no garantizan el precio ni las comisiones de una operación. El BCE tampoco es una cotización en tiempo real. Comprueba siempre el importe final con el banco o proveedor donde realices el cambio.

El BCE suele actualizar sus tipos de referencia alrededor de las **16:00 CET cada día hábil**, excepto los días de cierre de TARGET. Son tipos diarios de referencia, no precios en tiempo real.

## Privacidad

Divisa&Go guarda en el almacenamiento local de la extensión de Chrome únicamente el idioma elegido y las monedas favoritas, para recordar esas preferencias entre sesiones. El importe, las monedas seleccionadas, el tema y el idioma aún no confirmado se guardan temporalmente en el almacenamiento de sesión de Chrome para restaurarlos si se cierra el popup; se borran al cerrar Chrome. Las cotizaciones solo permanecen en memoria y se vuelven a consultar al abrir el popup. No hay cuenta, analítica ni seguimiento propio. Las preferencias locales se eliminan al borrar los datos de la extensión o desinstalarla.

Para obtener tipos, se hacen solicitudes a Frankfurter y al BCE; para las otras referencias se solicitan páginas de Wise, Xe y TradingView. Se envían los códigos del par de monedas, pero **no el importe introducido**. Como en cualquier conexión web, los proveedores pueden recibir datos técnicos de conexión y tratar las solicitudes según sus propias políticas de privacidad. El resultado solo se copia al portapapeles cuando pulsas el recuadro del resultado.

## Interfaz e identidad

El icono de la barra sigue el diseño amarillo de Divisa&Go. Las banderas se incluyen como archivos SVG locales de [Twemoji](https://github.com/jdecked/twemoji), bajo licencia [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), para que se vean aunque el sistema no tenga fuentes de emoji con banderas.

## Créditos

Desarrollado por **Demkor Consultants**.  
Desarrollador principal: **Danny Medina Coronel**.


© 2026 Demkor Consultants. Todos los derechos reservados.
