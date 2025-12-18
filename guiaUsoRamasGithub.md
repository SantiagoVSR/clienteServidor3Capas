# Guía de Uso de Ramas en GitHub

## 📚 Índice

1. [Introducción](#introducción)
2. [Conceptos Básicos](#conceptos-básicos)
3. [Flujo de Trabajo con Ramas](#flujo-de-trabajo-con-ramas)
4. [Comandos Esenciales](#comandos-esenciales)
5. [Ejemplo Práctico: Agregar Nueva Funcionalidad](#ejemplo-práctico-agregar-nueva-funcionalidad)
6. [Crear un Pull Request](#crear-un-pull-request)
7. [Resolución de Conflictos](#resolución-de-conflictos)
8. [Buenas Prácticas](#buenas-prácticas)
9. [Comandos de Referencia Rápida](#comandos-de-referencia-rápida)

---

## Introducción

Esta guía te enseñará cómo trabajar con ramas (branches) en Git y GitHub para agregar nuevas funcionalidades al proyecto de manera organizada y colaborativa.

### ¿Por qué usar ramas?

- ✅ Permite trabajar en nuevas funcionalidades sin afectar el código principal
- ✅ Facilita la colaboración entre varios desarrolladores
- ✅ Permite revisar cambios antes de integrarlos
- ✅ Mantiene el historial del proyecto organizado
- ✅ Facilita la reversión de cambios si algo sale mal

---

## Conceptos Básicos

### ¿Qué es una rama?

Una **rama (branch)** es una línea independiente de desarrollo que te permite trabajar en cambios sin modificar la rama principal (`main` o `master`).

```
main (rama principal)
  │
  ├── feature/nueva-empresa (tu nueva rama)
  │     └── commits de tu trabajo
  │
  └── feature/mejora-contratos (otra rama)
        └── commits de otro trabajo
```

### Ramas Importantes

- **`main` o `master`**: Rama principal del proyecto, contiene el código estable
- **`develop`**: Rama de desarrollo (opcional), donde se integran nuevas funcionalidades
- **`feature/nombre-funcionalidad`**: Ramas para nuevas funcionalidades
- **`bugfix/nombre-bug`**: Ramas para corregir errores
- **`hotfix/nombre-urgente`**: Ramas para correcciones urgentes

---

## Flujo de Trabajo con Ramas

### Flujo Básico

```
1. Clonar/Fork el repositorio
   ↓
2. Crear una nueva rama desde main
   ↓
3. Trabajar en tu funcionalidad
   ↓
4. Hacer commits de tus cambios
   ↓
5. Subir la rama a GitHub (push)
   ↓
6. Crear un Pull Request
   ↓
7. Revisar y resolver comentarios
   ↓
8. Merge a la rama principal
```

---

## Comandos Esenciales

### 1. Verificar el Estado Actual

```bash
# Ver en qué rama estás
git branch

# Ver el estado de tus archivos
git status

# Ver el historial de commits
git log --oneline --graph --all
```

### 2. Crear una Nueva Rama

```bash
# Opción 1: Crear y cambiar a la nueva rama
git checkout -b feature/nombre-funcionalidad

# Opción 2: Crear rama sin cambiar (Git 2.23+)
git switch -c feature/nombre-funcionalidad

# Opción 3: Crear rama desde otra rama específica
git checkout -b feature/nueva-funcionalidad main
```

### 3. Cambiar Entre Ramas

```bash
# Cambiar a otra rama
git checkout nombre-rama

# O con Git moderno
git switch nombre-rama

# Cambiar a la rama principal
git checkout main
# o
git switch main
```

### 4. Trabajar en tu Rama

```bash
# 1. Asegúrate de estar en tu rama
git checkout feature/mi-funcionalidad

# 2. Haz tus cambios en los archivos

# 3. Ver qué archivos has modificado
git status

# 4. Agregar archivos al staging
git add archivo1.py archivo2.js
# O agregar todos los cambios
git add .

# 5. Hacer commit con un mensaje descriptivo
git commit -m "Agregar funcionalidad de empleados"

# 6. Subir la rama a GitHub
git push origin feature/mi-funcionalidad
```

### 5. Sincronizar con la Rama Principal

```bash
# 1. Cambiar a la rama principal
git checkout main

# 2. Actualizar la rama principal desde GitHub
git pull origin main

# 3. Volver a tu rama
git checkout feature/mi-funcionalidad

# 4. Integrar cambios de main en tu rama
git merge main
# O mejor, usar rebase:
git rebase main
```

---

## Ejemplo Práctico: Agregar Nueva Funcionalidad

Vamos a agregar una nueva funcionalidad: **"Gestión de Empleados"** siguiendo el flujo completo.

### Paso 1: Preparar el Entorno

```bash
# 1. Clonar el repositorio (si no lo tienes)
git clone https://github.com/tu-usuario/arqCS-NCapas.git
cd arqCS-NCapas

# 2. Verificar que estás en la rama main
git checkout main

# 3. Actualizar la rama main
git pull origin main
```

### Paso 2: Crear la Nueva Rama

```bash
# Crear y cambiar a la nueva rama
git checkout -b feature/gestion-empleados

# Verificar que estás en la nueva rama
git branch
# Deberías ver un asterisco (*) junto a feature/gestion-empleados
```

### Paso 3: Trabajar en la Funcionalidad

Ahora puedes trabajar normalmente en tu código:

```bash
# Crear los archivos necesarios según la Guía del Estudiante
# - backend/app/models/empleado.py
# - backend/app/repositories/empleado_repository.py
# - backend/app/services/empleado_service.py
# - backend/app/controllers/empleado_controller.py
# - frontend/src/views/EmpleadoView.js
# etc.
```

### Paso 4: Hacer Commits Incrementales

Es buena práctica hacer commits pequeños y frecuentes:

```bash
# Commit 1: Agregar modelo de Empleado
git add backend/app/models/empleado.py
git commit -m "feat: agregar modelo Empleado (Tier 3)"

# Commit 2: Agregar repositorio
git add backend/app/repositories/empleado_repository.py
git commit -m "feat: agregar EmpleadoRepository (Tier 3)"

# Commit 3: Agregar servicio
git add backend/app/services/empleado_service.py
git commit -m "feat: agregar EmpleadoService con validaciones (Tier 2)"

# Commit 4: Agregar controlador
git add backend/app/controllers/empleado_controller.py
git commit -m "feat: agregar EmpleadoController con endpoints REST (Tier 2)"

# Commit 5: Actualizar __init__.py del backend
git add backend/app/__init__.py backend/app/models/__init__.py
git commit -m "refactor: registrar blueprint de empleados en app"

# Commit 6: Agregar vista del frontend
git add frontend/src/views/EmpleadoView.js
git commit -m "feat: agregar EmpleadoView (Tier 1)"

# Commit 7: Actualizar API service y App.js
git add frontend/src/services/api.js frontend/src/App.js
git commit -m "feat: integrar gestión de empleados en frontend"
```

### Paso 5: Subir la Rama a GitHub

```bash
# Subir la rama por primera vez
git push origin feature/gestion-empleados

# En commits posteriores, solo necesitas:
git push
```

---

## Crear un Pull Request

### Desde la Línea de Comandos (GitHub CLI)

Si tienes GitHub CLI instalado:

```bash
# Crear Pull Request directamente
gh pr create --title "Agregar gestión de empleados" \
  --body "Esta PR agrega la funcionalidad completa de gestión de empleados siguiendo la arquitectura de 3 capas." \
  --base main
```

### Desde la Interfaz Web de GitHub

1. **Ir al repositorio en GitHub**
   - Navega a `https://github.com/tu-usuario/arqCS-NCapas`

2. **Verás un banner** que dice:
   ```
   feature/gestion-empleados had recent pushes
   [Compare & pull request]
   ```
   - Haz clic en "Compare & pull request"

3. **Completar el formulario del Pull Request**:
   - **Título**: Descriptivo y claro
     ```
     Agregar gestión de empleados
     ```
   
   - **Descripción**: Explicar qué hace el PR
     ```markdown
     ## Descripción
     Esta PR agrega la funcionalidad completa de gestión de empleados siguiendo la arquitectura de 3 capas.
     
     ## Cambios Realizados
     - ✅ Modelo Empleado (Tier 3)
     - ✅ EmpleadoRepository (Tier 3)
     - ✅ EmpleadoService con validaciones (Tier 2)
     - ✅ EmpleadoController con endpoints REST (Tier 2)
     - ✅ EmpleadoView en React (Tier 1)
     - ✅ Integración en App.js
     
     ## Testing
     - [x] Probado localmente
     - [x] Endpoints funcionando correctamente
     - [x] Validaciones funcionando
     
     ## Checklist
     - [x] Código sigue el patrón MVC
     - [x] Separación de responsabilidades por tier
     - [x] Sin errores de linting
     - [x] Documentación actualizada
     ```

4. **Seleccionar revisores** (si aplica)

5. **Hacer clic en "Create pull request"**

### Buenas Prácticas para Pull Requests

- ✅ **Título descriptivo**: "Agregar gestión de empleados" es mejor que "Cambios"
- ✅ **Descripción clara**: Explica qué y por qué, no solo qué
- ✅ **Commits pequeños**: Un PR con muchos commits pequeños es mejor que uno enorme
- ✅ **Referencias**: Menciona issues relacionados con `#123`
- ✅ **Screenshots**: Si hay cambios visuales, incluye capturas

---

## Resolución de Conflictos

### ¿Qué son los conflictos?

Los conflictos ocurren cuando dos ramas modifican las mismas líneas de código de manera diferente.

### Cómo Resolver Conflictos

#### Paso 1: Actualizar tu Rama

```bash
# 1. Asegúrate de estar en tu rama
git checkout feature/gestion-empleados

# 2. Traer cambios de main
git fetch origin main

# 3. Intentar merge o rebase
git merge origin/main
# O
git rebase origin/main
```

#### Paso 2: Si hay Conflictos

Git te mostrará qué archivos tienen conflictos:

```bash
Auto-merging backend/app/__init__.py
CONFLICT (content): Merge conflict in backend/app/__init__.py
```

#### Paso 3: Resolver Manualmente

Abre el archivo con conflictos. Verás marcadores:

```python
<<<<<<< HEAD
# Tu código
from app.controllers.empleado_controller import empleado_bp
=======
# Código de main
from app.controllers.otro_controller import otro_bp
>>>>>>> origin/main
```

**Resuelve el conflicto**:
- Mantén ambas importaciones si es necesario
- Elimina los marcadores `<<<<<<<`, `=======`, `>>>>>>>`
- Asegúrate de que el código quede correcto

```python
# Solución correcta
from app.controllers.empleado_controller import empleado_bp
from app.controllers.otro_controller import otro_bp
```

#### Paso 4: Marcar como Resuelto

```bash
# Agregar el archivo resuelto
git add backend/app/__init__.py

# Si usaste merge:
git commit -m "resolve: resolver conflictos con main"

# Si usaste rebase:
git rebase --continue
```

#### Paso 5: Subir los Cambios

```bash
# Si usaste merge:
git push origin feature/gestion-empleados

# Si usaste rebase (puede requerir force push):
git push --force-with-lease origin feature/gestion-empleados
```

---

## Buenas Prácticas

### Convenciones de Nombres para Ramas

Usa prefijos descriptivos:

- `feature/` - Para nuevas funcionalidades
  ```
  feature/gestion-empleados
  feature/reporte-contratos
  feature/exportar-datos
  ```

- `bugfix/` - Para corrección de errores
  ```
  bugfix/correccion-validacion-email
  bugfix/error-calculo-precio
  ```

- `hotfix/` - Para correcciones urgentes
  ```
  hotfix/seguridad-api
  hotfix/caida-servidor
  ```

- `refactor/` - Para refactorización
  ```
  refactor/mejorar-repositorios
  refactor/optimizar-queries
  ```

- `docs/` - Para documentación
  ```
  docs/actualizar-readme
  docs/agregar-ejemplos
  ```

### Mensajes de Commit

Usa el formato **Conventional Commits**:

```
tipo(alcance): descripción breve

Descripción más detallada (opcional)

- tipo: feat, fix, docs, style, refactor, test, chore
- alcance: opcional, indica qué parte del código
- descripción: en presente, imperativo
```

**Ejemplos**:

```bash
# Nueva funcionalidad
git commit -m "feat(empleados): agregar CRUD completo de empleados"

# Corrección de bug
git commit -m "fix(contratos): corregir validación de fechas"

# Documentación
git commit -m "docs(readme): actualizar instrucciones de instalación"

# Refactorización
git commit -m "refactor(services): mejorar validaciones de negocio"

# Estilo/formato
git commit -m "style(frontend): formatear código con prettier"
```

### Frecuencia de Commits

- ✅ **Commits pequeños y frecuentes**: Cada cambio lógico en un commit separado
- ✅ **Commits atómicos**: Un commit debe representar un cambio completo y funcional
- ❌ **Evita**: Commits enormes con muchos cambios no relacionados

**Ejemplo Bueno**:
```bash
git commit -m "feat(models): agregar modelo Empleado"
git commit -m "feat(repositories): agregar EmpleadoRepository"
git commit -m "feat(services): agregar validaciones de empleado"
```

**Ejemplo Malo**:
```bash
git commit -m "agregar empleados"  # Muy vago, muchos cambios juntos
```

### Mantener tu Rama Actualizada

```bash
# Regularmente sincroniza con main
git checkout main
git pull origin main
git checkout feature/tu-rama
git rebase main  # O git merge main
```

### Antes de Crear el PR

```bash
# 1. Verificar que todo funciona
./run.sh install
./run.sh backend  # En una terminal
./run.sh frontend # En otra terminal

# 2. Verificar linting
cd backend
flake8 app/
cd ../frontend
npm run lint

# 3. Verificar que no hay errores
git status
git diff main  # Ver todos tus cambios

# 4. Asegurarte de estar actualizado
git checkout main
git pull origin main
git checkout feature/tu-rama
git rebase main
```

---

## Comandos de Referencia Rápida

### Configuración Inicial

```bash
# Configurar tu identidad (solo primera vez)
git config --global user.name "Tu Nombre"
git config --global user.email "tu.email@ejemplo.com"

# Ver configuración
git config --list
```

### Trabajo Diario con Ramas

```bash
# Ver ramas locales
git branch

# Ver todas las ramas (locales y remotas)
git branch -a

# Crear nueva rama
git checkout -b feature/nombre

# Cambiar de rama
git checkout nombre-rama

# Ver diferencias con main
git diff main

# Ver historial de commits
git log --oneline --graph --all
```

### Sincronización

```bash
# Traer cambios del remoto
git fetch origin

# Actualizar rama actual
git pull origin main

# Subir cambios
git push origin nombre-rama

# Subir y establecer upstream
git push -u origin nombre-rama
```

### Limpieza

```bash
# Eliminar rama local (después de merge)
git branch -d nombre-rama

# Eliminar rama local forzadamente
git branch -D nombre-rama

# Eliminar rama remota
git push origin --delete nombre-rama
```

---

## Ejemplo Completo: Flujo de Trabajo

### Escenario: Agregar Reporte de Contratos

```bash
# 1. Preparar
git checkout main
git pull origin main

# 2. Crear rama
git checkout -b feature/reporte-contratos

# 3. Trabajar
# ... hacer cambios en los archivos ...

# 4. Commits incrementales
git add backend/app/services/contrato_service.py
git commit -m "feat(services): agregar método generarReporte"

git add backend/app/controllers/contrato_controller.py
git commit -m "feat(controllers): agregar endpoint GET /api/contratos/reporte"

git add frontend/src/views/ContratoView.js
git commit -m "feat(frontend): agregar componente de reporte"

# 5. Sincronizar con main
git checkout main
git pull origin main
git checkout feature/reporte-contratos
git rebase main

# 6. Subir rama
git push origin feature/reporte-contratos

# 7. Crear PR en GitHub (interfaz web o gh cli)
gh pr create --title "Agregar reporte de contratos" \
  --body "Implementa funcionalidad de generación de reportes de contratos"
```

---

## Troubleshooting

### Error: "Your branch is ahead of 'origin/main'"

```bash
# Simplemente sube tus cambios
git push origin nombre-rama
```

### Error: "Updates were rejected because the remote contains work"

```bash
# Trae los cambios remotos primero
git pull origin nombre-rama
# Resuelve conflictos si los hay
git push origin nombre-rama
```

### Error: "Cannot switch branch, uncommitted changes"

```bash
# Opción 1: Hacer commit de los cambios
git add .
git commit -m "WIP: trabajo en progreso"

# Opción 2: Guardar cambios temporalmente (stash)
git stash
git checkout otra-rama
# ... trabajar ...
git checkout rama-original
git stash pop  # Recuperar cambios
```

### Deshacer Cambios

```bash
# Deshacer cambios en archivos no commiteados
git checkout -- archivo.py

# Deshacer último commit (mantener cambios)
git reset --soft HEAD~1

# Deshacer último commit (eliminar cambios)
git reset --hard HEAD~1  # ⚠️ CUIDADO: elimina cambios permanentemente
```

---

## Recursos Adicionales

- [Documentación oficial de Git](https://git-scm.com/doc)
- [GitHub Guides - Understanding the GitHub Flow](https://guides.github.com/introduction/flow/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Branching Model](https://nvie.com/posts/a-successful-git-branching-model/)

---

## Conclusión

Trabajar con ramas te permite:

- ✅ Desarrollar nuevas funcionalidades de forma aislada
- ✅ Colaborar sin interferir con el trabajo de otros
- ✅ Revisar código antes de integrarlo
- ✅ Mantener un historial limpio y organizado

**Recuerda**:
- Crea ramas descriptivas con prefijos claros
- Haz commits pequeños y frecuentes
- Mantén tu rama actualizada con main
- Crea PRs claros y descriptivos
- Resuelve conflictos cuidadosamente

¡Buena suerte con tu desarrollo! 🚀

