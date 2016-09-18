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
+ *HTTP-version*: HTTP / 1.0 o HTTP / 1.1. Este cliente negocia el protocolo a utilizar para la sesión actual. Por ejemplo, el cliente puede solicitar el uso de HTTP / 1.1. Si el servidor no soporta el protocolo HTTP / 1.1, puede informar al cliente en la respuesta a utilizar HTTP / 1.0.
+ El cliente utiliza una cabecera de petición opcional (como Accept, Accept-Language, y etc.) para *negociar* con el servidor y perdirle que entregue contenidos de preferencia (por ejemplo, en el lenguaje de preferencia del cliente).
+ El mensaje de petición GET tiene un cuerpo de petición opcional que contiene la búsqueda (que será explicada después).

**Probar peticiones HTTP**

Hay varias formas de probar las peticiones HTTP. Se puede utilizar un programa como "telnet" o "hyperterm" (busque "telnet.exe" o "hipertrm.exe" en C:\Windows), o escriba su propio programa de la red para enviar mensaje de solicitud a un servidor HTTP para poner a prueba las diversas peticiones HTTP.

**Telnet**

Se puede utilixar telnet para establecer conecciones TCP con un servidor, y emitir peticiones HTTP puras.  Por ejemplo, suponga que ha comenzado su servidor HTTP en la máquina local (la dirección IP 127.0.0.1) en el puerto 8000:

```
 > **telnet**
 telnet> **help**
 ... telnet help menu ...
 telnet> **open 127.0.0.1 8000**
 Connecting To 127.0.0.1...
 **GET /index.html HTTP/1.0**
 *(Hit enter twice to send the terminating blank line ...)*
 ... HTTP response message ...
```

Telnet es un protocolo basado en caracteres. Cada caracter que se introduce en el cliente-telnet se enviará inmediatamente al servidor. Por lo tanto, no se puede hacer un error tipográfico al ingresar comandos puros, como borrar y la tecla de retroceso que se envían al servidor. Puede que tenga que activar la opción de "loal echo" para ver los caracteres que ingresa. Consulte el manual de telnet (ayuda de búsqueda de Windows) para obtener más información sobre el uso de telnet.

**Programa de red**

También puede escribir su propio programa de red para emitir peticiones puras de HTTP a un servidor HTTP. El programa de la red deberá establecer primero una conexión TCP / IP con el servidor. Una vez establecida la conexión TCP, puede emitir la solicitud.

Un ejemplo de un programa de red escrito en Java, como se muestra (suponiendo que el servidor HTTP se ejecuta en el localhost 127.0.0.1 dirección (IP) en el puerto 8000):

```java
 import java.net.*;
 import java.io.*;
   
 public class HttpClient {
    public static void main(String[] args) throws IOException {
       // The host and port to be connected.
       String host = "127.0.0.1";
       int port = 8000;
       // Create a TCP socket and connect to the host:port.
       Socket socket = new Socket(host, port);
       // Create the input and output streams for the network socket.
       BufferedReader in
          = new BufferedReader(
               new InputStreamReader(socket.getInputStream()));
       PrintWriter out
          = new PrintWriter(socket.getOutputStream(), true);
       // Send request to the HTTP server.
       out.println(**"GET /index.html HTTP/1.0")**;
       out.println();   // blank line separating header & body
       out.flush();
       // Read the response and display on console.
       String line;
       // readLine() returns null if server close the network socket.
       while((line = in.readLine()) != null) {
          System.out.println(line);
       }
       // Close the I/O streams.
       in.close();
       out.close();
    }
 }
```

### HTTP/1.0 petición GET  

A continuación se muestra la respuesta de una petición HTTP / 1.0 GET (tema a través de telnet o en su propio programa de red - suponiendo que haya comenzado su servidor HTTP):

```
 **GET /index.html HTTP/1.0**
 (enter twice to create a blank line)
```
```
 **HTTP/1.1 200 OK**
 Date: Sun, 18 Oct 2009 08:56:53 GMT
 Server: Apache/2.2.14 (Win32)
 Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
 ETag: "10000000565a5-2c-3e94b66c2e680"
 Accept-Ranges: bytes
 Content-Length: 44
 Connection: close
 Content-Type: text/html
 X-Pad: avoid browser bug
   
 <html><body><h1>It works!</h1></body></html>
   
 Connection to host lost.
```

En este ejemplo, el cliente envía una solicitud GET para pedir un documento llamado ```"/index.html"```; y negocia para utilizar el protoclo HTTP / 1.0. Se necesita una línea en blanco después de la cabecera de la solicitud. Este mensaje de petición no contiene un cuerpo. 
El servidor recibe el mensaje de petición, interpreta y asigna la *URI-request* de un documento bajo su directorio de documentos. Si el documento solicitado está disponible, el servidor devuelve el documento con un código de estado de respuesta "200 OK". Las cabeceras de respuesta proporcionan la descripción necesaria del documento devuelto, tal como la última fecha de modificación (```Last-Modified```), el tipo MIME (```Content-Type```), y la longitud del documento (```Content-Length```). El cuerpo de la respuesta contiene el documento solicitado. El navegador formateará y mostrará el documento de acuerdo con su tipo de medio (por ejemplo, texto plano, HTML, JPEG, GIF, etc) y diversa información obtenida de las cabeceras de respuesta.

Notas:
+ El nombre de método de petición "GET" es sensible en su escritura, y debe estar en mayúsculas.
+ Si el nombre del método de solicitud fue escrito incorrectamente, el servidor devolverá un mensaje de error "501 Método no implementado".
+ Si no se permite el nombre del método de petición, el servidor devolverá un mensaje de error "405 Método no permitido". Por ejemplo, DELETE es un nombre de método válido, pero no se puede permitir (o implementar) por el servidor.
+ Si la *URI-request* no existe, el servidor devolverá un mensaje de error "404 Not Found". Se tiene que emitir una *URI-request* adecuada, a partir de la raíz del documento " /". De lo contrario, el servidor devolverá un mensaje de error "400 Bad Request".
+ Si la *versión HTTP* es incorrecta, el servidor devolverá un mensaje de error "400 Bad Request".
+ En HTTP / 1.0, de forma predeterminada, el servidor cierra la conexión TCP después de que se entregó la respuesta. Si utiliza telnet para conectarse al servidor, el mensaje "conexión al host perdido" aparece inmediatamente después que se recibe el cuerpo de la respuesta. Se podría utilizar un encabezado de solicitud opcional " Connection: Keep-Alive" para solicitar una persistencia (o keep-aliveconexión), de modo que otra petición puede ser enviada a través de la misma conexión TCP para lograr una mejor eficiencia de la red. Por otro lado, utiliza HTTP / 1.1 keep-alive como conexión predeterminada.

###Código de estado de respuesta

La primera línea del mensaje de respuesta (es decir, la línea de estado) contiene el código de estado de respuesta, que se genera por el servidor para indicar el resultado de la solicitud.

El código de estado es un número de 3 dígitos:
+ 1xx (Informativo): Solicitud recibida, el servidor continúa el proceso.
+ 2xx (Éxito): La petición fue recibida con éxito, entendido, aceptado y resuelta.
+ 3xx (redirección): La acción será tomada en orden con el fin de completar la solicitud.
+ 4xx (Error de cliente): La solicitud contiene sintaxis incorrecta o no se puede entender.
+ 5xx (Error del servidor): El servidor no pudo cumplir con una solicitud aparentemente válida.

