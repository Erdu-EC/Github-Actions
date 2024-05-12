# GitHub Workflow Action: .Net Build and push to history branch

Esta acción de GitHub se encarga de realizar la compilación de un proyecto .NET y empujar los cambios a una rama de historial.

## Secretos
### `PUBLISH_TOKEN`
**Requerido** | Token de GitHub con permisos de escritura en el repositorio de destino.

## Entradas
### `target_repository`

**Requerido** | Repositorio al que se va a desplegar (por ejemplo, owner/repo).

### `target_branch`

**Requerido** | Rama a la que se va a desplegar.

### `project_folder`

**Requerido** | Carpeta del proyecto a compilar.

### `project_structure`

**Requerido** | Estructura del proyecto para realizar el checkout solo de los proyectos necesarios.

### `push`
**Opcional** | Valor por defecto: `true` | Indica si se deben empujar los cambios a la rama de historial.

## Uso

Puedes utilizar esta acción en tu flujo de trabajo de GitHub Actions de la siguiente manera:

```yaml
- uses: Erdu-EC/Github-Actions/.github/workflows/net-build-and-push.yml@v1
  secrets:
    PUBLISH_TOKEN: ${{ secrets.GITHUB_TOKEN }} # Or any other token with write access to the target repository
  with:
    target_repository: 'owner/repo'
    target_branch: 'branch-to-deploy'
    project_folder: 'src/ProyectoRaiz'
    project_structure: |
        - src/Proyecto1
        - src/Proyecto2
```

## Nota
Los proyectos .NET Core deben tener la siguiente configuración en su archivo `.csproj` dentro de la etiqueta `PropertyGroup` para que la acción funcione correctamente:

```xml
<RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
```

## Licencia
El contenido de este repositorio está protegido bajo la licencia [MIT](https://opensource.org/licenses/MIT)