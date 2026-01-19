# 📊 Metrics & KPIs - ShopNow Mobile

Este documento establece los indicadores clave de desempeño (KPIs) y las métricas de calidad que se utilizarán para evaluar el éxito de la estrategia de pruebas y la estabilidad de la aplicación.

---

## 1. KPIs de Automatización
Estos indicadores miden la salud y eficiencia de nuestro framework de Espresso y XCTest.

| KPI | Objetivo (Target) | Descripción |
| :--- | :--- | :--- |
| **Test Pass Rate** | > 95% | Porcentaje de pruebas automatizadas que pasan exitosamente. |
| **Flakiness Ratio** | < 2% | Porcentaje de tests que fallan por causas ajenas al código (red, sincronización). |
| **Execution Time** | < 10 min | Tiempo total de ejecución de la suite de UI en el pipeline de CI/CD. |
| **Automation Coverage** | > 80% | Porcentaje de "Happy Paths" definidos en el Test Plan que están automatizados. |

---

## 2. Métricas de Calidad del Producto
Miden la estabilidad de la aplicación desde la perspectiva del usuario final.

* **Crash-Free Sessions:** Objetivo **99.9%**. Porcentaje de sesiones de usuario que no terminan en un cierre inesperado.
* **Defect Leakage:** Porcentaje de errores encontrados en producción vs. errores encontrados en QA. (Fórmula: `[Bugs Prod / (Bugs QA + Bugs Prod)] * 100`).
* **Mean Time to Repair (MTTR):** Tiempo promedio que tarda el equipo en corregir un bug crítico desde su reporte.

---

## 3. Métricas de Performance (Módulo 4)
Basadas en el uso de Android Profiler e iOS Instruments.

| Métrica | Umbral (Threshold) | Herramienta |
| :--- | :--- | :--- |
| **Cold Start** | < 2.0 segundos | Android Profiler / Instruments |
| **Warm Start** | < 1.0 segundo | Android Profiler / Instruments |
| **Time to Interactive** | < 3.0 segundos | Medición de carga de productos con delay de red. |
| **Memory Leaks** | 0 Leaks | LeaksTool (iOS) / LeakCanary (Android) |

---

## 4. Matriz de Riesgos y Priorización
Para ShopNow, los riesgos se gestionan bajo la siguiente lógica:

| Nivel de Riesgo | Acción Requerida |
| :--- | :--- |
| **Crítico (Rojo)** | Bloquea el lanzamiento (Release Stopper). |
| **Alto (Naranja)** | Requiere aprobación de Product Manager para lanzar con el bug conocido. |
| **Bajo (Verde)** | Se documenta como "Deuda Técnica" y se programa para el siguiente sprint. |

---

## 5. Visualización y Reporte
* **Reportes de Test:** Se generarán reportes automáticos en formato **Allure** o **HTML** al finalizar cada ejecución en el CI.
* **Dashboard:** Se recomienda la integración con herramientas como SonarQube para medir la mantenibilidad del código de los tests.

---

> **Nota para el revisor:** > Estas métricas han sido seleccionadas específicamente para validar la robustez de la aplicación ShopNow frente a condiciones adversas de red y asegurar una experiencia de usuario fluida y libre de bloqueos.