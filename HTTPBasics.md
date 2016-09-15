# HTTP (Protocolo de Transferencia de HiperTexto)

## Escencial
***


### Introducción
***

**LA WEB**

Internet (o la Web) es un sistema de información distribuído cliente/servidor masivo como el descrito en el siguiente diagrama:

![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/TheWeb.png)


Muchas aplicaciones están corriendo al mismo tiempo en la Web, por ejemplo un buscador/navegador web, correo electrónico, transferencia de archivos, transmisión de audio y video, etc.. Para que pueda haber una correcta comunicación entre el cliente y el servidor, estas aplicaciones deben seguir un protocolo específico de nivekl-aplicación tal como HTTP, FTP, SMTP, POP, etc..

**Protocolo de Tranferencia de HiperTexto (HTTP)**

HTTP(Protocolo de Transferencia de HiperTexto) es quizá el protocolo de aplicaciones más popular en Internet (o la Web).

+ HTTP es un *protocolo asimétrico de petición-respuesta cliente-servidor* como se ilustra. Un cliente HTTP envía un mensaje de petición a un servidor HTTP. El servidor, a su vez, regresa un mensaje de respuesta. En otras palabras, HTTP es un *protocolo de extracción*, el cliente *extrae* información desde el servidor (y el servidor *ingresa* información hasta el cliente).
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP.png)

+ HTTP es un protocolo sin estado. En otras palabras, la petición en curso no conoce qué fue hecho en las peticiones anteriores.

+ HTTP permite la negociación de tipos de datos y representación, a fin de permitir que los sitemas que se construyan de forma independiente de los datos que se tranfieren. 

+ Citando el RFC2616: "El protocolo de Transferencia de HiperTexto(HTTP) es un protocolo de nivel-aplicación para sistemas de información de hipermedia distribuídos, colaborativos. Es un protocolo genérico, sin estado que puede ser usado para muchas tareas más allá del hipertexto, tal como nombrar servidores y sistemas de gestión de objetos distribuídos,  a través de la extensión de sus métodos de petición, códigosde error y encabezados".

**Buscador**

Cada vez que se emite una dirección URL de su navegador para obtener un recurso web utilizando HTTP, por ejemplo `http://www.nowhere123.com/index.html`, el buscador convierte la URL en un *mensaje de petición* y lo envía al servidor HTTP. El servidor HTTP interpreta la petición, y regresa un mensaje de respuesta apropiado, el cual puede ser la respuesta a su petición o un mensaje de error. Este proceso se ilustra a continuación:
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_Steps.png)

**Localizador Uniforme de Recursos (URL)**

Una URL (Localizador Uniforme de Recursos) es usado para identificar de forma única un recurso en la web. Las URL tienen la siguiente sintaxis:
```
_protocolo://nombredelservidor:puerto/ruta-y-nombre-del-archivo_
```

Hay 4 partes en una URL:

1. _Protocolo:_ El protocolo de nivel-aplicaciín utilizado por el cliente y el servidor, por ejemplo, HTTP, FTP, y telnet.
2. _Nombre del servidor:_ El nombre del dominio DNS (p.ej., www.nowhere123.com) o la dierección IP (p.ej., 192.128.1.2) del servidor.
3. _Port:_ El número de puerto TCP que el servidor está escuchando para peticiones entrantes de los clientes.
4. _Ruta-y-nombre-del-archivo:_ El nombre y localización del recurso solicitado, bajo el directorio base de documentos del servidor.

Por ejemplo, en la URL http://www.nowhere123.com/docs/index.html, el protoclo de comunicación es HTTP; el nombre del servidor es www.nowhere123.com. El número del puerto no se especifica en la URL, y asume un número por defecto, que es el puerto TCP 80 for HTTP. La ruta y nombre del archivo que para el recurso a localizar es "/docs/index.html".
Otros ejemplos de URL son:
```
ftp://www.ftp.org/docs/test.txt
mailto:user@test101.com
news:soc.culture.Singapore
telnet://www.nowhere123.com/
```
**Protocolo HTTP**
Como ya se ha mencionado, siempre que se ingresa una URL en la bara de direcciones del buscador, el buscador traduce la URL en un mensaje de petición acorde a lo especificado en el protocolo; y encía el mensaje de petición al servidor.

Por ejemplo, el buscador traduce the la URL ```http://www.nowhere123.com/doc/indes.html``` en el siguiente mensaje de petición:
```
**Get /docs/index.html** HTTP/1.1
Host: **www.nowhere123.com**
Accept: image7gif, image/jpeg, */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
(blank line)
```
Cuando este mensaje de petición llega al servidor, el servidor puede tomar alguna de estas acciones:
1. El servidor interpreta la petición recibida, mapea la petición en un *archivo* bajo el directorio de documentos del servidor, y regresa el archivo solicitado al cliente.
2. El servidor intepreta la petición recibida, mapea la petición en el *programa* alojado en el servidor, ejecuta el programa, y regresa la salida del progrmama al cliente.
3. Si la petición no puede ser completada, el servidor regresa un mensaje de error.

