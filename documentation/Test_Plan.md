# 📋 Test Plan - ShopNow Mobile

Este Plan de Pruebas detalla el alcance, los recursos, el cronograma y las actividades necesarias para validar la primera versión de la aplicación **ShopNow Mobile**.

---

## 1. Alcance de las Pruebas (Scope)

### 1.1. Funcionalidades Incluidas (In-Scope)
| Módulo | Descripción |
| :--- | :--- |
| **Autenticación** | Login con email/password, validaciones de formato y manejo de errores. |
| **Catálogo** | Visualización de lista de productos y funcionalidad de refresco manual. |
| **Detalle** | Carga de imágenes, descripción, precio y persistencia de favoritos. |
| **Favoritos** | Gestión de estado (añadir/quitar) y persistencia durante la sesión. |
| **Ajustes** | Cambio de tema (Dark Mode) y cierre de sesión. |

### 1.2. Funcionalidades Fuera de Alcance (Out-of-Scope)
* Pasarela de pagos real (Checkout).
* Registro de nuevos usuarios.
* Pruebas de seguridad (Pentesting).

---

## 2. Casos de Prueba (Test Cases)

### 2.1. Pruebas de Interfaz de Usuario (UI/E2E)
* **TC-LOGIN-01:** Inicio de sesión exitoso y transición al Listado de Productos.
* **TC-LOGIN-02:** Validación de error al ingresar credenciales incorrectas.
* **TC-FAV-01:** Marcar un producto como favorito desde el detalle y verificar estado en el listado.
* **TC-FAV-02:** Persistencia de favoritos tras navegar entre diferentes pantallas.
* **TC-ASYNC-01:** (Tarea A) Verificación de visualización de Loader durante la carga de datos con delay de backend.

### 2.2. Pruebas de Rendimiento (Performance)
* **PERF-01:** Medición del *Cold Start* (Tiempo desde el lanzamiento hasta la UI interactiva).
* **PERF-02:** Uso de memoria (RAM) durante el scroll infinito en el Listado de Productos.

---

## 3. Estrategia de Ejecución

### 3.1. Tipos de Pruebas
1.  **Smoke Tests:** Ejecución de los flujos críticos (Login y Favoritos) en cada compilación.
2.  **Regression Tests:** Set completo de pruebas automatizadas antes de cada lanzamiento.
3.  **Exploratory Testing:** Sesiones manuales de 30 minutos para identificar comportamientos inesperados en la UI.

### 3.2. Configuración de Entorno (Test Environment)
* **Dispositivos Android:** * Emulador: Pixel 6 (API 33).
    * Físico: Samsung Galaxy S21 (Android 13).
* **Dispositivos iOS:**
    * Simulador: iPhone 15 (iOS 17).
    * Físico: iPhone 13 (iOS 16).

---

## 4. Gestión de Defectos

Los defectos encontrados serán categorizados por severidad:
* **S1 - Crítica:** Bloquea una funcionalidad principal (ej. No se puede iniciar sesión).
* **S2 - Mayor:** Funcionalidad con errores pero tiene un *workaround*.
* **S3 - Menor:** Errores visuales, de ortografía o cosméticos.

---

## 5. Criterios de Aceptación y Salida

Para dar por concluida la fase de pruebas de ShopNow Mobile:
1.  **Ejecución:** 100% de los casos de prueba planificados han sido ejecutados.
2.  **Pass Rate:** Al menos el 95% de los tests automatizados deben estar en estado "Passed".
3.  **Bugs Críticos:** 0 defectos abiertos de severidad S1 o S2.
4.  **Automatización:** El escenario asíncrono (Tarea A) debe ser 100% estable en el pipeline.

---

## 6. Sincronización Asíncrona (Detail)

Cumpliendo con el requisito de la **Tarea B**, se define que:
* **Espresso:** Se utilizará `CountingIdlingResource` para sincronizar las llamadas de red asíncronas.
* **XCTest:** Se utilizará `XCTWaiter` con una política de espera de máximo 5 segundos para la desaparición del Loader de carga.