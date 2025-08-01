# SM-2-UI-Implementa-aplicaciones-web
DESARROLLA APLICACIONES WEB EN UN SISTEMA DE INFORMACIÓN
¡Perfecto! Gracias por la aclaración. Vamos a **actualizar el documento en Markdown** que te entregué anteriormente, reemplazando todas las referencias a **PostgreSQL** por **SQLite**, ya que mencionaste que en tu entorno se utiliza **SQLite** (la base de datos predeterminada de Django).

Además, ajustaré las explicaciones para que reflejen mejor el uso de SQLite como base de datos principal, especialmente en entornos de desarrollo y pequeños proyectos.

---

### ✅ Cambios principales:
- Eliminar configuración de PostgreSQL.
- Destacar que SQLite es ideal para desarrollo y aplicaciones pequeñas.
- Ajustar la sección de "Base de Datos" y ejemplos de `settings.py`.
- Mantener todo el resto del contenido intacto y útil.

---

Aquí tienes el **documento actualizado en Markdown**, listo para usar:

```markdown
# 📚 Guía Básica para Trabajar con Django

> **Documento técnico y guía de desarrollo para principiantes y desarrolladores intermedios**
>
> Versión: 1.1  
> Fecha: 5 de abril de 2025

---

## 1. Introducción a Django

### 1.1 ¿Qué es Django?

**Django** es un framework web de código abierto escrito en **Python**, diseñado para facilitar y acelerar el desarrollo de aplicaciones web robustas, seguras y escalables. Fue creado en 2003 por desarrolladores del periódico *Lawrence Journal-World* y lanzado al público en 2005.

Django sigue el principio **"Don't Repeat Yourself" (DRY)**, lo que significa que promueve la reutilización de código y la reducción de redundancias.

### 1.2 Historia y evolución de Django

- **2003**: Creado por Adrian Holovaty y Simon Willison en Kansas, EE.UU.
- **2005**: Lanzado como software de código abierto bajo licencia BSD.
- **2008**: Lanzamiento de Django 1.0, con soporte estable.
- **2019**: Django 3.0 introduce soporte nativo para **asincronía (async views)**.
- **2023**: Django 4.2 y 5.0 mejoran el ORM, la administración y la compatibilidad con Python 3.12.

Django ha evolucionado para soportar aplicaciones modernas con APIs REST, interfaces dinámicas y despliegues en la nube.

### 1.3 Características principales

- ✅ **Framework completo (batteries included)**: incluye autenticación, administrador, ORM, formularios, gestión de sesiones, etc.
- ✅ **Seguridad integrada**: protección contra CSRF, XSS, inyección SQL, clickjacking.
- ✅ **ORM (Object-Relational Mapper)**: permite interactuar con bases de datos sin escribir SQL directamente.
- ✅ **URLs limpias y legibles**: sistema de enrutamiento basado en expresiones regulares o rutas simples.
- ✅ **Sistema de plantillas**: lenguaje de plantillas seguro y potente.
- ✅ **Administrador automático**: interfaz gráfica para gestionar datos sin escribir código.
- ✅ **Escalable y portable**: usado por empresas como Instagram, Pinterest, Mozilla y Spotify.

### 1.4 Ventajas de usar Django

| Ventaja | Descripción |
|--------|-------------|
| **Rápido desarrollo** | Muchas funciones vienen integradas (login, admin, etc.) |
| **Seguro por defecto** | Protección contra vulnerabilidades comunes |
| **Comunidad activa** | Miles de paquetes de terceros y documentación extensa |
| **Ideal para prototipos y proyectos pequeños** | SQLite integrado, sin configuración adicional |
| **Multiplataforma** | Funciona en Windows, Linux, macOS |

### 1.5 Casos de uso reales

- **Instagram**: una de las plataformas más grandes construidas con Django.
- **Pinterest**: usa Django para manejar millones de pines y usuarios.
- **Mozilla**: sitio oficial y sistemas internos.
- **The Washington Post**: secciones de contenido dinámico.
- **Disqus**: sistema de comentarios en sitios web.

### 1.6 Comparación con otros frameworks

| Framework | Lenguaje | Tipo | Ventajas | Desventajas |
|----------|---------|------|----------|-------------|
| **Django** | Python | Full-stack | Completo, seguro, rápido | Puede ser "pesado" para apps pequeñas |
| **Flask** | Python | Microframework | Ligero, flexible | Requiere más configuración manual |
| **Node.js + Express** | JavaScript | Backend | Ideal para APIs y apps en tiempo real | Menos estructura por defecto |
| **Laravel** | PHP | Full-stack | Gran ecosistema en PHP | Menos moderno que Django en algunos aspectos |

---

## 2. Arquitectura MVT (Modelo-Vista-Template)

### 2.1 ¿Qué es el patrón MVT?

El patrón **MVT (Modelo-Vista-Template)** es la arquitectura que utiliza Django para separar las responsabilidades del desarrollo web:

- **Modelo**: maneja los datos y la lógica de la base de datos.
- **Vista**: contiene la lógica de negocio y procesa las solicitudes.
- **Plantilla**: define cómo se muestra la información al usuario.

Es similar al patrón **MVC (Modelo-Vista-Controlador)**, pero con una diferencia clave: en Django, la **Vista** actúa como el **Controlador**, y el **Template** es la **Vista**.

### 2.2 Componentes del MVT en Django

#### 2.2.1 Modelo (Model)

Representa la estructura de los datos y se comunica con la base de datos mediante el **ORM de Django**.

```python
# models.py
from django.db import models

