# GCP Cloud Task: Patrón Productor/Consumidor usando funciones y colas de tareas

## Objetivos

- Orquestar un conjunto de microservicios de manera asíncrona empleando colas de mensajería.
- Crear y configurar el servicio de Pub/Sub para orquestar llamados de Cloud Function
- Explorar el funcionamiento del patrón publicador suscriptor 

## Estructura de carpetas

En el proyecto encontrará tres carpetas principales:

- La carpeta `collections` en donde se encuentra la colección de Postman para poder realizar pruebas sobre las funciones publicadas
- La carpeta `function-consumir-http` en donde se encuentra la implementación de la función que será llamada por cada tarea del servicio de Cloud Task
- La carpeta `function-producir-http` en donde se encuentra la implementación de la función que nos permitirá crear tareas al servicio de Cloud Task

## Creación de un tópico de publicación

Para poder utilizar el servicio de Pub/Sub:

> No olvide remplazar <nombre_topico> con el nombre del tópico al que se suscribirán las funciones

```console
gcloud pubsub topics create <nombre_topico> --message-encoding=utf-8 --message-retention-duration=1h
```

## Publicación de la funciones 

Debe tener presente que las funciones utilizarán la cuenta de almacenamiento para configurar los permisos que tienen. Además, se conectará a la cola previamente creada.

### Función Suscriptor Liga

Para poder publicar la función, debe abrir una consola de comandos en la ubicación donde descargamos el repositorio. Posteriormente, debe ejecutar los siguientes comandos:

> No olvide remplazar <nombre_topico> con el nombre del tópico al que se suscribirán las funciones

```console
cd function-suscriptor-liga
gcloud functions deploy funcion-pubsub-tutorial-suscriptor-liga --entry-point liga --runtime python39 --trigger-topic <nombre_tema> --allow-unauthenticated --memory 128MB --region us-central1 --timeout 60 --min-instances 0 --max-instances 1
cd ..
```

En la consola deberá observar un mensaje de confirmación de creación de la función

### Función Suscriptor Policia

Para poder publicar la función, debe abrir una consola de comandos en la ubicación donde descargamos el repositorio. Posteriormente, debe ejecutar los siguientes comandos:

> No olvide remplazar <nombre_topico> con el nombre del tópico al que se suscribirán las funciones

```console
cd function-suscriptor-policia
gcloud functions deploy funcion-pubsub-tutorial-suscriptor-policia --entry-point policia --runtime python39 --trigger-topic <nombre_tema> --allow-unauthenticated --memory 128MB --region us-central1 --timeout 60 --min-instances 0 --max-instances 1
cd ..
```

En la consola deberá observar un mensaje de confirmación de creación de la función

### Función Suscriptor Bomberos

Para poder publicar la función, debe abrir una consola de comandos en la ubicación donde descargamos el repositorio. Posteriormente, debe ejecutar los siguientes comandos:

> No olvide remplazar <nombre_topico> con el nombre del tópico al que se suscribirán las funciones

```console
cd function-suscriptor-bomberos
gcloud functions deploy funcion-pubsub-tutorial-suscriptor-bomberos --entry-point bomberos --runtime python39 --trigger-topic <nombre_tema> --allow-unauthenticated --memory 128MB --region us-central1 --timeout 60 --min-instances 0 --max-instances 1
cd ..
```

En la consola deberá observar un mensaje de confirmación de creación de la función

### Función Publicador Ciudadano Http

Para poder publicar la función, debe abrir una consola de comandos en la ubicación donde descargamos el repositorio. Posteriormente, debe ejecutar los siguientes comandos:

> No olvide remplazar <nombre_topico> con el nombre del tópico al que se suscribirán las funciones y <id_proyecto> con el identificador del proyecto que está utilizando

```console
cd function-publicador-ciudadano-http
gcloud functions deploy funcion-pubsub-tutorial-publicador-ciudadano --entry-point peticion_ayuda --runtime python39 --trigger-http --allow-unauthenticated --memory 128MB --region us-central1 --timeout 60 --min-instances 0 --max-instances 1 --set-env-vars TOPIC=<nombre_topico>,PROJECT_ID=<id_proyecto>
cd ..
```

En la consola deberá observar un mensaje de confirmación de creación de la función
