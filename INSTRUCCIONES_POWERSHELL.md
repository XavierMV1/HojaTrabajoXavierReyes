# Instrucciones para PowerShell - Docker Compose: Flask + PostgreSQL

## Comandos Específicos para PowerShell

### 1. Construye y ejecuta los servicios:
```powershell
docker compose up -d
```

### 2. Verifica los contenedores:
```powershell
docker ps
```

### 3. Prueba la aplicación:

#### Verificar conexión a la base de datos:
```powershell
Invoke-WebRequest -Uri "http://localhost:8080"
```

#### Agregar un nuevo mensaje:
```powershell
Invoke-WebRequest -Uri "http://localhost:8080/add?texto=HolaDocker" -Method POST
```

#### Listar todos los mensajes:
```powershell
Invoke-WebRequest -Uri "http://localhost:8080/list"
```

### 4. Prueba de persistencia:
```powershell
# Detener los contenedores
docker compose down

# Volver a levantarlos
docker compose up -d

# Esperar a que se inicien (opcional)
Start-Sleep -Seconds 10

# Verificar que los mensajes siguen existiendo
Invoke-WebRequest -Uri "http://localhost:8080/list"
```

## Alternativa con curl (si está disponible):
```powershell
# Si tienes curl instalado, puedes usar:
curl.exe http://localhost:8080
curl.exe -X POST "http://localhost:8080/add?texto=HolaDocker"
curl.exe http://localhost:8080/list
```

## Comandos útiles adicionales:

### Ver logs de los contenedores:
```powershell
docker compose logs
```

### Ver logs de un servicio específico:
```powershell
docker compose logs app
docker compose logs db
```

### Detener y limpiar todo:
```powershell
docker compose down -v  # Esto elimina también los volúmenes
```

## Notas importantes:
- Los mensajes deberían persistir gracias al volumen `db_data`
- La aplicación Flask está disponible en el puerto 8080
- PostgreSQL está configurado con credenciales: admin/admin123
- La base de datos se llama: mensajesdb
