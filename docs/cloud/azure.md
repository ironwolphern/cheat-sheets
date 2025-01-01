# Azure CLI Commands Cheatsheet

## Comandos Básicos y Autenticación

### Login y Configuración
```bash
# Iniciar sesión en Azure
az login

# Listar todas las suscripciones
az account list

# Establecer la suscripción activa
az account set --subscription "nombre_suscripción"

# Mostrar la suscripción actual
az account show
```

## Grupos de Recursos

### Gestión de Recursos
```bash
# Crear un grupo de recursos
az group create --name miGrupoRecursos --location westeurope

# Listar grupos de recursos
az group list

# Eliminar un grupo de recursos
az group delete --name miGrupoRecursos --yes --no-wait
```

## Máquinas Virtuales

### Operaciones con VMs
```bash
# Crear una VM
az vm create \
    --resource-group miGrupoRecursos \
    --name miVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys

# Listar VMs
az vm list

# Iniciar una VM
az vm start --resource-group miGrupoRecursos --name miVM

# Detener una VM
az vm stop --resource-group miGrupoRecursos --name miVM

# Eliminar una VM
az vm delete --resource-group miGrupoRecursos --name miVM --yes
```

## Storage

### Gestión de Storage Accounts
```bash
# Crear storage account
az storage account create \
    --name mistorage \
    --resource-group miGrupoRecursos \
    --location westeurope \
    --sku Standard_LRS

# Listar storage accounts
az storage account list

# Crear un container
az storage container create \
    --account-name mistorage \
    --name micontainer

# Subir un archivo
az storage blob upload \
    --account-name mistorage \
    --container-name micontainer \
    --name archivo.txt \
    --file ./archivo.txt
```

## App Service

### Gestión de Web Apps
```bash
# Crear un plan de App Service
az appservice plan create \
    --name miPlan \
    --resource-group miGrupoRecursos \
    --sku FREE

# Crear una Web App
az webapp create \
    --name miWebApp \
    --resource-group miGrupoRecursos \
    --plan miPlan

# Desplegar código desde Git
az webapp deployment source config \
    --name miWebApp \
    --resource-group miGrupoRecursos \
    --repo-url https://github.com/usuario/repo \
    --branch master
```

## Base de Datos

### Azure SQL Database
```bash
# Crear servidor SQL
az sql server create \
    --name miservidor \
    --resource-group miGrupoRecursos \
    --location westeurope \
    --admin-user adminuser \
    --admin-password miContraseña123!

# Crear base de datos
az sql db create \
    --resource-group miGrupoRecursos \
    --server miservidor \
    --name miDB \
    --edition Basic
```

## Redes

### Virtual Networks y NSGs
```bash
# Crear Virtual Network
az network vnet create \
    --name miVnet \
    --resource-group miGrupoRecursos \
    --subnet-name default

# Crear NSG
az network nsg create \
    --name miNSG \
    --resource-group miGrupoRecursos

# Agregar regla NSG
az network nsg rule create \
    --name permitir-ssh \
    --nsg-name miNSG \
    --resource-group miGrupoRecursos \
    --priority 1000 \
    --destination-port-ranges 22 \
    --access Allow
```

## Monitoreo

### Logs y Métricas
```bash
# Ver logs de una webapp
az webapp log tail \
    --name miWebApp \
    --resource-group miGrupoRecursos

# Obtener métricas de una VM
az monitor metrics list \
    --resource miVM \
    --resource-group miGrupoRecursos \
    --resource-type "Microsoft.Compute/virtualMachines"
```

## Container Registry y Kubernetes

### ACR
```bash
# Crear registro de contenedores
az acr create \
    --name miRegistro \
    --resource-group miGrupoRecursos \
    --sku Basic

# Login en ACR
az acr login --name miRegistro

# Listar imágenes en ACR
az acr repository list --name miRegistro
```

### AKS
```bash
# Crear cluster de Kubernetes
az aks create \
    --resource-group miGrupoRecursos \
    --name miClusterAKS \
    --node-count 1 \
    --enable-addons monitoring

# Obtener credenciales
az aks get-credentials \
    --resource-group miGrupoRecursos \
    --name miClusterAKS

# Escalar cluster
az aks scale \
    --resource-group miGrupoRecursos \
    --name miClusterAKS \
    --node-count 3
```

## Tips y Trucos

### Útiles
```bash
# Formatear salida en tabla
az {comando} --output table

# Formatear salida en JSON
az {comando} --output json

# Usar queries JMESPath
az {comando} --query "[].[name,resourceGroup]"

# Activar modo debug
az {comando} --debug

# Obtener ayuda de un comando
az {comando} -h
```