Algunos códigos de estado que se encuentran comúnmente son:
+ 100 Continue: El servidor ha recibido la solicitud y está en proceso de dar la respuesta.
+ 200 OK: La solicitud se ha cumplido.
+ 301 Move Permanently: el recurso solicitado se ha movido permanentemente a una nueva ubicación. La URL de la nueva ubicación se da en la cabecera de respuesta llamada Location. El cliente debe emitir una nueva petición a la nueva ubicación. La aplicación debe actualizar todas las referencias a esta nueva ubicación.
+ 302 Found & Redirect (or Move Temporarily): Igual que el 301, pero la nueva ubicación está temporalmente en libre. El cliente debe emitir una nueva solicitud, para las aplicaciones no es necesario actualizar las referencias.
+ 304 Not Modified: En respuesta a la If-Modified-Sincepetición de GET condicional, el servidor notifica que el recurso solicitado no se ha modificado.
+ 400 Bad Request: el servidor no puede interpretar o comprender la solicitud, probablemente hay un error de sintaxis en el mensaje de petición.
+ 401 Authentication Required: El recurso solicitado está protegido, y requieren credenciales de cliente (usuario / contraseña). El cliente debe volver a presentar la solicitud con su credencial (usuario / contraseña).
+ 403 Forbidden: El servidor se niega a suministrar el recurso, independientemente de la identidad del cliente.
+ 404 Not Found: El recurso solicitado no se encuentra en el servidor.
+ 405 Method Not Allowed: El método de solicitud utilizado, por ejemplo, POST, PUT, DELETE, es un método válido. Sin embargo, el servidor no permite el método para el recurso solicitado.
+ 408 Request Timeout:
+ 414 Request URI too Large:
+ 500 Internal Server Error: El servidor se confunde, a menudo causado por un error en el programa del servidor al responder a la solicitud.
+ 501 Method Not Implemented: El método de solicitud utilizado no es válido (podría ser causado por un error de escritura, por ejemplo, "GET" misspell como "Get").
+ 502 Bad Gateway: proxy o el puerto de enlace indica que se recibió una mala respuesta del servidor en sentido ascendente.
+ 503 Service Unavailable: El servidor no puede responder debido a una sobrecarga o mantenimiento. El cliente puede volver a intentarlo más tarde.
+ 504 Gateway Timeout: proxy o el puerto de enlace indican que se recibió un tiempo de espera de un servidor ascendente.

### Mas ejemplos de peticiones GET HTTP/1.0 

**Ejemplo:  Método se petición misspelt**

En la solicitud, "GET" está mal escrito como "get". El servidor devuelve un error "501 Método no implementado". El encabezado de respuesta " Allow" le dice al cliente los métodos permitidos.

```
 **get** /test.html HTTP/1.0
 (enter twice to create a blank line)
```
```
 HTTP/1.1 **501 Method Not Implemented**
 Date: Sun, 18 Oct 2009 10:32:05 GMT
 Server: Apache/2.2.14 (Win32)
 **Allow: GET,HEAD,POST,OPTIONS,TRACE**
 Content-Length: 215
 Connection: close
 Content-Type: text/html; charset=iso-8859-1
   
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <html><head>
 <title>501 Method Not Implemented</title>
 </head><body>
 <h1>Method Not Implemented</h1>
 <p>get to /index.html not supported.<br />
 </p>
 </body></html>
```

**Ejemplo: 404 Documento no encontrado**

En esta solicitud GET, la solicitud de URL " /t.html" no se puede encontrar en el directorio de documentos del servidor. El servidor devuelve un error "404 Not Found".

```
 GET **/t.html** HTTP/1.0
 (enter twice to create a blank line)
```
```
 HTTP/1.1 404 Not Found
 Date: Sun, 18 Oct 2009 10:36:20 GMT
 Server: Apache/2.2.14 (Win32)
 Content-Length: 204
 Connection: close
 Content-Type: text/html; charset=iso-8859-1
   
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <html><head>
 <title>404 Not Found</title>
 </head><body>
 <h1>Not Found</h1>
 <p>The requested URL /t.html was not found on this server.</p>
 </body></html>
```

**Ejmeplo: Número incorrecto fr versión**

En esta solicitud GET, la versión HTTP está mal escrita, con un error en la sintaxis. El servidor devuelve un error "404 Bad Request". La versión HTTP debe ser HTTP / 1.0 o HTTP / 1.1.

```
 GET /index.html **HTTTTTP/1.0**
 (enter twice to create a blank line)
```
```
 HTTP/1.1 **400 Bad Request**
 Date: Sun, 08 Feb 2004 01:29:40 GMT
 Server: Apache/1.3.29 (Win32)
 Connection: close
 Content-Type: text/html; charset=iso-8859-1

 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <HTML><HEAD>
 <TITLE>400 Bad Request</TITLE>
 </HEAD><BODY>
 <H1>Bad Request</H1>
 Your browser sent a request that this server could not understand.<P>
 The request line contained invalid characters following the protocol   string.<P><P> 
 </BODY></HTML>
```

Nota: La última versión de Apache 2.2.14 ignora este error y devuelve el documento con código de estado "200 OK".

**Ejemplo: URI-Request incorrecto**

En la solicitud GET siguiente, la *URI-Request* no comenzó de la raíz " /", lo que dio lugar a una "solicitud incorrecta".

```
 GET test.html HTTP/1.0
 (blank line)
```
```
 HTTP/1.1 **400 Bad Request**
 Date: Sun, 18 Oct 2009 10:42:27 GMT
 Server: Apache/2.2.14 (Win32)
 Content-Length: 226
 Connection: close
 Content-Type: text/html; charset=iso-8859-1
   
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <html><head>
 <title>400 Bad Request</title>
 </head><body>
 <h1>Bad Request</h1>
 <p>Your browser sent a request that this server could not understand.<br />
 </p>
 </body></html>
```

**Ejemplo: conexión Keep-Alive**

Por defecto, a petición de HTTP / 1.0 GET, el servidor cierra la conexión TCP una vez la respuesta se entrega. Se podría solicitar que se mantenga la conexión TCP, (a fin de enviar otra solicitud a través de la misma conexión TCP, para mejorar la eficiencia de la red), a través de un encabezado de solicitud opcional " Connection: Keep-Alive". El servidor incluye una " Connection: Keep-Alive cabecera de respuesta" para informar al cliente que puede enviar otra solicitud a través de esta conexión, antes que el mantenimiento de conexión de tiempo de espera . Otra cabecera de respuesta " Keep-Alive: timeout=x, max=x" indica al cliente el tiempo de espera (en segundos) y el número máximo de solicitudes que se pueden enviar a través de esta conexión persistente.

```
 GET /test.html HTTP/1.0
 *Connection: Keep-Alive*
 (blank line)
```
```
 HTTP/1.1 **200 OK**
 Date: Sun, 18 Oct 2009 10:47:06 GMT
 Server: Apache/2.2.14 (Win32)
 Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
 ETag: "10000000565a5-2c-3e94b66c2e680"
 Accept-Ranges: bytes
 Content-Length: 44
 **Keep-Alive: timeout=5, max=100
 Connection: Keep-Alive**
 Content-Type: text/html
   
 <html><body><h1>It works!</h1></body></html>
```

