# Proveedor de AzureRM

# Configuración del proveedor


Para configurar el proveedor de AzureRM en Terraform, se utiliza el bloque `provider` de la siguiente manera:

```hcl
provider "azurerm" {
  features {}
}
```

## Patrones de los recursos

Los recursos generados del proveedor de AzureRM deben seguir:

- Los primeros atributos y siguiendo este orden deben ser: `name`, `resource_group_name`, `location`, `tags`. Si algún atributo no esta soportado, se omite.
- Si existe algún `resource` o `data` de `azurerm_resource_group`, los recursos generados deben heredar los valores de `resource_group_name`, `location` y `tags`. En caso de que haya más de uno, debe ser consultado con el usuario, dándole la opción de elegir si uno para todos en esta petición, o seleccionar individualmente. No asumir como contexto la selección, cada nueva solicitud, nueva consulta.

## Configuraciones por defecto

La generar ciertos recursos, se deben seguir configuraciones por defecto:

- La máquinas virtuales deben usar credenciales de usuario y contraseña.
- Los recursos que lo soporte deben tener deshabilitado el acceso público.