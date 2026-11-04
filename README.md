# practica-wifi-segura
Informe de Auditoría de Red Wi-Fi Insegura

1. Introducción

El presente reporte técnico ha sido desarrollado desde la perspectiva de un auditor de seguridad junior con el objetivo de evaluar los riesgos asociados a la navegación en redes Wi-Fi públicas o no confiables.

Cuando nos conectamos a una red inalámbrica compartida (como la de un aeropuerto, cafetería o plaza pública), el medio de transmisión —el aire— es compartido por todos los dispositivos en el rango de alcance. A través de este informe se analiza la exposición de datos sensibles al navegar en sitios no cifrados (HTTP) y se detallan los mecanismos de protección mediante el uso de Redes Privadas Virtuales (VPN).

2. Sitio Analizado

Para llevar a cabo el análisis de tráfico y exploración de cabeceras, se examinó el comportamiento de navegación sobre el siguiente host:

Host / URL analizada: http://neverssl.com (http://ejemplo-inseguro.com)

Entorno de prueba: Herramientas de Desarrollador del Navegador (DevTools / Pestaña Network) y captura de paquetes.

3. Evidencia Observada

Durante la inspección de la primera solicitud enviada al cargar la página mediante la pestaña Network (Red), se capturaron y corroboraron los siguientes parámetros técnicos:

URL Solicitada: http://neverssl.com/

Protocolo Utilizado: HTTP / 1.1 (sin capa de cifrado TLS/SSL).

Método HTTP: GET

Host: neverssl.com

Headers Enviados:

Host: neverssl.com

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8

Accept-Language: es-ES,es;q=0.9,en;q=0.8

Información visible durante la solicitud:

Debido a la ausencia de cifrado, cualquier intermediario en la red puede visualizar abiertamente:

La dirección completa (URL) y el Host visitado: Se observa claramente qué sitio exacto está consultando el usuario.

El Método HTTP y las Cabeceras (Headers): Revela información sobre el navegador, sistema operativo (User-Agent) y tipo de contenido aceptado.

El cuerpo de la petición y respuesta (Payload): Toda información transmitida (datos de formularios, credenciales o cookies de sesión) viaja en texto plano.

4. Riesgos Encontrados

El uso del protocolo HTTP en una red Wi-Fi pública representa una vulnerabilidad grave debido a la falta de autenticación y confidencialidad. Los principales riesgos identificados son:

Intercepción de datos (Sniffing): Al ser una red inalámbrica abierta, un atacante cercano utilizando herramientas como Wireshark o tcpdump puede capturar los paquetes de datos que viajan por el aire y leer su contenido directamente, ya que la información equivale a una "postal escrita a mano".

Ataques de Intermediario (Man-in-the-Middle - MitM): Un ciberdelincuente puede interponerse entre el dispositivo de la víctima y el punto de acceso (router), interceptando o incluso modificando el tráfico transmitido sin que el usuario lo note.

Redes Gemelas Malignas (Evil Twins): Creación de un punto de acceso falso con un nombre idéntico o similar al del establecimiento (ej. "Starbucks_Gratis"). Si el usuario se conecta, todo su tráfico pasa directamente por el equipo del atacante.

Secuestro de Sesión (Session Hijacking): Las cookies de autenticación transmitidas en texto plano sobre HTTP pueden ser robadas para suplantar la identidad del usuario en servicios web sin necesidad de conocer su contraseña.

5. Cómo Ayuda una VPN

La implementación de una VPN (Virtual Private Network) transforma completamente el escenario de seguridad mediante los siguientes pilares técnicos:

Encapsulamiento y Túnel Seguro: La VPN crea un túnel de comunicación virtual entre el dispositivo del usuario y el servidor VPN remoto. Todos los datos salientes son encapsulados dentro de paquetes especiales antes de transmitirse por la Wi-Fi pública.

Cifrado de Extremo a Extremo (en el tramo local): Antes de salir del dispositivo, la información es procesada mediante algoritmos de cifrado robustos (como AES-256). Incluso si un atacante aplica sniffing o administra un Evil Twin, solo capturará datos ilegibles (ruido aleatorio).

Protección del Tráfico y Privacidad: La dirección IP pública del usuario queda oculta, adoptando la IP del servidor VPN. Asimismo, el proveedor de la red local (y cualquier intermediario) solo podrá observar que existe una conexión cifrada hacia una IP de VPN, pero no podrá saber qué sitios web o servicios específicos está consumiendo el usuario.

6. Las 3 Reglas de Oro para Navegar en Redes Wi-Fi Públicas

🔒 Utilizar siempre una VPN confiable: Activa un túnel VPN cifrado inmediatamente al conectarte a cualquier red Wi-Fi pública o abierta antes de iniciar cualquier sesión o navegación.

🌐 Verificar que los sitios utilicen HTTPS: Asegúrate de que todas las páginas web visitadas utilicen el protocolo seguro HTTPS (indicado con el candado en la barra de direcciones), evitando introducir credenciales o datos financieros en sitios HTTP.

🚫 Desactivar la conexión automática y el uso compartido: Configura tu dispositivo para que no se conecte automáticamente a redes Wi-Fi abiertas conocidas y deshabilita la visibilidad en red, la detección de dispositivos y el uso compartido de archivos/impresoras.