Notas:
+ El mensaje "Connection to host lost" (para telnet) aparece después de "keep-alive" en tiempo de espera
+ Antes del mensaje "Connection to host lost" aparezca (es decir, mantenimiento de conexión de tiempo de espera), se puede enviar una nueva solicitud a través de la misma conexión TCP.
+ El encabezado " Connection: Keep-alive" no distingue entre mayúsculas y minúsculas. El espacio es opcional.
+ Si una cabecera opcional está mal escrita o no es válida, se omite en el servidor.

**Ejemplo: Acceder a un recurso protegido**

La siguiente petición GET ha intentado acceder a un recurso protegido. El servidor devuelve un error "403 Forbidden". En este ejemplo, el directorio " htdocs\forbidden" está configurado para denegar el acceso completo con el archivo de configuración del servidor Apache HTTP " httpd.conf" de la siguiente manera:

```
 <Directory "C:/apache/htdocs/forbidden">
    Order deny,allow
    deny from all
 </Directory>
```
```
 GET /forbidden/index.html HTTP/1.0
 (blank line)
```
```
 HTTP/1.1 **403 Forbidden**
 Date: Sun, 18 Oct 2009 11:58:41 GMT
 Server: Apache/2.2.14 (Win32)
 Content-Length: 222
 Keep-Alive: timeout=5, max=100
 Connection: Keep-Alive
 Content-Type: text/html; charset=iso-8859-1
   
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <html><head>
 <title>403 Forbidden</title>
 </head><body>
 <h1>Forbidden</h1>
 <p>You don't have permission to access /forbidden/index.html
 on this server.</p>
 </body></html>
```

### Solicitud HTTP / 1.1 GET 
---
El servidor HTTP / 1.1 es compatible con las llamadas máquinas virtuales. Es decir, el mismo servidor físico podría albergar varios hosts virtuales, con diferentes nombres de host (por ejemplo, www.nowhere123.comy www.test909.com) y sus propios directorios dedicados a documentos de raíz. Por lo tanto, en una petición HTTP / 1.1 GET, es obligatorio incluir un encabezado de solicitud llamado " Host", para seleccionar uno de los hosts virtuales.

**Ejemplo: Solicitud HTTP / 1.1**

HTTP / 1.1 mantiene persistencia (o keep-alive) de conexión por defecto para mejorar la eficiencia de la red. Puede utilizar un encabezado de solicitud " Connection: Close" para pedir al servidor cerrar la conexión TCP una vez que se entrega la respuesta.

```
 GET /index.html HTTP/1.1
 **Host: 127.0.0.1**
 (blank line)
```
```
 HTTP/1.1 200 OK
 Date: Sun, 18 Oct 2009 12:10:12 GMT
 Server: Apache/2.2.14 (Win32)
 Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
 ETag: "10000000565a5-2c-3e94b66c2e680"
 Accept-Ranges: bytes
 Content-Length: 44
 Content-Type: text/html
   
 <html><body><h1>It works!</h1></body></html>
```

**Ejemplo: HTTP / 1.1 falta el encabezado de host**

El siguiente ejemplo muestra que la cabecera " Host" es obligatoria en una petición HTTP / 1.1. Si la cabecera " Host" no se encuentra, el servidor devuelve un error "400 Bad Request".

```
 GET /index.html HTTP/1.1
 (blank line)
```
```
 HTTP/1.1 400 Bad Request
 Date: Sun, 18 Oct 2009 12:13:46 GMT
 Server: Apache/2.2.14 (Win32)
 Content-Length: 226
 Connection: close
 Content-Type: text/html; charset=iso-8859-1
   
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <html><head>
 <title>400 Bad Request</title>
 </head><body>
 <h1>Bad Request</h1>
 <p>Your browser sent a request that this server could not understand.<br />
 </p>
 </body></html>
```

###Las peticiones GET condicionales

En todos los ejemplos anteriores, el servidor devuelve todo el documento si la petición puede ser satisfecha (es decir incondicional). Es posible utilizar el encabezado de la solicitud adicional para emitir una "solicitud condicional". Por ejemplo, para que se solicite un documento basado en la fecha de la última modificación (a fin de decidir si utilizar la copia caché local), o para pedir una parte del documento (o rango) en lugar de todo el documento (útil para la descarga de documentos de gran tamaño).

Los encabezados de solicitud condicional incluyen:

+ If-Modified-Since (Verificar el código de estado de respuesta "304 Not Modified").
+ If-Unmodified-Since
+ If-Match
+ If-None-Match
+ If-Range

###Cabeceras de petición

En esta sección se describen algunas de las cabeceras de petición de uso común. Consulte la especificación HTTP para más detalles. La sintaxis del nombre de la cabecera, es decir, con inicial-cap se unen utilizando guión ( -), por ejemplo, Content-Length, If-Modified-Since.

**Host: *domain-name* ** - HTTP / 1.1 soporta máquinas virtuales. Múltiples nombres DNS (por ejemplo, www.nowhere123.com y www.nowhere456.com) pueden residir en el mismo servidor físico, con sus propios directorios para documentos de raíz. La cabecera Host es obligatoria en HTTP / 1.1 para seleccionar uno de los anfitriones.

Los siguientes encabezados pueden ser utilizados para la negociación del contenido por el cliente para pedir al servidor entregar el tipo preferido del documento (en términos del tipo de medio, por ejemplo, JPEG vs GIF, o el lenguaje usado por ejemplo Inglés vs francés) si el servidor mantiene múltiples versiones de un mismo documento.

**Accept: mime-type-1, mime-type-2, ...**- El cliente puede utilizar el encabezado Accept para indicar al servidor los tipos MIME que prefiere y puede manejar. Si el servidor tiene varias versiones del documento solicitado (por ejemplo, una imagen en formato GIF y PNG, o un documento en formato TXT y PDF), se puede comprobar esta cabecera para decidir qué versión entregar al cliente. (Por ejemplo, PNG es más avanzado más GIF, pero no todas navegador soporta PNG.) Este proceso se denomina tipo de contenido de negociación .

**Accept-Language: language-1, language-2, ...**- El cliente puede utilizar el encabezado Accept-Language para indicar al servidor qué idiomas puede manejar o cuáles prefiere. Si el servidor tiene varias versiones del documento solicitado (por ejemplo, en Inglés, chino, francés), se puede comprobar esta cabecera para decidir cuál es la versión que regresa. Este proceso se llama negociación de idioma .

**Accept-Charset: Charset-1, Charset-2, ...**- Para el conjunto de caracteres de negociación, el cliente puede utilizar esta cabecera para indicar al servidor qué juegos de caracteres puede manejar o cuáles prefiere. Ejemplos de conjuntos de caracteres ISO-8859-1, ISO-8859-2, ISO-8859-5, Big5, UCS2, UCS4, UTF8.

**Accept-Encoding: encoding-method-1, encoding-method-2, ...**- El cliente puede utilizar esta cabecera para indicar al servidor el tipo de codificación que soporta. Si el servidor ha codificado (o comprimido) la versión del documento solicitado, puede devolver una versión codificada soportada por el cliente. El servidor también puede elegir codificar el documento antes de devolverlo al cliente para reducir el tiempo de transmisión. El servidor debe establecer la cabecera de respuesta " Content-Encoding" para informar al cliente que se codificó el documento devuelto. Los métodos de codificación comunes son " x-gzip( .gz, .tgz)" y " x-compress( .Z)".

