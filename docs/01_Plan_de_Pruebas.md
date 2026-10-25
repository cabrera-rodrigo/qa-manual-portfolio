# Plan de Pruebas - E-Commerce Automation Exercise

## 1. Objetivo
Validar los flujos criticos de negocio de la plataforma web Automation Exercise , asegurando que un usuario pueda registrarse, buscar productos, gestionar su carrito de compras y procesar una orden sin bloqueos funcionales ni errores de interfaz

## 2. Alcance
Se realizaran pruebas funcionales sobre los siguientes modulos:
* **Autenticacion:** Registro de usuario nuevo, Login y Logout.
* **Catalogo y Busqueda:** Filtrado por categoria y barra de busqueda de productos.
* **Carrito de Compras:** Agregado de items, modificacion de cantidades y eliminacion.
* **Checkout:** Flujo de compra y formulario de contacto/envio.

## 3. Fuera de alcance
* Pruebas de performance o carga del servidor.
* Pruebas sobre pasarelas de pago reales con tarjetas de credito vigente.
* Pruebas en dispositivos moviles nativos (solo se evalua la version web desktop).

## 4. Estrategia y tipos de prueba
* **Smoke Testing:** Verificacion rapida inicial para confirmar que las secciones principales cargan.
* **Pruebas Funcionales (Caja Negra):** Validacion de caminos felices (Happy Path) y caminos negativos (validacion de campos vacios, formatos invalidos).
* **Pruebas de UI/UX basicas:** Verificacion visual de alineacion de elementos, textos superpuestos o enlaces rotos.
* **Verificacion en DevTools:** Inspeccion basica de consola y pestaña Network ante errores inesperados (codigos de estado 4xx/5xx).

## 5. Entorno de pruebas
* **Url base:** https://automationexercise.com/
* **Sistema Operativo:** Windows 11 Home
* **Navegador:** Google Chrome Versión 156.0.8078.48
* **Resolucion:** 1920x1080 px

## 6. Criterios de aceptacion y suspension
* **Criterio de aprobacion:** El 100% de los casos de prioridad alta ejecutados sin defectos criticos (Blockers) abiertos.
* **Criterio de suspension:** Caida total del entorno (Error 500 generalizado) que impida navegar la web.
