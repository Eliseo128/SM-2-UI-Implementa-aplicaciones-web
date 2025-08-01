## Secuencia Didáctica: Desarrollando Aplicaciones Web con Python y Django

---

### Descripción General

Esta secuencia didáctica está diseñada para introducir a estudiantes de preparatoria de 16 a 17 años en el desarrollo de aplicaciones web utilizando **Python** y el framework **Django**. Con una duración de 30 horas, el objetivo es proporcionar una experiencia práctica y atractiva, combinando teoría con ejercicios prácticos. Los estudiantes aprenderán a configurar su entorno de desarrollo, a comprender la arquitectura MVT (Modelo-Vista-Template), y a construir proyectos reales.

El enfoque se centra en el aprendizaje activo, el trabajo en equipo y el uso de herramientas modernas como **VS Code**, **GitHub** y asistentes de inteligencia artificial como **ChatGPT** y **Gemini**.

---

### **Apertura (6 horas)**

El propósito de esta fase es motivar a los estudiantes y establecer las bases teóricas y prácticas iniciales.

#### **Actividades**

1.  **Presentación y Encuesta Interactiva (30 min):**
    * Comenzar con una breve presentación del módulo y los temas a cubrir.
    * Usar una herramienta como Mentimeter o Google Forms para una encuesta rápida y anónima sobre sus conocimientos y expectativas en programación. Preguntas como: *¿Qué es una página web?*, *¿Has programado antes?*, *¿Qué te gustaría aprender a hacer?*

2.  **Mitos y Realidades del Desarrollo Web (1 hora):**
    * Iniciar un debate sobre lo que los estudiantes creen que es el desarrollo web.
    * Ver videos cortos y dinámicos que muestren el impacto de las aplicaciones web en la vida diaria (e-commerce, redes sociales, plataformas de streaming).
    * Discutir conceptos clave como **Aplicaciones web**, **Sistemas de información** y **Pruebas (testing)** de forma accesible, usando analogías. Por ejemplo: una prueba es como probar un videojuego antes de que salga al público para encontrar errores.

3.  **Primer Contacto con Python: Google Colab (3 horas):**
    * Configurar rápidamente el entorno de trabajo usando **Google Colaboratory (Colab)**, sin necesidad de instalaciones complejas.
    * Explorar conceptos básicos de Python a través de ejercicios guiados y muy prácticos:
        * **Variables:** Crear variables para almacenar su nombre, edad, etc.
        * **Estructuras de control:** Usar `if/else` para crear un "quiz" simple que responda según la edad del usuario, y `for` loops para imprimir los números del 1 al 10.
        * **Estructuras de datos:** Crear listas de sus series favoritas o diccionarios con información de un amigo.
    * Fomentar el uso de **ChatGPT** o **Gemini** para generar explicaciones simples o ejemplos de código para practicar.

4.  **Configurando el Entorno Productivo (1.5 horas):**
    * Introducir el concepto de **entorno productivo**. Compararlo con una "cocina profesional" donde se prepara la comida para los clientes, a diferencia de la "cocina de práctica" donde se aprende.
    * Verificar el funcionamiento de una aplicación web ya desplegada (por ejemplo, una página de prueba) para que los estudiantes entiendan el objetivo final.

---

### **Desarrollo (18 horas)**

En esta fase, los estudiantes se sumergen en el núcleo del curso: **Django**. Se enfocarán en la configuración del entorno, la arquitectura del framework y la construcción de proyectos.

#### **Actividades**

1.  **Introducción a Django y Arquitectura MVT (2 horas):**
    * Explicar qué es **Django** y por qué es tan popular (framework "batteries-included").
    * Desglosar la **Arquitectura MVT (Modelo-Vista-Template)** usando un diagrama visual.
        * **Modelo:** La base de datos, donde se guardan los datos (analogía: un almacén).
        * **Vista:** La lógica de la aplicación, que decide qué hacer con los datos (analogía: la cocina que procesa el pedido).
        * **Template:** La interfaz de usuario, lo que ve el usuario (analogía: el menú del restaurante).

2.  **Configuración del Entorno con VS Code (4 horas):**
    * Guiar a los estudiantes en la instalación de **Python** y **VS Code**.
    * Instalar las **Extensiones recomendadas** para VS Code: Python, Django, Pylance, Prettier.
    * Crear un **entorno virtual** para aislar las dependencias del proyecto.
    * Configurar Git y GitHub para el control de versiones. Explicar su importancia: "Si un error rompe tu código, siempre puedes volver a una versión anterior".

3.  **Primer Proyecto: "Hello, Django!" (2 horas):**
    * Crear un proyecto de Django desde cero.
    * Configurar una **URL** y una **vista** simple para mostrar el texto "Hello, Django!".
    * Ejecutar el servidor de desarrollo y ver el resultado en el navegador.