**Connection: Close|Keep-Alive**- El cliente puede utilizar esta cabecera para indicar al servidor la posibilidad de cerrar la conexión después de la solicitud, o para mantener la conexión activa durante otra solicitud. HTTP / 1.1 usa conexión persistente (keep-alive) de forma predeterminada. HTTP / 1.0 se cierra la conexión por defecto.

**Referer: referer-URL**- El cliente puede utilizar esta cabecera para indicar la referencia de esta solicitud. Si hace clic en un enlace para visitar la página web 2 desde la página web 1, la página web 1 es la referencia para la solicitud de la página web 2. Todos los navegadores más importantes establecen esta cabecera, que puede ser utilizada para hacer un seguimiento de la solicitud proveniente (por publicidad en la web o la personalización del contenido). No obstante, esta cabecera no es fiable y se puede suplantar fácilmente. Tenga en cuenta que Referencia está mal escrito como "Referer" (por desgracia, usted tiene que seguirla también).

**User-Agent: browser-type**- Identifica el tipo de navegador que se utiliza para realizar la solicitud. El servidor puede utilizar esta información para devolver un documento diferente dependiendo del tipo de navegador.

**Content-Length: number-of-bytes **- Utilizado por solicitud POST, para informar al servidor de la longitud del cuerpo de la petición.

**Content-Type: mime-type **- Utilizado por solicitud POST, para informar al servidor el tipo de medio del cuerpo de la petición.

**Cache-Control: no-cache|...**- El cliente puede utilizar esta cabecera para especificar cómo las páginas se van a almacenar en caché por el servidor proxy. " no-cache" Requiere proxy para obtener una nueva copia del servidor original, a pesar de que una copia en caché local este disponible. (HTTP / 1.0 servidor no reconoce " Cache-Control: no-cache". En su lugar, utiliza " Pragma: no-cache". Incluye dos cabeceras de la petición si no está seguro acerca de la versión del servidor.)

**Authorization**: Usado por el cliente para suministrar su credencial (usuario / contraseña) para tener acceso a los recursos protegidos. (Esta cabecera se describirá en el capítulo después de la autenticación.)

**Cookie: cookie-name-1=cookie-value-1, cookie-name-2=cookie-value-2, ...**- El cliente utiliza esta cabecera para devolver la cookie (s) de vuelta al servidor, que fue creada por este servidor antes de la administración del estado. (Esta cabecera se discutirá en el capítulo más adelante en la administración del estado.)

**If-Modified-Since: date ** - Dice al servidor la página para enviar sólo si ha sido modificado después de la fecha específica.

###Solicitud GTE para Directorio

Supongamos que un directorio llamado " testdir" está presente en el directorio raíz de documentos " htdocs".

Si un cliente emite una solicitud GET a " /testdir/" (es decir, en el directorio). 
1. El servidor devolverá " /testdir/index.html" si el directorio contiene un " index.htmlarchivo". 
2. De lo contrario, el servidor devuelve el listado de directorios, si el listado de directorios está habilitado en la configuración del servidor. 
3. De lo contrario, el servidor devuelve "404 página no encontrada".

Es interesante tomar nota de que si surge un problema del cliente en una solicitud GET "``` /testdir```" (sin especificar la ruta del directorio "/"), el servidor devuelve un" 301 trasladarse permanentemente "con un nuevo" Location"del "``` /testdir/```", de la siguiente manera.

```
 GET /testdir HTTP/1.1
 Host: 127.0.0.1
 (blank line)
```
```
 HTTP/1.1 301 Moved Permanently
 Date: Sun, 18 Oct 2009 13:19:15 GMT
 Server: Apache/2.2.14 (Win32)
 **Location: http://127.0.0.1:8000/testdir/**
 Content-Length: 238
 Content-Type: text/html; charset=iso-8859-1
   
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <html><head>
 <title>301 Moved Permanently</title>
 </head><body>
 <h1>Moved Permanently</h1>
 <p>The document has moved <a href="http://127.0.0.1:8000/ testdir/">here</a>.</p>

 </body></html>
```

La mayor parte del navegador seguirá con otra petición de " /testdir/". Por ejemplo, si emite http://127.0.0.1:8000/testdirsin el arrastre " /" desde un navegador, se puede notar que un arrastre " /se añadió" a la dirección después se le dio la respuesta. La moral de la historia es: usted debe incluir el " /" en una solicitud GET para la petición de directorio para un ahorro adicional.

###Petición GET a través de un servidor proxy

Para enviar una petición GET a través de un servidor proxy, (a) establecer una conexión TCP con el servidor proxy; (b) utilizar un URI de solicitud absoluto al servidor de destino.http://hostname:port/path/fileName.

El siguiente seguimiento fue capturado por medio de telnet. Se establece una conexión con el servidor proxy, y emitió una petición GET. Una solicitud absoluta URI se utiliza en la línea de petición.

```
 GET **http://www.amazon.com/index.html HTTP/1.1**
 Host: www.amazon.com
 Connection: Close
 (blank line)
```
```
 HTTP/1.1 302 Found
 Transfer-Encoding: chunked
 Date: Fri, 27 Feb 2004 09:27:35 GMT
 Content-Type: text/html; charset=iso-8859-1
 Connection: close
 Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
 Set-Cookie: skin=; domain=.amazon.com; path=/; expires=Wed, 01-Aug-01 12:00:00 GMT
 Connection: close
 Location: http://www.amazon.com:80/exec/obidos/subst/home/home.html
 Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
   
 ed
 <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
 <HTML><HEAD>
 <TITLE>302 Found</TITLE>
 </HEAD><BODY>
 <H1>Found</H1>
 The document has moved
 <A HREF="http://www.amazon.com:80/exec/obidos/subst/home/home.html">
 here</A>.<P>
 </BODY></HTML>
   
 0
```
Tome en cuenta que la respuesta se devuelve en "trozos".

###Método de petición "HEAD"
 ---

La petición HEAD es similar a la petición GET. Sin embargo, el servidor devuelve sólo el encabezado de respuesta sin el cuerpo de la respuesta, que contiene el documento actual. La petición HEAD es útil para comprobar las cabeceras, tales como Last-Modified, Content-Type, Content-Length, antes de enviar una solicitud GET adecuada para recuperar el documento.

La sintaxis de la petición HEAD es la siguiente:

```
 HEAD *request-URI HTTP-version*
 (other optional request headers)
 (blank line)
 (optional request body)
```

**Ejemplo**

```
 **HEAD** /index.html HTTP/1.0
 (blank line)
 HTTP/1.1 200 OK
 Date: Sun, 18 Oct 2009 14:09:16 GMT
 Server: Apache/2.2.14 (Win32)
 Last-Modified: Sat, 20 Nov 2004 07:16:26 GMT
 ETag: "10000000565a5-2c-3e94b66c2e680"
 Accept-Ranges: bytes
 Content-Length: 44
 Connection: close
 Content-Type: text/html
 X-Pad: avoid browser bug
```

Observe que la respuesta consiste sólo en la cabecera sin el cuerpo, que contiene el documento real.


### Método de petición"OPTIONS" 
 ---

Un cliente puede utilizar un método de petición OPTIONS para consultar el servidor el que se apoyan los métodos de petición. La sintaxis de mensaje de solicitud de OPTIONS es:


```
 OPTIONS request-URI|* HTTP-version
 (other optional headers)
 (blank line)

```

