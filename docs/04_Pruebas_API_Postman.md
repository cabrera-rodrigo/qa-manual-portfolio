# Pruebas de Integración de API (Postman)

## 1. Alcance y Objetivo
Validar el comportamiento de los endpoints provistos por la API de **Automation Exercise**, verificando contratos de respuesta (JSON Schema), códigos de estado HTTP, mensajes de validación en escenarios negativos y tiempos de respuesta aceptables (< 1500 ms).

* **URL Base:** `https://automationexercise.com/api`
* **Herramienta:** Postman
* **Formato de Respuesta:** JSON

---

## 2. Resumen de Casos Ejecutados

| ID | Endpoint | Método | Escenario de Prueba | HTTP Esperado | HTTP Actual | Response Code (JSON) | Estado |

| **API-01** | `/productsList` | `GET` | Obtener listado completo de productos | `200 OK` | `200 OK` | `200` | **PASS** |
| **API-02** | `/searchProduct` | `POST` | Buscar producto enviando parámetro válido (`search_product`) | `200 OK` | `200 OK` | `200` | **PASS** |
| **API-03** | `/searchProduct` | `POST` | Buscar producto omitiendo el parámetro obligatorio | `400 Bad Request` | `200 OK`  | `400` | **FAIL (Observación)** |
| **API-04** | `/verifyLogin` | `DELETE` | Intentar método no permitido sobre endpoint de Login | `405 Not Allowed` | `200 OK`  | `405` | **FAIL (Observación)** |

---

## 3. Detalle de Ejecución de Pruebas

### [API-01] GET - Obtener listado completo de productos
* **URL:** `https://automationexercise.com/api/productsList`
* **Headers:** `Accept: application/json`
* **Validaciones realizadas:**
  1. El servidor responde en un tiempo menor a `1800 ms`.
  2. El cuerpo de la respuesta contiene la clave `"products"` como un array no vacío.
  3. Cada objeto dentro de `"products"` incluye los atributos obligatorios: `id`, `name`, `price`, `brand` y `category`.
* **Evidencia:** [](../evidencias/Captura%20de%20pantalla%202026-10-25%20192526.png)

**Fragmento del Response obtenido:**
```json
{
  "responseCode": 200,
  "products": [
    {
      "id": 1,
      "name": "Blue Top",
      "price": "Rs. 500",
      "brand": "Polo",
      "category": {
        "usertype": { "usertype": "Women" },
        "category": "Tops"
      }
    }
  ]
}
```

### [API-02] POST - Búsqueda de producto por parámetro
* **URL:** `https://automationexercise.com/api/productsList`
* **Body:** (form-data):
  - Key: search_product | Value: top
* **Validaciones realizadas:**
  1. Se retorna "responseCode": 200.
  2. Todos los items devueltos en el array coinciden con el criterio de busqueda enviado
* **Evidencia:** [](../evidencias/Captura%20de%20pantalla%202026-10-25%20192731.png)
 
### [API-03] POST - Busqueda de producto sin enviar parametro obligatorio
* **URL:** `https://automationexercise.com/api/searchProduct`
* **Body:** Vacio
* **Resultado esperado:** El servidor deberia rechazar la peticion con estado HTTP 400 Bad request e indicar el parametro faltante
* **Resultado actual:** 
  - Status HTTP: 200 OK
  - Body JSON:
    ```json
    {
    "responseCode": 400,
    "message": "Bad request, search_product parameter is missing in POST request."
    }
    ```
* **Observacion tecnica:** El mensaje dentro del JSON indica un codigo 400, el encabezado HTTP devuelve 200 OK (Falso positivo). Esto se reporta como defecto de arquitectura en [](../docs/03_Reporte_de_Bugs.md)

### [API-04] DELETE - Verificar login con metodo HTTP no soportado
* **URL:** `https://automationexercise.com/api/verifyLogin``
* **Metodo utilizado:** DELETE
* **Resultado esperado:** Estado HTTP 405 Method Not Allowed
* **Resultado actual:** Estado HTTP 200 OK con payload interno:
  ```json
  {
    "responseCode": 405,
    "message": "This request method is not supported."
  }
  ```