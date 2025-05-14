# Bot Multiservicio para WhatsApp con Rasa

Este repositorio contiene el código fuente y la documentación para un **bot multiservicio** que opera en WhatsApp, desarrollado con **Rasa**, **FastAPI**, **Twilio** (para pruebas iniciales), y la **API de WhatsApp de Meta** (en producción). El bot permite a los usuarios realizar consultas, pagos, y recargas, con registro de conversaciones en **Google Sheets** y un diseño modular para integrar servicios como **Culqi**, **Distriluz**, y **Caja Huancayo**

## Cronograma del Proyecto

El desarrollo del bot se divide en tres etapas, con un plazo total de **8 semanas** (14 de mayo al 9 de julio de 2025). A continuación, se detalla el cronograma por etapa, incluyendo tareas, fechas, duraciones, y entregables.

### Etapa 1: Chatbot Menú Multiservicio (Interacción Base)

**Objetivo**: Implementar un bot con Rasa conectado a WhatsApp vía Twilio, con un menú interactivo (servicios, recargas, cambio de divisas, préstamos, asesor) y registro de conversaciones en Google Sheets.  
**Duración**: 2 semanas (14-27 May 2025).  
**Entregables**:
- Código fuente (Rasa, FastAPI, Twilio, Google Sheets).
- Archivos de Rasa configurados (`domain.yml`, `nlu.yml`, `rules.yml`).
- Bot funcional en WhatsApp con menú multiservicio.
- Hoja de cálculo con conversaciones registradas.
- Documentación inicial (`README.md`, `docs/flujos.md`).

#### Tareas
| Día | Fecha | Tareas | Entregables |
|-----|-------|--------|-------------|
| 1-2 | 14-15 May | - Verificar entorno (Python 3.9, Rasa).<br>- Instalar dependencias (`rasa`, `fastapi`, `twilio`, etc.).<br>- Crear estructura del proyecto (`src/`, `rasa/`, `tests/`).<br>- Configurar Twilio (cuenta, número, webhook con `ngrok`).<br>- Crear `.env`. | Estructura del proyecto, Twilio configurado, `requirements.txt`, `.env`. |
| 3-4 | 16-17 May | - Configurar Google Sheets (hoja "ConversacionesBot", API, `credentials.json`).<br>- Implementar `src/storage/google_sheets.py`.<br>- Probar guardar una fila en Google Sheets. | Hoja de cálculo configurada, `credentials.json`, `GoogleSheetsRepository`. |
| 5-7 | 19-21 May | - Actualizar `rasa/domain.yml`, `nlu.yml`, `rules.yml` con menú multiservicio.<br>- Entrenar modelo (`rasa train`).<br>- Probar localmente (`rasa shell`, `rasa interactive`). | Archivos de Rasa configurados, modelo entrenado. |
| 8-10 | 22-24 May | - Implementar `src/whatsapp/twilio_client.py`, `src/bot/rasa_handler.py`, `src/main.py`.<br>- Conectar Rasa, FastAPI, Twilio, Google Sheets.<br>- Probar bot en WhatsApp ("hola", "menú"). | Bot funcional, registro de conversaciones. |
| 11-13 | 25-27 May | - Probar flujos del menú.<br>- Corregir errores.<br>- Añadir pruebas unitarias (`tests/`).<br>- Documentar (`README.md`, `docs/flujos.md`).<br>- Subir a Git. | Repositorio Git, bot estable, documentación inicial, pruebas. |
| 14 | 28 May | - Revisar bot y corregir errores menores.<br>- Preparar informe de Etapa 1. | Informe de Etapa 1. |

### Etapa 2: Pasarela de Pago con Culqi

**Objetivo**: Integrar Culqi para procesar pagos con tarjeta, Yape, o Plin, con confirmación en WhatsApp y registro en Google Sheets.  
**Duración**: 2 semanas (28 May-10 Jun 2025).  
**Entregables**:
- Código con integración de Culqi.
- Flujo de pagos en Rasa (intención `pay`, slots).
- Registro de pagos en Google Sheets.
- Manual de configuración de Culqi.
- Documentación actualizada.

