# Informe de Auditoría de Red Wi-Fi Insegura

## Introducción

En esta práctica analicé qué información queda visible al navegar por un sitio que utiliza HTTP. La idea fue comprobar por qué una conexión sin cifrado puede ser un riesgo, sobre todo cuando se usa una red Wi-Fi pública.

Para hacer la prueba utilicé las herramientas de desarrollador de Chrome, entrando en **F12 > Network** y revisando la solicitud principal que hizo el navegador.

## Sitio analizado

El sitio indicado para la práctica fue:

`http://neverssl.com`

Al entrar, el navegador lo marca como **Not secure** porque trabaja con HTTP y no con HTTPS.

Durante la prueba, NeverSSL me llevó a este subdominio:

`http://beautifulsublimeinnerplay.neverssl.com/online/`

## Evidencia observada

Después de abrir la pestaña **Network**, recargar la página y seleccionar la solicitud principal, pude ver los siguientes datos:

- **Request URL:** `http://beautifulsublimeinnerplay.neverssl.com/online/`
- **Request Method:** `GET`
- **Status Code:** `200 OK`
- **Remote Address:** `34.223.124.45:80`
- **Host:** `beautifulsublimeinnerplay.neverssl.com`
- **Referer:** `http://neverssl.com/`
- **Connection:** `keep-alive`
- **User-Agent:** información del navegador y del sistema operativo
- También aparecen otros headers como `Accept`, `Accept-Encoding` y `Accept-Language`.

El sitio utiliza **HTTP**. A diferencia de HTTPS, HTTP no cifra por sí mismo la información enviada entre el navegador y el servidor.

## Riesgos encontrados

El principal riesgo de navegar mediante HTTP en una Wi-Fi pública es que el tráfico no tiene el cifrado que aporta HTTPS.

Si un atacante logra interceptar el tráfico de la red, por ejemplo mediante un ataque de intermediario o **Man-in-the-Middle**, podría llegar a observar o modificar información transmitida por HTTP.

Entre los datos que pueden quedar expuestos están:

- La dirección o URL visitada.
- El host al que se conecta el navegador.
- El método HTTP utilizado, como `GET`.
- Los headers de la solicitud.
- Información del navegador a través del `User-Agent`.
- Datos enviados por una página si esta los transmite mediante HTTP.

Por eso no sería seguro ingresar contraseñas, datos personales o información sensible en un sitio que solamente utilice HTTP, especialmente desde una red pública.

## Cómo ayuda una VPN

Una VPN crea un **túnel seguro** entre el dispositivo y el servidor de la VPN. El tráfico se protege mediante **cifrado** y **encapsulamiento** antes de atravesar la red Wi-Fi pública.

Esto hace que una persona conectada a la misma red no pueda leer fácilmente el contenido que circula dentro de ese túnel.

Una VPN ayuda a:

- Proteger el tráfico mientras atraviesa una red pública.
- Evitar que otros usuarios de la misma Wi-Fi puedan leer directamente la información transmitida.
- Mejorar la privacidad frente a observadores de la red local.
- Reducir el riesgo de intercepción entre el dispositivo y el servidor VPN.

Igualmente, una VPN no reemplaza a HTTPS. Si el sitio final sigue utilizando HTTP, el tramo entre el servidor VPN y ese sitio continúa sin el cifrado propio de HTTPS.

## 3 Reglas de Oro para usar Wi-Fi pública

1. **Revisar que el sitio use HTTPS:** no ingresar contraseñas ni datos personales en páginas que aparezcan como no seguras.
2. **Usar una VPN cuando me conecto a una red pública:** así el tráfico viaja cifrado dentro de un túnel seguro hasta el servidor VPN.
3. **Evitar operaciones sensibles si no son necesarias:** no realizar pagos, iniciar sesión en cuentas importantes o enviar información privada desde una Wi-Fi pública si puedo esperar a tener una conexión más segura.

## Conclusión

Con esta práctica pude ver que una conexión HTTP deja visible bastante información sobre una solicitud, como la URL, el host, el método y distintos headers.

En una Wi-Fi pública esto puede convertirse en un riesgo si otra persona consigue interceptar el tráfico. El uso de HTTPS y una VPN agrega protección y hace mucho más difícil que terceros puedan leer la información que se está transmitiendo.