Un ejemplo de un mensaje de respuesta HTTP es mostrado a continuación:
```
**HTTP/1.1 200 OK**
Date: Sun, 18 Oct 2009 08:56:53 GMT
Server: Apche/2.2.14 (Win32)
Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
ETag: "10000000565a5-2c-3e94b66c2e680"
Accept-Ranges: bytes
Content-Length: 44
Connection: close
**Content-Type: text/html**
X-Pad: avoid browser bug
**<html><body><h1>It works!</h1></body></html>
```
El buscador recibe el mensaje de respuesta, interpreta el mensaje y muestra el contenido del mensaje en la pantalla del buscador de acuerdo al tipo de medio de la respuesta (como en el tipo-de-contenido de la cabecera de respuesta). El tipo de dato común incluye "text/plain", "text/html", "image/gif", "image/jpeg", "audio/mpeg", "video/mpeg", "aplication/msword", and "application/pdf".

En su estado de reposo, un servidor HTTP no hace nada más que escuchar a la(s) dirección(es) IP y el (los) puerto(s) especificados en la configuración de la solicitud entrante. Cuando una petición llega, el servidor analiza el mensaje de cabecera, aplica las reglas especificadas en la configuración, y toma la acción aporpiada. El control principal del webmaster sobre la acción del servidor web es por medio de la configuración, el cual será tratado con mayor profundidar en secciones posteriores.

**HTTP cobre TCP/IP**

