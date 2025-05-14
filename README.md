# Bot Multiservicio para WhatsApp con Rasa

Este repositorio contiene el código fuente y la documentación para un **bot multiservicio** que opera en WhatsApp, desarrollado con **Rasa**, **FastAPI**, **Twilio** (para pruebas iniciales), y la **API de WhatsApp de Meta** (en producción). El bot permite a los usuarios realizar consultas, pagos, y recargas, con registro de conversaciones en **Google Sheets** y un diseño modular para integrar servicios como **Culqi**, **Distriluz**, y **Caja Huancayo**

## Cronograma del Proyecto

El desarrollo del bot se divide en tres etapas, con un plazo total de **8 semanas** (14 de mayo al 9 de julio de 2025). A continuación, se detalla el cronograma por etapa, incluyendo tareas, fechas, duraciones, y entregables.

### Etapa 1: Chatbot Menú Multiservicio (Interacción Base)

**Objetivo**: Implementar un bot con Rasa conectado a WhatsApp vía la API de Meta, con un menú interactivo (servicios, recargas, cambio de divisas, préstamos, asesor) y registro de conversaciones en Google Sheets.  
**Duración**: 2 semanas (14-27 May 2025).  
**Entregables**:
- Código fuente (Rasa, FastAPI, API de Meta, Google Sheets).
- Archivos de Rasa configurados (`domain.yml`, `nlu.yml`, `rules.yml`).
- Bot funcional en WhatsApp con menú multiservicio.
- Hoja de cálculo con conversaciones registradas.
- Documentación inicial (`README.md`, `docs/flujos.md`).
- Manual de configuración de la API de Meta.

#### Tareas
| Día | Fecha | Tareas | Entregables |
|-----|-------|--------|-------------|
| 1-2 | 14-15 May | - Verificar entorno (Python 3.9, Rasa).<br>- Instalar dependencias (`rasa`, `fastapi`, `requests`, etc.).<br>- Crear estructura del proyecto (`src/`, `rasa/`, `tests/`).<br>- Configurar API de Meta (cuenta, aplicación, webhook con `ngrok`, token de acceso).<br>- Crear `.env`. | Estructura del proyecto, API de Meta configurada, `requirements.txt`, `.env`. |
| 3-4 | 16-17 May | - Configurar Google Sheets (hoja "ConversacionesBot", API, `credentials.json`).<br>- Implementar `src/storage/repository.py`, `src/storage/google_sheets.py`.<br>- Probar guardar una fila en Google Sheets. | Hoja de cálculo configurada, `credentials.json`, `GoogleSheetsRepository`. |
| 5-7 | 19-21 May | - Actualizar `rasa/domain.yml`, `nlu.yml`, `rules.yml` con menú multiservicio (intenciones: `greet`, `list_services`, etc.).<br>- Entrenar modelo (`rasa train`).<br>- Probar localmente (`rasa shell`, `rasa interactive`). | Archivos de Rasa configurados, modelo entrenado. |
| 8-10 | 22-24 May | - Implementar `src/whatsapp/meta_client.py`, `src/bot/rasa_handler.py`, `src/main.py`.<br>- Conectar Rasa, FastAPI, API de Meta, Google Sheets.<br>- Probar bot en WhatsApp ("hola", "menú"). | Bot funcional, registro de conversaciones. |
| 11-13 | 25-27 May | - Probar flujos del menú (greet, list_services, recharge, etc.).<br>- Corregir errores.<br>- Añadir pruebas unitarias (`tests/test_meta_client.py`, `tests/test_google_sheets.py`).<br>- Documentar (`README.md`, `docs/flujos.md`).<br>- Subir a Git. | Repositorio Git, bot estable, documentación inicial, pruebas. |
| 14 | 28 May | - Revisar bot y corregir errores menores.<br>- Preparar informe de Etapa 1 (estado, limitaciones). | Informe de Etapa 1. |

### Etapa 2: Pasarela de Pago con Culqi

**Objetivo**: Integrar Culqi para procesar pagos con tarjeta, Yape, o Plin, con confirmación en WhatsApp y registro en Google Sheets.  
**Duración**: 2 semanas (28 May-10 Jun 2025).  
**Entregables**:
- Código con integración de Culqi.
- Flujo de pagos en Rasa (intención `pay`, slots para monto/método).
- Registro de pagos en Google Sheets.
- Manual de configuración de Culqi.
- Documentación actualizada.

