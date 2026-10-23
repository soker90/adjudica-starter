# Adjudica Starter

Plantilla para crear una instancia de Adjudica. Este repositorio guarda la identidad visual, configuración de organismos y datos propios de la instancia. El código de la aplicación se incorpora como submódulo desde [`soker90/adjudica`](https://github.com/soker90/adjudica).

## Crear una instancia

1. Usa **Use this template** en GitHub para crear el repositorio de la nueva instancia.
2. Edita `site.config.json` con el nombre, descripción, URL, ámbito geográfico, colores y datos de localización del portal.
3. Sustituye `public/logo.svg` por el logotipo de la instancia.
4. Añade un objeto por organismo a `data/contracting-authorities.json`. Usa `data/contracting-authorities.example.json` como referencia.
5. Añade la base SQLite de la instancia en `data/contracts.db`.
6. Añade el secreto `DNI_SALT` en **Settings → Secrets and variables → Actions** del repositorio nuevo. Lo necesitan los flujos que anonimizan identificadores personales.
7. Inicializa el submódulo y configura el proyecto de despliegue para compilar desde la raíz de la instancia:

   ```sh
   git submodule update --init --recursive
   ```

En el proyecto de Vercel, conecta el repositorio nuevo y conserva la raíz del proyecto en `.`. El comando de compilación prepara el submódulo con `site.config.json`, `public/logo.svg` y `data/contracts.db` de esta instancia.

La instancia conserva aquí sus datos y configuración. Los cambios de funcionalidad se realizan en el repositorio `adjudica`.