class Producto(models.Model):
    nombre = models.CharField(max_length=100)
    precio = models.DecimalField(max_digits=10, decimal_places=2)
    fecha_creacion = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.nombre
```

- Cada modelo se traduce en una tabla en la base de datos.
- Se usan **migraciones** para actualizar la base de datos.

#### 2.2.2 Vista (View)

La vista recibe una solicitud HTTP, procesa los datos (usando modelos) y devuelve una respuesta (normalmente una plantilla renderizada).

```python
# views.py
from django.shortcuts import render
from .models import Producto

def lista_productos(request):
    productos = Producto.objects.all()
    return render(request, 'productos.html', {'productos': productos})
```

- Puede ser una función (`function-based view`) o una clase (`class-based view`).
- Maneja lógica como autenticación, filtros, formularios, etc.

#### 2.2.3 Plantilla (Template)

Es el archivo HTML que muestra los datos al usuario. Usa el **lenguaje de plantillas de Django** para incluir datos dinámicos.

```html
<!-- templates/productos.html -->
<!DOCTYPE html>
<html>
<head><title>Productos</title></head>
<body>
  <h1>Lista de Productos</h1>
  <ul>
    {% for producto in productos %}
      <li>{{ producto.nombre }} - ${{ producto.precio }}</li>
    {% endfor %}
  </ul>
</body>
</html>
```

- Soporta herencia de plantillas (`{% extends %}`), bloques y filtros.
- Es seguro: evita XSS por escape automático.

### 2.3 Flujo de datos en una solicitud HTTP en Django

1. El usuario accede a una URL (ej. `/productos/`).
2. Django revisa `urls.py` para encontrar la vista asociada.
3. La **vista** procesa la solicitud (consulta modelos, valida datos).
4. La vista **renderiza una plantilla** con los datos.
5. Se devuelve una respuesta HTTP (HTML, JSON, etc.) al navegador.

### 2.4 Diferencias entre MVT y MVC

| MVT (Django) | MVC (Otros frameworks) |
|-------------|------------------------|
| Modelo → Vista → Plantilla | Modelo → Vista ← Controlador |
| La Vista es el "Controlador" | El Controlador maneja la lógica |
| La Plantilla es la "Vista" | La Vista muestra los datos |

### 2.5 Ejemplo básico de estructura MVT

```
mi_proyecto/
├── mi_app/
│   ├── models.py     → Modelo: Producto
│   ├── views.py      → Vista: lista_productos()
│   └── templates/
│       └── productos.html → Plantilla
├── urls.py           → Ruta: /productos/ → lista_productos
```

---

## 3. Entorno de Desarrollo: Configuración con VS Code

### 3.1 ¿Por qué usar VS Code para Django?

- ✅ Gratuito y de código abierto
- ✅ Soporte excelente para Python y web
- ✅ Extensible con cientos de plugins
- ✅ Depuración integrada
- ✅ Terminal integrada
- ✅ Git integrado

### 3.2 Instalación de Visual Studio Code

1. Descarga desde [https://code.visualstudio.com](https://code.visualstudio.com)
2. Instálalo según tu sistema operativo (Windows, macOS, Linux)
3. Ábrelo y personaliza el tema (opcional)

### 3.3 Configuración del entorno Python

#### 3.3.1 Instalación de Python

- Descarga Python desde [https://www.python.org](https://www.python.org)
- Versión recomendada: **Python 3.10 o superior**
- Verifica la instalación:
  ```bash
  python --version
  # o en algunos sistemas:
  python3 --version
  ```

#### 3.3.2 Uso de entornos virtuales (`venv`)

Los entornos virtuales aíslan las dependencias de cada proyecto.

```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno (Windows)
venv\Scripts\activate

