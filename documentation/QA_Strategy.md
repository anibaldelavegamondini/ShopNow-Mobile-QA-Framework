# 🚀 QA Strategy - ShopNow Mobile

Este documento define el enfoque estratégico, las metodologías y las herramientas necesarias para garantizar la calidad de la aplicación **ShopNow Mobile**. Como Arquitecto de Pruebas, el objetivo es establecer un marco de trabajo (framework) que sea escalable, mantenible y orientado a la detección temprana de defectos.

---

## 1. Visión General y Objetivos
La estrategia se centra en la entrega de una aplicación móvil de alto rendimiento, asegurando que las funcionalidades de **Login, Catálogo y Favoritos** operen sin fricción bajo condiciones de red variables.

### Objetivos Principales:
* **Detección Temprana:** Implementar una cultura *Shift-Left*.
* **Automatización Robusta:** Reducir el *flakiness* mediante sincronización nativa.
* **Visibilidad:** Proveer métricas claras (KPIs) sobre el estado de la salud del software.

---

## 2. Pirámide de Pruebas (Test Pyramid)
Para optimizar el Retorno de Inversión (ROI), distribuiremos las pruebas de la siguiente manera:

* **UI / End-to-End (10%):** Pruebas críticas de flujo de usuario usando **Espresso (Android)** y **XCTest (iOS)**.
* **Integración / API (30%):** Validación de contratos entre el frontend y el backend (Mocks de servicios).
* **Unit Tests (60%):** Pruebas de lógica de negocio y validadores de datos en la capa de código.

---

## 3. Stack Tecnológico y Arquitectura
Utilizaremos herramientas nativas para garantizar la máxima velocidad y acceso a las APIs internas del sistema operativo.

| Componente | Android | iOS |
| :--- | :--- | :--- |
| **Framework de Test** | Espresso | XCUITest |
| **Lenguaje** | Kotlin | Swift |
| **Patrón de Diseño** | Screen Object Pattern | Screen Object Pattern |
| **Sincronización** | IdlingResources | XCTWaiter / Expectations |
| **Performance** | Android Profiler | Instruments (Time Profiler) |

### Screen Object Pattern
Para ambas plataformas, separaremos la **interacción con la UI** de las **aserciones**. Esto permite que si el ID de un botón cambia, solo se deba actualizar un archivo y no todos los casos de prueba.

---

## 4. Estrategia de Sincronización (Manejo de Asincronía)
Dado que el backend de **ShopNow** presenta delays controlados, la estrategia prohíbe el uso de `Thread.sleep()`.

1.  **Android:** Implementación de `IdlingResource` para monitorear el estado del Loader de red.
2.  **iOS:** Uso de `NSPredicate` y `XCTWaiter` para realizar esperas explícitas basadas en estados de los elementos de la UI.

---

## 5. Gestión de Riesgos y Mitigación

| Riesgo | Impacto | Mitigación |
| :--- | :--- | :--- |
| **Tests Intermitentes (Flaky)** | Alto | Implementar reintentos en CI y sincronización por estados, no por tiempo. |
| **Fragmentación de OS** | Medio | Ejecución en emuladores con diferentes niveles de API (Android 10 a 14) y versiones de iOS. |
| **Backend Inestable** | Medio | Uso de **MockWebServer** para pruebas de UI aisladas para asegurar que el test valide la UI y no la red. |

---

## 6. Definición de "Done" (DoD)
Una funcionalidad se considera "lista para producción" si cumple con:
1.  **Cobertura:** Mínimo 80% en unit tests.
2.  **Automatización:** El "Happy Path" está automatizado y pasa en el pipeline de CI.
3.  **Performance:** El *Cold Start* de la app es inferior a 2 segundos.
4.  **Revisión:** Código de test revisado por un par (Code Review).

---

## 7. Métricas y KPIs
* **Pass Rate:** > 95% de los tests en la regresión deben pasar.
* **Execution Time:** El set total de UI tests no debe superar los 10 minutos.
* **Defect Leakage:** Menos del 5% de errores reportados por usuarios finales.