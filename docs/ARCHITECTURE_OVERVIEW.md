# 🏛️ Arquitectura del Sistema – Visión General

Este documento describe la arquitectura general del sistema de compras desarrollado en Spring Boot (Etapa 08).

---

# 1️⃣ Arquitectura General

El sistema sigue una estructura **modular por capas**, basada en:

- **Capa Controller** → Entrada de peticiones HTTP.
- **Capa Service** → Reglas de negocio.
- **Capa Repository** → Acceso a datos (JPA/Hibernate o repositorio propio).
- **Capa Model** → Entidades del dominio.
- **Capa Util** → Funciones auxiliares.

---

# 2️⃣ Flujo Básico de una Operación

1. El cliente (Front, móvil o Postman) hace una petición.
2. El Controller valida y delega a un servicio.
3. El Service ejecuta reglas de negocio.
4. El Repository consulta o guarda datos.
5. Se devuelve respuesta limpia (DTO opcional).

---

# 3️⃣ Módulos Principales

- **User Module** → Registro, login, sesiones.
- **Product Module** → Productos y categorías.
- **Cart Module** → Carrito de compras por sesión.
- **Order Module** → Checkout.
- **Payment Module** → Gestión de pagos.

---

# 4️⃣ Estándares y buenas prácticas

- DTOs para comunicación externa (si aplica).
- Validaciones en capa service.
- Modelos limpios con Lombok.
- Manejo de errores controlado.
- Logs en puntos críticos del flujo.