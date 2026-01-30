# Django WebScraper con Selenium y Firefox

Un proyecto de web scraping desarrollado con Django y Selenium, utilizando Firefox como navegador headless dentro de un entorno Docker.

## 📋 Descripción

Este proyecto implementa un sistema de web scraping que utiliza:
- **Django** como framework web
- **Selenium** para la automatización del navegador
- **Firefox ESR** como navegador headless
- **GeckoDriver** para la comunicación con Firefox
- **Docker** para el entorno de desarrollo y producción

## 🚀 Características

- Web scraping automatizado con Selenium
- Navegador headless (sin interfaz gráfica)
- Entorno dockerizado para consistencia
- Configuración optimizada para servidores
- Manejo de errores y debugging

## 📁 Estructura del Proyecto

```
webscraper_project/
├── manage.py                 # Django management script
├── requirements.txt          # Dependencias de Python
├── docker-compose.yml        # Configuración de Docker Compose
├── Dockerfile               # Imagen Docker personalizada
├── README.md               # Este archivo
├── webscraper_project/     # Configuración principal de Django
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── scraper/               # Aplicación de scraping
    └── services/
        └── scrape.py      # Lógica principal de scraping
```

## 🛠️ Tecnologías Utilizadas

- **Python 3.11**
- **Django 5.2.10**
- **Selenium 4.40.0**
- **Firefox ESR**
- **GeckoDriver v0.35.0**
- **Docker & Docker Compose**

## 📦 Instalación

### Opción 1: Con Docker (Recomendado)

```bash
# Clonar el repositorio
git clone <repository-url>
cd webscraper_project

# Construir y ejecutar con Docker Compose
docker-compose up --build
```

### Opción 2: Instalación Local

```bash
# Instalar dependencias
pip install -r requirements.txt

# Ejecutar migraciones
python manage.py migrate

# Ejecutar servidor de desarrollo
python manage.py runserver
```

## 🎯 Uso

El módulo principal de scraping se encuentra en `scraper/services/scrape.py`. Ejemplo de uso:

```python
from scraper.services.scrape import scrape_website

# Ejecutar scraping
data = scrape_website()
print(data)
```

## 📚 Docker

Para información detallada sobre el setup de Docker, consulta la documentación específica en la sección Docker de este proyecto.

## 🤝 Contribuir

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT.