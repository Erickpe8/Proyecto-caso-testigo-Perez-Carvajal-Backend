# 🚀 Task Management API - Backend

## 📋 Descripción

API RESTful profesional para gestión de tareas desarrollada con **FastAPI**, implementando principios **SOLID**, patrones de diseño y buenas prácticas de desarrollo. Este sistema permite crear, leer, actualizar y eliminar tareas, además de búsquedas avanzadas y generación de estadísticas en tiempo real.

## ✨ Características Principales

### Funcionalidades Core
- ✅ **CRUD Completo**: 10 endpoints para gestión total de tareas
- 🔍 **Búsqueda Avanzada**: Búsqueda por título y descripción
- 📊 **Estadísticas en Tiempo Real**: Métricas por estado de tareas
- 🔐 **Gestión de Sesiones**: Sistema de sesiones basado en cookies HTTP-only
- 🏷️ **Sistema de Etiquetas**: Organización mediante tags personalizables
- ⏰ **Fechas de Vencimiento**: Seguimiento de deadlines
- 🎯 **Niveles de Prioridad**: 4 niveles (Baja, Media, Alta, Urgente)
- 📈 **Estados de Tareas**: Pending, In Progress, Completed, Cancelled

### Características Técnicas
- 🏗️ **Arquitectura Limpia**: Separación en capas (Repository, Service, Controller)
- 🔒 **Thread-Safe**: Protección contra race conditions con locks
- ✅ **Validaciones Robustas**: Pydantic V2 con validadores personalizados
- 📝 **Logging Estructurado**: Sistema de logs para debugging y monitoreo
- 🌐 **CORS Configurado**: Soporte completo para aplicaciones web
- 📚 **Documentación Automática**: Swagger UI y ReDoc integrados

## 🛠️ Tecnologías Utilizadas

```python
FastAPI 0.115.6      # Framework web moderno y rápido
Uvicorn 0.34.0       # Servidor ASGI de alto rendimiento
Pydantic 2.10.5      # Validación de datos y serialización
Python 3.11+         # Lenguaje de programación

# Testing
pytest 8.4.2         # Framework de testing
pytest-cov 7.0.0     # Cobertura de código
httpx 0.28.1         # Cliente HTTP para tests
```

## 📁 Estructura del Proyecto

```
Backend/
├── app/
│   ├── main.py                 # Aplicación principal FastAPI
│   ├── models.py              # Modelos Pydantic (opcional)
│   ├── repository.py          # Capa de acceso a datos (opcional)
│   └── services.py            # Lógica de negocio (opcional)
├── tests/
│   ├── __init__.py
│   ├── test_basic.py          # 100+ tests unitarios
│   ├── test_integration.py    # Tests de integración
│   └── test_e2e.py            # Tests end-to-end
├── .gitignore
├── requirements.txt           # Dependencias Python
├── README.md                  # Este archivo
└── render.yaml               # Configuración para Render
```

## 🚀 Instalación y Configuración

### Prerrequisitos
```bash
Python 3.11 o superior
pip (gestor de paquetes Python)
Git
```

### Instalación Local

1. **Clonar el repositorio**
```bash
git clone https://github.com/Erickpe8/Proyecto-caso-testigo-Perez-Carvajal-Backend.git
cd Proyecto-caso-testigo-Perez-Carvajal-Backend
```

2. **Crear entorno virtual**
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

3. **Instalar dependencias**
```bash
pip install -r requirements.txt
```

4. **Ejecutar el servidor**
```bash
# Modo desarrollo
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# Modo producción
uvicorn app.main:app --host 0.0.0.0 --port 8000 --workers 4
```

5. **Verificar instalación**
```bash
# Abrir navegador en:
http://localhost:8000/docs          # Swagger UI
http://localhost:8000/redoc         # ReDoc
http://localhost:8000/health        # Health Check
```

## 📡 Endpoints de la API

### 🏥 Health Check
```http
GET /health
```
**Respuesta:**
```json
{
  "status": "healthy",
  "timestamp": "2025-11-19T10:30:00.000Z",
  "version": "2.0.0"
}
```

### 📝 Tareas

#### Listar todas las tareas
```http
GET /tasks?status=PENDING
```

#### Obtener tarea por ID
```http
GET /tasks/{task_id}
```

#### Crear nueva tarea
```http
POST /tasks
Content-Type: application/json

{
  "title": "Completar documentación",
  "description": "Escribir README completo",
  "priority": 3,
  "tags": ["docs", "urgente"],
  "due_date": "2025-12-31"
}
```

#### Actualizar tarea
```http
PUT /tasks/{task_id}
Content-Type: application/json

{
  "title": "Título actualizado",
  "status": "IN_PROGRESS",
  "priority": 4
}
```

#### Actualizar solo estado
```http
PATCH /tasks/{task_id}/status?status=COMPLETED
```

#### Eliminar tarea
```http
DELETE /tasks/{task_id}
```

#### Eliminar todas las tareas
```http
DELETE /tasks
```

