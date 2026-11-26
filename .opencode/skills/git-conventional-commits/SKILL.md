---
name: git-conventional-commits
description: Usar siempre que se quiera generar uno o varios commits de Git.
---

Los commits siempre deben generarse en ingles.

# Tipos de commits

- feat: Añadir una nueva funcionalidad, ya sea un recurso de terraform, una nueva función de código, actualización de sku, tier o característica similares.
- fix: Corregir, modificar, actualizar una implementación que generar errores o comportamientos no deseados.
- docs: Añadir o modificar archivos de documentación.
- style: Cambios de formato o estilo de código, sin afectar la funcionalidad.
- refactor: Refactorización de código sin cambios funcionales, como reorganización de funciones o renombrado de variables.
- test: Añadir o modificar pruebas, incluyendo unitarias, de integración o de extremo a extremo.
- chore: Tareas de mantenimiento o configuración, como actualizaciones de dependencias o cambios en scripts de construcción. Borrado de archivos o limpieza de código.

## Orden de prioridad

Si al generar uno o varios commits, la cabecera de los mismos incluye diferentes tipos, se debe seguir el siguiente orden de prioridad como cabecera del commit:

1. feat
2. fix
3. test
4. docs
5. style
6. refactor
7. chore

# Ámbito de los commits

Los commits deberán incluir siempre el ámbito al que afecta la modificación. Ejemplos:

- feat(terraform): Añadir un nuevo recurso de terraform.
- fix(python): Corregir un error en el código Python.
- docs(style): Modificar archivos de documentación relacionados con el estilo.
- style(ci): Cambios de formato o estilo en la configuración de integración continua.
- chore(deps): Actualizar dependencias del proyecto.

# Descripción del commit

La descripción del primer párrafo debe resumir en menos de diez palabras los cambios realizados.
El resto de la descripción puede detallar el contexto, la motivación y cualquier información relevante para entender el cambio.

# División de commits

Antes de generar commits, analiza el alcance y la naturaleza de todos los cambios. Agrúpalos en commits pequeños, coherentes y revisables. Decide los límites por la relación lógica entre los cambios, no por los archivos que modifican: un mismo archivo puede aparecer en varios commits si contiene cambios independientes.

- Mantén juntos los cambios que implementan, configuran, prueban o documentan una misma capacidad cuando separarlos deje una parte incompleta o menos comprensible. Por ejemplo, incluye la documentación de uso junto con la configuración que documenta cuando ambas forman un cambio coherente.
- Separa funcionalidades, correcciones, pruebas, documentación y tareas de mantenimiento que sean independientes, aunque afecten al mismo archivo.
- Un commit puede contener solo una parte de los cambios de un archivo. Revisa los cambios por secciones o fragmentos y asigna cada parte al commit que le corresponda; los cambios restantes del mismo archivo pueden ir en uno o varios commits posteriores.
- Al proponer o preparar commits parciales, especifica qué cambios del archivo pertenecen a cada commit. No incluyas accidentalmente cambios no relacionados ni des por hecho que todo el archivo debe entrar en un único commit.
- Identifica las dependencias entre cambios de cualquier tipo. Si el cambio A requiere el cambio B y B tiene sentido por sí solo, ordena primero el commit de B y después el de A. Explica la relación en el cuerpo del commit de A cuando ayude a entenderlo.
- Si dos cambios dependen entre sí y no pueden separarse coherentemente, agrúpalos en un commit y explica por qué.

# Comportamiento

Cuando se solicita uno o varios commits, antes de proceder a generarlos, debe ser generada siempre una propuesta para ser aprobada por el usuario.