HTTP es un protocolo cliente-servidor de nivel-aplicación. Usualmente correo sobre una conección TCP, como se ilustra. (HTTP no necesita correr en TCP/IP. Sólo supone un transporte confiable. Se puede utilizar cualquier protocolo de transporte que proporcione este tipo de garantías.

![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_OverTCPIP.png)

TCP/IP (Contro de tranmisión de protocolos/Protocolo de Internet) es un conjunto de protocolos de tranporte y conexión de red para máquinas con el fin de comunicarlas entre las que estén en la red.

IP(Protocolo de internet) es un protocolo de capa-de-red, se ocupa de direccionamiento y enrutamiento de la red. En una red IP, a cada máquina se le es asignado una dirección IP única (p.ej., 165.1.2.3), y el software IP es responsable de enrutar en mendaje desde la fuente IP hasta el IP de destino.

En IPv4 (IP versión 4), la dirección de IP consiste en 4 bytes, cada uno con un rango de 0 a 255, separado por puntos, que es llamada la *forma quad-fotted*. Este esquema de numeración soporta arriba de 4G direcciones en la red. La última IPv6 (IP versión 6) soporta más direcciones. Como memorizar el número es difícil para la mayoría de la gente, utilizar un nombre de dominio, como www.nowhere123.com  es preferible. El DNS (Servicio de Nombre de Dominio) traduce el nombre del dominio al la dirección IP (por medio de tablas de búsqueda distribuídas). Una dirección IP especial es 127.0.0.1 siempre se refiere a nuestra máquina. El nombrede ese dominio es `"localhost"` y puede ser utilizado para *pruebas de bucle de retorno local*.

TCP (Protocolo de Control de Transmisión) es un protocolo-de-capa de transporte, responsable de establecer una conexión entre dos máquinas. TCP consta de 2 protocolos: TCP y UDP (Diagrama de Paquete de Usuarios). TCP es *fiable*, cada paquete tiene un número de secuencia, y se espera un acuse de recibo. Un paquete puede ser re-transmitido si no es recibido por el receptor.
La entrega de paquetes está garantizado en el TCP. UDP no garantiza la entrega de paquetes, y por lo tanto no es fiable. Sin embargo, UDP tiene menos sobrecarga de la red y se puede utilizar para aplicaciones tales como transmisión video y audio, donde la fiabilidad no es crítica.

TCP *multiplexa* aplicaciones sin una máquina IP. Para cada máquina IP, TCP soporta (multiplexa) arriba de 65536 puertos (or sockets), del puerto número 0 al 65535. Una aplicación, como HTTP o FTP, corre (o escucha) un número particular de puerto para peticiones entrantes. El puerto 0 al 1023 están pre-asignados para protocolos populares, p.ej., HTTP en el 80, FTP en el 21, Telnet en el 23, SMTP en el 25, NNTP en el 119, y DNS en el 53. El puerto 1024 y superior están disponibles para los usuarios.

A pesar de que el puerto 80 está pre-asignado para HTTP, como el puerto predeterminado para HTTP, esto no hace prohibitivo correr un servidor HTTP en un puerto asignado para usuario (1023-65535) por ejemplo 8000, 8080, especialmente para probar el servidor. De igual manera se pueden correr múltiples servidores HTTP en la misma máquina en diferentes números de puertos. Cuando un cliente ingresa una URL sin especificar explícitamente el número del puerto, p.ej, ```http://www.nowhere123.com/docs/index.html```, el buscador conectará al puerto predeterminado, el número 80, del servidor ```www.nowhere123.com```. Se necesita especificar explícitamente el número del puerto en la URL, p.ej, ```http://www.nowhere123.com:8000/docs/index.html``` si el servidor que se está escuchando está en el puerto 8000 y no en el puerto por defecto (puerto 80).

**Especificaciones HTTP**

Las especificaciones HTTP son sustentadas por [W3C (World-wide Web Consortium)](http://www.w3.org/ "W3C (World-wide Web Consortium)") y están disponibles en http://www.w3.org/standards/techs/http . Actualmente hay dos versiones de HTTP, llamadas, HTTP/1.0 y HTTP/1.1. La versión original, HTTP/0.9 (1991), escrita por Tim Berners-Lee, es un protocolo simple de tranferencia de datos crudos a través de Internet. HTTP/1.0 (1996) (definida en RFC 1945), mejorando el protocolo permitiendo los mensajes tipo MIME. HTTP/1.0 no se ocupa de los problemas de servidores de proxy, almacenamiento en caché de conexión persistente, servidores virtuales, y el rango de descarga. Estas características se proporcionan en HTTP/1.1 (1999) (definido en RFC 2616).

**Apache HTTP Server or Apache Tomcat Server**

Se necesita un servidor HTTP (como Apache HTTP Server o un Apache Tomcat Server) para estudiar el protocolo HTTP.
El servidor Apache HTTP es un servidor de producción industrial, hecho por Apahe Software Foundation (ASF) @ http://www.apache.org/ . ASF es una fundación de software de código libre. Lo que significa que el servidor de Apache HTTP es gratuito, con código fuente.

El primer sercidor HTTP está escrito por Tim Berners Lee en el CERN (Centro Europer de Investigación Nuclear) en Ginebra, Suiza, que también inventó HTML. Apche fue construidp en NCSA (Centro Nacional de Aplicaciones de Supercóputo, EE.UU.), el servidor"httpd 1.3", a principios de 1995. Apache probablemente recibe su nombre del hecho de que consiste en un código original (desde un servidor web httpd anterior NCSA) además de algunos parches; o del nombre de una tribu india americana.
Leer "[Apache How-to](https://www.ntu.edu.sg/home/ehchua/programming/howto/Apache_HowToInstall.html "Apache how-to") en cómo instalar y configurar un servidor Apache HTTP; o [Tomcat How-to](https://www.ntu.edu.sg/home/ehchua/programming/howto/Tomcat_HowTo.html) para instalar y empezar con el Servidor Apache Tomcat.

**HTTP Peticiones y Mensajes de Respuesta**

HTTP la comunicación entre el cliente y el servidor mediante el envío de mensajes de texto. El cliente envía un *mensaje de petición* al servidor. El servidor en turno regrea un *mensaje de respuesta*.

Un mensaje de HTTP consiste en una *cabecera de mensaje* y un *cuerpo de mensaje* opcional, separado por una *salto de línea*, como se ilustra a continuacuón:
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_MessageFormat.png)

**Mensajes de Peticiones HTTP**

El formato de un mensaje de petición HTTP es el siguiente:
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessage.png)

**Lineas de petición**
La primera línea de la cabecera se llama *línea de petición*, seguido de una *cabecera de petición* opcional.
La línes de petición tiene la siguiente sitaxis:

```https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessage.png```

+ request-method-name: El protocolo HTTP define una serie de métodos de petición, p.ej., GET, POST, HEAD, and OPTIONS. El cliente puede utilizar uno de esos métodos para enviar una petición al servidor.
+ request-URL: Especifica el recurso requisitado.
+ HTTP-version: Dos versiones son actualmente utilizadas: HTTP/1.0 y HTTP/1.1.

