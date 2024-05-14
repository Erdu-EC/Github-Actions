# Github-Actions
Este repositorio contiene acciones de GitHub y flujos de trabajo para la compilación y despliegue de proyectos .NET Core.

## Acciones

### Checkout y compilación de un proyecto .NET Core

Esta acción realiza el checkout y la compilación de un proyecto .NET, con almacenamiento en caché de las dependencias. 

Puedes encontrar más detalles en [net-core-build](.github/actions/net-core-build/README.md).

### Custom Commit and push changes
Esta acción realiza un commit y opcionalmente un push de los cambios realizados en el repositorio, con un mensaje generado automáticamente o un mensaje personalizado.

Puedes encontrar más detalles en [commit-message](.github/actions/commit-message/README.md).

## Flujos de trabajo

### Compilación de .NET Core y push a la rama de historial

Este flujo de trabajo se encarga de realizar la compilación de un proyecto .NET y empujar los cambios a una rama de historial.

Puedes encontrar más detalles en [net-build-and-push](.github/workflows/README.md).

## Uso

Para utilizar estas acciones y flujos de trabajo en tu propio proyecto, puedes referenciarlos en tu archivo de flujo de trabajo de GitHub Actions. Asegúrate de proporcionar los valores correctos para las entradas requeridas.

## Licencia

El contenido de este repositorio está protegido bajo la licencia [MIT](https://opensource.org/licenses/MIT).