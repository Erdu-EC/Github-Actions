# GitHub Composite Action: Obtener y compilar un proyecto .NET Core

Esta acción de GitHub se encarga de realizar el checkout y la compilación de un proyecto .NET Core, con almacenamiento en caché de las dependencias.

## Entradas
### `project_folder`

**Requerido** | Carpeta del proyecto a compilar.

### `project_structure`

**Requerido** | Estructura del proyecto para realizar el checkout solo de los proyectos necesarios.

### `checkout_to_path`

Ruta para realizar el checkout del proyecto, si se desea que se haga en un subdirectorio. No es obligatorio.

## Uso

Puedes utilizar esta acción en tu flujo de trabajo de GitHub Actions de la siguiente manera:

```yaml
- uses: ./.github/actions/net-core-build
  with:
    project_folder: 'src/ProyectoRaiz'
    project_structure: |
        - src/Proyecto1
        - src/Proyecto2
    checkout_to_path: 'ruta/para/checkout'
```

Para que esta acción funcione correctamente debe existir en el workflow un paso que la preceda y que realice el checkout del repositorio en donde esté contenida esta acción, que no necesariamente debe ser el mismo al de tu proyecto .net.

Por ejemplo:

```yaml
- name: Prepare local github actions
  uses: actions/checkout@v4
  with:
    repository: Erdu-EC/Github-Actions
    ref: main
    sparse-checkout: .github/actions/net-core-build/action.yml
    sparse-checkout-cone-mode: false
```

## Ejemplo de uso

```yaml
name: Build .NET Core project
on: [push]

jobs:
  build:
    name: Build project
    runs-on: ubuntu-latest
    
    steps:
      - name: Prepare local github actions
        uses: actions/checkout@v4
        with:
          repository: Erdu-EC/Github-Actions
          ref: main
          sparse-checkout: .github/actions/net-core-build/action.yml
          sparse-checkout-cone-mode: false
          
      - uses: ./.github/actions/net-core-build
        with:
          project_folder: 'src/ProyectoRaiz'
          project_structure: |
            - src/Proyecto1
            - src/Proyecto2
        checkout_to_path: 'ruta/para/checkout'
```

## Nota
Los proyectos .NET Core deben tener la siguiente configuración en su archivo `.csproj` dentro de la etiqueta `PropertyGroup` para que la acción funcione correctamente:

```xml
<RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
```

## Licencia
El contenido de este repositorio está protegido bajo la licencia [MIT](https://opensource.org/licenses/MIT)