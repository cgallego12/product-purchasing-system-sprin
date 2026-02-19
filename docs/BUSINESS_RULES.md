# 📘 Reglas de Negocio – Sistema de Compras

Este documento detalla las reglas de negocio aplicadas en el sistema.

---

# 1️⃣ Usuarios

- El email del usuario debe ser único.
- Un usuario debe estar activo para comprar.
- Un usuario debe tener al menos **una dirección** para completar un pago.

---

# 2️⃣ Carrito (Cart)

- Un carrito está asociado a una sesión.
- Si el usuario agrega el mismo producto, debe **aumentar la cantidad**, no duplicarse.
- El precio unitario se congela al momento de agregarlo.

---

# 3️⃣ Productos

- Un producto debe estar activo para mostrarse.
- No se permite stock negativo.
- No se puede agregar al carrito un producto sin stock.

---

# 4️⃣ Checkout y órdenes

- Solo usuarios registrados pueden crear órdenes.
- La dirección de envío y facturación deben existir.
- El total final debe recalcularse siempre antes de guardar la orden.

---

# 5️⃣ Pagos

- Se permiten montos negativos para reembolsos.
- Un pago exitoso define `paidAt`.
- Un pago “refunded” debe generar un registro histórico adicional.

---

# 6️⃣ Sesiones

- Una sesión de invitado puede convertirse en sesión de usuario.
- Las sesiones expiran después de X horas (parámetro configurable).