#### Tareas
| Día | Fecha | Tareas | Entregables |
|-----|-------|--------|-------------|
| 1-3 | 28-30 May | - Crear cuenta en Culqi, obtener claves de prueba.<br>- Instalar `culqi`.<br>- Implementar `src/services/culqi_service.py` (Strategy Pattern).<br>- Probar cargo localmente. | `CulqiService`, claves de Culqi. |
| 4-6 | 31 May-2 Jun | - Añadir intención `pay` en `rasa/data/nlu.yml`, `domain.yml`.<br>- Usar slots para capturar detalles de pago.<br>- Actualizar `src/bot/rasa_handler.py`.<br>- Entrenar modelo (`rasa train`). | Flujo de pagos en Rasa, modelo actualizado. |
| 7-9 | 3-5 Jun | - Actualizar `src/main.py` para enviar enlaces de pago vía API de Meta.<br>- Registrar pagos en Google Sheets.<br>- Configurar webhook para validar pagos con Culqi. | Backend con pagos, registro en Google Sheets. |
| 10-12 | 6-8 Jun | - Probar pagos (tarjeta, Yape, Plin).<br>- Verificar confirmaciones en WhatsApp.<br>- Añadir pruebas unitarias (`tests/test_culqi_service.py`).<br>- Corregir errores. | Bot con pagos funcionales, pruebas. |
| 13-14 | 9-10 Jun | - Actualizar `README.md`, `docs/flujos.md`.<br>- Crear manual de configuración de Culqi.<br>- Preparar informe de Etapa 2. | Documentación actualizada, manual de Culqi, informe. |

### Etapa 3: Consultas y Pagos vía APIs REST

**Objetivo**: Integrar APIs REST de Distriluz y Caja Huancayo para consultas de deudas y pagos, con diseño modular para futuros servicios (ONP, AFP, etc.), y desplegar el bot en un VPS.  
**Duración**: 3.5 semanas (11 Jun-9 Jul 2025).  
**Entregables**:
- Código modular con integración de Distriluz y Caja Huancayo.
- Bot desplegado en VPS (Ubuntu 22.04) con API de Meta.
- Documentación completa (instalación, uso, flujos).
- Manuales de configuración de Distriluz, Caja Huancayo, y API de Meta.
- Informe final.

#### Tareas
| Día | Fecha | Tareas | Entregables |
|-----|-------|--------|-------------|
| 1-4 | 11-14 Jun | - Obtener credenciales de Distriluz y Caja Huancayo.<br>- Estudiar documentación de APIs.<br>- Implementar `src/services/base_service.py`, `src/services/service_factory.py` (Factory Pattern). | Credenciales de APIs, `BaseService`, `ServiceFactory`. |
| 5-9 | 15-19 Jun | - Implementar `src/services/distriluz_service.py` para consultas de deudas.<br>- Añadir intenciones `consult_debt`, `pay_debt` en Rasa.<br>- Integrar con FastAPI y Google Sheets.<br>- Entrenar modelo (`rasa train`). | Servicio de Distriluz funcional, Rasa actualizado. |
| 10-14 | 20-24 Jun | - Implementar `src/services/caja_huancayo_service.py` para pagos de crédito.<br>- Actualizar Rasa y FastAPI.<br>- Registrar transacciones en Google Sheets.<br>- Entrenar modelo. | Servicio de Caja Huancayo funcional, integración completa. |
| 15-20 | 25-30 Jun | - Probar flujos de Distriluz y Caja Huancayo.<br>- Implementar servicio ficticio para probar modularidad.<br>- Añadir pruebas unitarias (`test_distriluz_service.py`, `test_caja_huancayo_service.py`).<br>- Optimizar rendimiento (por ejemplo, caché en consultas). | Bot modular, pruebas, optimizaciones. |
| 21-25 | 1-6 Jul | - Configurar VPS (Ubuntu 22.04, Python, Rasa, FastAPI).<br>- Configurar HTTPS con Let’s Encrypt.<br>- Desplegar bot y probar con API de Meta.<br>- Realizar pruebas de integración completas. | Bot desplegado en VPS, pruebas de integración. |
| 26-29 | 7-10 Jul | - Finalizar `README.md`, `docs/flujos.md`.<br>- Crear manuales de configuración para Distriluz, Caja Huancayo, API de Meta.<br>- Preparar informe final (estado, limitaciones, recomendaciones).<br>- Subir código a Git. | Repositorio completo, documentación final, informe. |
