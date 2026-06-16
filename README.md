# FundApp — Backend API (FastAPI + Supabase)

Backend REST con **arquitectura limpia** para la plataforma de voluntariado y donaciones FundApp.

---

##  Estructura del proyecto

```
fundapp-backend/
├── app/
│   ├── api/v1/             # Capa de presentación — Routers HTTP
│   │   ├── auth.py
│   │   ├── actividades.py
│   │   ├── donaciones.py
│   │   ├── voluntarios.py
│   │   ├── certificados.py
│   │   ├── admin.py
│   │   └── router.py
│   ├── core/               # Configuración central
│   │   ├── config.py       # Settings (pydantic-settings)
│   │   ├── security.py     # JWT + SHA256 hashing
│   │   └── dependencies.py # Dependencias de FastAPI (auth guards)
│   ├── domain/
│   │   └── schemas/        # DTOs y modelos de request/response
│   ├── infrastructure/
│   │   ├── supabase_client.py
│   │   └── repositories/   # Capa de acceso a datos (Supabase)
│   ├── services/           # Capa de lógica de negocio
│   └── main.py             # Entry point
├── .env.example
├── requirements.txt
└── README.md
```

---

##  Instalación y ejecución

### 1. Clonar e instalar dependencias

```bash
cd fundapp-backend
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 2. Configurar variables de entorno

```bash
cp .env.example .env
# Editar .env con tus credenciales de Supabase
```

Variables requeridas:
```
SUPABASE_URL=https://xxxx.supabase.co
SUPABASE_KEY=tu-anon-key
SUPABASE_SERVICE_KEY=tu-service-role-key
JWT_SECRET=tu-jwt-secret   # El mismo que usabas en SUPABASE_JWT_SECRET
```

### 3. Levantar el servidor

```bash
uvicorn app.main:app --reload --port 8000
```


##  Documentación interactiva

- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

---

##  Autenticación

El API usa **JWT Bearer tokens**. Para endpoints protegidos:

```
Authorization: Bearer <token>
```

El token se obtiene en `/api/v1/auth/login`.
