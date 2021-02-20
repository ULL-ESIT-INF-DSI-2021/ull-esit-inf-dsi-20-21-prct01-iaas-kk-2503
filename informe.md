# Práctica 1 - Configuración de Máquina Virtual en el IaaS
En esta práctica se pretende configurar la **máquina virtual** que se le asignó a cada alumno en el servicio **IaaS** de la **Universidad de La Laguna**
para trabajar en la asignatura **Desarrollo de Sistemas Informáticos**. También se configurarán todas las herramientas necesarias.

## Objetivos
- **Conectar remotamente** a la máquina virtual del IaaS de una manera sencilla.
- Generar **clave pública-privada** para SSH.
- Configurar **git** y **prompt** en la máquina.
- Añadir la clave SSH pública a la cuenta personal de GitHub.
- Configurar **Node.js**.

## Desarrollo.
### Conocer la IP de la máquina virtual.
Para trabajar con la máquina virtual alojada en el servicio IaaS de la ULL, debemos conectarnos a la VPN de dicha universidad. Yo ya lo tenía configurado en mi máquina local, 
pero se pueden seguir las instrucciones disponibles en este [link](https://www.ull.es/servicios/stic/2020/12/01/servicio-de-vpn-de-la-ull/) para configurarlo.

Una vez configurado hay que conectarse a la VPN hay que acceder al servicio IaaS de la ULL (puedes hacerlo pulsando [aqui](https://iaas.ull.es/ovirt-engine/sso/login.html)).
Se deben introducir las credenciales para poder acceder. Se pueden observar todas las máquinas virtuales del usuario que están alojadas en el IaaS, debemos encender la máquina
llamada **DSI**. Después de unos minutos verá que el nombre ha cambiado, ahora es DSI-XX, donde X es un número natural comprendido entre 0-9.

![Máquina virtual IaaS](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/1.JPG)

A continuación haga click en el nombre de la máquina, en la parte derecha se encuentra una sección llamada **Interfaces de Red** donde verá la direccion IP asignada a su máquina
virtual. En mi caso es 10.6.129.210.

![Interfaces de Red](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/2.JPG)

### Conectarse a la máquina virtual mediante SSH.
Lo siguiente que debemos hacer es conectarnos a la máquina virtual mediante una conexión SSH. Para ello debemos abrir una terminal en nuestra máquina local y escribir lo siguiente:
'ssh usuario@XX.X.XXX.XXX', donde en vez de XX.X.XXX.XXX debemos poner la dirección IP de la máquina virtual.

![Conexion SSH](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/3.png)

Introduzca **yes** e intro para avanzar:

![Introducir yes](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/4.png)

Le va a pedir la contraseña, deberá introducir **usuario**:

![Introducir usuario](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/5.png)

Como observa el sistema está pidiendo una contraseña nueva, primero pedirá la actual (usuario) y luego la nueva que la pedirá dos veces. Como es obvio, la próxima vez que inicié
sesión en su máquina virtual deberá hacerlo con la contraseña nueva que le acaba de poner.

![Contraseña actual](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/6.png)

![Contraseña nueva](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/7.png)

![Sesión iniciada](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/8.png)

### Modificar el nombre de host de la máquina virtual
Vamos a proceder a cambiar el nombre de host de la máquina. Para ello debemos modificar el fichero /etc/hostname. En esta imagen primero mostramos el contenido actual del 
fichero (host actual), luego pretendemos cambiarlo con el comando "sudo vi /etc/hostname". Como la instrucción se va a ejecutar en modo superusuario, necesitamos 
introducir su contraseña:

![Modificar fichdero](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/10.png)

Se va a abrir un editor de texto (vi) con el contenido actual, para cambiarlo debemos entrar a modo edición presionando la tecla "i" y procederemos a cambiar el nombre de la máquina, quitamos el
nombre actual e introducimos el que deseamos. En mi caso lo nombre "iaas-dsi":

![Cambiar nombre](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/12.png)

Para salir del modo edición debemos presionar la tecla "esc" y guardaremos el contenido actualizado del fichero introduciendo ":wq" ("w" para guardarlo y "q" 
para salir del editor).

![Guardar fichdero](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/13.png)

Después modificaremos otro fichero (/etc/hosts) actualizando el nombre host. En el fichero debemos buscar "ubuntu" que era el nombre antiguo de la máquina y ponemos el actual.
Para modificar dicho fichero ejecutamos el siguiente comando: *sudo vi /etc/hosts* y hacemos lo mismo que hicimos antes para modificar el fichero (tecla "i" para editar, "esc"
para salir del modo edición y ":wq" para guardar).

Contenido anterior:

![Contenido anterior](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/17.png)

Contenido actual:

![Contenido actual](https://github.com/ULL-ESIT-INF-DSI-2021/ull-esit-inf-dsi-20-21-prct01-iaas-kk-2503/blob/main/img/18.png)
