# Hoja de Trabajo - Docker Compose: Flask + PostgreSQL

## Estructura del Proyecto
```
docker-lab/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## Instrucciones de Ejecución

### 1. Construye y ejecuta los servicios:
```bash
docker compose up -d
```

### 2. Verifica los contenedores:
```bash
docker ps
```

### 3. Prueba la aplicación:

#### Verificar conexión a la base de datos:
```bash
curl http://localhost:8080
```

#### Agregar un nuevo mensaje:
```bash
curl -X POST "http://localhost:8080/add?texto=HolaDocker"
```

#### Listar todos los mensajes:
```bash
curl http://localhost:8080/list
```

### 4. Prueba de persistencia:
```bash
# Detener los contenedores
docker compose down

# Volver a levantarlos
docker compose up -d

# Verificar que los mensajes siguen existiendo
curl http://localhost:8080/list
```

Los mensajes deberían seguir existiendo gracias al volumen `db_data`.

## Descripción de Archivos

### app.py
- Aplicación Flask con endpoints para conectar a PostgreSQL
- `/` - Verifica conexión y crea tabla si no existe
- `/add` - Agrega un nuevo mensaje (POST)
- `/list` - Lista todos los mensajes (GET)

### requirements.txt
- Dependencias de Python: Flask y psycopg2

### Dockerfile
- Imagen base: python:3.11-slim
- Instala dependencias y expone puerto 5000

### docker-compose.yml
- Servicio `app`: Aplicación Flask en puerto 8080
- Servicio `db`: PostgreSQL con volumen persistente
- Variables de entorno para conexión a la base de datos

## Criterios de Evaluación (100 pts)
- Dockerfile funcional: 20 pts
- docker-compose.yml correctamente configurado: 30 pts
- Aplicación accede y guarda datos en PostgreSQL: 25 pts
- Persistencia mediante volumen: 15 pts
- Buenas prácticas y limpieza: 10 pts

## Preguntas de Reflexión

1. ¿Por qué es mejor usar variables de entorno que hardcodear credenciales?
2. ¿Qué ventaja ofrece Docker Compose frente a ejecutar contenedores por separado?
3. ¿Qué sucede si eliminas el volumen db_data?