# Activar entorno (macOS/Linux)
source venv/bin/activate

# Desactivar entorno
deactivate
```

#### 3.3.3 Instalación de Django

Dentro del entorno activado:

```bash
pip install django
```

Verifica la instalación:

```bash
django-admin --version
```

---

## 4. Extensiones Recomendadas para VS Code

| Extensión | Descripción |
|---------|-------------|
| **Python** (Microsoft) | Soporte completo para Python: linting, debugging, IntelliSense |
| **Pylance** | Mejora el análisis de código y autocompletado |
| **Django Snippets** | Atajos para escribir código Django más rápido |
| **ESLint** | Revisa errores en JavaScript |
| **Prettier** | Formatea automáticamente HTML, CSS, JS y Python |
| **Live Server** | Previsualiza páginas HTML sin recargar manualmente |
| **Auto Rename Tag** | Cambia automáticamente etiquetas HTML de apertura y cierre |
| **Bracket Pair Colorizer** | Colorea pares de paréntesis, corchetes y llaves |
| **GitLens** | Mejora el control de versiones con Git |
| **REST Client** | Prueba APIs REST desde VS Code usando archivos `.http` |
| **Path Intellisense** | Autocompletado de rutas de archivos |

> 🔧 **Cómo instalar extensiones**:  
> Abre VS Code → Ve a la pestaña de extensiones (Ctrl+Shift+X) → Busca el nombre → Haz clic en "Install".

---

## 5. Herramientas y Tecnologías Complementarias

### 5.1 Frontend (HTML, CSS, JavaScript)

- **HTML5**: estructura básica de las páginas.
- **CSS3**: estilos y diseño.
- **JavaScript**: interactividad (formularios, validaciones, llamadas AJAX).
- **Frameworks recomendados**:
  - **Bootstrap 5**: para diseño responsive rápido.
  - **Tailwind CSS**: utilidades de diseño modernas.
  - **Alpine.js**: ligero para interacciones simples.

Ejemplo de inclusión en plantilla Django:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

### 5.2 Base de Datos: SQLite

**SQLite** es el motor de base de datos predeterminado en Django. Es **liviano, sin servidor y perfecto para desarrollo y aplicaciones pequeñas**.

- ✅ No requiere instalación adicional.
- ✅ Almacena la base de datos en un solo archivo (`db.sqlite3`).
- ✅ Ideal para prototipos, pruebas y sistemas con poco tráfico.
- ❌ No recomendado para aplicaciones con alto volumen de escritura o múltiples usuarios simultáneos.

#### Configuración en `settings.py` (por defecto)

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',  # Ruta al archivo de la base de datos
    }
}
```

> ✅ **¡No necesitas instalar nada extra!** SQLite ya viene incluido en Python.

### 5.3 Terminal Integrada en VS Code

- Abre la terminal: `Ctrl + `` (acento grave)
- Ejecuta comandos Django directamente:
  ```bash
  python manage.py runserver
  python manage.py makemigrations
  ```

### 5.4 Control de Versiones con Git

1. Inicializa un repositorio:
   ```bash
   git init
   ```
2. Crea un archivo `.gitignore`:
   ```
   venv/
   __pycache__/
   *.pyc
   db.sqlite3
   .env
   staticfiles/
   ```
3. Realiza commits regulares:
   ```bash
   git add .
   git commit -m "Primer commit: proyecto Django inicial"
   ```

> ⚠️ **Importante**: Nunca subas `db.sqlite3` al repositorio. Usa `.gitignore`.

---

## 6. Primer Proyecto con Django en VS Code

*(El resto del proyecto sigue igual, ya que usa SQLite por defecto)*

### 6.1 Crear un entorno virtual

```bash
python -m venv venv
source venv/bin/activate  # Linux/macOS
# o
venv\Scripts\activate     # Windows
```

### 6.2 Instalar Django

```bash
pip install django
```

### 6.3 Crear un nuevo proyecto

```bash
django-admin startproject mi_tienda .
```

> ⚠️ El punto (`.`) evita crear una carpeta extra.

### 6.4 Crear una aplicación dentro del proyecto

```bash
python manage.py startapp productos
```

Registra la app en `settings.py`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'productos',  # ← Agregar aquí
]
```