### 🔍 Búsqueda y Estadísticas

#### Buscar tareas
```http
GET /tasks/search?q=backend
```

#### Obtener estadísticas
```http
GET /tasks/stats
```

**Respuesta:**
```json
{
  "total": 25,
  "pending": 8,
  "in_progress": 12,
  "completed": 4,
  "cancelled": 1
}
```

## 🧪 Testing

### Suite Completa de Pruebas

El proyecto incluye **100+ tests** organizados en diferentes categorías:

#### Ejecutar todos los tests
```bash
python -m pytest tests/test_basic.py -v
```

#### Tests con cobertura
```bash
python -m pytest tests/test_basic.py --cov=app.main --cov-report=html --cov-report=term-missing
```

#### Tests específicos
```bash
# Solo tests de creación
python -m pytest tests/test_basic.py::TestCreateTask -v

# Solo tests de búsqueda
python -m pytest tests/test_basic.py::TestSearchTasks -v

# Solo tests de CORS
python -m pytest tests/test_basic.py::TestCORS -v
```

### Categorías de Tests

1. **Health Check (3 tests)**: Verificación de disponibilidad
2. **Create/POST (14 tests)**: Creación y validaciones
3. **Read/GET (7 tests)**: Lectura de datos
4. **Update/PUT (11 tests)**: Actualización de tareas
5. **Delete (6 tests)**: Eliminación de recursos
6. **Search (5 tests)**: Búsqueda y filtrado
7. **Statistics (4 tests)**: Generación de métricas
8. **Validation (4 tests)**: Validación de campos
9. **Session Management (3 tests)**: Gestión de sesiones
10. **Edge Cases (5 tests)**: Casos límite
11. **CORS (2 tests)**: Configuración CORS
12. **Error Handling (3 tests)**: Manejo de errores
13. **Business Logic (3 tests)**: Lógica de negocio
14. **Performance (2 tests)**: Pruebas de rendimiento
15. **Concurrency (1 test)**: Operaciones concurrentes
16. **Data Integrity (3 tests)**: Integridad de datos

### Resultados Esperados
```bash
================================ 101 passed in 4.01s ================================
```

### Cobertura de Código
- **Objetivo**: 80%+ de cobertura
- **Actual**: 95%+ en funciones críticas
- **Reporte HTML**: Generado en `htmlcov/index.html`

## 🎯 Principios SOLID Implementados

### Single Responsibility Principle (SRP)
- `InMemoryTaskRepository`: Solo maneja acceso a datos
- `TaskService`: Solo maneja lógica de negocio
- `SessionManager`: Solo maneja sesiones

### Open/Closed Principle (OCP)
- `IRepository`: Interface abstracta para diferentes implementaciones
- Fácil extensión sin modificar código existente

### Liskov Substitution Principle (LSP)
- Cualquier implementación de `IRepository` es intercambiable

### Interface Segregation Principle (ISP)
- Interfaces específicas y enfocadas
- No se fuerza implementación de métodos innecesarios

### Dependency Injection Principle (DIP)
- Dependencias inyectadas via FastAPI `Depends()`
- Bajo acoplamiento entre componentes

## 🏗️ Patrones de Diseño

### Repository Pattern
```python
class IRepository(ABC):
    @abstractmethod
    def find_all(self, session_id: str) -> List[Dict]: pass
    
    @abstractmethod
    def create(self, session_id: str, task: Dict) -> Dict: pass
```

### Service Layer Pattern
```python
class TaskService:
    def __init__(self, repository: IRepository):
        self._repo = repository
    
    def create_task(self, session_id: str, task_data: TaskCreate) -> Task:
        # Lógica de negocio
```

### Dependency Injection
```python
def get_task_service() -> TaskService:
    return task_service

@app.get("/tasks")
def list_tasks(service: TaskService = Depends(get_task_service)):
    # ...
```

### Factory Pattern
```python
@staticmethod
def get_or_create_session(request: Request, response: Response) -> str:
    # Crea sesiones bajo demanda
```

## 🔐 Seguridad

### Características de Seguridad
- ✅ **HTTP-Only Cookies**: Protección contra XSS
- ✅ **CORS Configurado**: Control de orígenes permitidos
- ✅ **Validación de Entrada**: Todos los datos validados con Pydantic
- ✅ **Thread-Safe**: Protección contra race conditions
- ✅ **Error Handling**: Mensajes de error seguros

### Configuración CORS
```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Cambiar en producción
    allow_methods=["*"],
    allow_headers=["*"],
    allow_credentials=True
)
```

## 🌐 Despliegue en Render

### Configuración de Render

1. **Crear cuenta en Render**: https://render.com

2. **Crear nuevo Web Service**:
   - Conectar repositorio de GitHub
   - Seleccionar rama: `main`
   - Nombre del servicio: `task-management-api`
   - Entorno: `Python 3`

