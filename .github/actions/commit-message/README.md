# GitHub Composite Action: Custom commit and push

Esta acción de GitHub se encarga de realizar un commit y opcionalmente un push de los cambios realizados en el
repositorio.

El commit se realiza con un mensaje personalizado, que se puede configurar en la entrada `commit_message`.

Si no se especifica un mensaje de commit, se utilizará un mensaje generado automáticamente con información sobre el
commit, el repositorio y la rama donde se hizo.

## Entradas

### `commit_message`

**Opcional** | Valor por defecto: `''` | Mensaje del commit, si no se especifica se generará uno automáticamente.

### `push`

**Opcional** | Valor por defecto: `''` | Indica si se deben empujar los cambios al repositorio, acepta los
valores `true` o `false`.

### `cd`

**Opcional** | Valor por defecto: `.` | Ruta para cambiar el directorio de trabajo antes de realizar el commit.

## Uso

Puedes utilizar esta acción en tu flujo de trabajo de GitHub Actions de la siguiente manera:

```yaml
    - uses: ./.github/actions/commit-message
      with:
        commit_message: 'Custom commit message'
        push: true
        cd: 'path/to/working/directory' # Or '.' for the root directory
```

Para que esta acción funcione correctamente debe existir en el workflow un paso que la preceda y que realice el checkout
del repositorio en donde esté contenida esta acción, que no necesariamente debe ser el mismo al de tu proyecto .net.

Por ejemplo:

```yaml
- name: Prepare local github actions
  uses: actions/checkout@v4
  with:
    repository: Erdu-EC/Github-Actions
    ref: v1.3 # Or the version you want to use (check the releases)
    sparse-checkout: .github/actions/commit-message/action.yml
    sparse-checkout-cone-mode: false
```

## Ejemplo de uso

```yaml
name: Commit and push changes
on: [ push ]

jobs:
  build:
    name: Build project
    runs-on: ubuntu-latest

    steps:
      - name: Prepare local github actions
        uses: actions/checkout@v4
        with:
          repository: Erdu-EC/Github-Actions
          ref: v1.3 # Or the version you want to use (check the releases)
          sparse-checkout: .github/actions/commit-message/action.yml
          sparse-checkout-cone-mode: false

      - uses: ./.github/actions/commit-message
        with:
          commit_message: 'Custom commit message'
          push: true
          cd: 'path/to/working/directory' # Or '.' for the root directory

```

## Caso de uso (El mio):

Esta acción puede ser util para realizar un commit y push de los cambios realizados en el repositorio.

Por ejemplo, después de realizar una compilación exitosa de un proyecto .NET Core, se puede utilizar esta acción para realizar un
commit y push de los cambios realizados en el repositorio, o incluso en otro repositorio.

En mi caso, envió los binarios de la compilación a un repositorio de "deployments", ya que en el entorno que utilizo para
producción solo se puede realizar la integración continúa obteniendo los binarios de un repositorio.

## Licencia

Este contenido está protegido bajo la licencia [MIT](https://opensource.org/licenses/MIT)