# Proyecto-caso-testigo-Perez-Carvajal-Backend

# 🚀 Task Manager Backend (FastAPI)

Backend oficial del proyecto **Proyecto Caso Testigo**, desarrollado con **FastAPI**, siguiendo principios **SOLID**, uso de **Repository Pattern**, manejo de sesiones con **cookies**, y almacenamiento en memoria (no requiere base de datos).

Este backend expone un API REST completo para gestionar tareas (CRUD + búsqueda + métricas), y está desplegado en **Render**.

## 📌 Características principales
- ✔ FastAPI con validaciones Pydantic
- ✔ Sesiones usando cookies seguras
- ✔ Patrones SOLID + Repository Pattern
- ✔ CORS configurado para producción
- ✔ Endpoints REST completos
- ✔ Estadísticas en tiempo real
- ✔ Manejo de errores centralizado
- ✔ Tests con pytest + httpx
- ✔ Sin base de datos
- ✔ Deployment en Render

## 🧱 Arquitectura
```
Proyecto-Backend/
│── app/
│   ├── main.py
│   ├── __init__.py
│── tests/
│   ├── test_basic.py
│── requirements.txt
│── README.md
```

## ⚙️ Requisitos
- Python 3.11+
- pip
- Virtualenv

## 🚀 Instalación
```
git clone https://github.com/Erickpe8/Proyecto-caso-testigo-Perez-Carvajal-Backend
cd Proyecto-caso-testigo-Perez-Carvajal-Backend
python -m venv venv
source venv/Scripts/activate  # Windows
pip install -r requirements.txt
```

## ▶ Ejecutar servidor
```
uvicorn app.main:app --reload
```

## 🧪 Tests
```
pytest -v
```

## 🌐 Deploy en Render
Start Command obligatorio:
```
uvicorn app.main:app --host 0.0.0.0 --port $PORT
```

Health Check:
```
/health
```

## 📡 API Endpoints
- GET /health
- GET /tasks
- POST /tasks
- GET /tasks/{id}
- PUT /tasks/{id}
- PATCH /tasks/{id}/status
- DELETE /tasks
- GET /tasks/search
- GET /tasks/stats

## 📦 Session System
Cookies seguras con session_id.

## 🧩 Licencia
MIT

## 👨‍💻 Autor
Erick Sebastián Pérez Carvajal
