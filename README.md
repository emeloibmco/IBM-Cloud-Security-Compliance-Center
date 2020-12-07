# IBM-Cloud-Security-Compliance-Center

# GUÍA DE CONFIGURACIÓN Y HABILITACIÓN DE SECURITY AND COMPLIANCE CENTER


### Indice
1. [Pre-requisitos](#Pre-requisitos-)
2. [Prepación para instalación de Knative en Kubernetes desde la consola web del cluster](#preparación-para-instalación-de-Knative-en-Kubernetes-desde-la-consola-web-del-cluster-)
3. [Instalación de Knative en el cluster de Kubernetes (IKS)](#instalación-de-Knative-en-el-cluster-de-kubernetes-iks-)
4. [Despliegue en Kubernetes de una aplicación HelloWord de nodejs Serverless](#despliegue-en-Kubernetes-de-una-aplicación-helloWord-de-nodejs-serverless-)
5. [Referencias](#Referencias)

## Pre-requisitos 📋

_1. Docker para Linux. Para iniciar Docker, puede ejecutar systemctl start docker._

_2.Una clave de API de ID de servicio con permisos de acceso de lectura para los recursos que desea escanear._

_3. VPC y/o VSI con las siguientes especificaciones:
Perfil de Red Hat Enterprise Linux, CentOS o Ubuntu : cx2-2x4(2 vCPU, 4 GB de RAM y 4 GBPS)
Volumen de arranque : 50 GB de espacio en disco._


## CREAR LAS CREDENCIALES 🚀

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

### Haga 'login' a IBM Cloud desde la línea de comando.

Paso 3: instala un colector
Un recopilador es un módulo de software empaquetado como una imagen de Docker. Se instala "a la vista" de su entorno, donde puede tener acceso de red a sus recursos de TI. Para obtener más información sobre los recopiladores y cómo se lleva a cabo la comunicación, consulte Comprensión de los recopiladores .

En la página Configurar> Configuración> Recopiladores del Centro de seguridad y cumplimiento, haga clic en Crear .
Dale a tu coleccionista un nombre y una descripción significativos. Haga clic en Crear .
Descargue el initiate_collector.sharchivo del recopilador que creó.

En la tabla de recopiladores , haga clic en el nombre del recopilador que desea registrar. La fila de la tabla se expande para proporcionar más información. Asegúrese de anotar también la clave de registro para un paso posterior.

En su terminal, inicie sesión en su máquina virtual usando SSH.


ssh <username>@<hostname_or_IP_address>
Si no inicia sesión como usuario root, debe anteponer los siguientes comandos con sudo.

Asegúrese de que la imagen de su sistema operativo esté actualizada. Si está trabajando con Ubuntu, puede ejecutar el siguiente comando.


[sudo] apt-get update
Instale Docker Compose usando el comando para su sistema operativo. Si está trabajando con Ubuntu, puede usar el siguiente comando.


[sudo] apt-get install docker-compose
Transfiera el inititate_collector.sharchivo a su máquina virtual y luego cambie los permisos para permitir que se ejecute.


chmod +x initiate_collector.sh
Instale el recopilador ejecutando el siguiente comando.


./initiate_collector.sh
Cuando se le solicite, ingrese la siguiente información:

La ruta de datos de su máquina host. Por ejemplo /root/folder_name/,.
No, para indicar que no desea ejecutar un escaneo de Nmap.
La clave de registro que anotó cuando descargó el inititate_collector.sharchivo de la interfaz de usuario del servicio.
En la página Configurar> Configuración> Recopiladores del Centro de seguridad y cumplimiento, haga clic en Aprobar en la fila de la tabla que corresponde al recopilador con el que está trabajando.

Paso 4: crea un alcance
Cuando trabaja con el Centro de seguridad y cumplimiento, puede limitar el enfoque de sus escaneos a un entorno, región o incluso recurso específico. Al crear alcances, puede determinar su puntuación de seguridad y cumplimiento en un área específica de su negocio.

En la página Ámbitos del Centro de seguridad y cumplimiento, haga clic en el icono Nuevo ámbito .
Dé a su alcance un nombre y una descripción significativos.
Seleccione un entorno.
Seleccione el recopilador que desea utilizar.
Seleccione las Credenciales que brindan acceso a los recursos que desea escanear.
Haga clic en Siguiente .
Seleccione los grupos de recursos que desea analizar y haga clic en Crear .
Paso 5: programe un escaneo
Para descubrir recursos, evaluar su configuración y validar su cumplimiento frente a un perfil predefinido, puede programar un análisis de validación.

En la página Análisis> Análisis programados del Centro de seguridad y cumplimiento, haga clic en Programación . Se abre un panel lateral.
Dé a su escaneo un nombre y una descripción significativos.
Seleccione Validación .
Seleccione el alcance que creó en el paso anterior.
Seleccione uno de los perfiles predefinidos y haga clic en Siguiente .
Seleccione la frecuencia a la que desea que se ejecute el escaneo.
Seleccione cuándo desea que se detenga el escaneo. Las opciones incluyen nunca, un número específico de escaneos o en una fecha determinada.
Haga clic en Crear .
```
### Acceda al cluster de Kubernetes (IKS) desplegado en IBM Cloud 📦


_1.	Despues de haber iniciado sesión en IBM Cloud, debe dirigirse al clúster en el que se va a trabajar._

_Para ingresar al clúster que tengamos aprovisionado en nuestra cuenta de IBM Cloud se deben realizar los siguientes pasos:_

_•	Diríjase al resource list._
_Primero debe dar clic en el **navigation menu** y luego donde dice **Resource list**, como se puede ver en la siguiente imagen:_

<p align="center">
<img width="696" alt="7" src="https://user-images.githubusercontent.com/60987042/76996077-da434b00-691e-11ea-92be-558da48f7d97.PNG">
</p>

_•	Diríjase a la sección de **clústers** y dar clic en el que se desea acceder._

_•	Se da clic en el botón **Actions...** y luego en la sección que dice **Terminal Web**._

![WhatsApp Image 2020-06-09 at 11 30 23 AM](https://user-images.githubusercontent.com/60628267/84174858-bc304700-aa44-11ea-99d7-02065ad676cc.jpeg)

 
_La terminal que se abre al terminar el paso anterior, es una terminal similar a la que maneja un sistema operativo como Ubuntu._

### Instalación de Knative en el cluster de Kubernetes (IKS) 📦

**NOTA: En este punto de la guía debemos estar en la consola web del cluster**
_Para instalar corectamente Knative en el cluster se deben seguir los siguientes pasos:_ 

_1. Habilite el complemento Knative gestionado en el clúster, esto lo puede hacer mediante el siguiente comado:_

```
ibmcloud ks cluster addon enable knative --cluster <cluster_name_or_ID> -y
```
_La salida de este comado debe ser:_

```
Enabling add-on knative for cluster knative...
OK
```

_2. Verifique que Istio se ha instalado correctamente. Todos los pods correspondientes a los servicios de Istio deben estar en el estado **Running**, y para poder verificarlo debemos utilizar el siguiente comando:_

```
kubectl get pods --namespace istio-system
```
_La salida de este comado debe ser:_

```
NAME                                       READY     STATUS      RESTARTS   AGE
istio-citadel-748d656b-pj9bw               1/1       Running     0          2m
istio-egressgateway-6c65d7c98d-l54kg       1/1       Running     0          2m
istio-galley-65cfbc6fd7-bpnqx              1/1       Running     0          2m
istio-ingressgateway-f8dd85989-6w6nj       1/1       Running     0          2m
istio-pilot-5fd885964b-l4df6               2/2       Running     0          2m
istio-policy-56f4f4cbbd-2z2bk              2/2       Running     0          2m
istio-sidecar-injector-646655c8cd-rwvsx    1/1       Running     0          2m
istio-statsd-prom-bridge-7fdbbf769-8k42l   1/1       Running     0          2m
istio-telemetry-8687d9d745-mwjbf           2/2       Running     0          2m
prometheus-55c7c698d6-f4drj                1/1       Running     0          2m
```

_3. **Opcional:** si desea utilizar Istio para todas las demás apps en el espacio de nombres **default**, añada la etiqueta **istio-injection=enabled** al espacio de nombres, si desea realizarlo el comado es el siguiente:_


```
kubectl label namespace default istio-injection=enabled
```
_4. Verifique que todos los pods del componente Serving de Knative están en el estado Running. Verifiquelo mediante el siguiente comando:_

```
kubectl get pods --namespace knative-serving
```
_La salida de este comado debe ser:_

```
NAME                          READY     STATUS    RESTARTS   AGE
activator-598b4b7787-ps7mj    2/2       Running   0          21m
autoscaler-5cf5cfb4dc-mcc2l   2/2       Running   0          21m
controller-7fc84c6584-qlzk2   1/1       Running   0          21m
webhook-7797ffb6bf-wg46v      1/1       Running   0          21m
```

_En este punto de la guía, Knative ya está instalado en el cluster de Kubernetes (IKS), ahora debemos pasar al despliegue de una aplicación._



### Despliegue en Kubernetes de una aplicación HelloWord de nodejs Serverless: 🚀

**NOTA: Este despliegue se debe hacer de una manera local.**

_Para el despliegue de esta aplicación debemos seguir los siguientes pasos:_

_1. Descargar la Imagen Docker que contiene la aplicación a Desplegar:_

```
docker pull ibmcom/kn-helloworld
```

![WhatsApp Image 2020-06-08 at 4 46 41 PM](https://user-images.githubusercontent.com/60628267/84172330-83db3980-aa41-11ea-96be-bb13a7b007ac.jpeg)


_2. Cargue a su Docker personal esta imagen descargada, los comandos son los siguientes:_

```
docker tag <ID_IMAGE> <Docker_User>/kn-helloworld
```
_Luego debe ejecutar el siguiente:_

```
docker push <Docker_User>/kn-helloworld
```

![WhatsApp Image 2020-06-08 at 4 47 41 PM (1)](https://user-images.githubusercontent.com/60628267/84173324-c18c9200-aa42-11ea-9f93-984c770a43a0.jpeg)
 


_3. Cree un nuevo archivo con el nombre **service.yaml** y añada el siguiente contenido:_

```
nano service.yaml
```
**NOTA: Al ejecutar el editor de texto nano puede añadir el siguiente contenido y para Guardarlo y salir, debe presionar la tecla f2, luego debe aceptar los cambios y dar enter.

```
apiVersion: serving.knative.dev/v1alpha1
kind: Service
metadata:
  name: knative-example
  namespace: default
spec:
  runLatest:
    configuration:
      revisionTemplate:
        spec:
          container:
            image: docker.io/##DOCKERHUB_NAME##/knative-example
```


![WhatsApp Image 2020-06-08 at 4 49 31 PM (1)](https://user-images.githubusercontent.com/60628267/84173463-ef71d680-aa42-11ea-8a63-efdd8cfd73a8.jpeg)


_4. Una vez realizado el paso anterior se genera el servicio de Knative para esta aplicación, el cual se hace mediante el siguiente comando:_

```
kubectl apply -f service.yaml
```

![WhatsApp Image 2020-06-08 at 4 50 26 PM (1)](https://user-images.githubusercontent.com/60628267/84173533-031d3d00-aa43-11ea-8bb8-aa9546be98ec.jpeg)
 
_5. Mediante el siguiente comando, podemos observar cómo el servicio crea los diferentes recursos y entidades:_

```
kubectl get configuration
```

![WhatsApp Image 2020-06-08 at 4 50 55 PM (1)](https://user-images.githubusercontent.com/60628267/84173559-0e706880-aa43-11ea-9b07-519e584d5be8.jpeg)


_6. Ahora podemos verificar que efectivamente el sercicio este desplegado:_

```
kubectl get replicaset
```

![WhatsApp Image 2020-06-08 at 4 51 39 PM (1)](https://user-images.githubusercontent.com/60628267/84173584-19c39400-aa43-11ea-976f-81611f6bcfc6.jpeg)



_7. Ahora vamos a visualizar la ruta de despliegue de nuestra aplicación:_

```
kubectl get route
```

![WhatsApp Image 2020-06-08 at 4 52 09 PM (1)](https://user-images.githubusercontent.com/60628267/84173618-25af5600-aa43-11ea-83e6-c73cc2fce67c.jpeg)


**Nota: Esta ruta es la que debemos llevar a un navegador y ahi podremos ver la aplicación funcionando y ya desplegada**

_8. En este paso podremos ver en que pod fue asignado el despliegue al igual que podremos visualizar todas las aplicaciones que esten corriendo en nuestro Cluster:_

```
kubectl get pods
```
![WhatsApp Image 2020-06-08 at 4 52 57 PM (1)](https://user-images.githubusercontent.com/60628267/84173686-3f509d80-aa43-11ea-8806-2e71e5da7588.jpeg)


_9. Utilizando el link de despliegue en el navegador se podrá visualizar la aplicación funcionando._

![WhatsApp Image 2020-06-08 at 4 44 00 PM (1)](https://user-images.githubusercontent.com/60628267/84173739-50011380-aa43-11ea-8ec1-1c8bf6478003.jpeg)


## Referencias

La documentación en linea de Knative en IBM Cloud, se encuentra en el siguiente enlace:

https://cloud.ibm.com/docs/containers?topic=containers-serverless-apps-knative&locale=es#update-knative-addon

La documentación necesaria para una aplicación Serverless la puede encontrar en el siguiente enlace:

https://serverless-architecture.io/blog/serverless-workloads-on-kubernetes-with-knative/


## Autores ✒️