"*" Se puede utilizar en lugar de una solicitud-URI para indicar que la solicitud no se aplica a un recurso en particular.

**Ejemplo**

Por ejemplo, la siguiente petición OPTIONS se envía a través de un servidor proxy:

```
 OPTIONS http://www.amazon.com/ HTTP/1.1
 Host: www.amazon.com
 Connection: Close
 (blank line)
```
```
 HTTP/1.1 200 OK
 Date: Fri, 27 Feb 2004 09:42:46 GMT
 Content-Length: 0
 Connection: close
 Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
 Allow: GET, HEAD, POST, OPTIONS, TRACE
 Connection: close
 Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
 (blank line)
```

Todos los servidores que permiten la petición GET permitirán la petición HEAD. A veces, la cabeza no está en la lista.

###Método de petición "TRACE"
 ---
Un cliente puede enviar una solicitud de rastreo pidiendo al servidor devolver un diagnóstico de rastreo.

La solicitud de rastreo toma la siguiente sintaxis:

```
 TRACE / HTTP-version
 (blank line)
```

**Ejemplo**

El siguiente ejemplo muestra una petición TRACE emitida a través de un servidor proxy.
```
 TRACE http://www.amazon.com/ HTTP/1.1
 Host: www.amazon.com
 Connection: Close
 (blank line)
```
```
 HTTP/1.1 200 OK
 Transfer-Encoding: chunked
 Date: Fri, 27 Feb 2004 09:44:21 GMT
 Content-Type: message/http
 Connection: close
 Server: Stronghold/2.4.2 Apache/1.3.6 C2NetEU/2412 (Unix)
 Connection: close
 Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
   
 9d
 TRACE / HTTP/1.1
 Connection: keep-alive
 Host: www.amazon.com
 Via: 1.1 xproxy (NetCache NetApp/5.3.1R4D5)
 X-Forwarded-For: 155.69.185.59, 155.69.5.234
   
 0
```
(Para comparar la solicitud de rastreo con el trazado de ruta)

### Formularios HTML de envío y datos de cadena de consulta
 ---
En muhas de las aplicaciones de internet, como comercio-en-línea y los buscadores, se requiere que los clientes presenten información adicional(por ejemplo, nombre, dirección, y palabras clave). Basado en las datos suministrados, el sirvidor toma la acción apropiada y produce una respuesta customizada.

Los clientes son usualmente presentarse con un formulario (creado con la etiquetea HTML <form>). Una vez que terminan de llenar los datos requeridos y pulsan el boton de enviar, el buscador empaqueta los datos del formulario y los envía al servidor, utilizando una petición GET o POST.

El siguiente es un ejemplo de un formulario HTML, que es generado por el siguiente ódigo de HTML:
```HTML
 <html>
 <head><title>A Sample HTML Form</title></head>
 <body>
   <h2 align="left">A Sample HTML Data Entry Form</h2>
   <form method="get" action="/bin/process">
     Enter your name: <input type="text" name="username"><br />
     Enter your password: <input type="password" name="password"><br />
     Which year?
     <input type="radio" name="year" value="2" />Yr 1
     <input type="radio" name="year" value="2" />Yr 2
     <input type="radio" name="year" value="3" />Yr 3<br />
     Subject registered:
     <input type="checkbox" name="subject" value="e101" />E101
     <input type="checkbox" name="subject" value="e102" />E102
     <input type="checkbox" name="subject" value="e103" />E103<br />
     Select Day:
     <select name="day">
       <option value="mon">Monday</option>
       <option value="wed">Wednesday</option>
       <option value="fri">Friday</option>
     </select><br />
     <textarea rows="3" cols="30">Enter your special request here</textarea><br />
     <input type="submit" value="SEND" />
     <input type="reset" value="CLEAR" />
     <input type="hidden" name="action" value="registration" />
   </form>
 </body>
 </html>
```
![FormularioHTMLdeejemplo](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_SampleForm.png)

Un formulario contiene campos. Los tipos de campo incluyen:
+ Text Box: producida por ```<input type = "text">```.
+ Password Box: producida por ```<input type = "password">```.
+ Radio Button: producida por ```<input type = "radio">```.
+ CheckBox: producida por ```<input type = "checkbox">```.
+ Selection: producida por ```<select>``` y producida por ```<option>```.
+ Text Area: producida por ```<textarea>```.
+ Submit Button: producida por ```<input type = "submit">```.
+ Reset Button: producida por ```<input type = "reset">```.
+ Button: producida por ```<input type = "button">```.

Cada campo tiene un *nombre* y puede tomar un *valor* específico. Una vez que el cliente llena cada uno de los campos y pulsa el botón enviar, el buscador recoge cada uno de los nombres y valores de los campos, los empaqueta en pares "nombre = valor", y concatena todos los campos uilizando "&" como separador de campos. Esto es conocido como una *cadena de consulta*. Será enviada la cadena de consulta al servidor como parte de la petición.

```name1=value1&name2=value2&name3=value3&... ```

Los caracteres especiales no son admitidos dentro de la cadena de consulta. Estos debes ser remplazados por un "%" seguido de su código ASCII en hexadecimal. P. ej.m "~" es reemplazado por "%7E", "#" por "%23" y así. Puesto que el espacio es muy común, puede ser reemplazado por "%20" o "+" (el caracter "+" debe ser remplazado por "%2B"). Este proceso de reemplazamiento se llama *URL-encoding* (codificado de URL), y el resultado es un *URL-encoded query string*. POr ejemplo, suponga que hay 3 campos dentro de un formulario, con el nombre/valor de "name = Peter Lee", "address = #123 Happy Ave" y "language =C++", la URL-encoded es:

```name=Peter+Lee&address=%23123+Happy+Ave&Language=C%2B%2B ```

La cadena de consulta puede ser enviada al servidor utilizando el método de petici+on HTTP GET o POST, lo que se especifica en el atributo ```"method"``` de la etiqueta <form>.

``` <form method="get|post" action="url"> ```

Si se utiliza el método de petición GET, la URL-encoded query string (la cadena de consulta con codificación-URL) se añadirá detrás de la request-URI (URI de solicitud) después de un caracter "?", por ejemplo

```
GET request-URI?query-string HTTP-version
(other optional request headers)
(blank line)
(optional request body)
```

Utilizando la petición GET para enviar la cadena de consulta se tienen los siguientes inconvenientes:
+ La cantidad de datos se puede agregar detrás de *request-URI* es limitado. Si esta cantidad excede un umbral específico del servidor, el servidor devolverá un error "414 URI de la solicitud demasiado grande".
+ La URL-encoded query string debe aparecer en la caja de direcciones del buscador.

El método POST vence estos inconvenientes. Si el método de petición POST es utilizado, la cadena de consulta será enciada en el cuerpo del mensaje de petición, donde el tamaño no está limitado. La cabecera de petición ```Content - Type``` y ```Content - Length``` son utilizadas para notificar al servidor el tipo y longitud de la cadena de consulta. La cadena de consulta no aparecerá en la caja de direcciones del buscador. El método POSR será disutido después.

**Ejemplo**

El sigueinte formulario HTML es utilizado para recolecta el username (nombre de usuario) y contraseña en un menú de login (acceso).

