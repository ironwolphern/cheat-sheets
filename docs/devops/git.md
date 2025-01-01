# Git Command Cheatsheet 🚀

## Configuración Inicial
```bash
# Configurar nombre y email
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"

# Configuración adicional
git config --global core.editor "editor"      # Editor por defecto
git config --global color.ui true/false/auto  # Colores en la terminal

# Ver configuración actual
git config --list
```

## Comandos Básicos
```bash
# Iniciar un repositorio
git init

# Clonar un repositorio
git clone <url> # Clonar repositorio remoto
git clone <url> <nombre> # Clonar con nombre personalizado
git clone <url> --branch <rama> # Clonar rama específica
git clone <url> --depth 1 # Clonar solo la última versión
git clone <url> --shallow-submodules # Clonar submódulos sin historial
git clone <url> --recurse-submodules # Clonar con submódulos

# Ver estado del repositorio
git status

# Añadir archivos al staging area
git add <archivo>  # Añadir archivo específico
git add .          # Añadir todos los archivos
git add *.js       # Añadir archivos por patrón

# Crear commit
git commit -m "mensaje"  # Commit con mensaje
git commit -am "mensaje" # Add + commit para archivos tracked

# Ver historial
git log            # Ver historial completo
git log --oneline  # Ver historial resumido
git log --graph    # Ver historial con gráfico
```

## Ramas (Branches)
```bash
# Gestión de ramas
git branch              # Ver ramas locales
git branch -a           # Ver todas las ramas (incluidas remotas)
git branch <nombre>     # Crear rama
git branch -d <nombre>  # Eliminar rama
git branch -D <nombre>  # Forzar eliminación de rama

# Cambiar de rama
git checkout <rama>     # Cambiar a una rama existente
git checkout -b <rama>  # Crear y cambiar a nueva rama
git switch <rama>       # Cambiar a una rama (Git moderno)
git switch -c <rama>    # Crear y cambiar a nueva rama (Git moderno)
```

## Fusionar y Rebasar
```bash
# Fusionar ramas
git merge <rama>   # Fusionar rama con la actual
git merge --abort  # Abortar fusión en caso de conflictos

# Rebase
git rebase <rama>     # Rebasar rama actual sobre otra
git rebase -i HEAD~3  # Rebase interactivo de últimos 3 commits
```

## Trabajo Remoto
```bash
# Gestionar remotos
git remote add origin <url>        # Añadir remoto
git remote add <nombre> <url>      # Añadir remoto con nombre
git remote -v                      # Ver remotos configurados
git remote show <nombre>           # Ver información de remoto
git remote rename <nombre> <nuevo> # Renombrar remoto
git remote remove <nombre>         # Eliminar remoto

# Sincronizar con remoto
git fetch origin           # Traer cambios sin fusionar
git pull origin <rama>     # Traer y fusionar cambios
git push origin <rama>     # Enviar cambios al remoto
git push -u origin <rama>  # Push y establecer upstream
```

## Gestión de Cambios
```bash
# Ver diferencias
git diff                  # Ver cambios no staged
git diff --staged         # Ver cambios staged
git diff <rama1> <rama2>  # Comparar ramas

# Deshacer cambios
git restore <archivo>        # Descartar cambios en archivo
git restore --staged <archivo> # Quitar archivo del staging
git reset --hard HEAD~1      # Eliminar último commit
git reset --soft HEAD~1      # Eliminar último commit manteniendo cambios
git reset --hard             # Eliminar todos los cambios
git revert <commit>          # Crear nuevo commit que deshace cambios
```

## Stash (Guardado Temporal)
```bash
git stash                    # Guardar cambios en stash
git stash list              # Ver lista de stashes
git stash pop               # Aplicar y eliminar último stash
git stash apply             # Aplicar último stash sin eliminarlo
git stash drop              # Eliminar último stash
git stash clear             # Eliminar todos los stashes
```

## Etiquetas (Tags)
```bash
git tag                      # Listar tags
git tag -a v1.0 -m "mensaje" # Crear tag anotado
git tag v1.0                # Crear tag ligero
git push origin v1.0        # Subir tag específico
git push origin --tags      # Subir todos los tags
```

## Herramientas Avanzadas
```bash
# Buscar en el historial
git grep "texto"            # Buscar texto en archivos
git blame <archivo>         # Ver quién modificó cada línea
git reflog                  # Ver historial de referencias

# Limpieza
git clean -n                # Ver qué archivos se eliminarían
git clean -f                # Eliminar archivos no tracked
git clean -fd               # Eliminar archivos y directorios no tracked

# Submodulos
git submodule add <url>     # Añadir submódulo
git submodule update --init # Inicializar submódulos
```

## Consejos Pro 💡
1. Usa `git commit --amend` para modificar el último commit
2. Utiliza aliases para comandos frecuentes en `.gitconfig`
3. Configura un `.gitignore` global para archivos comunes
4. Usa `git reflog` para recuperar commits "perdidos"
5. Aprende a usar `git bisect` para encontrar bugs
6. Utiliza `git cherry-pick` para aplicar commits específicos

## Configuración Recomendada
```bash
# Aliases útiles
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'

# Configuración de color
git config --global color.ui true

# Editor predeterminado
git config --global core.editor "code --wait"
```
