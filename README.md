# IBM Cloud Security & Compliance Center :lock: :cloud:

IBM Cloud Security & Compliance Center le permite gestionar los controles de seguridad y cumplimiento directamente dentro de la plataforma de IBM Cloud. Puede ver sus posturas de seguridad y cumplimiento desde un panel de control unificado, permitiéndole de una manera fácil la automatización de políticas de seguridad, habilitar la gobernanza de la configuración en su cuenta y la detección de vulnerabilidades y amenazas.

<br />

# Guía de instalación y configuración de security and compliance center :hammer:

Esta guía esta enfocada en la instalación y configuración de security and compliance center para la recolección de datos, activación del panel de control, creación de ambitos, creación de exploraciones, generación de informes y exportación de información.

<br />

### Indice
1. [Pre-requisitos](#Pre-requisitos-)
2. [Crear las credenciales](#crear-las-credenciales-key)
3. [Instalar un colector/recopilador](#instalar-un-colectorrecopilador-hammer)
4. [Crear un alcance](#crear-un-alcance-white_flag)
5. [Programe un escaneo](#programe-un-escaneo-)
6. [Genere un informe](#genere-un-informe-newspaper)
<br />

## Pre-requisitos 📋

1. VSI con las siguientes especificaciones mínimas:

  * Perfil de Red Hat Enterprise Linux, CentOS o Ubuntu : cx2-2x4(2 vCPU, 4 GB de RAM y 4 GBPS)
  * Volumen de arranque : 50 GB de espacio en disco.
<br />

2. Docker para Linux. Para iniciar Docker, puede ejecutar systemctl start docker.
<br />

3. Una clave de API de ID de servicio con permisos de acceso de lectura para los recursos que desea escanear.
<br />

## Crear las credenciales :key:

Las credenciales se utilizan para permitir que el recopilador tome información sobre sus recursos, evalúe sus configuraciones e inicie cualquier corrección necesaria.

 1. En la consola de IBM Cloud, haga clic en el icono de ```Menú``` y seleccione ```Security and Compliance / Seguridad y cumplimiento```.
 2. En la navegación, haga clic en ```Configure / Configurar```, luego diríjase a ```Credentials / Credenciales```.
 3. Haga clic en el icono ```Create / Create```. Y complete lo siguiente:
 * ```Name / Nombre```: Seleccione un nombre para su credencial.
 * ```Description / Descripción```: Opcionalmente proporcione una descripción para su servicio.
 * ```Purpose / Proposito```: Seleccione la opción Discovery/Collection.
 <br />
 
 A continuación de click en siguiente y complete:
* ```Credential type / Tipo de credencial```: Seleccione IBM Cloud.
* ```API Key```: Ingrese la clave API de su servicio. Para obtener ayuda para crear una clave de API consulte [Descripción de las claves de API](https://cloud.ibm.com/docs/account?topic=account-manapikey). Tenga en cuenta que su clave de API debe tener permisos de acceso de lector a los recursos que desea escanear.

 4. Verifique sus configuraciones y haga clic en ```Create / Crear```. La credencial se agrega a una lista de credenciales disponibles.

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/Imagenes/security.gif>
</p>

<br />

## Instalar un colector/recopilador :hammer:

Un recopilador es un módulo de software empaquetado como una imagen de Docker. Se instala "a la vista" de su entorno, donde puede tener acceso de red a sus recursos de TI. 

 1. En la consola de IBM Cloud, haga clic en el icono de ```Menú``` y seleccione ```Security and Compliance / Seguridad y cumplimiento```.
 2. En la navegación, haga clic en ```Configure / Configurar```, luego diríjase a ```Collectors / Colectores```.
 3. Haga clic en el icono ```Create / Create```. Y complete lo siguiente:
 * ```Name / Nombre```: Seleccione un nombre para su colector.
 * ```Description / Descripción```: Opcionalmente proporcione una descripción para su servicio.

  A continuación de click en siguiente y complete:
  
 * ```Managed by / Manejado por```: Elija la opción Customer.
 * ```Endpoint type / Tipo Punto Final```: Elija la opción Public.

Verifique sus configuraciones y haga clic en ```Create / Crear```
  
<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/Imagenes/collector.gif>
</p>

<br />

4. Descargue el archivo **initiate_collector.sh** del recopilador que creó.
5. En la tabla de recopiladores, haga clic en el nombre del recopilador que desea registrar. La fila de la tabla se expande para proporcionar más información. Asegúrese de anotar también la clave de registro para un paso posterior.

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/Imagenes/collectorsh.PNG>
</p>

5. En su terminal, inicie sesión en su máquina virtual usando SSH.
```
ssh <username>@<hostname_or_IP_address>:
```

_**Nota**: Si no inicia sesión como usuario root, debe anteponer los siguientes comandos con sudo._

6. Asegúrese de que la imagen de su sistema operativo esté actualizada. Si está trabajando con Ubuntu, puede ejecutar el siguiente comando.

```
apt-get update
```
 6. Instale Docker Compose usando el comando para su sistema operativo. Si está trabajando con Ubuntu, puede usar el siguiente comando.

```
apt-get install docker-compose
```

7. Transfiera el **inititate_collector.sh** archivo a su máquina virtual y luego cambie los permisos para permitir que se ejecute.

```
chmod +x initiate_collector.sh
```
8. Instale el recopilador ejecutando el siguiente comando.

```
./initiate_collector.sh
```
En la siguiente imagen se ejemplifican los pasos 4 a 8, previamente ya se ha trasnferido e instalado el archivo a la máquina virtual.

![image](https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/securitycenter/pasosshcolector.gif)

9. Cuando se le solicite, ingrese la siguiente información:

* La ruta de datos de su máquina host. Por ejemplo /root/folder_name/ .

* Indique **No**, para indicar que no desea ejecutar un escaneo de Nmap.

* Ingrese la clave de registro que anotó cuando descargó el inititate_collector.sh archivo de la interfaz de usuario del servicio. _(Paso 2 subindice 3)._

En la página  ```Configure / Configurar```, diríjase a ```Collectors / Colectores```, haga clic en ```Aprobar``` en la fila de la tabla que corresponde al recopilador con el que está trabajando. Deberá obtener un resultado como el siguiente:

![image](https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/securitycenter/resultado.png)

<br />

## Crear un alcance :white_flag:

Cuando trabaja con el Centro de seguridad y cumplimiento, puede limitar el enfoque de sus escaneos a un entorno, región o incluso a un recurso específico. Al crear alcances, puede determinar su puntuación de seguridad y cumplimiento en un área específica de su negocio. Para generar un alcance o scope, complete los siguientes pasos:
<br />

1. En la página ```Security and Compliance/Seguridad y cumplimiento```, visualice la sección ```Manage Posture``` y de click en la pestaña ```Configure/Configurar```.
<br />

2. En la pestaña de ```Configure/Configurar``` seleccione la opción ```Scopes/Alcances```.
<br />

3. Presione el botón ```Create +/Crear +``` y complete los campos solicitados de la siguiente manera:
   
   **Details/Detalles**
   * ```Name/Nombre```: asigne un nombre exclusivo para el alcance.
   
   **Environment/Ambiente**
   * ```Environment/Ambiente```: seleccione IBM Cloud.
   * ```Credentials/Credenciales```: seleccione las credenciales que va a utilizar.
   
   **Collectors/Colectores**
   * Seleccione el colector que desea utilizar.
   
   Para finalizar de click en el botón ```Create/Crear```
<br />

 ![image](https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/Imagenes/CrearScope.gif)

<br />

## Programe un escaneo 🚀

Para descubrir recursos, evaluar su configuración y validar su cumplimiento frente a un perfil predefinido, puede programar un análisis de validación.

 1. En la consola de IBM Cloud, haga clic en el icono de ```Menú``` y seleccione ```Security and Compliance / Seguridad y cumplimiento```.
 2. En la navegación, haga clic en ```Configure / Configurar```, luego diríjase a ```Scans / Escaneos```.
 3. Haga clic en el icono ```Schedule / Programar```. Y complete lo siguiente:
 * ```Name / Nombre```: Seleccione un nombre para su escaneo.
 * ```Description / Descripción```: Opcionalmente proporcione una descripción para su servicio.
 * ```Scan type / Tipo de escaneo```: Seleccione la opción Validation.
 * ```Scope / Alcance```: Seleccione el alcance realizado en el paso anterior.
 * ```Profile / Perfil```: Seleccione el perfil que desea escanear. (En este caso se presentan los resultados del escaneo del perfil **IBM Cloud Best Practices Controls 1.0** y el perfil **CIS IBM Foundations Benchmark 1.0.0** )
 
 A continuación de click en siguiente y complete:
 
* ```Remediation preference / Preferencia de remediación```: Seleccione la opción automatico.
* ```Frecuency / Frecuencia```: Ingrese la frecuencia con la que quiere que se realice el escaneo.
* ```Ends / Termina```: Seleccione cuando desea que finalice el escaneo.

 4. Verifique sus configuraciones y haga clic en ```Create / Crear```.

<p align="center">
<img width="800" alt="img8" src=https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/Imagenes/scan-best.gif>
</p>
<br />

5. Espere de 10 a 30 minutos se completa el escaneo. Para ver los resultados del escaneo de click en la pestaña ```Assess``` ➡ ```Scan results``` y seleccione el resultado de escaneo que desea visualizar. Allí prodrá explorar con más detalle los resultados obtenidos.
<br /> 

 ![image](https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/Imagenes/ResultadosEscaneo.gif)

<br />

## Genere un informe :newspaper:

Security and Compliance Center le permite exportar los resultados que ha obtenido en sus diferentes exploraciones, por lo que puede visualizar estos datos en informes detallados en diferentes formatos. Si desea generar un informe realice los siguientes pasos:
<br />

1. En la página ```Security and Compliance/Seguridad y cumplimiento```, visualice la sección ```Assess``` y de click en la pestaña ```Scan results```.
<br />

2. Haga clic en el resultado que desea visualizar con detalle.
<br />

3. Espere mientras cargan los datos y posteriormente de click en la opción ```Download report```.
<br />

4. Seleccione el tipo de informe, formato, y los detalles de la información que quiere obtener.
<br />

5. Haga clic en el botón ```Download/Descargar```.
<br />

 ![image](https://github.com/emeloibmco/IBM-Cloud-Security-Compliance-Center/blob/master/Imagenes/GenerarInforme.gif)


<br />

## Autores ✒️
Equipo *IBM Cloud Tech Sales Colombia*.
