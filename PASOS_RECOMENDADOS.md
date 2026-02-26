# Pasos recomendados: publicar el workshop

Guía paso a paso para dejar el workshop listo para compartir con otros desarrolladores.

---

## Paso 1: Definir la URL de tu repositorio

Antes de editar nada, decide cómo se llamará el repo en GitHub y en qué organización/cuenta vivirá.

**Ejemplos:**

- Cuenta personal: `https://github.com/tu-usuario/talkwalker-api-workshop`
- Organización: `https://github.com/mi-empresa/talkwalker-api-workshop`

La **ruta corta** para reemplazar en los archivos es: `tu-usuario/talkwalker-api-workshop` o `mi-empresa/talkwalker-api-workshop`.

---

## Paso 2: Reemplazar la URL en el README

1. Abre `talkwalker-api-workshop/README.md`.
2. Busca todas las apariciones de `TU_ORG/talkwalker-api-workshop`.
3. Sustitúyelas por tu ruta real, por ejemplo: `tu-usuario/talkwalker-api-workshop`.

**Buscar y reemplazar:**

- Buscar: `TU_ORG/talkwalker-api-workshop`
- Reemplazar por: `tu-usuario/talkwalker-api-workshop` (o la que uses)

Deberías tener **11 reemplazos** (una en el texto + una por cada badge de Colab en la tabla).

---

## Paso 3: Reemplazar la URL en mkdocs.yml

1. Abre `talkwalker-api-workshop/mkdocs.yml`.
2. Localiza la línea:
   ```yaml
   repo_url: https://github.com/your-org/talkwalker-api-workshop
   ```
3. Cámbiala por tu URL completa, por ejemplo:
   ```yaml
   repo_url: https://github.com/tu-usuario/talkwalker-api-workshop
   ```

Así el enlace "Repository" del sitio MkDocs apuntará a tu repo.

---

## Paso 4: Crear el repositorio en GitHub

