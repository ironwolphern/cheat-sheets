# HashiCorp Packer - Cheatsheet Completa de Comandos

## Comandos Básicos

### Inicialización y Validación
```bash
# Inicializar un directorio de Packer
packer init .

# Validar la sintaxis de un template
packer validate template.pkr.hcl

# Formatear el código HCL
packer fmt template.pkr.hcl
```

### Construcción de Imágenes
```bash
# Construir una imagen
packer build template.pkr.hcl

# Construir una imagen específica del template
packer build -only=amazon-ebs template.pkr.hcl

# Construir con variables
packer build -var 'aws_access_key=foo' template.pkr.hcl

# Construir con archivo de variables
packer build -var-file=vars.pkrvars.hcl template.pkr.hcl

# Construir en modo debug
packer build -debug template.pkr.hcl
```

### Inspección y Consulta
```bash
# Inspeccionar un template
packer inspect template.pkr.hcl

# Mostrar versión de Packer
packer version

# Listar builders disponibles
packer plugins installed
```

## Opciones Avanzadas

### Control de Ejecución
```bash
# Forzar construcción sin confirmación
packer build -force template.pkr.hcl

# Construcción en paralelo
packer build -parallel-builds=2 template.pkr.hcl

# Tiempo máximo de espera
packer build -timeout=1h30m template.pkr.hcl
```

### Debug y Logging
```bash
# Habilitar logs detallados
PACKER_LOG=1 packer build template.pkr.hcl

# Especificar archivo de log
PACKER_LOG_PATH=packer.log packer build template.pkr.hcl

# Modo debug con pausa en cada paso
packer build -debug template.pkr.hcl
```

### Manejo de Variables
```bash
# Usar variables de entorno
PKR_VAR_aws_region=us-west-2 packer build template.pkr.hcl

# Múltiples archivos de variables
packer build \
  -var-file=common.pkrvars.hcl \
  -var-file=prod.pkrvars.hcl \
  template.pkr.hcl
```

### Plugins y Extensiones
```bash
# Instalar un plugin
packer plugins install github.com/hashicorp/amazon

# Actualizar plugins
packer plugins install -upgrade github.com/hashicorp/amazon

# Listar plugins instalados
packer plugins installed
```

## Buenas Prácticas

### Variables Sensibles
```bash
# Usar variables de entorno para credenciales
export PKR_VAR_aws_secret_key="tu-clave-secreta"
packer build template.pkr.hcl

# Archivo de variables secretas (no comitear)
packer build -var-file=secrets.pkrvars.hcl template.pkr.hcl
```

### Validación y Testing
```bash
# Validar sintaxis y variables requeridas
packer validate -syntax-only template.pkr.hcl

# Validar con variables
packer validate \
  -var-file=test.pkrvars.hcl \
  template.pkr.hcl
```

### Gestión de Caché
```bash
# Limpiar caché de Packer
packer plugins clean

# Forzar descarga de plugins
packer init -upgrade
```

## Sintaxis HCL Común

```hcl
# Definición básica de source
source "amazon-ebs" "example" {
  ami_name = "example-ami"
  instance_type = "t2.micro"
  region = "us-west-2"
  source_ami_filter {
    most_recent = true
    owners = ["amazon"]
  }
}

# Build block básico
build {
  sources = ["source.amazon-ebs.example"]
  
  provisioner "shell" {
    inline = ["echo 'Hello, World!'"]
  }
  
  post-processor "manifest" {
    output = "manifest.json"
  }
}
```

## Tips y Trucos

1. Usa `packer fmt` antes de cada commit para mantener consistencia en el código
2. Implementa variables para valores reutilizables
3. Utiliza `source blocks` para definiciones de imagen reutilizables
4. Aprovecha el sistema de plugins para extender funcionalidad
5. Mantén los secretos fuera del código usando variables de entorno
6. Usa tags para organizar y rastrear imágenes
7. Implementa manifiestos para documentar builds
8. Utiliza provisioners en orden lógico
9. Aprovecha los post-processors para tareas adicionales
10. Mantén los templates modulares y reutilizables