#### Tareas
| Día | Fecha | Tareas | Entregables |
|-----|-------|--------|-------------|
| 1-3 | 28-30 May | - Crear cuenta en Culqi, obtener claves de prueba.<br>- Instalar `culqi`.<br>- Implementar `src/services/culqi_service.py`.<br>- Probar cargo localmente. | `CulqiService`, claves de Culqi. |
| 4-6 | 31 May-2 Jun | - Añadir intención `pay` en Rasa.<br>- Usar slots para detalles de pago.<br>- Actualizar `rasa_handler.py`.<br>- Entrenar modelo (`rasa train`). | Flujo de pagos en Rasa, modelo actualizado. |
| 7-9 | 3-5 Jun | - Actualizar `main.py` para enviar enlaces de pago.<br>- Registrar pagos en Google Sheets.<br>- Configurar webhook para validar pagos. | Backend con pagos, registro en Google Sheets. |
| 10-12 | 6-8 Jun | - Probar pagos (tarjeta, Yape, Plin).<br>- Verificar confirmaciones en WhatsApp.<br>- Añadir pruebas unitarias.<br>- Corregir errores. | Bot con pagos funcionales, pruebas. |
| 13-14 | 9-10 Jun | - Actualizar `README.md`, `docs/flujos.md`.<br>- Crear manual de Culqi.<br>- Preparar informe de Etapa 2. | Documentación actualizada, manual de Culqi, informe. |

### Etapa 3: Consultas y Pagos vía APIs REST

**Objetivo**: Integrar APIs REST de Distriluz y Caja Huancayo para consultas y pagos, con diseño modular para futuros servicios.  
**Duración**: 3.5 semanas (11 Jun-9 Jul 2025).  
**Entregables**:
- Código modular con Distriluz y Caja Huancayo.
- Bot desplegado en VPS con API de Meta.
- Documentación completa (instalación, uso, flujos).
- Manuales de configuración de APIs.
- Informe final.

#### Tareas
| Día | Fecha | Tareas | Entregables |
|-----|-------|--------|-------------|
| 1-4 | 11-14 Jun | - Obtener credenciales de Distriluz y Caja Huancayo.<br>- Estudiar documentación de APIs.<br>- Implementar `base_service.py`, `service_factory.py`. | Credenciales, `BaseService`, `ServiceFactory`. |
| 5-9 | 15-19 Jun | - Implementar `distriluz_service.py` para consultas.<br>- Añadir intenciones `consult_debt`, `pay_debt`.<br>- Integrar con FastAPI y Google Sheets.<br>- Entrenar modelo. | Servicio de Distriluz, Rasa actualizado. |
| 10-14 | 20-24 Jun | - Implementar `caja_huancayo_service.py` para pagos.<br>- Actualizar Rasa y FastAPI.<br>- Registrar transacciones.<br>- Entrenar modelo. | Servicio de Caja Huancayo, integración completa. |
| 15-20 | 25-30 Jun | - Probar flujos de Distriluz y Caja Huancayo.<br>- Añadir servicio ficticio para modularidad.<br>- Implementar pruebas unitarias.<br>- Corregir errores. | Bot modular, pruebas. |
| 21-25 | 1-6 Jul | - Configurar VPS (Ubuntu 22.04, HTTPS).<br>- Implementar `meta_client.py` para API de Meta.<br>- Migrar de Twilio a Meta.<br>- Probar bot en VPS. | Bot en VPS, integración con API de Meta. |
| 26-29 | 7-10 Jul | - Finalizar `README.md`, `docs/flujos.md`.<br>- Crear manuales de Distriluz, Caja Huancayo, Meta.<br>- Preparar informe final.<br>- Subir a Git. | Repositorio completo, documentación, informe. |