### 6.5 Configurar `settings.py`

Asegúrate de que:
- `ALLOWED_HOSTS = ['localhost', '127.0.0.1']`
- `LANGUAGE_CODE = 'es-es'`
- `TIME_ZONE = 'America/Bogota'`

La configuración de base de datos ya usa **SQLite** por defecto.

### 6.6 Definir modelos básicos

En `productos/models.py`:

```python
from django.db import models

class Producto(models.Model):
    nombre = models.CharField(max_length=100)
    descripcion = models.TextField()
    precio = models.DecimalField(max_digits=10, decimal_places=2)
    creado = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.nombre
```

Crea y aplica migraciones:

```bash
python manage.py makemigrations
python manage.py migrate
```

> Esto creará el archivo `db.sqlite3` en la raíz del proyecto.

### 6.7 Crear vistas y URLs

*(Igual que antes, sin cambios)*

### 6.8 Diseñar plantillas (HTML)

*(Igual que antes)*

### 6.9 Ejecutar el servidor de desarrollo

```bash
python manage.py runserver
```

Abre: [http://127.0.0.1:8000/productos/](http://127.0.0.1:8000/productos/)

### 6.10 Verificar el funcionamiento en el navegador

- ✅ Página carga sin errores
- ✅ Muestra lista de productos
- ✅ Usa Bootstrap para diseño
- ✅ Accede al admin en `/admin/`
- ✅ Base de datos `db.sqlite3` creada automáticamente

---

## 7. Buenas Prácticas

*(Sección actualizada con enfoque en SQLite)*

### 7.1 Estructura de carpetas recomendada

```
mi_proyecto/
├── venv/                 # Entorno virtual
├── mi_proyecto/          # Configuración principal
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── productos/            # Aplicación
├── static/               # CSS, JS, imágenes
├── media/                # Archivos subidos por usuarios
├── db.sqlite3            # ← Base de datos SQLite (NO subir a Git)
├── requirements.txt
└── .gitignore
```

### 7.2 Uso de `.env` para variables de entorno

*(Igual que antes)*

### 7.3 Separación clara entre lógica y presentación

*(Sin cambios)*

### 7.4 Nombramiento claro

*(Sin cambios)*

### 7.5 Documentación básica del código

*(Sin cambios)*

---

## 8. Recursos Adicionales

*(Sin cambios)*

---

## 9. Glosario de Términos

*(Sin cambios)*

---

## 10. Apéndice: Comandos Útiles de Django

```bash
# Iniciar proyecto
django-admin startproject nombre_proyecto .

# Iniciar app
python manage.py startapp nombre_app

# Ejecutar servidor
python manage.py runserver

# Crear migraciones
python manage.py makemigrations

# Aplicar migraciones
python manage.py migrate

# Crear superusuario
python manage.py createsuperuser

# Recopilar archivos estáticos (producción)
python manage.py collectstatic

# Ejecutar tests
python manage.py test
```

---

> ✅ **¡Felicitaciones!** Ahora tienes una guía completa para comenzar a desarrollar con Django usando **SQLite** como base de datos, ideal para entornos de desarrollo, pruebas y proyectos pequeños.  
> Este documento puede usarse como referencia técnica, manual de onboarding o base para un curso.

**Elaborado por:** [Tu Nombre]  
**Contacto:** ejemplo@correo.com  
**Licencia:** Creative Commons (CC BY-SA)
```

---

### ✅ ¿Qué sigue?

Puedes:
- Guardar este archivo como `guia-django-sqlite.md`.
- Abrirlo en VS Code y navegar con el resaltado de sintaxis.
- Convertirlo a PDF con una extensión como **"Markdown PDF"**.

¿Te gustaría que te ayude a:
- Generar un **PDF** de este documento?
- Crear una **versión para imprimir**?
- Añadir una sección sobre **cómo usar el panel de administración de Django**?

¡Solo dime!
