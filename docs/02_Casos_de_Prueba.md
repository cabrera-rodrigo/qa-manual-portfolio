# Matriz de casos de prueba (Test Cases)

## Resumen de Cobertura
* **Modulos cubiertos:** Autenticacion, Catalogo, Carrito, Checkout.
* **Total de casos:** 15

---

## Modulo 1: Autenticacion y registro

| ID | Titulo / Escenario | Prioridad | Precondiciones | Pasos / BDD | Resultado Esperado | Resultado Actual | Estado |

| **TC-01** | Login exitoso con credenciales validas | Alta | Usuario previamente registrado en el sistema | 1. Ir a seccion `/login`<br>2. Ingresar email valido y password correcto<br>3. Clic en "Login" | Redireccion al Home y visualizacion del texto "Logged in as ..." en el navbar. | Comportamiento acorde al esperado | PASS | 
| **TC-02** | Login fallido con contraseña incorrecta | Alta | Usuario registrado | 1. Ir a `/login`<br>2. Ingresar email valido y password erroneo<br>3. Clic en "Login" | Se bloquea el acceso y aparece alerta roja: "Your email or password is incorrect!". | Comportamiento acorde al esperado | PASS |
| **TC-03** | Registro de usuario con email ya existente | Media | Email ya registrado en base de datos | 1. En "New User Signup", ingresar nombre y un email ya usado.<br>2. Clic en "Signup" | El sistema impide avanzar al formulario y muestra el mensaje "Email Adress already exist!". | Comportamiento acorde al esperado | PASS | 
| **TC-04** | Intentar registrarse dejando campos obligatorios vacios | Media | Estar en el formulario de alta | 1. En formulario de alta, dejar varios campos vacios.<br>2. Clic en "Create Account" | Se impide registrar al usuario, alertando los campos obligatorios que dejo vacios | Comportamiento acorde al esperado | PASS |

---

## Modulo 2: Catalogo y busqueda

| ID | Titulo / Escenario | Prioridad | Precondiciones | Pasos / BDD | Resultado Esperado | Resultado Actual | Estado |

| **TC-05** | Busqueda de producto existente por palabra clave | Alta | Estar en `/products` | 1. Ingresar "[Nombre de prenda, ej: Blue top]" en el buscador.<br>2. Clic en el boton de lupa. | Se listan unicamente los productos que coinciden con el criterio buscado | Comportamiento acorde al esperado | PASS | 
| **TC-06** | Busqueda sin resultados (texto inexistente) | Baja | Estar en `/products` | 1. Ingresar texto aleatorio ("xyz1234") en el buscador.<br>2. Clic en buscar. | La grilla queda vacia o muestra un mensaje indicando que no hay coincidencias | Comportamiento acorde al esperado | PASS |
| **TC-07** | Filtrar productos por categoria lateral women > Dress | Media | Estar en home o productos | 1. Hacer clic en "+".<br>2. Seleccionar "Dress" | Se muestra los resultados segun la categoria seleccionada | Comportamiento acorde al esperado | PASS |

---

## Modulo 3: Carrito de compras y checkout

| ID | Titulo / Escenario | Prioridad | Precondiciones | Pasos / BDD | Resultado Esperado | Resultado Actual | Estado |

| **TC-08** | Agregar producto al carrito desde el catalogo | Alta | Ninguna | 1. Hacer hover sobre el primer producto.<br>2. Clic en "Add to cart".<br>3. Clic en "View cart" en el modal emergente. | El producto figura en la tabla del carrito con cantidad = 1 y el precio unitario correcto | Comportamiento acorde al esperado | PASS |
| **TC-09** | Verificar calculo de precio total al sumar multiples unidades | Alta | Estar en el detalle del producto | 1. Cambiar el input de "Quantity" a `3`.<br>2. Clic en "Add to cart" e ir al carrito. | El campo "Total" de la fila multiplica exactamente el precio unitario por 3. | El input acepta numeros negativos y se altera el saldo. (**Ver BUG-01**) | FAIL |
| **TC-10** | Eliminar producto del carrito | Media | Tener al menos 1 ítem en el carrito | 1. Ir a `/view_cart`.<br>2. Hacer clic en el botón "X" al final de la fila del producto. | El producto desaparece de la lista y si era el único, se muestra "Cart is empty!". | Se muestra "Cart is empty", pero al recargar la pagina vuelve a aparecer el producto. (**Ver BUG-02**) | FAIL |
| **TC-11** | Intentar avanzar al checkout sin haber iniciado sesion | Alta | Carrito con productos y usuario deslogueado | 1. Ir a `/view_cart`.<br>2.Hacer clic en el boton "Proceed To Checkout". | El sistema impide continuar al checkout y muestra un pop up para registrarse/loguearse | Comportamiento acorde al esperado | PASS |