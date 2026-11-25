---
name: terraform-editor
description: Usar siempre que se quiera crear o modificar un archivo de Terraform.
---

# Tipos de archivos

## versions.tf

Este fichero gestiona la versión de terraform, el versionado de los proveedores y la configuración de backend para el terraform state. Unicamente contendrá un único bloque `terraform`. Los bloques hijos deben seguir el orden:

- `required_version`: El patron a debe ser `>= X.Y.0`. Se debe fijar la ultima version mayor y minor estable.
- `required_providers`: 
  - Los proveedores deben ordenarse alfabéticamente.
  - El nombre por defecto debe ser el propio del proveedor. En caso de necesitarse dos configuraciones del mismos proveedor, consultar alias.
  - El patron a debe ser `~> N.0`. Se debe fijar la ultima version mayor estable.
- `backend`: Consulta con el usuario.

Una vez establecida la configuración, no se debe modificar a menos que sea solicitada explícitamente. En caso de modificarse, hay que investigar y compartir con el usuario los breaking changes que pueden producir, y esperar respuesta.

## providers.tf

Este fichero gestiona la configuración de los proveedores de Terraform. Unicamente contendrá los bloques `provider`. Los bloques deben seguir:

- Orden alfabéticamente.
- Nombre por defecto del proveedor, salvo que se necesiten múltiples configuraciones del mismo proveedor, en cuyo caso se debe usar `alias`.
- No modificar la versión del proveedor a menos que sea necesario y se haya consultado con el usuario.

## main.tf

Este fichero gestiona los recursos principales de Terraform. Unicamente contendrá bloques `resource`, `data`, `module`. Los bloques deben seguir:

- Los nombres de los bloques deben ser `snake_case`.
- Los bloques deben organizarse de manera que los recursos que dependen de otros se definan después de los recursos de los que dependen.
- Si un `data` se queda huérfano, debe eliminarse.

Los bloques `import` y `removed` pueden ser añadidos por solicitud explícita. El bloque deben ir antes de los bloques `resource` que correspondan. Al implementar `removed`, consultar si debe ser comentado o borrado el bloque que remueve.

## locals.tf

Este fichero gestiona las variables locales de Terraform. Unicamente contendrá un único bloque `locals`. Los atributos deben seguir:

- Orden alfabéticamente por el nombre de la variable local.
- Definir solo las variables locales necesarias para evitar redundancia y mejorar la legibilidad.
- Los valores de las variables locales deben ser expresiones claras y concisas.
- Si una variable local se queda huérfana, debe eliminarse.

## variables.tf

Este fichero gestiona las variables de Terraform. Unicamente contendrá bloques `variable`. Solo se generan variables por solicitud explícita. Los bloques deben seguir:

- Orden alfabéticamente por el nombre de la variable.
- El orden de los atributos debe ser: `type`,  `sensitive`, `default`, `description`, y `validation`
- `type` debe tener como valor el tipo más restrictivo posible que sea compatible con los valores esperados.
- `sensitive` debe usarse solo cuando la variable contiene información sensible.
- `default` debe usarse solo en la creación de modulo, y cuando se solicite un valor por defecto o predeterminado.
- `description` debe contener una explicación clara y concisa del propósito de la variable.
- `validation` debe usarse para establecer los criterios para los valores de entrada cuando tenga sentido.
- Si una variable se queda huérfana, debe eliminarse.

## outputs.tf

Este fichero gestiona las salidas de Terraform. Unicamente contendrá bloques `output`. Solo se generan salidas por solicitud explícita. Los bloques deben seguir:

- Orden alfabéticamente por el nombre de la salida.
- Definir solo las salidas necesarias para exponer información relevante.
- Los valores de las salidas deben ser expresiones claras y concisas.
- `sensitive` debe usarse solo cuando la salida contiene información sensible.
- Si una salida se queda huérfana, debe eliminarse.