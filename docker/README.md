# 🐳 Configuración Docker - WebScraper con Firefox

Esta documentación detalla la configuración y uso del entorno Docker para el proyecto de web scraping.

## 📋 Configuración del Entorno

### Dockerfile

El proyecto utiliza una imagen basada en **Python 3.11.11-slim** con las siguientes características:

- **Firefox ESR** instalado para navegación headless
- **GeckoDriver v0.35.0** para comunicación con Firefox
- **Dependencias del sistema** necesarias para entornos headless
- **Configuración de fuentes** para evitar errores de cache

### Docker Compose

```yaml
version: '3.8'

services:
  webscraper-server:
    build: .
    container_name: webscraper-server-1
    ports:
      - "8000:8000"
    volumes:
      - .:/app
    environment:
      - PYTHONPATH=/app
    command: tail -f /dev/null
```

## 🚀 Comandos de Uso

### Construir la imagen
```bash
docker-compose build
```

### Reconstruir sin cache (recomendado tras cambios)
```bash
docker-compose build --no-cache
```

### Ejecutar el contenedor
```bash
docker-compose up
```

### Ejecutar en background
```bash
docker-compose up -d
```

### Parar los contenedores
```bash
docker-compose down
```

## 🔍 Comandos de Depuración para Firefox/GeckoDriver

En caso de que falle Firefox, usar estos comandos para depurar:

### 1. Ver contenedores activos
```bash
docker ps
```

### 2. Acceder al contenedor
```bash
docker exec -it webscraper-server-1 bash
# O usar el nombre que aparezca en docker ps
docker exec -it <container_name> bash
```

### 3. Verificar instalaciones dentro del contenedor
```bash
# Verificar que geckodriver existe
which geckodriver

# Verificar que firefox existe  
which firefox

# Verificar versiones
geckodriver --version
firefox --version
```

### 4. Ejecutar geckodriver en modo debug
```bash
docker exec -it webscraper-server-1 /usr/local/bin/geckodriver --log debug
```
> **Importante**: Dejar esta ventana abierta para monitorear errores en tiempo real

### 5. Verificar logs del contenedor
```bash
docker logs webscraper-server-1

# Para seguir logs en tiempo real
docker logs -f webscraper-server-1
```

### 6. Verificar estructura de archivos
```bash
# Verificar binarios en el contenedor
docker exec -it webscraper-server-1 ls -la /usr/local/bin/
docker exec -it webscraper-server-1 ls -la /usr/bin/firefox*

# Verificar permisos
docker exec -it webscraper-server-1 ls -la /usr/local/bin/geckodriver
```

## 🛠️ Solución de Problemas Comunes

### Error: "selenium.common.exceptions.WebDriverException"
- Verificar que geckodriver esté en `/usr/local/bin/`
- Comprobar permisos de ejecución
- Usar el comando debug de geckodriver

### Error: "Firefox binary not found"
- Verificar instalación de firefox-esr
- Comprobar que firefox esté en el PATH
- Usar `which firefox` dentro del contenedor

### Error: "Display not found"
- Asegurarse de usar `--headless` en las opciones de Firefox
- Verificar configuración de display virtual

### Problemas de memoria
- Usar `--disable-dev-shm-usage` en opciones de Firefox
- Aumentar memoria disponible para Docker si es necesario

## 📂 Volúmenes y Persistencia

- **Código fuente**: Mapeado como volumen (`.:/app`)
- **Base de datos**: SQLite persistente en `/app/webscraper_project/db.sqlite3`
- **Logs**: Accesibles vía `docker logs`

## 🔧 Variables de Entorno

| Variable | Valor | Descripción |
|----------|--------|-------------|
| `PYTHONPATH` | `/app` | Path de Python para imports |
| `PYTHONDONTWRITEBYTECODE` | `1` | Evita archivos .pyc |
| `PYTHONUNBUFFERED` | `1` | Output sin buffer |
| `FONTCONFIG_PATH` | `/tmp/cache/fontconfig` | Cache de fuentes |

## 📝 Notas Importantes

1. **Compatibilidad**: Django 5.2.10 es compatible con Python 3.11
2. **Arquitectura**: El Dockerfile soporta AMD64 y ARM64
3. **Permisos**: El contenedor se ejecuta como root para evitar problemas de permisos
4. **Networking**: Puerto 8000 expuesto para el servidor Django

## 🚦 Estado del Proyecto

- ✅ Dockerfile configurado y funcional
- ✅ Docker Compose configurado
- ✅ Firefox ESR instalado
- ✅ GeckoDriver v0.35.0 instalado
- ✅ Dependencias Python instaladas
- ✅ Compatibilidad Django/Python verificada
- ✅ Imagen construida exitosamente
