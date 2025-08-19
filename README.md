# Mi-Portafolio-una-guia-en-django
El portafolio en django
# **Aplicación Portafolio Personal en Python Django – Guía Paso a Paso para Estudiantes**

Este documento guía paso a paso al estudiante para crear un **portafolio personal** utilizando **Python y Django**, con interfaz web sencilla, usando **Bootstrap** y estructura de carpetas organizada.

---

## ✅ **1. Procedimiento para acceder a la terminal de Windows**

1. Presiona `Win + R` (tecla Windows + R).
2. Escribe `cmd` y presiona `Enter`.
3. Se abrirá la **terminal CMD** (Command Prompt).

---

## ✅ **2. Crear carpeta de trabajo: “Mi_Portafolio”**

En la terminal, escribe:

```bash
mkdir Mi_Portafolio
```

Luego, entra a la carpeta:

```bash
cd Mi_Portafolio
```

---

## ✅ **3. Abrir VS Code desde la terminal**

Escribe en la terminal:

```bash
code .
```

Esto abrirá Visual Studio Code en la carpeta actual (`Mi_Portafolio`).

---

## ✅ **4. Verificar instalación de Python**

En la terminal, ejecuta:

```bash
python --version
```

O si no funciona, prueba:

```bash
python3 --version
```

Deberías ver algo como: `Python 3.10.6` o similar.

---

## ✅ **5. Crear entorno virtual**

Ejecuta el siguiente comando:

```bash
python -m venv venv
```

Esto crea un entorno virtual llamado `venv`.

---

## ✅ **6. Activar el entorno virtual**

### En Windows:
```bash
venv\Scripts\activate
```

> 🟩 Al activar, verás `(venv)` al inicio del prompt.

---

## ✅ **7. Seleccionar intérprete de Python en VS Code**

1. Abre VS Code.
2. Haz clic en la barra inferior izquierda donde dice "Python" (o "Select Interpreter").
3. Elige `venv` como intérprete.

---

## ✅ **8. Instalar Django**

Con el entorno activado, ejecuta:

```bash
pip install django
```

---

## ✅ **9. Crear proyecto Django: “backend_portafolio”**

```bash
django-admin startproject backend_portafolio .
```

> ⚠️ Usa el punto (`.`) al final para que el proyecto se cree en la carpeta actual, evitando duplicar carpetas.

---

## ✅ **10. Ejecutar el servidor Django**

Desde la terminal, ejecuta:

```bash
python manage.py runserver
```

Abre el navegador y ve a: [http://127.0.0.1:8000](http://127.0.0.1:8000)

---

## ✅ **11. Crear aplicación “app_portafolio”**

```bash
python manage.py startapp app_portafolio
```

---

## ✅ **12. Usar migrate y makemigrations**

Aunque no usamos modelos, aún así ejecutamos:

```bash
python manage.py makemigrations
python manage.py migrate
```

Esto asegura que la base de datos esté preparada.

---

## ✅ **13. Configurar `settings.py` y `urls.py`**

### 🔧 Modificar `backend_portafolio/settings.py`

Agrega `'app_portafolio'` a `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app_portafolio',  # <-- Añadir esta línea
]
```

Configurar `STATICFILES_DIRS` para que Django encuentre los archivos estáticos:

```python
import os

STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / 'app_portafolio/static',
]
```

---

### 🔧 Modificar `backend_portafolio/urls.py`

Asegúrate de incluir las URLs de la app:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_portafolio.urls')),  # <-- Incluir urls de app
]
```

---

## ✅ **14. Crear `urls.py` en `app_portafolio`**

Crea el archivo: `app_portafolio/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio, name='inicio'),
    path('acerca_de_mi/', views.acerca_de_mi, name='acerca_de_mi'),
    path('proyectos/', views.proyectos, name='proyectos'),
    path('experiencia/', views.experiencia_laboral, name='experiencia_laboral'),
    path('certificados/', views.certificados, name='certificados'),
    path('contacto/', views.contacto, name='contacto'),
]
```

---

## ✅ **15. Crear `views.py` en `app_portafolio`**

Crea el archivo: `app_portafolio/views.py`

```python
from django.shortcuts import render

def inicio(request):
    return render(request, 'inicio.html')

def acerca_de_mi(request):
    return render(request, 'acerca_de_mi.html')

def proyectos(request):
    mis_proyectos = [
        {'titulo': 'Crud postres con foto en Django',
         'ruta_imgen': 'images/image.png'},
        {'titulo': 'Crud de Alumnos con Django',
         'ruta_imgen': 'images/crudalu.png'},
        {'titulo': 'gestor de ordenes con Django',
         'ruta_imgen': 'images/ordenes.png'},
    ]
    context = {'proyectos': mis_proyectos}
    return render(request, 'proyectos.html', context)

def experiencia_laboral(request):
    experiencia = [
        {'preparatoria': 'Cbtis 128',
         'carrera': 'Programacion',
         'fecha_inicio': '1989',
         'fecha_fin': '2025'},
        {'preparatoria': 'Conalep I Juarez',
         'carrera': 'Informatica',
         'fecha_inicio': '1991',
         'fecha_fin': '2022'},
    ]
    context = {'experiencia': experiencia}
    return render(request, 'experiencia_laboral.html', context)

def certificados(request):
    return render(request, 'certificados.html')

def contacto(request):
    return render(request, 'contacto.html')
```

---

## ✅ **16. Crear estructura de carpetas y archivos**

### 📂 Estructura esperada:

```
Mi_Portafolio/
│
├── backend_portafolio/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── app_portafolio/
│   ├── __init__.py
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── static/
│   │   └── css/
│   │       └── styles.css
│   └── templates/
│       ├── base.html
│       ├── navbar.html
│       ├── footer.html
│       ├── inicio.html
│       ├── acerca_de_mi.html
│       ├── certificados.html
│       ├── contacto.html
│       ├── experiencia_laboral.html
│       └── proyectos.html
│
└── venv/
```

---

## ✅ **17. Crear carpeta `static` dentro de `app_portafolio`**

```bash
mkdir app_portafolio/static
mkdir app_portafolio/static/css
```

---

## ✅ **18. Crear carpeta `templates` y subcarpetas**

```bash
mkdir app_portafolio/templates
mkdir app_portafolio/templates/images
mkdir app_portafolio/templates/css
```

> ❗ Nota: La carpeta `css` dentro de `templates` no es necesaria si ya tienes una en `static`.  
> Aquí solo se usa para organizar imágenes.

---

## ✅ **19. Crear archivo `styles.css` en `static/css`**

Crea: `app_portafolio/static/css/styles.css`

```css
/* styles.css */
body {
    background-color: #0a0a1a;
    color: #e0e0ff;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
}

.card {
    background-color: #1a1a3a;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
}

h1, h2, h3 {
    color: #00f7ff;
}

p {
    line-height: 1.6;
}

img {
    max-width: 100%;
    height: auto;
}

.avatar {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    object-fit: cover;
    border: 3px solid #00f7ff;
}

.iconos-redes {
    display: flex;
    gap: 15px;
    justify-content: center;
    margin-top: 20px;
}

.iconos-redes img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    transition: transform 0.3s;
}

.iconos-redes img:hover {
    transform: scale(1.2);
}

.tech-icons {
    display: flex;
    justify-content: center;
    gap: 30px;
    margin: 30px 0;
}

.tech-icons img {
    width: 70px;
    height: 70px;
    opacity: 0.9;
}

.tech-icons img:hover {
    opacity: 1;
    transform: scale(1.1);
}

.footer {
    text-align: center;
    color: #ccc;
    margin-top: 40px;
    padding: 20px;
    background-color: #000;
    border-top: 1px solid #333;
}

.form-group {
    margin-bottom: 15px;
}

.form-control {
    width: 100%;
    padding: 10px;
    border: none;
    border-radius: 5px;
    background-color: #1a1a3a;
    color: white;
    border: 1px solid #444;
}

.form-control:focus {
    outline: none;
    border-color: #00f7ff;
}

