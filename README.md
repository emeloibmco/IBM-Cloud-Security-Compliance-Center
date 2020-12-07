# IBM-Cloud-Security-Compliance-Center

# GUÍA DE CONFIGURACIÓN Y HABILITACIÓN DE SECURITY AND COMPLIANCE CENTER


### Indice
- [Pre-requisitos](#Pre-requisitos-)
- [1. CREAR LAS CREDENCIALES](#1. CREAR LAS CREDENCIALES-)
- [2. instala un colector/recopilador](#2.-instala-un-colector/recopilador-)
- [3. CREA UN ALCANCE](#3.-CREA-UN-ALCANCE-)
- [4. PROGRAME UN ESCANEO](#4.-PROGRAME-UN-ESCANEO-)

## Pre-requisitos 📋

_1. Docker para Linux. Para iniciar Docker, puede ejecutar systemctl start docker._

_2.Una clave de API de ID de servicio con permisos de acceso de lectura para los recursos que desea escanear._

_3. VPC y/o VSI con las siguientes especificaciones:
Perfil de Red Hat Enterprise Linux, CentOS o Ubuntu : cx2-2x4(2 vCPU, 4 GB de RAM y 4 GBPS)
Volumen de arranque : 50 GB de espacio en disco._


## 1. CREAR LAS CREDENCIALES 🚀

Las credenciales se utilizan para permitir que el recopilador recopile información sobre sus recursos, evalúe sus configuraciones e inicie cualquier corrección necesaria.

En la consola de IBM Cloud, haga clic en el icono Menú Icono de menú > Seguridad y cumplimiento para acceder al Centro de seguridad y cumplimiento.
En la navegación, haga clic en Configurar> Configuración> Credenciales .
Haga clic en el icono Nueva credencial .
Dé a su credencial un nombre y una descripción significativos.
Seleccione IBM Cloud .
Seleccione Descubrimiento / Colección .
Pegue su clave de API en el campo de clave de API de IBM . Para obtener ayuda para crear una clave de API, consulte Descripción de las claves de API .

Su clave de API debe tener permisos de acceso de lector a los recursos que desea escanear.

Verifique sus actualizaciones y haga clic en Guardar . La credencial se agrega a una lista de credenciales disponibles.

### 2. instala un colector/recopilador
Un recopilador es un módulo de software empaquetado como una imagen de Docker. Se instala "a la vista" de su entorno, donde puede tener acceso de red a sus recursos de TI. 

   1.En la página Configurar> Configuración> Recopiladores del Centro de seguridad y cumplimiento, haga clic en **Crear**.
   2.Dale a tu colecctor un nombre y una descripción significativos. Haga clic en **Crear**.
   3.Descargue el initiate_collector.sh archivo del recopilador que creó.

En la tabla de recopiladores , haga clic en el nombre del recopilador que desea registrar. La fila de la tabla se expande para proporcionar más información. Asegúrese de anotar también la clave de registro para un paso posterior.

   4. En su terminal, inicie sesión en su máquina virtual usando SSH.
```
_ssh <username>@<hostname_or_IP_address>:_

```

**Nota**: Si no inicia sesión como usuario root, debe anteponer los siguientes comandos con sudo.

  5. Asegúrese de que la imagen de su sistema operativo esté actualizada. Si está trabajando con Ubuntu, puede ejecutar el siguiente comando.

```
[sudo] apt-get update
```
 6. Instale Docker Compose usando el comando para su sistema operativo. Si está trabajando con Ubuntu, puede usar el siguiente comando.


[sudo] apt-get install docker-compose

7. Transfiera el inititate_collector.sharchivo a su máquina virtual y luego cambie los permisos para permitir que se ejecute.

```
chmod +x initiate_collector.sh
```
8. Instale el recopilador ejecutando el siguiente comando.


./initiate_collector.sh

9. Cuando se le solicite, ingrese la siguiente información:

La ruta de datos de su máquina host. Por ejemplo /root/folder_name/,.
No, para indicar que no desea ejecutar un escaneo de Nmap.

La clave de registro que anotó cuando descargó el inititate_collector.sharchivo de la interfaz de usuario del servicio.

En la página Configurar> Configuración> Recopiladores del Centro de seguridad y cumplimiento, haga clic en Aprobar en la fila de la tabla que corresponde al recopilador con el que está trabajando.

### 3.CREA UN ALCANCE

Cuando trabaja con el Centro de seguridad y cumplimiento, puede limitar el enfoque de sus escaneos a un entorno, región o incluso recurso específico. Al crear alcances, puede determinar su puntuación de seguridad y cumplimiento en un área específica de su negocio.

1. En la página Ámbitos del Centro de seguridad y cumplimiento, haga clic en el icono **Nuevo ámbito**.
2. Dé a su alcance un nombre y una descripción significativos.
3. Seleccione un entorno.
4. Seleccione el recopilador que desea utilizar.
5. Seleccione las Credenciales que brindan acceso a los recursos que desea escanear.
6. Haga clic en Siguiente .
7. Seleccione los grupos de recursos que desea analizar y haga clic en Crear .

### 4. PROGRAME UN ESCANEO

Para descubrir recursos, evaluar su configuración y validar su cumplimiento frente a un perfil predefinido, puede programar un análisis de validación.

1. En la página Análisis> Análisis programados del Centro de seguridad y cumplimiento, haga clic en Programación . Se abre un panel lateral.
2. Dé a su escaneo un nombre y una descripción significativos.
3. Seleccione Validación .
4. Seleccione el alcance que creó en el paso anterior.
5. Seleccione uno de los perfiles predefinidos y haga clic en Siguiente .
6. Seleccione la frecuencia a la que desea que se ejecute el escaneo.
7. Seleccione cuándo desea que se detenga el escaneo. Las opciones incluyen nunca, un número específico de escaneos o en una fecha determinada.
Haga clic en **Crear**.
```

## Autores ✒️
Javier Jiménez
