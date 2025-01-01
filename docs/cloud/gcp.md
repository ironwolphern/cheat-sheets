# Google Cloud Platform (GCP) Command Cheatsheet

## Configuración Inicial
```bash
# Iniciar sesión en GCP
gcloud auth login

# Configurar el proyecto predeterminado
gcloud config set project PROJECT_ID

# Listar configuraciones actuales
gcloud config list

# Cambiar la región predeterminada
gcloud config set compute/region REGION

# Cambiar la zona predeterminada
gcloud config set compute/zone ZONE
```

## Gestión de Proyectos
```bash
# Listar proyectos
gcloud projects list

# Crear nuevo proyecto
gcloud projects create PROJECT_ID --name="PROJECT_NAME"

# Eliminar proyecto
gcloud projects delete PROJECT_ID

# Establecer proyecto activo
gcloud config set project PROJECT_ID
```

## Compute Engine
```bash
# Listar instancias
gcloud compute instances list

# Crear instancia
gcloud compute instances create INSTANCE_NAME \
    --machine-type=MACHINE_TYPE \
    --zone=ZONE \
    --image-family=IMAGE_FAMILY \
    --image-project=IMAGE_PROJECT

# Iniciar instancia
gcloud compute instances start INSTANCE_NAME

# Detener instancia
gcloud compute instances stop INSTANCE_NAME

# Eliminar instancia
gcloud compute instances delete INSTANCE_NAME

# SSH a una instancia
gcloud compute ssh INSTANCE_NAME

# Crear disco
gcloud compute disks create DISK_NAME --size=SIZE --zone=ZONE

# Adjuntar disco a instancia
gcloud compute instances attach-disk INSTANCE_NAME --disk=DISK_NAME
```

## Cloud Storage
```bash
# Crear bucket
gsutil mb gs://BUCKET_NAME

# Listar buckets
gsutil ls

# Copiar archivos al bucket
gsutil cp LOCAL_FILE gs://BUCKET_NAME/

# Descargar archivos del bucket
gsutil cp gs://BUCKET_NAME/FILE LOCAL_PATH

# Eliminar bucket
gsutil rb gs://BUCKET_NAME

# Sincronizar directorios
gsutil rsync -r LOCAL_DIR gs://BUCKET_NAME/DIR

# Establecer ACL
gsutil acl ch -u USER_EMAIL:PERMISSION gs://BUCKET_NAME/
```

## Kubernetes Engine (GKE)
```bash
# Crear cluster
gcloud container clusters create CLUSTER_NAME \
    --num-nodes=NUM_NODES \
    --zone=ZONE

# Obtener credenciales
gcloud container clusters get-credentials CLUSTER_NAME

# Listar clusters
gcloud container clusters list

# Redimensionar cluster
gcloud container clusters resize CLUSTER_NAME --num-nodes=NUM_NODES

# Eliminar cluster
gcloud container clusters delete CLUSTER_NAME

# Actualizar cluster
gcloud container clusters upgrade CLUSTER_NAME
```

## Cloud SQL
```bash
# Crear instancia MySQL
gcloud sql instances create INSTANCE_NAME \
    --database-version=MYSQL_VERSION \
    --tier=MACHINE_TYPE

# Crear base de datos
gcloud sql databases create DATABASE_NAME --instance=INSTANCE_NAME

# Listar instancias
gcloud sql instances list

# Crear usuario
gcloud sql users create USERNAME --instance=INSTANCE_NAME --password=PASSWORD

# Eliminar instancia
gcloud sql instances delete INSTANCE_NAME
```

## IAM & Administración
```bash
# Listar roles
gcloud iam roles list

# Crear role personalizado
gcloud iam roles create ROLE_ID --project=PROJECT_ID \
    --title="ROLE_TITLE" \
    --permissions=PERMISSION_1,PERMISSION_2

# Agregar binding de IAM
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member=user:USER_EMAIL \
    --role=roles/ROLE_NAME

# Listar service accounts
gcloud iam service-accounts list

# Crear service account
gcloud iam service-accounts create SA_NAME \
    --display-name="SA_DISPLAY_NAME"

# Crear key para service account
gcloud iam service-accounts keys create KEY_FILE \
    --iam-account=SA_NAME@PROJECT_ID.iam.gserviceaccount.com
```

## VPC Networks
```bash
# Crear VPC
gcloud compute networks create VPC_NAME --subnet-mode=auto

# Crear subred
gcloud compute networks subnets create SUBNET_NAME \
    --network=VPC_NAME \
    --range=IP_RANGE \
    --region=REGION

# Crear regla de firewall
gcloud compute firewall-rules create RULE_NAME \
    --network=VPC_NAME \
    --allow=tcp:PORT \
    --source-ranges=IP_RANGES

# Listar VPCs
gcloud compute networks list

# Listar subredes
gcloud compute networks subnets list

# Listar reglas de firewall
gcloud compute firewall-rules list
```

## Cloud Functions
```bash
# Desplegar función
gcloud functions deploy FUNCTION_NAME \
    --runtime=RUNTIME \
    --trigger-http \
    --entry-point=ENTRY_POINT

# Listar funciones
gcloud functions list

# Describir función
gcloud functions describe FUNCTION_NAME

# Eliminar función
gcloud functions delete FUNCTION_NAME

# Ver logs
gcloud functions logs read FUNCTION_NAME
```

## Cloud Run
```bash
# Desplegar servicio
gcloud run deploy SERVICE_NAME \
    --image=IMAGE_URL \
    --platform=managed \
    --region=REGION

# Listar servicios
gcloud run services list

# Describir servicio
gcloud run services describe SERVICE_NAME

# Eliminar servicio
gcloud run services delete SERVICE_NAME

# Ver revisiones
gcloud run revisions list
```

## Logging & Monitoring
```bash
# Ver logs
gcloud logging read "resource.type=RESOURCE_TYPE"

# Escribir log
gcloud logging write LOG_NAME "MESSAGE"

# Crear sink
gcloud logging sinks create SINK_NAME \
    DESTINATION \
    --log-filter="FILTER"

# Listar sinks
gcloud logging sinks list

# Ver métricas
gcloud monitoring metrics list

# Crear política de alerta
gcloud alpha monitoring policies create \
    --display-name="POLICY_NAME" \
    --condition="CONDITION"
```

## Tips Adicionales
```bash
# Formato de salida
gcloud config set core/output_format [json|yaml|text]

# Activar autocompletado
gcloud components install beta
source /path/to/completion.bash.inc

# Ver todas las configuraciones
gcloud config list --all

# Cambiar entre cuentas
gcloud config configurations activate CONFIG_NAME

# Ver información de facturación
gcloud billing accounts list

# Habilitar APIs
gcloud services enable SERVICE_NAME

# Ver cuotas
gcloud compute project-info describe --project=PROJECT_ID
```

## Notas Importantes:
1. Reemplaza los valores en MAYÚSCULAS con tus valores específicos
2. Algunos comandos pueden requerir permisos adicionales
3. Verifica la documentación oficial para opciones adicionales
4. Usa `gcloud help COMANDO` para más información sobre cualquier comando
5. La mayoría de los comandos tienen banderas adicionales para personalización