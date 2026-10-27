# Privacidad de Divisa&Go (extensión de Chrome)

*Actualizado: 27 de octubre de 2026 · Versión 1.5.0 · Responsable: Demkor Consultants / Danny Medina Coronel ([empresademkor@gmail.com](mailto:empresademkor@gmail.com))*

## En pocas palabras

Divisa&Go no tiene cuentas, analítica ni seguimiento propio. No se recopilan, venden ni transmiten datos personales. Las consultas solo envían el par de monedas y el periodo elegidos a los servicios indicados más abajo.

## Qué se guarda en tu navegador

- **Almacenamiento local de la extensión** (`chrome.storage.local`): únicamente el idioma elegido y las monedas favoritas, para recordarlas entre sesiones.
- **Almacenamiento de sesión de Chrome**: el importe, las monedas seleccionadas, el tema y el idioma aún no confirmado, para restaurarlos si se cierra el popup. Se borran al cerrar Chrome.
- **Memoria**: las cotizaciones solo permanecen en memoria y se vuelven a consultar al abrir el popup.
- Las preferencias locales se eliminan al borrar los datos de la extensión o desinstalarla.

## Qué se envía y a quién

| Servicio | Para qué | Qué recibe |
|---|---|---|
| Frankfurter (`api.frankfurter.dev`) | Tipos diarios y datos históricos del gráfico | Códigos de las monedas y el periodo |
| Banco Central Europeo (`data-api.ecb.europa.eu`) | Tipo de referencia oficial | Códigos de las monedas |
| Wise, Xe, TradingView | Tasas indicativas para comparar (lectura de sus páginas públicas) | Códigos del par |
| CoinGecko, Binance, Coinbase, Kraken | Precios cripto (solo al abrir esa sección) | Moneda y criptomoneda consultadas |

**Nunca se envía el importe que introduces.** Como en cualquier conexión web, esos proveedores pueden recibir datos técnicos de conexión (por ejemplo la dirección IP) y tratan las solicitudes según sus propias políticas de privacidad. El resultado solo se copia al portapapeles cuando pulsas el recuadro del resultado.

## Permisos

| Permiso | Uso |
|---|---|
| `storage` | Guardar idioma, favoritas y estado temporal del popup. |
| `clipboardWrite` | Copiar el resultado cuando pulsas el recuadro. |
| `sidePanel` | Anclar Divisa&Go como panel lateral si lo eliges. |
| Acceso a los servicios de tipos de cambio | Consultar las APIs indicadas arriba (solo lectura). |

## Código remoto

No. Todo el código va dentro del paquete; no se carga ni ejecuta código externo.

## Contacto

Para consultas sobre privacidad: [empresademkor@gmail.com](mailto:empresademkor@gmail.com). Más información: [divisaandgo.netlify.app/soporte](https://divisaandgo.netlify.app/soporte.html#privacidad).
