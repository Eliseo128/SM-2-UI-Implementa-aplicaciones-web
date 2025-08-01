¡Perfecto! A continuación, te presento un **documento completo en formato Markdown** que desarrolla cada uno de los puntos del índice sobre **cómo trabajar con Django**, incluyendo introducción, arquitectura MVT, configuración de VS Code, extensiones recomendadas y buenas prácticas.

Puedes copiar este contenido directamente a un archivo `.md` (por ejemplo, `guia-django.md`) y visualizarlo en cualquier editor que soporte Markdown (como VS Code, Typora, Obsidian, etc.).

---

```markdown
# 📚 Guía Básica para Trabajar con Django

> **Documento técnico y guía de desarrollo para principiantes y desarrolladores intermedios**
>
> Versión: 1.0  
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
| **Escalabilidad** | Soporta desde pequeñas apps hasta sistemas enterprise |
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

### 5.2 Base de Datos

- **SQLite**: predeterminado en Django, ideal para desarrollo.
- **PostgreSQL**: recomendado para producción (más robusto, soporta relaciones complejas).
- **MySQL / MariaDB**: alternativa común.

Configuración en `settings.py` para PostgreSQL:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mi_db',
        'USER': 'usuario',
        'PASSWORD': 'contraseña',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

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

---

## 6. Primer Proyecto con Django en VS Code

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

### 6.7 Crear vistas y URLs

En `productos/views.py`:

```python
from django.shortcuts import render
from .models import Producto

def lista_productos(request):
    productos = Producto.objects.all()
    return render(request, 'productos/lista.html', {'productos': productos})
```

Crea `productos/urls.py`:

```python
from django.urls import path
from . import views

app_name = 'productos'
urlpatterns = [
    path('', views.lista_productos, name='lista'),
]
```

En `mi_tienda/urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('productos/', include('productos.urls')),
]
```

### 6.8 Diseñar plantillas (HTML)

Crea la carpeta: `productos/templates/productos/lista.html`

```html
<!DOCTYPE html>
<html>
<head>
  <title>Productos</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="container mt-4">
  <h1>Productos Disponibles</h1>
  <div class="row">
    {% for producto in productos %}
      <div class="col-md-4 mb-3">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ producto.nombre }}</h5>
            <p class="card-text">{{ producto.descripcion|truncatewords:20 }}</p>
            <p class="text-primary"><strong>${{ producto.precio }}</strong></p>
          </div>
        </div>
      </div>
    {% endfor %}
  </div>
</body>
</html>
```

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

---

## 7. Buenas Prácticas

### 7.1 Estructura de carpetas recomendada

```
mi_proyecto/
├── venv/                 # Entorno virtual
├── mi_proyecto/          # Configuración principal
│   ├── settings/
│   │   ├── base.py
│   │   ├── development.py
│   │   └── production.py
│   ├── urls.py
│   └── wsgi.py
├── apps/
│   └── productos/
│       ├── models.py
│       ├── views.py
│       ├── urls.py
│       └── templates/
│           └── productos/
├── static/               # CSS, JS, imágenes
├── media/                # Archivos subidos por usuarios
├── requirements.txt      # Dependencias
└── .gitignore
```

### 7.2 Uso de `.env` para variables de entorno

Instala `python-decouple`:

```bash
pip install python-decouple
```

Crea `.env`:

```
SECRET_KEY=tu_clave_secreta_aqui
DEBUG=True
DB_NAME=mi_db
DB_USER=usuario
DB_PASSWORD=contraseña
```

En `settings.py`:

```python
from decouple import config

SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', default=False, cast=bool)
```

### 7.3 Separación clara entre lógica y presentación

- La **vista** maneja la lógica.
- La **plantilla** solo muestra datos.
- Evita lógica compleja en HTML.

### 7.4 Nombramiento claro

- `views.py`: `detalle_producto`, `crear_pedido`
- `urls.py`: usa `app_name` y `name` en rutas
- `models.py`: nombres en singular (`Producto`, no `Productos`)

### 7.5 Documentación básica del código

```python
def calcular_descuento(precio, porcentaje):
    """
    Calcula el descuento aplicado a un precio.
    
    Args:
        precio (float): Precio original
        porcentaje (int): Porcentaje de descuento (0-100)
    
    Returns:
        float: Precio con descuento
    """
    return precio * (1 - porcentaje / 100)
```

---

## 8. Recursos Adicionales

### 8.1 Documentación oficial
- [https://docs.djangoproject.com](https://docs.djangoproject.com)

### 8.2 Tutoriales recomendados
- **Mozilla Django Tutorial** (gratis): [https://developer.mozilla.org/es/docs/Learn/Server-side/Django](https://developer.mozilla.org/es/docs/Learn/Server-side/Django)
- **Django for Beginners** (William Vincent)
- **Corey Schafer (YouTube)**: excelente para principiantes

### 8.3 Comunidad
- Stack Overflow: etiqueta `django`
- Reddit: r/django
- Discord: Django Community Server
- GitHub: repositorios oficiales y de terceros

### 8.4 Plantillas gratuitas
- [https://startbootstrap.com](https://startbootstrap.com)
- [https://tailwindui.com](https://tailwindui.com)
- [https://html5up.net](https://html5up.net)

---

## 9. Glosario de Términos

| Término | Significado |
|-------|-------------|
| `manage.py` | Script para gestionar el proyecto (migraciones, servidor, etc.) |
| `settings.py` | Archivo de configuración del proyecto |
| `urls.py` | Define las rutas de la aplicación |
| `views.py` | Contiene la lógica de las vistas |
| `models.py` | Define las estructuras de datos |
| `makemigrations` | Crea archivos de migración |
| `migrate` | Aplica cambios a la base de datos |
| `static` | Archivos estáticos (CSS, JS, imágenes) |
| `media` | Archivos subidos por usuarios |
| `ORM` | Object-Relational Mapper: interactúa con la base de datos sin SQL |
| `CSRF` | Cross-Site Request Forgery: protección contra falsificación de solicitudes |

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

# Ver todas las URLs
python manage.py show_urls  # requiere django-extensions
```

> 💡 Instala `django-extensions` para más comandos útiles:
> ```bash
> pip install django-extensions
> ```
> Luego añade `'django_extensions'` a `INSTALLED_APPS`.

---

> ✅ **¡Felicitaciones!** Ahora tienes una guía completa para comenzar a desarrollar con Django usando VS Code.  
> Este documento puede usarse como referencia técnica, manual de onboarding o base para un curso.

**Elaborado por:** [Tu Nombre]  
**Contacto:** ejemplo@correo.com  
**Licencia:** Creative Commons (CC BY-SA)
```

---

### ✅ ¿Qué puedes hacer con este archivo?

- Guardarlo como `guia-django.md` y usarlo como referencia personal.
- Compartirlo con tu equipo de desarrollo.
- Convertirlo a PDF o Word usando herramientas como Pandoc, Typora o VS Code.
- Publicarlo en un wiki interno o en GitHub.

---

Si deseas, puedo ayudarte a:
- Generar una versión en **PDF** o **Word**.
- Adaptarla a un **curso con ejercicios**.
- Agregar secciones sobre **Django REST Framework** o **despliegue en producción**.

¿Te gustaría que lo haga?