4.  **Proyectos con Django en VS Code (12 horas):**
    * Los estudiantes trabajarán en proyectos prácticos, aplicando todos los conceptos aprendidos. Cada proyecto está diseñado para introducir nuevas funcionalidades de Django.

    * **Ejemplo 1: Blog personal simple (4 hrs)**
        * **Objetivo:** Crear un blog donde se puedan crear, leer, actualizar y eliminar publicaciones (CRUD).
        * **Funcionalidades:**
            * **Modelo:** Crear un modelo para las publicaciones (título, contenido, fecha de publicación).
            * **Vistas:** Vistas para listar todas las publicaciones, ver una publicación en detalle, y formularios para crear y editar.
            * **Templates:** Diseñar las páginas HTML para el listado y el detalle de las publicaciones.
            * **URL:** Mapear las URLs a las vistas correspondientes.

    * **Ejemplo 2: Aplicación de Tareas (To-Do List) (4 hrs)**
        * **Objetivo:** Desarrollar una aplicación interactiva para gestionar una lista de tareas.
        * **Funcionalidades:**
            * **Modelo:** Crear un modelo `Task` con campos como `title`, `description` y `completed` (booleano).
            * **Vistas:** Vistas para mostrar la lista de tareas, agregar una nueva, marcar una como completada y eliminarla.
            * **Templates:** Utilizar templates para mostrar la lista y los formularios. Introducir el concepto de **formularios de Django**.

    * **Ejemplo 3: Catálogo de Películas (4 hrs)**
        * **Objetivo:** Crear una aplicación para listar películas, con capacidad de búsqueda y visualización de detalles.
        * **Funcionalidades:**
            * **Modelo:** Crear un modelo `Movie` con campos como `title`, `year`, `director` y una imagen (opcional).
            * **Vistas:** Vista principal con el listado de películas. Crear una vista para mostrar el detalle de una película.
            * **Búsqueda:** Implementar una funcionalidad básica de búsqueda que filtre las películas por título.

---

### **Cierre (6 horas)**

Esta fase consolida el aprendizaje, evalúa los conocimientos y motiva a los estudiantes a seguir explorando.

#### **Actividades**

1.  **Evaluación y Retroalimentación (2 horas):**
    * Presentación de los proyectos finales: Los estudiantes mostrarán y explicarán uno de los proyectos que construyeron. Se fomentará la retroalimentación constructiva entre compañeros.
    * Discutir las **buenas prácticas** de programación aprendidas (código limpio, comentarios, organización del proyecto).
    * Crear un repositorio en **GitHub** para cada proyecto y subir el código, aprendiendo a usar `git add`, `git commit` y `git push`.

2.  **Pruebas (Testing) Finales (2 horas):**
    * Regresar al concepto de **pruebas**. Explicar cómo escribir pruebas unitarias simples en Django para asegurar que una función o una vista se comporta como se espera.
    * Ejecutar las pruebas en el proyecto para verificar su funcionamiento.

3.  **Recursos Adicionales y Futuro (2 horas):**
    * Presentar **Recursos Adicionales** para continuar el aprendizaje: la documentación oficial de Django, canales de YouTube, blogs y comunidades en línea.
    * Discutir caminos futuros: ¿Qué sigue después de Django? (APIs, Front-end con JavaScript, etc.).
    * Conclusión y preguntas: Abrir un espacio para resolver dudas y compartir reflexiones sobre la experiencia. Animar a los estudiantes a seguir practicando y creando.

---

### Tecnologías Utilizadas

* **Python:** Lenguaje de programación principal.
* **Django:** Framework web de alto nivel.
* **VS Code:** Entorno de Desarrollo Integrado (IDE).
* **Google Colab:** Entorno de notebook de Python en la nube para prácticas iniciales.
* **GitHub:** Plataforma de control de versiones y colaboración.
* **ChatGPT, Gemini:** Asistentes de IA para resolver dudas y generar ejemplos.
* **Google Studio, Gwen:** Tecnologías para la creación de interfaces (dependiendo del contexto, pueden ser herramientas para el diseño visual o de prototipado).

### Links de Referencia

* **Documentación oficial de Django:** `https://docs.djangoproject.com/en/stable/`
* **Tutorial de Django para principiantes:** `https://tutorial.djangogirls.org/es/`
* **Tutorial de Google Colab:** `https://colab.research.google.com/notebooks/intro.ipynb`
* **Documentación de VS Code:** `https://code.visualstudio.com/docs`
* **Guía de GitHub para principiantes:** `https://guides.github.com/activities/hello-world/`

### Glosario de Términos

* **Aplicación web:** Un programa que se ejecuta en un servidor y se accede a través de un navegador web.
* **Backend:** La parte de una aplicación que gestiona la lógica del servidor y la base de datos, invisible para el usuario final.
* **Frontend:** La parte de una aplicación que interactúa directamente con el usuario, visible en el navegador (HTML, CSS, JavaScript).
* **Framework:** Un conjunto de herramientas y librerías predefinidas que facilitan el desarrollo de software, proporcionando una estructura base.
* **Entorno Virtual:** Un entorno aislado de Python para instalar las librerías de un proyecto sin afectar a otros proyectos en la misma máquina.
* **ORM (Object-Relational Mapper):** Una herramienta que permite interactuar con una base de datos usando código Python, sin necesidad de escribir SQL directamente. En Django, el ORM está integrado en los Modelos.
* **MVT (Modelo-Vista-Template):** El patrón de diseño de Django. El **Modelo** maneja la base de datos, la **Vista** maneja la lógica de la aplicación y el **Template** maneja la interfaz de usuario.
* **Debugging:** El proceso de encontrar y corregir errores en el código.
* **CRUD:** Acrónimo de **Create, Read, Update, Delete** (Crear, Leer, Actualizar, Eliminar), las cuatro operaciones básicas de persistencia de datos.
