# opencode-config
Configuración de IA generalista para Opencode

## Skills

- **git-conventional-commits**: guía para proponer, revisar y crear mensajes de
  commit según Conventional Commits 1.0.0, incluidos cambios incompatibles.

## Servidores MCP

La configuración utiliza el formato de OpenCode v2 e incluye los servidores
oficiales de Azure, Microsoft Learn, Azure DevOps, GitHub, Git local, Terraform
y AWS.

- **Azure**: instala Node.js y npm para disponer de `npx`. La autenticación está
  fijada a Azure CLI (`AzureCliCredential`): ejecuta `az login` antes de iniciar
  OpenCode. El servidor MCP se inicia con `--read-only`, que deshabilita las
  operaciones de escritura.
  Puedes establecer el tenant y la suscripción predeterminados en el entorno
  que inicia OpenCode:

  ```sh
  export AZURE_MCP_TENANT_ID="mi-tenant-id"
  export AZURE_MCP_SUBSCRIPTION_ID="mi-suscripcion-id"
  ```

  OpenCode los pasa al servidor como `AZURE_TENANT_ID` y
  `AZURE_SUBSCRIPTION_ID`. La suscripción se usa como predeterminada si una
  operación no especifica otra. Inicia sesión en el tenant deseado con
  `az login --tenant "$AZURE_MCP_TENANT_ID"` y selecciona la suscripción con
  `az account set --subscription "$AZURE_MCP_SUBSCRIPTION_ID"`.
  Consulta la [referencia de herramientas de Azure MCP](https://learn.microsoft.com/en-us/azure/developer/azure-mcp-server/tools/).
- **Microsoft Learn**: no requiere credenciales.
- **Azure DevOps**: usa el servidor local para repositorios y para consultar
  pipelines y boards. Instala Node.js 20 o posterior, npm y Azure CLI;
  inicia sesión con `az login` antes de iniciar OpenCode. El servidor usa la
  sesión de Azure CLI, sin registrar un cliente OAuth. Consulta la
  [guía de Microsoft](https://github.com/microsoft/azure-devops-mcp/blob/main/docs/GETTINGSTARTED.md).

  Define la organización y, opcionalmente, el proyecto y el equipo por defecto
  en el entorno que inicia OpenCode:

  ```sh
  export AZURE_DEVOPS_MCP_ORG="mi-organizacion"
  export AZURE_DEVOPS_MCP_PROJECT="mi-proyecto"
  export AZURE_DEVOPS_MCP_TEAM="mi-equipo"
  ```

  OpenCode pasa el proyecto y el equipo al servidor como `ado_mcp_project` y
  `ado_mcp_team`. Se usan como valores por defecto cuando corresponda.

  Las políticas de OpenCode permiten las herramientas de repositorios y una
  lista explícita de herramientas de lectura de pipelines y boards; bloquean las
  demás. La herramienta de backlog queda bloqueada porque también permite
  reordenar elementos. La versión del servidor está fijada para revisar sus
  herramientas antes de actualizarla.

  Estas políticas solo restringen las llamadas MCP en OpenCode, no los permisos
  del usuario ni otras vías como la terminal. Restringe también los permisos de
  pipelines y boards en Azure DevOps. Un archivo YAML de pipeline almacenado
  en un repositorio sigue pudiendo modificarse con permisos de repositorio.
- **GitHub**: `github` habilita los toolsets `repos` e `issues` en modo de solo
  lectura. `github-pr` habilita el toolset completo `pull_requests` para
  gestionar PR: crearlas, actualizarlas, revisarlas, comentarlas y fusionarlas.
  Autentica ambas conexiones con `opencode mcp auth github` y
  `opencode mcp auth github-pr`; las operaciones dependen de los permisos de tu
  cuenta de GitHub.
- **Terraform**: requiere el binario local `terraform-mcp-server` en el `PATH`.
  Se limita al toolset `registry` para consultar providers, módulos y políticas
  públicas, sin `TFE_TOKEN`. Puedes instalarlo con
  `go install github.com/hashicorp/terraform-mcp-server/cmd/terraform-mcp-server@latest`
  o seguir las [instrucciones oficiales](https://developer.hashicorp.com/terraform/mcp-server/deploy/local).

Define las variables en el entorno que inicia OpenCode, sin añadir credenciales
al repositorio. Comprueba el estado con `opencode mcp list` o con `/mcps`
dentro de OpenCode. Algunos servidores permiten modificar recursos: revisa sus
permisos y las operaciones propuestas antes de ejecutarlas.
