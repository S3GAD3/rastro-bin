# RASTRO BIN

**Consulta de prefijos BIN/IIN para la identificación del emisor de tarjetas bancarias.** Forma parte del kit RASTRO de investigación en fuentes abiertas.

[**Abrir RASTRO BIN**](https://s3gad3.github.io/rastro-bin/)

## Qué es y para qué sirve

El BIN/IIN es el prefijo que identifica un rango de tarjetas dentro de una red de pago. RASTRO BIN consulta ese prefijo en fuentes externas y presenta los datos disponibles sobre el emisor y la tarjeta.

En una investigación de fraude con tarjeta, el resultado ayuda a **orientar la identificación de la entidad emisora** a partir de un prefijo que conste en la documentación del caso. También permite contrastar el emisor, el país o el tipo de tarjeta con los datos facilitados por un comercio o un proveedor de pagos y documentar la consulta para su revisión posterior.

| Información | Según los datos de la fuente |
| --- | --- |
| Emisor | Nombre de la entidad, ciudad, sitio web y teléfono |
| Tarjeta | Red de pago, tipo de tarjeta, categoría comercial e indicador de prepago |
| País y divisa | País asociado al rango, código ISO y moneda indicada |
| Datos técnicos | Longitud del número de tarjeta y uso del algoritmo de Luhn en el rango |

## Cómo se utiliza

1. Abre [RASTRO BIN](https://s3gad3.github.io/rastro-bin/) e introduce únicamente el prefijo, de **6 a 8 dígitos**. Deja fuera el número completo de la tarjeta, la fecha de caducidad y el CVV.
2. Pulsa **Consultar**. La herramienta muestra la fuente de la respuesta y los datos que esta ha facilitado. Los campos vacíos aparecen como **Sin dato**.
3. Abre **Ver respuesta JSON original** para revisar lo devuelto por el proveedor o pulsa **Descargar JSON** para conservar la consulta. El archivo incluye el prefijo introducido, el modo de consulta, el proveedor, la URL de origen, la fecha y hora UTC de registro y la respuesta original.

### Si falla la consulta automática

Despliega **Importar respuesta manual de Binlist** con el prefijo ya introducido. Abre el enlace que genera la herramienta, copia el JSON que devuelva Binlist, pégalo en el cuadro de texto y pulsa **Mostrar datos**. La importación requiere que Binlist haya devuelto una respuesta JSON con datos.

## Cómo funciona la consulta

RASTRO BIN es una página HTML con JavaScript que se ejecuta en el navegador. La consulta automática prueba las siguientes rutas en orden y se detiene en la primera respuesta que contiene datos reconocibles.

| Orden | Ruta | Prefijo enviado |
| --- | --- | --- |
| 1 | HandyAPI, consulta directa | Primeros 6 dígitos |
| 2 | Binlist, consulta directa | Prefijo introducido |
| 3 | Binlist a través de CodeTabs | Prefijo introducido |
| 4 | Binlist a través de AllOrigins | Prefijo introducido |
| 5 | CardBinCheck a través de CodeTabs | Primeros 6 dígitos |

El navegador envía el prefijo a los proveedores y, cuando corresponde, a los servicios proxy indicados. La disponibilidad depende de la respuesta de esos servicios y de las restricciones que aplique el navegador a las peticiones entre dominios (CORS).

## Cómo interpretar el resultado

- **Comprueba la precisión del prefijo.** Si introduces ocho dígitos y la respuesta procede de HandyAPI o CardBinCheck, la fuente solo ha consultado los seis primeros. El prefijo que aparece en pantalla y en la exportación es el que introdujiste.
- **Trata la respuesta como un indicio.** Los proveedores pueden tener datos incompletos, desactualizados o discrepantes. El país corresponde al rango emisor y por sí solo no sitúa al titular ni a la operación.
- **Conserva la fuente y la fecha junto a la conclusión.** El resultado describe un rango de emisión. La identificación del titular o la confirmación de una operación requieren información de la entidad o del proveedor de pagos.

---

Creado por **S3GAD3** · Kit RASTRO
