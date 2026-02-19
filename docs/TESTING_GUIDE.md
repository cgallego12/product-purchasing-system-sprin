# 🧪 Guía de Pruebas – Etapa 08

Este documento explica cómo probar el sistema de manera formal.

---

# 1️⃣ Pruebas Unitarias

Bibliotecas sugeridas:
- JUnit 5
- Mockito

### Ejemplos de pruebas:

✔️ Validar cálculo de carrito  
✔️ Validar subtotal de OrderItem  
✔️ Validación de setters personalizados

---

# 2️⃣ Pruebas de Integración

Pruebas realizadas con:
- Spring Boot Test
- H2 como base temporal

### Qué probar:

- Crear usuario → login → crear sesión
- Agregar productos → checkout → crear orden
- Procesar pago → validar estados

---

# 3️⃣ Pruebas Manuales (Postman)

Conjunto básico:

1. `POST /auth/register`
2. `POST /auth/login`
3. `POST /cart/{sessionId}/add`
4. `POST /orders/checkout`
5. `POST /payments`

Incluye ejemplos de cuerpos JSON para facilitar pruebas.