```

Ejemplos de líneas de petición:

```
GET /test.html HTTP/1.1
HEAD /query.html HTTP/1.0
POST /index.html HTTP/1.1
```
**Cabeceras de petición**
Las forma de nombrar las cabeceras de petición es en pares de valores. Los valores múltiples, seprados por comas, se pueden especificar.

```request-header-name: request-header-value1, request-header-value2, ...```

Un ejemplo de una cabecera de petición es:

```
Host: www.xyz.com
Connection: Keep-Alive
Accept: image/gif, image/jpeg, */*
Accept-Language: us-en, fr, cn
```


**Ejemplo**

La siguiente imagen muestra un ejemplo de un mensaje de petición HTTP
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_RequestMessageExample.png)

**Mensaje de respuesta HTTP**

El formato de un mensaje de respuesta se muestra a continuación:
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessage.png)

**Linea de Status**

La primera línea es llamada *línea de status*, seguido, opcionalmente, por las cabeceras de respuesta.
La línea de status tiene la siguiente sintaxis

```HTTP-version status-code reason-phrase```

+ HTTP-version: La versión HTTP utilizada en esta sesión. Puede ser HTTP/1.0 and HTTP/1.1.
+ status-code: un número de 3 dígitos generado por el servidor para reflejar el resultado de la solicitud.
+ reason-phrase: Da una pequeña explicación del estado del código.
+ Códigos de estado comunes y frases de resultado son "200 OK", "404 Not Found", "403 Forbidden", "500 Internal Server Error".

Ejemplos de línea de estado:
```
HTTP/1.1 200 OK
HTTP/1.0 404 Not Found
HTTP/1.1 403 Forbidden
```
**Cabeceras de respuesta**

Las cabeceras de respuesta están nombradas en valores pares.

```response-header-name: response-header-value1, response-header-value2, ...```

El cuerpo del mensaje de respuesta contiene los datos de los recursos solicitados.

**Ejemplo**

En la imagen se muestra un ejemplo de un mensaje de respuesta:
![alt text](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTTP_ResponseMessageExample.png)

**Métodos de Petición HTTP**
 --- 
El protocolo HTTP define una serie de métodos de petición. Un cliente puede utilizar uno de esos métodos para enviar mensajes de petición a un servidor HTPP. Los métodos son:
+ GET: Un cliente puede utilizar una petición GET para obtener un recurso web de unl servidor.
+ HEAD: Un cliente puede utilizar una petición HEAD para obtenert la cabecera que la petición GET obtuvo. Como la cabecera contiene las fecha de última modificación puede ser utilizado para ompararlo con la copia caché local.
+ POST: Es utilizado para publicar información en el servidor web.
+ PUT: Pide al servidor que almacene datos.
+ DELETE: Pide al servidor eliminar datos.
+ TRACE: Pide al servidor un rastreo de diagnóstico de las medidas que adopta.
+ OPTIONS: Pide al servidor que regrese una lista de métodos de petición que maneja.
+ CONNECT: Se utiliza para pedirle a un proxy que establezca una conexión con otro host y sólo debe responder el contenido, sin intentar analizar o almacenar en caché. Esto a menudo se utiliza para hacer la conexión SSL a través del proxy.
+ Otros métodos de extensión.

**Método de petición "GET"**
 ---
GET es el método de petición más común en HTTP. Un cliente use el método de petición GET para solicitar (u "obtener") una parte de un recurso en un servidor HTTP. Un mensaje de petición GET tiene la siguiente sintaxis:

```
 GET *request-URI HTTP-version
 (optional request headers)
 (blank line)
 (optional request body)*
```

+ La palabra clave GET es distingue entre mayúsculas y minúsculas.
+ *request-URI*: Especifica la ruta del recurso solicitado, la cual debe empezar desde la raíz "/" del directorio de la base de documentos.
+ *HTTP-version**: HTTP / 1.0 o HTTP / 1.1. Este cliente negocia el protocolo a utilizar para la sesión actual. Por ejemplo, el cliente puede solicitar el uso de HTTP / 1.1. Si el servidor no soporta el protocolo HTTP / 1.1, puede informar al cliente en la respuesta a utilizar HTTP / 1.0.
+ El cliente utiliza una cabecera de petición opcional (como Accept, Accept-Language, y etc.) para *negociar* con el servidor y perdirle que entregue contenidos de preferencia (por ejemplo, en el lenguaje de preferencia del cliente).
+ El mensaje de petición GET tiene un cuerpo de petición opcional que contiene la búsqueda (que será explicada después).

**Probar peticiones HTTP*
Hay varias formas de probar las peticiones HTTP. Se puede utilizar un programa como "telnet" o "hyperterm" (busque "telnet.exe" o "hipertrm.exe" en C:\Windows), o escriba su propio programa de la red para enviar mensaje de solicitud a un servidor HTTP para poner a prueba las diversas peticiones HTTP.

**Telnet**
"Telnet" es una utilidad de red muy útil. Puede utilizar telnet para establecer un TCP