```HTML
<html>
<head><title>Login</title></head>
<body>
  <h2>LOGIN</h2>
  <form method="get" action="/bin/login">
    Username: <input type="text" name="user" size="25" /><br />
    Password: <input type="password" name="pw" size="10" /><br /><br />
    <input type="hidden" name="action" value="login" />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```

![LoginForm](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_LoginForm.png)

El método de petición HTTP GET es utilizado para enviar cadenas de consulta. Suponga que el usuario ingresa "Peter Lee" como el nombre de usuria y como contraseña "123456"; y presiona el botón de enviar. La petición GET sería:

```
GET /bin/login?user=Peter+Lee&pw=123456&action=login HTTP/1.1
Accept: image/gif, image/jpeg, */*
Referer: http://127.0.0.1:8000/login.html
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: 127.0.0.1:8000
Connection: Keep-Alive
```

Tenga en cuenta que aunque la contraseña que introduzca no se muestra en la pantalla, se muestra claramente en el cuadro de dirección del navegador. Nunca se debe utilizar enviar la contraseña sin cifrado adecuado.

```http://127.0.0.1:8000/bin/login?user=Peter+Lee&pw=123456&action=login ```

### URL y URI
 ---

Una URL (Uniform Resource Locator, Localizador Uniforme de Recursos), definida en RFC 2396, es utilizasa para identificar de forma única un recuerso en la web. La URL tiene la siguiente sintaxis:
``` protocol://hostname:port/path-and-file-name ```

Hay 4 partes en una URL:
1. *Protocolo*: El protocolo de capa de aplicación utilizado por el ciente y el servidor, p.ej., HTTP, FTP, y telnet.
2. *Hostname*(nombre del host): El dominio DNS (p.ejm, ``` www.nowhere123.com ```) o la dirección IP (p.ejm., 192.128.1.2) del servidor.
3. *Puerto*: El núemro del puerto TCP que el servidor está escuchando por peticiones entrantes del cliente.
4. *Path-and-file-name*: El nombre y localización del recuerso solicitado, bajo el directorio de documentos del servidor.

Por ejemplo, en la URL ``` http://www.nowhere123.com/docs/index.html ```, el protocolo de comunicación es HTTP; el nombre del servidor es www.nowhere123.com. El número del puerto no es espeificado en la URL, y toma el número por defecto, que para HTTP en TCP el puerto es 80 [STD 2]. El path-and-file-name del recurso a ser localizado es ``` "/docs/index.html ```.

Otros ejemplos de URL son:

```
ftp://www.ftp.org/docs/test.txt
mailto:user@test101.com
news:soc.culture.Singapore
telnet://www.nowhere123.com/
```

*URL codifiada*

La UR no puede contener caracteres especiales, como espacios o '~'. Los caracteres especiales con codificados de la forma %xx, donde xx es el código ASCII en hexadecimal. Por ejemplo, '~' es codificado como %2b. El espacio puede ser codificado como %20 o '+'. La URL codificado es llamada *encoded-URL* (URL codificada).

*URI (Uniform Resoure Identifier, Identificador uniforme de recursos)*

El URI está definido en RFC3986, es más general que la URL, que puede incluso localizar un fragmento dentro de un recurso. La sintaxis de URL para el protocolo HTTP es:

``` http://host:port/path?request-parameters#nameAnchor ```

+ Los parámetros de la petición, en forma de pares name/value, se separan de la URL por un '?'. Los pares de name = value están separados por un '&'.
+ El #nameAnchor identifica un fragmento dentro de un documento HTML, definido por la etiqueta anchor <a name = "anchorName">...>/a>.
+ Reescritura de URL para la gestión de sesiones, por ejemplo: "...; sessionID = xxxxxx".

### Método de petición "POST"
 ---

El método de petición POST es utilizado para enviar datos adicionales al servidor. (p. ejem., enviar datos de un formulario HTML o subir un archivo). Emitir una HTTP-URL del seridor siempre desencadena una petición GET. Para desencadenar una petición POST, puede utilizar un formulario HTML con el attributo ``` method = "post" ``` o escribir su propio programa de red. Para enviar datos de un formulario HTML, la petición POST es la misma que la petiión GET exceptuando que la cadena de consulta con codificación-URL es enviada en el cuerpo de la petición, en lugar de añadir detrás de la *request-URI* (URI de solicitud).

La petición POST tiene la sigueinte sintaxis:

```
POST request-URI HTTP-version
Content-Type: mime-type
Content-Length: number-of-bytes
(other optional request headers)
  
(URL-encoded query string)
```

Las cabeceras de petición ``` Content - Type ``` y ``` Content - Length ``` es necesario en la petición POST para informar al servidor el tipo de dato y longitud del cuerpo de petición.

**Ejemplo: Envío de formulario de datos utilizando método de petición POST**
Usaremos el mismo script HTML de arriba, pero cambiando el método de petición lo cambiaremos por POST.

```HTML
<html>
<head><title>Login</title></head>
<body>
  <h2>LOGIN</h2>
  <form method="post" action="/bin/login">
    Username: <input type="text" name="user" size="25" /><br />
    Password: <input type="password" name="pw" size="10" /><br /><br />
    <input type="hidden" name="action" value="login" />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
```

Supongamos que el usuario ingresa "Peter Lee" como nombre de usuario y "123456" como ontraseña, y presiona el botón de enviar, la siguiente petición POST será generada por el buscador:

```
POST /bin/login HTTP/1.1
Host: 127.0.0.1:8000
Accept: image/gif, image/jpeg, */*
Referer: http://127.0.0.1:8000/login.html
Accept-Language: en-us
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Content-Length: 37
Connection: Keep-Alive
Cache-Control: no-cache

User=Peter+Lee&pw=123456&action=login
```

Note que la cabecera ``` Content - Type ``` informa al servisor que los datos son una URL codificada (con un tipo especial MIME application/x-www-form-urlencoded), y la cabecera ``` Content - Length ``` informa al servidor cuántos bytes debe leer del cuerpo del mensaje.

**POST vs GET para enviar datos de formularios**

omo se mencionó en la sección anterior, la petici+on POST tiene las siguientes ventajas comparadas con la petición GET en envío de cadenas de consulta:
+ El largo de los datos que puede ser enviado es ilimitado, siempre que se mantenga en el cuerpo de la solicitud, que a menudo se envía al servidor en un flujo de datos independiente.
+ La cadena de consulta no se muestra en la caja de direcciones del buscador.

Note que aunque la contraseña no se muestra en el cuadro de dirección del navegador, se transmite al servidor en clear-text, y se somete a una inspección de red. Por lo tanto, el envío de la contraseña mediante una solicitud POST absolutamente no es seguro.

### Subir archivos usando una petición POST multipart/form-data
 ---
 
 "RFC 1867: basado en la forma de subida de archivos HTML" especifica como un archivo puede ser subido al servidor utilizando una petición POST de un formulario HTML. Un nuevo atributo ``` type = "file" ``` es añadido a la etiqueta ``` <input> ``` del HTML ``` <form> ``` para soportar la carga de archivos. La carga-de-archivos POST no está en URL-encoded (en el estándar application/x-www-form-urlencoded), pero utiliza un nuevo tipo de MIME multipart/form-data.
 
 *Ejemplo*
 
 El siguiente formulario HTML puede ser utilizado para subir un archivo:
 
 ```HTML
 <html>
<head><title>File Upload</title></head>
<body>
  <h2>Upload File</h2>
  <form method="post" enctype="multipart/form-data" action="servlet/UploadServlet">
    Who are you: <input type="text" name="username" /><br />
    Choose the file to upload:
    <input type="file" name="fileID" /><br />
    <input type="submit" value="SEND" />
  </form>
</body>
</html>
 ```
 
 
