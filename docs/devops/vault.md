# HashiCorp Vault - Cheatsheet Completa

## Configuración Inicial y Gestión del Servidor

### Inicialización y Gestión Básica
```bash
# Inicializar Vault
vault operator init

# Desbloquear Vault
vault operator unseal

# Verificar estado
vault status

# Comprobar versión
vault version
```

### Gestión del Servidor
```bash
# Iniciar servidor en modo dev
vault server -dev

# Iniciar servidor en modo producción
vault server -config=config.hcl

# Rotación de las claves de sellado
vault operator rekey
```

## Autenticación y Gestión de Tokens

### Autenticación
```bash
# Login con token
vault login <token>

# Login con userpass
vault login -method=userpass username=<user>

# Login con GitHub
vault login -method=github token=<token>
```

### Gestión de Tokens
```bash
# Crear nuevo token
vault token create

# Crear token con rol específico
vault token create -role=<role_name>

# Revocar token
vault token revoke <token>

# Renovar token
vault token renew <token>

# Ver información del token actual
vault token lookup
```

## Gestión de Secretos

### Secrets KV Version 2
```bash
# Escribir secreto
vault kv put secret/app/config username=admin password=secret

# Leer secreto
vault kv get secret/app/config

# Listar secretos
vault kv list secret/app

# Eliminar secreto
vault kv delete secret/app/config

# Recuperar versión anterior
vault kv undelete -versions=2 secret/app/config

# Ver historial de versiones
vault kv metadata get secret/app/config
```

### Políticas
```bash
# Crear política
vault policy write my-policy policy.hcl

# Leer política
vault policy read my-policy

# Listar políticas
vault policy list

# Eliminar política
vault policy delete my-policy
```

## Gestión de Auth Methods

### Configuración de Métodos de Autenticación
```bash
# Habilitar método de autenticación
vault auth enable userpass

# Listar métodos habilitados
vault auth list

# Deshabilitar método
vault auth disable userpass

# Configurar método userpass
vault write auth/userpass/users/myuser password=secret
```

## Gestión de Secrets Engines

### Operaciones Básicas
```bash
# Habilitar secrets engine
vault secrets enable -path=secret kv

# Listar secrets engines
vault secrets list

# Deshabilitar secrets engine
vault secrets disable secret/

# Mover secrets engine
vault secrets move secret/ new-path/
```

## Lease y Rotación

### Gestión de Leases
```bash
# Listar leases
vault list sys/leases/lookup/

# Revocar lease
vault lease revoke <lease_id>

# Renovar lease
vault lease renew <lease_id>

# Revocar todos los leases de un prefijo
vault lease revoke -prefix auth/token/create
```

## Herramientas Útiles

### Auditoría y Monitoreo
```bash
# Habilitar auditoría
vault audit enable file file_path=/var/log/vault_audit.log

# Listar dispositivos de auditoría
vault audit list

# Deshabilitar auditoría
vault audit disable file/
```

### Operaciones de Backup
```bash
# Crear snapshot
vault operator raft snapshot save backup.snap

# Restaurar snapshot
vault operator raft snapshot restore backup.snap
```

## Ejemplos de Configuración

### Ejemplo de Política (policy.hcl)
```hcl
path "secret/data/app/*" {
  capabilities = ["create", "read", "update", "delete", "list"]
}

path "auth/token/create" {
  capabilities = ["create", "read", "update"]
}
```

### Ejemplo de Configuración del Servidor (config.hcl)
```hcl
storage "raft" {
  path = "/vault/data"
  node_id = "node1"
}

listener "tcp" {
  address = "0.0.0.0:8200"
  tls_disable = 1
}

api_addr = "http://127.0.0.1:8200"
cluster_addr = "https://127.0.0.1:8201"
```

## Tips y Mejores Prácticas

1. Siempre mantén backups de las claves de sellado y el token root
2. Utiliza políticas con el mínimo privilegio necesario
3. Rota regularmente los tokens y credenciales
4. Habilita la auditoría en producción
5. Configura TLS para todas las comunicaciones en producción
6. Implementa alta disponibilidad para entornos críticos
7. Mantén un registro de todas las políticas y cambios de configuración