3. **Configuración del servicio**:
```yaml
# render.yaml
services:
  - type: web
    name: task-management-api
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: uvicorn app.main:app --host 0.0.0.0 --port $PORT
    envVars:
      - key: PYTHON_VERSION
        value: 3.11.0
```

4. **Variables de entorno** (opcional):
```bash
ENVIRONMENT=production
LOG_LEVEL=INFO
```

5. **Comandos de despliegue**:
```bash
# Build Command
pip install -r requirements.txt

# Start Command
uvicorn app.main:app --host 0.0.0.0 --port $PORT --workers 2
```

### URL de Producción
```
https://task-management-api.onrender.com
```

### Health Check en Producción
```bash
curl https://task-management-api.onrender.com/health
```

### Monitoreo y Logs
- **Dashboard Render**: Ver logs en tiempo real
- **Métricas**: CPU, Memoria, Requests
- **Alertas**: Configurar notificaciones de errores

## 📊 Monitoreo y Logging

### Sistema de Logs
```python
import logging

logger = logging.getLogger(__name__)
logger.info(f"Task created: {task_id}")
logger.error(f"Error occurred: {error}")
```

### Niveles de Log
- `DEBUG`: Información detallada de debugging
- `INFO`: Confirmación de funcionamiento normal
- `WARNING`: Advertencias de posibles problemas
- `ERROR`: Errores que requieren atención

## 🔧 Mantenimiento

### Actualizar Dependencias
```bash
pip list --outdated
pip install --upgrade package-name
pip freeze > requirements.txt
```

### Limpiar Datos de Sesión
```python
# En main.py, agregar endpoint de limpieza
@app.delete("/sessions/clear")
def clear_all_sessions():
    repository._storage.clear()
    return {"message": "All sessions cleared"}
```

### Backup de Datos (si usas BD)
```bash
# Para futuras implementaciones con PostgreSQL
pg_dump database_name > backup.sql
```

## 🐛 Troubleshooting

### Error: ModuleNotFoundError
```bash
# Solución: Verificar instalación de dependencias
pip install -r requirements.txt
```

### Error: Address already in use
```bash
# Solución: Cambiar puerto o matar proceso
# Windows
netstat -ano | findstr :8000
taskkill /PID <PID> /F

# Linux/Mac
lsof -ti:8000 | xargs kill -9
```

### Error: CORS Policy
```bash
# Solución: Verificar configuración CORS en main.py
# Asegurar que el origen del frontend esté permitido
```

### Tests Fallan
```bash
# Solución: Limpiar cache y reinstalar
pip cache purge
pip install -r requirements.txt --force-reinstall
python -m pytest tests/ -v --tb=short
```

## 📈 Roadmap Futuro

### Versión 3.0
- [ ] Integración con PostgreSQL
- [ ] Autenticación JWT
- [ ] Sistema de usuarios multi-tenant
- [ ] Notificaciones en tiempo real (WebSockets)
- [ ] Export/Import de tareas (CSV, JSON)
- [ ] API Rate Limiting
- [ ] Caché con Redis
- [ ] Containerización con Docker
- [ ] CI/CD con GitHub Actions
- [ ] Métricas con Prometheus

### Versión 2.1 (Próxima)
- [ ] Subtareas
- [ ] Adjuntos de archivos
- [ ] Recordatorios por email
- [ ] Dashboard analytics avanzado

## 👥 Contribución

### Cómo Contribuir
1. Fork el proyecto desde [GitHub](https://github.com/Erickpe8/Proyecto-caso-testigo-Perez-Carvajal-Backend)
2. Crear feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit cambios (`git commit -m 'Add AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abrir Pull Request

### Estándares de Código
- Seguir PEP 8
- Tests para nuevas features
- Documentación de funciones
- Type hints en todo el código

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para detalles.

## 👨‍💻 Autor

**Erick Pérez Carvajal**
- GitHub: [@Erickpe8](https://github.com/Erickpe8)
- Repositorio: [Backend](https://github.com/Erickpe8/Proyecto-caso-testigo-Perez-Carvajal-Backend)

## 📫 Conéctate conmigo

* **Correo electrónico**: ericksperezc@gmail.com
* **Instagram**: [@Erickperez_8](https://instagram.com/Erickperez_8)
* **YouTube**: [ErickPerez_8](https://youtube.com/@ErickPerez_8)

## 🙏 Agradecimientos

- FastAPI por el increíble framework
- Comunidad de Python
- Render por el hosting gratuito
- Todos los contribuidores

## 📞 Soporte

¿Tienes preguntas o problemas?
- 📧 Email: ericksperezc@gmail.com
- 📸 Instagram: [@Erickperez_8](https://instagram.com/Erickperez_8)
- 🎥 YouTube: [ErickPerez_8](https://youtube.com/@ErickPerez_8)
- 🐛 Issues: [GitHub Issues](https://github.com/Erickpe8/Proyecto-caso-testigo-Perez-Carvajal-Backend/issues)

---

**⭐ Si este proyecto te ayudó, considera darle una estrella en GitHub ⭐**

Última actualización: Noviembre 2025
