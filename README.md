# ShopNow Mobile - QA Automation Challenge

Este repositorio contiene la estrategia de calidad, el plan de pruebas y la automatización de la aplicación **ShopNow Mobile**. El proyecto demuestra habilidades de arquitectura de pruebas, manejo de asincronía y medición de performance en entornos nativos.

## 🛠 Estructura del Proyecto
* `/docs`: Estrategia de QA, Test Plan y KPIs.
* `/android-app`: Aplicación Android y tests en **Espresso**.
* `/ios-app`: Aplicación iOS y tests en **XCUITest**.
* `/performance`: Reportes de tiempos de carga y uso de recursos.

## 🚀 Ejecución de Tests
### Android (Espresso)
1. Abrir el proyecto en Android Studio.
2. Ejecutar el comando en la terminal:
   `./gradlew connectedAndroidTest`

### iOS (XCUITest)
1. Abrir `ShopNow.xcworkspace` en Xcode.
2. Seleccionar el esquema `ShopNowUITests`.
3. Presionar `Product > Test` (Command + U).

## 🧪 Explicación Técnica: Async Testing (Tarea C)

### 1. ¿Cómo gestionarías la sincronización en Android?
En Android, el uso de `Thread.sleep()` está prohibido por ser ineficiente. La solución profesional es **IdlingResource**.
* **Mecanismo:** Registramos un recurso que monitorea las llamadas a la API o el estado del hilo de fondo. Espresso espera automáticamente a que el recurso esté "Idle" (inactivo) antes de realizar la siguiente acción o aserción. Esto garantiza que el test solo continúe cuando el Loader ha desaparecido y los datos están en pantalla.

### 2. ¿Cómo lo harías en iOS?
En iOS (XCUITest), no existe un IdlingResource nativo tan integrado, por lo que usamos **Expected Conditions** y **XCTWaiter**.
* **Mecanismo:** Utilizamos `XCTNSPredicateExpectation` para definir una condición (ej: que el elemento "Loader" sea `exists == false`). El `XCTWaiter` detendrá la ejecución del test hasta que se cumpla la condición o se agote el tiempo de espera (timeout), evitando que el test falle si el backend responde con delay.

## 📈 KPIs Principales
* **Pass Rate Objetivo:** > 95%
* **Cold Start Máximo:** 2.0s
* **Sincronización:** 0% de uso de esperas estáticas (`sleep`).