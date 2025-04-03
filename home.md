---
title: INSTALACION DE DNS CON PI-HOLE EN UBUNTU SERVER VERSION 22.04
description: 
published: true
date: 2025-04-03T08:03:04.795Z
tags: 
editor: markdown
dateCreated: 2025-03-27T22:20:19.427Z
---

> Trabajo Sistemas Operativos 2 Implementación servicio DNS Goofy
>
> Estudiante: Leonardo López Salazar
>
> Profesor:
>
> SAMUEL GUILLERMO OROZCO MONTERO
>
> Universidad de Manizales
>
> Manizales – Caldas
>
> 2025

> **Que** **es** **un** **DNS:** Un DNS (Sistema de Nombres de Dominio, por sus siglas en inglés: **Domain** **Name** **System**) es un servicio que traduce nombres de dominio legibles por humanos (como [<u>www.example.com</u>)](http://www.example.com/) en direcciones IP numéricas (como 192.0.2.1) que las computadoras utilizan para identificarse entre sí en una red.
>
> La idea de hacer este paso a paso es que aprendas como implementar y activar un servicio de DNS en un servidor, en este caso vamos a implementar el servicio en un servidor llamado goofy el cual nos lo proporciono el profesor y la universidad para poder hacer este trabajo de forma más real e intuitiva.
>
> **Paso 1:**
>
> Lo primero que hay que hacer es entrar a proxmox para crear un LXC de Ubuntu server en caso tal de que no tengas proxmox puedes descargando e instalarlo siguiendo el paso a paso que te da la página oficial de proxmox para que así puedas empezar con el paso a paso que vamos hacer.hola
>
> Una vez que entremos a proxmox lo primero que hacemos es darle en la opción de crear LXC o créate ct como lo vemos en la imagen:
>
>![0.png](/dns/0.png)
>
> Luego de darle en créate CT se te va abrir una ventanita en el cual te va a pedir que pongas un nombre de usuario y una contraseña como vemos en la imagen:
>
>![1.jpg](/dns/1.jpg)


> Luego de llenar lo que te pide le damos a siguiente y te va a aparecer que escojas una plantilla el cual es el sistema operativo que se instalo previamente pero como en el servidor que nos proporcionaron ya lo tenia instalado solo toca es escoger la platilla el cual es Ubuntu server 22.04-1 como lo vemos en la siguiente imagen:
>
>![2.png](/dns/2.png)
>
> Lugo de escoger la plantilla le damos en siguiente y te va a parecer que definas la memoria de almacenamiento que decidas poner al sistema operativo en este caso yo le puse 8 gigas ya que con esto es más que suficiente para implementar el servicio y que este te valla de forma fluida, pero eso si tienes que tener en cuenta las especificaciones que tiene el servidor para que puedas tomar y definir cuanto almacenamiento quieres poner a la caja como lo vemos en la imagen:
>
>![3.jpg](/dns/3.jpg)


> Después de definir el tamaño del disco duro le damos en siguiente y te va aparecer que definas cuantos núcleos del procesador tenga la caja o el sistema operativo en este caso yo le puse 1 solo núcleo ya que con eso es más que suficiente para implementar este servicio de forma rápida y dinámica como se ve en la imagen:
>
>![4.png](/dns/4.png)
>
> Una vez definido los núcleos le damos en siguiente y te aparece que definamos cuanta memoria ram va a tener la caja o el sistema operativo para que este funcione bien pues en mi caso yo le puse 700 megabits ya que este servicio no necesita de mucha ram para que funcione bien con esta cantidad de memoria ram es mas que suficiente y queda, así como lo vemos en la imagen:
>
>![5.png](/dns/5.png)


> Luego le damos en siguiente y te va aparecer que definas el modo de red, si lo quieres con ip estática o con ip dinámica pues en mi caso yo lo definí con ip dinámica la ip versión 4 ósea en modo DHCP como lo vemos en la imagen:
>
>![6.png](/dns/6.png)
>
> Luego de definir esto le damos en siguiente y te aparece que pongas un DNS para que este tenga una conexión a internet en este caso yo le puse el DNS de Google el cual es el 8.8.8.8 como lo vemos en la imagen:
>
>![7.png](/dns/7.png)


> Después de definir el DNS le damos en siguiente y nos muestra por último todo lo que le configuramos a la caja para confirmar que todo si quedo bien configurado y si todo esta bien le damos en finalizar como lo vemos en la imagen:
>
>![8.png](/dns/8.png)
>
> Luego de darle finalizar se nos va a inicializar la caja con el sistema operativo Ubuntu pero para poder trabajar con él de forma más cómoda y dinámica vamos a usar una herramienta llamada MobaXterm para que nos podamos conectar con la caja y así poder trabajar mejor pero para poder conéctanos con la herramienta a la caja tenemos que hacer previamente en el mismo proxmox entrar en la carpeta configuración de conexión del sistema operativo y darle permiso para que pueda dar acceso a la caja esto se hace con el siguiente comando **nano /etc/ssh/sshd_config** le damos enter y se nos abrir lo siguiente:
>
>![9.png](/dns/9.png)
>
> Luego de que se nos abra la carpeta tenemos que bajar hasta donde dice authentication y desloguear la opción que dice PermitRootLogin y seguido de este borrar donde dice que no y cambiarlo por unas yes como lo vemos en la imagen:
>
>![10.png](/dns/10.png)
>
> Luego de organizar esta opción le damos en control (x) y después oprimimos la tecla (y) la cual dice que yes para que autorices que se guarde los cambios en la configuración y seguido de esto le damos enter, una sugerencia es cuando ya hallas salido de la carpeta de configuración vuelvas y entres para verificar si guardo o no guardo bien la configuración que se había hecho anterior mente si guardo bien la configuración entonces ya pasarías a inicializar la herramienta para que puedas conectarte a la caja pero si no quedo guardada bien la configuración puede ser que no lo guardasteis bien y por ende te toca repetir el mismo proceso que se hizo anteriormente pero si se te guardo bien entonces vamos a pasar al paso 2 que es inicializar la herramienta de trabajo y meter los diferentes comando que vamos a mencionar a continuación.
>
> Pero antes de incializar la herramienta tenemos que saber que ip tenemos en el sistema operativo por ende ponemos en el mismo proxmox el siguiente comando para saber nuestra ip: **ip a**
>
> Y nos va a mostrar la ip como lo vemos en la imagen:
>
>![11.jpg](/dns/11.jpg)


> **Paso2:**
>
> Luego de haber configurado y definido todo lo que se necesita para implementar el servicio y también conocer nuestra ip entonces abrimos la herramienta MobaXterm y una vez abierta le damos en la opción que esta en la parte superior izquierda que dice sesion le damos clic y nos va abrir la siguiente ventana como lo vemos en la imagen:
>
>![12.png](/dns/12.png)


> En la casilla donde dice remote host ponemos la ip de nuestra caja que haviamos visto anteriormente como lo vemos en la imagen:
>
>![13.png](/dns/13.png)
>
> Después de poner la ip le damos en ok y se nos va a inicializar la caja en la herramienta, pero para que puedas trabajar en ella te va a pedir las credenciales de usuario y el usuario que tienes que poner es root y le das entrer y seguido de esto pones la contraseña que definisteis al principio cuando empezasteis a crear la caja, si pusisteis bien las credenciales de usuario ya se te inicializa bien la caja y ya puedes trabajar con ella y te va a salir, así como lo vemos en la imagen:
>
>![14.jpg](/dns/14.jpg)
>
> Y en ese momento es que ya podemos empezar a trabajar con ella.
>
> Listo el primer comando que tienes que poner para inicializar con la instalación del servicio de DNS es el siguiente:
>
> • **sudo apt-get install curl**
>
> que hace este comando lo que hace este comando es instalar una herramienta de línea de comandos que permite transferir datos desde o hacia un servidor utilizando varios protocolos
>
> después de escribir el comando le damos enter y debe de quedar asi como lo vemos en la imagen:
>
>![15.jpg](/dns/15.jpg)
>
> Luego de que se halla instalado el curl seguimos con el siguiente comando:
>
> • **sudo curl -sSL [<u>https://install.pi-hole.net</u>](https://install.pi-hole.net/) \| bash**

> este comando lo que haces que instala pi hole que es la herramienta en la que vamos a organizar los DNS e implementar el servicio esto en específico lo que hace es que instala la herramienta desde la pagina web oficial de pi hole, debería de salir esto una vez que le demos enter después de haber escrito bien el comando:
>
>![16.png](/dns/16.png)
>
> Luego de darle enter nos va aparecer una series de recuadros los cuales nos dice si queremos implementar y autorizar a pi hole hacer una serie de instalaciones y configuraciones para que funcione en este caso le damos a todo que sí, lastimosamente en el momento que me aparecieron esta serie de recuadros no les tome pantallazo para que lo vean pero en teoría si le aparece esta serie de recuadros le tiene que dar a todo que si para que la herramienta y el servicio se les pueda inicializar, una vez que termine el la instalación les va a mostrar la contraseña con la cual ustedes pueden ingresar a pi hole para que puedan agregar y configurar los DNS como se ve en la imagen:
>
>![17.jpg](/dns/17.jpg)


> Para poder ingresar a la interfas de pi hole tienen que poner la ip de la caja que les arrojo la instalación de pi hole como lo muestra el recuadro de color verde que tiene también la flecha y cuando hallan cargado la interfaz en su navegador copian la contraseña que les dio también en el momento de la instalación que es la que aparece en el recuadro de color rojo señalada con la flecha roja como se ve en la imagen.
>
> Una vez que hallamos entrado a la interfaz de pi hole y hallamos puesto la contraseña nos va a cargar algo así como se ve en la imagen:
>
>![18.png](/dns/18.png)
>
> Una vez que tengamos la interfaz cargada y inicializada con la contraseña como lo vemos en la imagen anterior nos vamos a para en el botón que dice setings y se nos va a desplegar una serie de opciones le damos en la ultima que dice local DNS records como lo vemos en la imagen:
>
>![19.png](/dns/19.png)



> Luego se nos parace algo que nos dice listo of DNS records el cual es la lista en donde podemos poner los DNS que queremos configurar en mi caso yo puse la ip de la interfas de pi hole mio con un nombre que yo quise poner seguido de punto local después de poner esto la ip del sitio y el nombre de dominio le damos en el botón que (+) y si todo esta bien se agrega de forma exitosa el DNS del sitio que nosotros pongamos como lo vemos en la imagen:
>
>![20.png](/dns/20.png)
>
> Luego de haber agregado con éxito el DNS tenemos que entrar en la configuración del puesto de red de nuestro computador y configurar el DNS de nuestro puerto con la ip de pi hole para que nos pueda cargar todo de forma normal como lo vemos en esta serie de imágenes:
>
>![21.png](/dns/21.png)
>
>![22.png](/dns/22.png)
>
>![23.png](/dns/23.png)
>
>![24.png](/dns/24.png)
>
>![25.png](/dns/25.png)
>


> Luego de darle a todo aceptar nos dirigimos a nuestro navegador y ponemos el dominio que habíamos puesto en el DNS segudo de punto local y enseguda debe de cargar la pagina como lo vemos en las imágenes:
>
> •Esta es entrando directamente con la ip:
>
>![26.png](/dns/26.png)
>

> •Y esta es entrando con el dominio que se había puesto en el DNS:
>
>![27.jpg](/dns/27.jpg)
>
> Y así queda implementado el servicio de DNS en nuestro servidor espero que esto te haya servido y que te haya funcionado todo como lo explique acá en este documento.