.btn {
    background-color: #00f7ff;
    color: #000;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-weight: bold;
}

.btn:hover {
    background-color: #00bfff;
}
```

---

## ✅ **20. Crear `templates` HTML**

### ✅ `base.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Portafolio{% endblock %}</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="{% static 'css/styles.css' %}">
</head>
<body>
    <!-- Navbar -->
    {% include 'navbar.html' %}
    
    <!-- Main Content -->
    <div class="container mt-4">
        {% block content %}
        {% endblock %}
    </div>

    <!-- Footer -->
    {% include 'footer.html' %}

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

---

### ✅ `navbar.html`

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
        <a class="navbar-brand" href="/">Profe Nava</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ms-auto">
                <li class="nav-item"><a class="nav-link" href="/">Inicio</a></li>
                <li class="nav-item"><a class="nav-link" href="/acerca_de_mi/">Acerca de..</a></li>
                <li class="nav-item"><a class="nav-link" href="/proyectos/">Proyectos</a></li>
                <li class="nav-item"><a class="nav-link" href="/experiencia/">Experiencia</a></li>
                <li class="nav-item"><a class="nav-link" href="/certificados/">Certificados</a></li>
                <li class="nav-item"><a class="nav-link" href="/contacto/">Contacto</a></li>
            </ul>
        </div>
    </div>
</nav>
```

---

### ✅ `footer.html`

```html
<div class="footer">
    <p>&copy; {{ now|date:"Y" }} Mi Portafolio | Elaborado por Ing. Eliseo Nava</p>
</div>
```

---

### ✅ `inicio.html`

```html
{% extends 'base.html' %}
{% block title %}Inicio{% endblock %}

{% block content %}
<div class="text-center mt-5">
    <img src="{% static 'images/avatar.jpg' %}" alt="Avatar" class="avatar mb-4">
    <h2 style="color: #00f7ff;">Hola, mi nombre es</h2>
    <h1>Eliseo Nava</h1>
    <h2>Yo soy YouTuber</h2>
    <div class="iconos-redes">
        <img src="{% static 'images/linkedin.png' %}" alt="LinkedIn">
        <img src="{% static 'images/youtube.png' %}" alt="YouTube">
        <img src="{% static 'images/instagram.png' %}" alt="Instagram">
    </div>
</div>
{% endblock %}
```

---

### ✅ `acerca_de_mi.html`

```html
{% extends 'base.html' %}
{% block title %}Acerca de mí{% endblock %}

{% block content %}
<div class="row">
    <div class="col-md-4 text-center">
        <img src="{% static 'images/avatar.jpg' %}" alt="Avatar" class="avatar">
    </div>
    <div class="col-md-8">
        <h1>Hola !</h1>
        <p>Aporto una trayectoria diversa que abarca roles como formador de Django Full Stack, profesor de programación. Además, cuento con experiencia en la academia de Programación.</p>
        <p>Como instructor full stack de Python, me dedico a ayudar a otros a aprender Python y Django, a la vez que mejoro continuamente mis habilidades de programación. Tengo una sólida base en Python y un profundo conocimiento de sus conceptos, sintaxis y mejores prácticas.</p>
        <h2 style="color: #00f7ff;">Mi pila tecnológica</h2>
        <div class="tech-icons">
            <img src="{% static 'images/html5.png' %}" alt="HTML5">
            <img src="{% static 'images/css3.png' %}" alt="CSS3">
            <img src="{% static 'images/js.png' %}" alt="JavaScript">
            <img src="{% static 'images/python.png' %}" alt="Python">
            <img src="{% static 'images/react.png' %}" alt="React">
            <img src="{% static 'images/django.png' %}" alt="Django">
        </div>
    </div>
</div>
{% endblock %}
```

---

### ✅ `proyectos.html`

```html
{% extends 'base.html' %}
{% block title %}Proyectos{% endblock %}