![UploadFileForm](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_FileUploadForm.png)
 
Cuando el buscador encuentra auna etiqueta ``` >input> ``` con el atributo ``` type = "file" ```, despliega una caja de trxto y un botón de "Buscar...", para permitir al usuraio elegir el archivo que será enviado.
 
Cuando el usuario presiona el botón de enciar, el buscador envía los datos del formulario y el contenido del (los) archivo(s) seleccionado(s). El viejo tipo de codificación ```"application/x-www-form-urlencoded"``` es ineficiente para enviar datos binarios y caracteres no-ASCII. Un nuevo tipo de dato ```"multipart/form-data" ``` es utilizado en su lugar.
 
Cada parte identifica el nombre de entrada en el formulario HTML original, y el tipo de contenido si se conoce los medios de comunicación, o como ``` application / octet-stream``` de otro modo.
 
La ubicación original del archivo será suplida por el parámetro ```"filename"```, o por la cabecera "```ontent - Disposition: form-data```".
 
Un ejemplo del mensaje POST para subir archivos se muestra acontinuación:
 
```
POST /bin/upload HTTP/1.1
Host: test101
Accept: image/gif, image/jpeg, */*
Accept-Language: en-us
Content-Type: multipart/form-data; boundary=---------------------------7d41b838504d8
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Content-Length: 342
Connection: Keep-Alive
Cache-Control: no-cache
   
-----------------------------7d41b838504d8 Content-Disposition: form-data; name="username" 
Peter Lee
-----------------------------7d41b838504d8 Content-Disposition: form-data; name="fileID"; filename="C:\temp.html" Content-Type: text/plain 
<h1>Home page on main server</h1> 
-----------------------------7d41b838504d8--
```

Servlet 3.0 provee un soporte integrado para la carga de archivos de procesamiento. Lea " [Uplading File in Sevlet 3.0](https://www.ntu.edu.sg/home/ehchua/programming/java/JavaServletCaseStudyPart2.html#FileUpload) ".

### Método de petición "CONNECT"
 ---
La solicitud de HTTP CONNECT se utiliza para pedir un proxy para establecer una conexión el servidor y simplemente retransmitir el contenido, en lugar de intentar analizar o almacenar en caché el mensaje. Esto a menudo se utiliza para realizar una conexión a través de un proxy.
 
(Bajo construcción).
 
### Otros métodos de petición
 ---
PUT: Pide al servidor que almacene datos.
  
DELETE: Pide al servidor que elimine datos.
  
Por consideraciones de seguridad PUT y DELETE no son soportados por la mayor parte de los servidores de producción.
  
Los métodos de extensión (como son códigos de error y cabeceras) pueden ser definidos para extender la funcionalidad del protocolo HTTP.
  
(Bajo construcción).
  
### Negociación de contenido
   ---
Como se menciona anteriormente, HTTP soporta la negociación de contenido entre el cliente y el servidor. Un cliente puede utilizar cabeceras de solicitudes adicionales (como ``` Aceptar, Accept-Language, Accept-Charset, Accept-Encoding ```) para indicar al servidor que puede manejar el contenido que se prefiere. Si el servidor posee varias versiones de un mismo documento en un formato diferente, devolverá el formato que el cliente prefiera. Este proceso se llama negociación de contenido.
   
### Negociación del tipo de contenido
El servidor utiliza una configuración de archivo MIME  (llamada "```conf\mime.types ```") para mapear la extensión del archivo con el tipo de datos, de modo que pueda determinar el tipo de medio del archivo examinando su extensión de archivo. Por ejemplo, la extensión del archivo ".htm", ".html" están asociadas con el tipo de dato MIME "```text/html```", la extensión de archivo "..jpg", ".jpeg" están asociadas con "```image/jpeg```". Cuando un archivo es retornado al cliente, el servidor debe llenar la cabecera de respuesta ```Content-Type``` para informar al cliente la clase de datos del archivo.
   
Para negociar el tipo de contenido, suponga que el cliente solicita un archivo llamado "logo" si especificar ningún tipo, y envía la cabecera "```Accept: image/gif, image /jpeg, ...```". Si el servidor tiene 2 formatos de "logo": "logo.gif" y "logo.jpg", y la configuración MIME tiene las siguientes entradas:

```
image/gif        gif
image/jpeg       jpeg jpg jpe
```

El servidor regresará "logo.gif" al cliente, basado en la abecera ```Accept```, y el mapeo type/file MIME. El servidor será incluído en la cabecera de respuesta "```Content-type: image/gif```".

Se muestra la traza de mensaje:
```
GET /logo HTTP/1.1
Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg,
  application/x-shockwave-flash, application/vnd.ms-excel, 
  application/vnd.ms-powerpoint, application/msword, */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 01:42:22 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: logo.gif
Vary: negotiate,accept
TCN: choice
Last-Modified: Wed, 21 Feb 1996 19:45:52 GMT
ETag: "0-916-312b7670;404142de"
Accept-Ranges: bytes
Content-Length: 2326
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: image/gif
(blank line)
(body omitted)
```

De cualquier manera, si el sercidor tiene 3 archivos "logo.", "logo.gif", "logo.html", "logo.jpg", y "```Accept: * /*```" es utilizado:
```
GET /logo HTTP/1.1
Accept: */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 01:48:16 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: logo.html
Vary: negotiate,accept
TCN: choice
Last-Modified: Fri, 20 Feb 2004 04:31:17 GMT
ETag: "0-10-40358d95;404144c1"
Accept-Ranges: bytes
Content-Length: 16
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html
(blank line)
(body omitted)
```
```
Accept: */*
```

Las siguientes directivas de configuración de Apache son relevantes para la negociación de tipo de contenido:
+ La directiva ```TypeConfig``` puede ser utilizado para especificar la localización del mappeo de archivo MIME:
```TypeConfig conf/mime.types```
+ La directiva ```AddType``` puede ser utilizada para incluir un mapeo de tipo MIME en el archivo de configuración:
```AddType mime-type extension1 [extension2]```
+ La directiva ```DefaultType``` da el tipo MIME de un archivo con extensión desconocida (en la cabecera de respuesta ```Content-Type```)
```DefaultType text/plain```

### Negociación del lenguaje y "Opciones MultiView"

Las directivas de "```Opciones Multiview```"  es una manera simple de implementar las negociaciones de lenguaje. Por ejemplo:
```
AddLanguage en .en
<Directory "C:/_javabin/Apache1.3.29/htdocs">
    Options Indexes MultiViews
</Directory>
```

Suponga que el cliente solicita "```index.html```" y envía "```Accept-Language: en-us```". Si el servidor tiene "```ŧest.html```", "```test.html.en```" y "```test,html.cn```", basado en la preferencia del cliente, "```test.html.en```" será enviado de vuelta ("en" incluye "en-us".)