1. Entra en [GitHub](https://github.com) e inicia sesión.
2. Clic en **"+"** (arriba derecha) → **"New repository"**.
3. Configuración recomendada:
   - **Repository name:** `talkwalker-api-workshop`
   - **Description:** (opcional) "Workshop API Talkwalker: documentación y notebooks Colab"
   - **Visibility:** Public (o Private si solo es para tu equipo).
   - **No** marques "Add a README", "Add .gitignore" ni "Choose a license" (ya tienes contenido).
4. Clic en **"Create repository"**.
5. Anota la URL del repo que te muestra GitHub (ej. `https://github.com/tu-usuario/talkwalker-api-workshop.git`). La usarás en el siguiente paso.

---

## Paso 5: Subir el contenido del workshop a GitHub

El objetivo es que el **repositorio en GitHub contenga solo la carpeta del workshop** (README, docs, notebooks), no el resto del proyecto. Para eso, Git debe estar inicializado **dentro** de `talkwalker-api-workshop`.

**Importante:** Si `talkwalker-api-workshop` está dentro de otro repo (por ejemplo "Talkwalker Esteroides v2"), no hagas `git init` en la carpeta padre. Sigue los pasos **desde dentro** de `talkwalker-api-workshop`.

---

### 5.1 Abrir terminal e ir a la carpeta del workshop

Abre **PowerShell** o **Terminal** y navega hasta la carpeta del workshop. Puedes hacerlo de dos formas:

**Opción A – Desde la raíz de tu proyecto (donde está la carpeta `talkwalker-api-workshop`):**

```powershell
cd talkwalker-api-workshop
```

**Opción B – Ruta completa (ajusta si tu proyecto está en otra ruta):**

```powershell
cd "C:\Users\Nicolás\.cursor\Talkwalker Esteroides v2\talkwalker-api-workshop"
```

Comprueba que estás dentro del workshop:

```powershell
dir
```

Deberías ver `README.md`, `mkdocs.yml`, las carpetas `docs` y `notebooks`, etc.

---

### 5.2 Inicializar Git en esta carpeta

```powershell
git init
```

Verás algo como: `Initialized empty Git repository in .../talkwalker-api-workshop/.git/`

---

### 5.3 Conectar con el repositorio de GitHub

Sustituye `tu-usuario` por tu usuario (o organización) de GitHub. La URL debe ser la del repo que creaste en el Paso 4.

```powershell
git remote add origin https://github.com/tu-usuario/talkwalker-api-workshop.git
```

Si ya habías añadido un `origin` antes y quieres actualizarlo:

```powershell
git remote set-url origin https://github.com/tu-usuario/talkwalker-api-workshop.git
```

---

### 5.4 Añadir todos los archivos y hacer el primer commit

```powershell
git add .
```

Revisa qué se va a subir:

```powershell
git status
```

Deberían aparecer como "new file" o "to be committed": README, mkdocs.yml, docs/*, notebooks/*, PASOS_RECOMENDADOS.md, etc.

Crea el commit:

```powershell
git commit -m "Workshop Talkwalker API: docs + notebooks Colab"
```

---

### 5.5 Nombrar la rama principal y subir a GitHub

Asegura que la rama se llame `main` (GitHub suele usar este nombre por defecto):

```powershell
git branch -M main
```

Sube el contenido a GitHub:

```powershell
git push -u origin main
```

**Si te pide autenticación:**

- **Usuario:** tu nombre de usuario de GitHub.
- **Contraseña:** no uses la contraseña de la cuenta. Usa un **Personal Access Token (PAT)**.
  - Crear un token: GitHub → tu foto (arriba derecha) → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)** → **Generate new token**. Dale un nombre, marca el permiso `repo` y genera. Copia el token y úsalo como "contraseña" en la terminal.

**Si aparece un error de "rejected" o "failed to push":**

- Comprueba que en GitHub el repositorio esté vacío (sin README inicial creado en la web). Si añadiste algo en el Paso 4, en la pantalla del repo GitHub te dará comandos alternativos; si ya hay un commit, puede que tengas que hacer `git pull origin main --rebase` y luego `git push -u origin main`.

---

### Resumen del Paso 5 (copiar y pegar en orden)

Sustituye `tu-usuario` por tu usuario o organización de GitHub antes de ejecutar.

```powershell
cd talkwalker-api-workshop
git init
git remote add origin https://github.com/tu-usuario/talkwalker-api-workshop.git
git add .
git status
git commit -m "Workshop Talkwalker API: docs + notebooks Colab"
git branch -M main
git push -u origin main
```

---

## Paso 6: Comprobar que "Open in Colab" funciona

1. Abre tu repositorio en GitHub en el navegador.
2. Entra en `notebooks/` y abre cualquier `.ipynb`.
3. Arriba del notebook deberías ver el botón **"Open in Colab"** (o "Abrir en Colab").
4. Si no aparece, verifica que en el README las URLs de los badges usen exactamente la misma ruta que tu repo (usuario u org + nombre del repo) y que la rama sea `main` (o la que uses).

Los badges del README enlazan a:

`https://colab.research.google.com/github/TU_ORG/talkwalker-api-workshop/blob/main/notebooks/NOMBRE.ipynb`

Comprueba que `TU_ORG/talkwalker-api-workshop` y `main` coincidan con tu repo y tu rama.

---

## Paso 7 (opcional): Publicar la documentación con MkDocs en GitHub Pages

Solo si quieres que la documentación de `docs/` se vea como una web.

### 7.1 Instalar MkDocs y el tema Material

En la misma carpeta del workshop (o en un entorno virtual):

```bash
cd "c:\Users\Nicolás\.cursor\Talkwalker Esteroides v2\talkwalker-api-workshop"
pip install mkdocs-material
```

### 7.2 Ver el sitio en local

```bash
mkdocs serve
```

Abre el navegador en `http://127.0.0.1:8000` y revisa que todo se vea bien.

### 7.3 Publicar en GitHub Pages

Con el `repo_url` ya configurado en `mkdocs.yml`:

```bash
mkdocs gh-deploy
```

Esto genera la rama `gh-pages` y configura GitHub Pages. Tras unos minutos, la documentación estará en:

`https://tu-usuario.github.io/talkwalker-api-workshop/`

(En organizaciones a veces la URL es `https://mi-empresa.github.io/talkwalker-api-workshop/`.)

---

## Resumen rápido

| Paso | Acción |
|------|--------|
| 1 | Decidir URL del repo (usuario u org + nombre). |
| 2 | En `README.md`: reemplazar `TU_ORG/talkwalker-api-workshop` por tu ruta (11 veces). |
| 3 | En `mkdocs.yml`: cambiar `repo_url` por tu URL completa. |
| 4 | En GitHub: crear repo vacío `talkwalker-api-workshop`. |
| 5 | En terminal: `git init`, `remote add origin`, `add .`, `commit`, `push` a `main`. |
| 6 | Comprobar en GitHub que "Open in Colab" abre los notebooks. |
| 7 | (Opcional) `pip install mkdocs-material`, `mkdocs gh-deploy` para la web de documentación. |

Si en algún paso te pide usuario/contraseña al hacer `git push`, usa un **Personal Access Token** de GitHub como contraseña.
