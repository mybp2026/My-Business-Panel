# 🧭 Guía de Contribución

Este documento define el flujo de trabajo, estructura de ramas y reglas que todo el equipo de desarrollo debe seguir al colaborar en este repositorio.  
El objetivo es mantener un proceso ordenado, reproducible y sin conflictos, garantizando la calidad del código en cada entorno.

---

## 📁 Estructura de ramas

El repositorio cuenta con las siguientes ramas principales:

| Rama        | Descripción                                                                                       | Política de cambios                                                 |
| ----------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| master      | Ambiente de **producción**. Contiene código estable y datos reales.                               | 🔒 Solo se actualiza mediante _merge_ desde `staging`.              |
| staging     | Ambiente de **preproducción** o _QA_. Simula producción con datos no reales.                      | 🔒 Solo se actualiza mediante _merge_ desde `development`.          |
| development | Ambiente de **integración**. Recibe los _pull requests_ aprobados de cada desarrollador.          | 🔒 Solo se actualiza mediante PRs desde ramas personales (`dev/*`). |
| dev/\*      | Ramas personales de cada desarrollador (por ejemplo, `dev/david`). Espacio de trabajo individual. | ✏️ Libre commit y push directo.<br>                                 |

---

## 🧩 Convenciones de nombres de ramas

| Tipo de rama       | Formato                                 | Ejemplo                   |
| ------------------ | --------------------------------------- | ------------------------- |
| Rama personal      | `dev/<nombre>`                          | `dev/david`               |
| Subrama de feature | `dev/<nombre>/feature/<nombre-feature>` | `dev/david/feature/login` |
| Hotfix urgente     | `hotfix/<nombre-hotfix>`                | `hotfix/fix-login-error`  |
| Bugfix menor       | `bugfix/<nombre-bug>`                   | `bugfix/form-validation`  |

> 💡 Siempre usar nombres en minúsculas, separados por guiones (`-`), y sin espacios.

---

## ⚙️ Flujo de trabajo general

### 1️⃣ Clonar el repositorio

```bash
git clone git@github.com:<organizacion>/<repositorio>.git
cd <repositorio>
```

### 2️⃣ Crear y configurar tu rama personal

Cada desarrollador trabaja sobre su rama dev/<nombre> derivada de development.

```bash
git checkout development
git pull origin development
git checkout -b dev/david
git push -u origin dev/david
```

Esta rama será tu zona de trabajo.
Puedes subir commits y realizar pruebas sin afectar a los demás.

### 3️⃣ Mantener tu rama actualizada

Antes de comenzar a trabajar cada día, sincroniza tu rama personal con development:

```bash
git checkout dev/david
git fetch origin
git rebase origin/development
# Resolver conflictos si los hay
git rebase --continue
```

Siempre trabaja sobre la versión más reciente del código base.

### 4️⃣ Crear subramas por feature (opcional, pero recomendado)

Si trabajas en múltiples tareas simultáneamente:

```bash
git checkout dev/david
git checkout -b dev/david/feature/login
```

Al terminar, haz un Pull Request desde esa subrama hacia development.

### 6️⃣ Crear Pull Request (PR)

Cuando completes una feature o conjunto de cambios listos para integrar:

- Asegúrate de que tu rama esté actualizada con development.
- Haz commit de tus cambios.
- Crea un Pull Request (PR) desde tu rama hacia development.

```bash
dev/david → development
```

### 7️⃣ Merge y despliegue

Flujo de integración:

dev/tu-nombre → development → staging → master

- Merge a development: integración de código validado.
- Merge a staging: tras pruebas funcionales exitosas.
- Merge a master: solo cuando se confirma la estabilidad total.

**🚫 Está prohibido hacer push directo a development, staging o master.**

## ⚡ Ejemplo de flujo completo

```bash
# 1. Crear tu rama personal
git checkout -b dev/david
git push -u origin dev/david

# 2. Crear una subrama de feature
git checkout -b dev/david/feature/login

# 3. Desarrollar y hacer commits
git add .
git commit -m "feat(auth): agregar endpoint de login"
git push origin dev/david/feature/login

# 4. Crear un Pull Request → development
# 5. Esperar aprobación y merge
# 6. Actualizar tu rama personal después del merge
git checkout dev/david
git fetch origin
git rebase origin/development

```