{% block content %}
<h1>Proyectos Realizados</h1>
<div class="row">
    {% for proyecto in proyectos %}
    <div class="col-md-6 mb-4">
        <h3>{{ proyecto.titulo }}</h3>
        <img src="{{ proyecto.ruta_imgen }}" alt="{{ proyecto.titulo }}" style="width: 100%; max-height: 300px;">
    </div>
    {% endfor %}
</div>
{% endblock %}
```

---

### ✅ `experiencia_laboral.html`

```html
{% extends 'base.html' %}
{% block title %}Experiencia{% endblock %}

{% block content %}
<h1>Experiencia Laboral</h1>
<div class="row">
    {% for exp in experiencia %}
    <div class="card">
        <h3>{{ exp.preparatoria }}</h3>
        <p><small style="color: #00f7ff;">{{ exp.carrera }}</small></p>
        <p>{{ exp.fecha_inicio }} - {{ exp.fecha_fin }}</p>
    </div>
    {% endfor %}
</div>
{% endblock %}
```

---

### ✅ `certificados.html`

```html
{% extends 'base.html' %}
{% block title %}Certificados{% endblock %}

{% block content %}
<h1>Certificados</h1>
<div class="row">
    <div class="col-md-6 mb-3">
        <div class="card">
            <div class="card-body">
                <h5>Django</h5>
            </div>
        </div>
    </div>
    <div class="col-md-6 mb-3">
        <div class="card">
            <div class="card-body">
                <h5>Python</h5>
            </div>
        </div>
    </div>
</div>
{% endblock %}
```

---

### ✅ `contacto.html`

```html
{% extends 'base.html' %}
{% block title %}Contacto{% endblock %}

{% block content %}
<div class="row">
    <div class="col-md-6">
        <h2>Mantente conectado</h2>
        <p><strong>Email:</strong> manuel.nava@cbtis128.edu.mx</p>
        <div class="iconos-redes">
            <img src="{% static 'images/linkedin.png' %}" alt="LinkedIn">
            <img src="{% static 'images/youtube.png' %}" alt="YouTube">
            <img src="{% static 'images/instagram.png' %}" alt="Instagram">
        </div>
    </div>
    <div class="col-md-6">
        <form>
            <div class="form-group">
                <input type="text" class="form-control" placeholder="Nombre" required>
            </div>
            <div class="form-group">
                <input type="email" class="form-control" placeholder="Email" required>
            </div>
            <div class="form-group">
                <input type="tel" class="form-control" placeholder="Número Telefónico" required>
            </div>
            <div class="form-group">
                <textarea class="form-control" rows="5" placeholder="Mensaje" required></textarea>
            </div>
            <button type="submit" class="btn">Enviar</button>
        </form>
    </div>
</div>
{% endblock %}
```

---

## ✅ **21. Copiar imágenes**

Descarga las siguientes imágenes y colócalas en `app_portafolio/templates/images/`:

- `avatar.jpg` → Foto del usuario
- `image.png`, `crudalu.png`, `ordenes.png` → Capturas de pantalla de proyectos
- `html5.png`, `css3.png`, `js.png`, `python.png`, `react.png`, `django.png` → Iconos de tecnología
- `linkedin.png`, `youtube.png`, `instagram.png` → Redes sociales

> 📌 Puedes usar imágenes de [https://www.freepnglogos.com](https://www.freepnglogos.com) o [https://icons8.com](https://icons8.com)

---

## ✅ **22. Finalmente, ejecutar el servidor**

En la terminal:

```bash
python manage.py runserver
```

Abre tu navegador y visita: [http://127.0.0.1:8000](http://127.0.0.1:8000)

---

✅ **¡Listo! Tu portafolio personal está funcionando.**

---

## ✅ Recomendaciones Finales

- Guarda todo en GitHub para compartirlo.
- Usa nombres de carpetas y archivos en minúsculas y guiones bajos.
- No olvides agregar imágenes reales.
- Puedes mejorar con animaciones y más estilos.

---

📌 **Nota:** Este proyecto es ideal para estudiantes de programación que quieren mostrar su trabajo con Django sin usar bases de datos complejas.

¿Quieres que te genere un archivo ZIP con toda la estructura? Puedo ayudarte a organizarlo.
