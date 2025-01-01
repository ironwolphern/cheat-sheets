# Vagrant Commands Cheatsheet

## Gestión de Máquinas Virtuales

### Comandos Básicos
```bash
# Iniciar proyecto
vagrant init [box-name]              # Inicializa un nuevo proyecto Vagrant con un Vagrantfile
vagrant up                           # Crea e inicia la máquina virtual
vagrant halt                         # Detiene la máquina virtual
vagrant destroy                      # Elimina la máquina virtual por completo
vagrant destroy -f                   # Elimina la máquina virtual sin confirmación
vagrant reload                       # Reinicia la máquina virtual y carga nueva configuración
```

### Estado y Acceso
```bash
vagrant status                       # Muestra el estado de la máquina virtual
vagrant global-status                # Muestra el estado de todas las máquinas virtuales
vagrant global-status --prune        # Muestra el estado y elimina entradas inválidas
vagrant ssh                         # Conecta por SSH a la máquina virtual
vagrant ssh [nombre]                 # Conecta por SSH a una máquina específica
vagrant ssh-config                  # Muestra la configuración SSH
```

### Gestión de Boxes
```bash
vagrant box list                    # Lista todas las boxes instaladas
vagrant box add [nombre] [url]      # Añade una nueva box
vagrant box remove [nombre]         # Elimina una box
vagrant box update                  # Actualiza la box a la última versión
vagrant box outdated                # Comprueba si hay actualizaciones de boxes
vagrant box prune                   # Elimina versiones antiguas de boxes
```

### Snapshots
```bash
vagrant snapshot save [nombre]      # Crea un snapshot
vagrant snapshot restore [nombre]   # Restaura un snapshot
vagrant snapshot list              # Lista todos los snapshots
vagrant snapshot delete [nombre]    # Elimina un snapshot
```

### Provisioning
```bash
vagrant provision                   # Ejecuta los provisioners configurados
vagrant provision --debug           # Ejecuta provisioners con modo debug
vagrant up --provision             # Inicia la máquina y ejecuta provisioners
vagrant reload --provision         # Reinicia y ejecuta provisioners
```

### Networking
```bash
vagrant port                        # Muestra el mapeo de puertos
vagrant share                       # Comparte la máquina virtual públicamente
```

### Plugins
```bash
vagrant plugin list                 # Lista plugins instalados
vagrant plugin install [nombre]     # Instala un plugin
vagrant plugin uninstall [nombre]   # Desinstala un plugin
vagrant plugin update [nombre]      # Actualiza un plugin específico
```

### Depuración
```bash
vagrant status --debug                       # Muestra información detallada de depuración
vagrant up --debug                           # Inicia con logs de depuración
vagrant up --provision \| tee provision.log  # Logs de provisioners
vagrant ssh -- -v                            # Conecta SSH con modo verbose
```

### Comandos Avanzados
```bash
vagrant resume                      # Reanuda una máquina suspendida
vagrant suspend                     # Suspende la máquina virtual
vagrant package                     # Empaqueta la máquina virtual en una box
vagrant push                        # Despliega el proyecto según la configuración
```

### Variables de Entorno Útiles
```bash
VAGRANT_HOME                        # Directorio base de Vagrant
VAGRANT_LOG=debug                   # Nivel de logging
VAGRANT_NO_COLOR=1                  # Desactiva la salida con colores
```

## Tips Adicionales

1. Para usar una box específica:
   ```bash
   vagrant init hashicorp/bionic64
   ```

2. Para forzar la destrucción sin confirmación:
   ```bash
   vagrant destroy -f
   ```

3. Para verificar la sintaxis del Vagrantfile:
   ```bash
   vagrant validate
   ```

4. Para conectar a una máquina específica en un entorno multi-máquina:
   ```bash
   vagrant ssh [nombre-maquina]
   ```

5. Para ver los logs detallados:
   ```bash
   VAGRANT_LOG=debug vagrant up
   ```