Se muestra la traza de mensaje:
```
GET /index.html HTTP/1.1
Accept: */*
Accept-Language: en-us
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
Host: test101:8080
Connection: Keep-Alive
(blank line)
```
```
HTTP/1.1 200 OK
Date: Sun, 29 Feb 2004 02:08:29 GMT
Server: Apache/1.3.29 (Win32)
Content-Location: index.html.en
Vary: negotiate
TCN: choice
Last-Modified: Sun, 29 Feb 2004 02:07:45 GMT
ETag: "0-13-40414971;40414964"
Accept-Ranges: bytes
Content-Length: 19
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: text/html
Content-Language: en
(blank line)
(body omitted)
```

La directiva ```AddLanguage``` es necesaria para asociar un lenguaje de programación con una extensión de archivo, similar al mapeo type/file MIME.

Note que la directiva "```Options All``` no incluye la opción "MultiViews". Esto es, que explícitamente debe activar MultiViews.

La directiva ```LanguagePriority``` puede ser utilizada para especificar el lenguajes de preferencia en caso de empate durante la negociación de contenido o si el cliente no expresa una preferencia. Por ejemplo:

```
<IfModule mod_negotiation.c>
   LanguagePriority en da nl et fr de el it ja kr no pl pt pt-br
</IfModule>
```

### Negociación de juego de caracteres

Un cliente puede utilizar la cabecera de solicitud ```Accept-Charset``` a negociar con el servidor el conjunto de caracteres que prefiere.

```Accept-Charset: charset-1, charset-2, ...```

Los juegos de caracteres más comunes incluyen: ISO-8859-1 (Latin-I), ISO-8859-2, ISO-8859-5, BIG5 (Chinese Traditional), GB2312 (Chinese Simplified), UCS2 (2-byte Unicode), UCS4 (4-byte Unicode), UTF8 (Encoded Unicode), and etc.

Similarmente, la directiva ```AddChar``` es utilizada para asociar la extensión de una rchivo con el juego de caracteres. Por ejemplo:

```
AddCharset ISO-8859-8   .iso8859-8
AddCharset ISO-2022-JP  .jis
AddCharset Big5         .Big5  .big5
AddCharset WINDOWS-1251 .cp-1251
AddCharset CP866        .cp866
AddCharset ISO-8859-5   .iso-ru
AddCharset KOI8-R       .koi8-r
AddCharset UCS-2        .ucs2
AddCharset UCS-4        .ucs4
AddCharset UTF-8        .utf8
```

###Negociacion de codificación

Un cliente puede utilizar la cabecera ```Accept-Encoding``` para decirle al servidor el tipo de codificación que soporta. Los esquemas de odificación más comunes son "x-gzip (.gz, .tgz)" y "x-compress (.Z)".

```Accept-Encoding: encoding-method-1, encoding-method-2, ...```

Similarmente, la directiva ```AddEncoding``` es utilizada para asociar la extensión del archivo con el esquema de codificación. Por ejemplo
```
AddEncoding x-compress  .Z
AddEncoding x-gzip      .gz .tgz
```

### Conecciones persistentes (Keep-alive)
 ---
 En HTTP/1.0, el servidor cierra la conección TCP después de entregar la respuesta por default (```Connection: Close```). Esto es, cada conección TCP resuelve una sola petición. Esto no es eficiente en la mayoría de las páginas HTML que contienen hipercvínculos ( con la etiqueta ```>a href = "url" >```) a otros recuersos (como imágenes, escripts -alojados en un servidor local o remoto). Si se descarga una página que contiene 5 imágenes en-línea, el buscador tiene que establecer conecciones TCP 6 veces al mismo servidor.
 
 El cliente puede negociar con el servisor y pedirle que no cierre la conección después de netregar la respuesta, de este modo otra petición puede ser enviada a través de la misma conección. Esto es conocido como conección perskstente (o "Keep-alive"). Las conecciones persistentes aumentan considerablemente la eficiencia de la red. Para HTTP/1.0, la conección default es no-persistente. Para pedir una conexión persistente, el cliente debe incluir una cabeera de petición "```Connection: Keep-alive```" en el mensaje de petición para negociar con el servidor.
 
 Para HTTP/1.1, la conección por defecto es persistente. El cliente no tiene ue enviar la cabecera ```Connection: Keep-alive```. En su lugar, el cliente debe  enviar la cabecera ```Connection: Close``` para pedir al servidor que cierre la conección después de enviar la respuesta.
 
 Las conecciones persistentes son extremadamente utilizadas por páginas web con muchas imágenes pequeñas y otra información asociada, que pueden ser descargadas usando la misma conección. Los beneficios de la conecci+on persistente son:
 + El tiempo de CPU y ahorro de recursos en la apertura y cierre de conexión TCP en el cliente, proxy, puertas de enlace, y el servidor de origen.
 + La solicitud puede ser "pipelined".  Es decir, un cliente puede hacer varias solicitudes sin esperar a que cada respuesta, con el fin de utilizar la red de manera más eficiente.
 + Una respuesta más rápida ya que ningún tiempo necesario para realizar la conexión TCP protocolo de enlace de apertura.

En servidor HTTP Apache, varias directivas de configuración están relacionados con las conexiones persistentes:

La directiva ```KeepAlive``` decide cuando soportar conecciones persistentes. Puede tomar valores de On u Off.

```KeepAlive On|Off```

La directiva de ```MaxKeepRequests``` establece el máximo número de peticiones que pueden ser enviadas a través de la conección persistente. Se puede enviar desde 0 hasta un número ilimitado de peticiones. Es recomendable establecer un alto número para un mejor rendimiento y una mejor eficiencia de la red.

```MaxKeepAliveRequests 200```

La directiva ```KeepAliveTimeOut``` establece el tiempo en segudos que debe esperar la conneción persistente para aceptar la siguiente petición.

```KeepAliveTimeout 10```

### Rango de descarga
 ---
 
```
Accept-Ranges: bytes
Transfer-Encoding: chunked
```

(Bajo construcción)

### Control de Caché
 ---
 
 El cliente debe enviar una cabecera de petición "```Cache-control: no-cache```" para decirle al proxy que obtenga una nueva copia del servidor original, a pesar de que hay una copia en caché local. Desafortunadamente, un servidor HTTP/1.0 no entiende esta cabecera, per utiliza una vieja cabecera de petición "```Pragma: no-cache```". Debe incluir ambas cabeceras en la petición:
 
``` 
Pragma: no-cache
Cache-Control: no-cache
```

(Bajo construcción)

### REFERENCIAS Y RECURSOS
 ---

+ W3C HTTP specifications at http://www.w3.org/standards/techs/http.
+ RFC 2616 "Hypertext Transfer Protocol HTTP/1.1", 1999 @ http://www.ietf.org/rfc/rfc2616.txt.
+ RFC 1945 "Hypertext Transfer Protocol HTTP/1.0", 1996 @ http://www.ietf.org/rfc/rfc1945.txt.
+ STD 2: "Assigned numbers", 1994.
+ STD 5: "Internet Protocol (IP)", 1981.
+ STD 6: "User Datagram Protocol (UDP)", 1980.
+ STD 7: "Transmission Control Protocol (TCP)", 1983.
+ RFC 2396: "Uniform Resource Identifiers (URI): Generic Syntax", 1998.
+ RFC 2045: "Multipurpose Internet Mail Extension (MIME) Part 1: Format of Internet Message Bodies", 1996.
+ RFC 1867: "Form-based File upload in HTML", 1995, (obsoleted by RFC2854).
+ RFC 2854: "The text/html media type", 2000.
+ Mutlipart Servlet for file upload @ www.servlets.com
