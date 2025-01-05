# Terraform Command Cheatsheet

## Comandos Básicos

### Inicialización y Configuración
```bash
# Inicializar un directorio de trabajo de Terraform
terraform init

# Inicializar y descargar proveedores específicos
terraform init -upgrade

# Actualizar solo módulos específicos
terraform init -get-plugins=false

# Configurar backend remoto
terraform init -backend-config="path/to/config.hcl"
```

### Planificación y Aplicación
```bash
# Crear un plan de ejecución
terraform plan

# Crear un plan y guardarlo en un archivo
terraform plan -out=plan.tfplan

# Crear un plan de destrucción
terraform plan -destroy

# Aplicar cambios
terraform apply

# Aplicar un plan guardado
terraform apply plan.tfplan

# Aplicar cambios a recursos específicos
terraform apply -target=aws_instance.example

# Aplicar cambios automáticamente sin aprobación
terraform apply -auto-approve

# Aplicar número de cambios simultáneamente
terraform apply -parallelism=10

# No reconciliar el estado con recursos reales
terraform apply -refresh=false

# Bloquear el estado para evitar modificaciones
terraform apply -lock=true
```

### Destrucción y Limpieza
```bash
# Destruir todos los recursos
terraform destroy

# Destruir recursos específicos
terraform destroy -target=aws_instance.example

# Destruir automáticamente sin aprobación
terraform destroy -auto-approve
```

## Comandos de Workspace

```bash
# Listar workspaces
terraform workspace list

# Crear nuevo workspace
terraform workspace new dev

# Seleccionar workspace
terraform workspace select prod

# Mostrar workspace actual
terraform workspace show

# Eliminar workspace
terraform workspace delete dev
```

## Comandos de Estado

```bash
# Listar recursos en el estado
terraform state list

# Mostrar estado de un recurso específico
terraform state show aws_instance.example

# Mover recurso en el estado
terraform state mv aws_instance.example aws_instance.new

# Eliminar recurso del estado
terraform state rm aws_instance.example

# Remplazar recurso en el estado
terraform state replace-provider registry.terraform.io/hashicorp/aws registry.terraform.io/custom/aws

# Generar archivo de estado
terraform state pull > terraform.tfstate

# Importar recurso existente al estado
terraform import aws_instance.example i-1234567890abcdef0

# Actualizar estado desde infraestructura remota
terraform refresh
```

## Comandos de Validación y Formateo

```bash
# Validar configuración
terraform validate

# Formatear archivos
terraform fmt

# Formatear recursivamente todos los archivos
terraform fmt -recursive

# Verificar si los archivos están formateados
terraform fmt -check
```

## Comandos de Providers

```bash
# Listar providers instalados
terraform providers

# Actualizar providers
terraform providers mirror

# Eliminar providers no utilizados
terraform init -upgrade
```

## Comandos de Testing

```bash
# Ejecutar tests
terraform test

# Ejecutar tests con verbose
terraform test -verbose
```

## Variables y Outputs

```bash
# Establecer variable en línea de comando
terraform plan -var="instance_count=2"

# Usar archivo de variables
terraform plan -var-file="variables.tfvars"

# Usar archivo de variables con apply
terraform apply -var-file="variables.tfvars"

# Mostrar outputs
terraform output

# Mostrar output específico
terraform output instance_ip

# Mostrar outputs en formato JSON
terraform output -json
```

## Comandos Avanzados

```bash
# Generar gráfico de dependencias
terraform graph

# Mostrar versión
terraform version

# Desbloquear estado
terraform force-unlock LOCK_ID

# Marcar recurso para recreación
terraform taint aws_instance.example

# Desmarcar recurso marcado
terraform untaint aws_instance.example

# Mostrar información del workspace
terraform show
```

## Comandos de Terraform Cloud

```bash
# Iniciar sesión en Terraform Cloud
terraform login

# Cerrar sesión en Terraform Cloud
terraform logout
```

## Mejores Prácticas y Tips

1. Siempre ejecutar `terraform plan` antes de `terraform apply`
2. Usar `-target` con precaución, solo para casos específicos
3. Mantener el estado en un backend remoto
4. Utilizar workspaces para diferentes entornos
5. Versionar el código de infraestructura
6. Documentar las variables y outputs
7. Utilizar módulos para reutilizar código
8. Mantener los secrets fuera del código
9. Realizar backups regulares del estado
10. Implementar pruebas automatizadas

## Variables de Entorno Comunes

```bash
# Configuración de credenciales
export TF_VAR_access_key="YOUR_ACCESS_KEY"
export TF_VAR_secret_key="YOUR_SECRET_KEY"

# Configuración de logs
export TF_LOG=DEBUG
export TF_LOG_PATH="terraform.log"

# Configuración de CLI
export TF_CLI_ARGS="-input=false"
export TF_CLI_ARGS_plan="-refresh=false"
```
