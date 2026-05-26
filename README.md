# 🚖 Sistema de Gestión de Servicios - Cooperativa de Taxis Multizona

## 1. Resumen Ejecutivo del Proyecto
El sistema resuelve la problemática de gestión operativa de una cooperativa de taxis distribuidos en una red urbana multizona con restricciones dinámicas de conectividad vial. El software automatiza desde la recepción encolada de solicitudes por operadores hasta la asignación óptima de conductores basados en su habilitación de servicio y viabilidad de rutas, consolidando toda la información en un historial persistente. El objetivo general es construir una aplicación robusta, modular y extensible bajo el paradigma orientado a objetos, garantizando una arquitectura limpia. Su valor académico radica en la integración transversal de estructuras de datos complejas (grafos para la red vial) con patrones de diseño, principios SOLID, control estricto de excepciones y persistencia, sirviendo como métrica de la capacidad de diseño arquitectónico y sustentación técnica del estudiante.

---

## 2. Objetivos

### Objetivo General
Diseñar e implementar un sistema de gestión de servicios para una cooperativa de taxis multizona aplicando el paradigma de Programación Orientada a Objetos (POO), modelado UML, principios SOLID y patrones de diseño para asegurar una solución de software escalable, persistente y correctamente sustentada.

### Objetivos Específicos
* **Modelar formalmente** la arquitectura del sistema mediante diagramas de casos de uso, de clases y de secuencia coherentes con las reglas del negocio.
* **Abstraer e implementar** las entidades del dominio de taxis (Conductores, Vehículos, Solicitudes, Red Vial) garantizando el encapsulamiento y el polimorfismo en los tipos de servicios.
* **Construir un motor de asignación** que verifique la disponibilidad del conductor, la compatibilidad del servicio y la conectividad vial de la zona de origen en tiempo real.
* **Aplicar una separación clara de responsabilidades** mediante una arquitectura en capas que aísle la lógica del negocio de la persistencia de datos y de la interfaz de usuario.
* **Implementar al menos un patrón de diseño** (como *Strategy* o *Factory Method*) para resolver problemas específicos de variación de tarifas o creación de servicios.
* **Garantizar la robustez del sistema** mediante el diseño de una jerarquía de excepciones personalizadas para controlar flujos inválidos y mitigar caídas de la aplicación.
* **Garantizar la persistencia del estado** del sistema mediante archivos planos o serialización de objetos, permitiendo ciclos de carga y guardado íntegros.
* **Coordinar el ciclo de desarrollo** mediante el uso controlado de Git y GitHub, evidenciando el trabajo colaborativo e individual mediante commits trazables.

---

## 3. Alcance del Sistema

### Qué Incluye
* Registro y encolamiento FIFO (First-In, First-Out) de solicitudes de servicio con estados mutables.
* Catálogo de conductores con sus respectivas habilitaciones para tipos de servicio específicos (Estándar, Baúl/Parrilla, Mascotas).
* Simulación de la red vial interzona con capacidad de habilitar/deshabilitar conexiones de forma dinámica.
* Cálculo automático de tarifas estimadas basándose en una tarifa mínima fija (\$5.000 COP) más un costo calculado por la distancia transitable del tramo.
* Módulo de persistencia para guardar y cargar el estado completo del sistema en archivos locales.

### Qué No Incluye
* Geolocalización real por GPS (se trabaja mediante abstracción de zonas geográficas discretas/nodos).
* Procesamiento de pagos electrónicos en tiempo real (únicamente se calcula y registra el valor monetario).
* Módulo de nómina, contratación o liquidación laboral avanzada de los conductores.
* Concurrencia real multiusuario en red (se asume un entorno local operado secuencialmente por consola o GUI).

---

## 4. Arquitectura del Proyecto y Paquetes
Para garantizar el cumplimiento académico de separación de responsabilidades, la solución se divide en las siguientes capas de software:
* `co.edu.unimagdalena.taxis.domain`: Clases puras del modelo (`Conductor`, `Vehiculo`, `Solicitud`, `Zona`).
* `co.edu.unimagdalena.taxis.services`: Lógica central, asignación, cálculo de rutas e historial (`GestorServicios`, `CalculadorTarifas`).
* `co.edu.unimagdalena.taxis.persistence`: Clases encargadas del almacenamiento en disco (`ManejadorArchivos`, `SerializadorDAO`).
* `co.edu.unimagdalena.taxis.exceptions`: Jerarquía de excepciones personalizadas (`ZonaInexistenteException`, `SinConectividadVialException`).
* `co.edu.unimagdalena.taxis.ui`: Clases de la interfaz de usuario por consola.

---

## 5. Diseño UML
*(Nota: Puedes ver las imágenes completas en alta resolución dentro de la carpeta `/uml` de este repositorio)*

### Casos de Uso e Implementación de Código
El sistema cuenta con un control estricto de flujos críticos de la rúbrica:
1. **Asignación de Servicio:** Valida disponibilidad del conductor, tipo de vehículo y conectividad de rutas en la red vial.
2. **Cierre de Servicio:** Modifica estados de la solicitud, calcula la tarifa final exacta aplicando la fórmula polinómica y libera al conductor a estado disponible.

---

## 6. Instrucciones de Ejecución
Para compilar y ejecutar este proyecto de forma local:
1. Descargue o clone este repositorio.
2. Abra el proyecto en su IDE de preferencia (NetBeans, IntelliJ, Eclipse, VS Code).
3. Asegúrese de contar con el SDK de Java (versión 11 o superior) o el intérprete de Python configurado.
4. Ejecute la clase principal ubicada en la capa de UI para desplegar el menú interactivo.
