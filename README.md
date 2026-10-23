# Adjudica Starter

Plantilla para crear una instancia de Adjudica. Este repositorio guarda la identidad visual, configuración de organismos y datos propios de la instancia. El código de la aplicación se incorpora como submódulo desde [`soker90/adjudica`](https://github.com/soker90/adjudica).

## Crear una instancia

1. Usa **Use this template** en GitHub para crear el repositorio de la nueva instancia.
2. Edita `site.config.json` con el nombre, descripción, URL, ámbito geográfico, colores y datos de localización del portal.
3. Sustituye `public/logo.svg` por el logotipo de la instancia.
4. Añade un objeto por organismo a `data/contracting-authorities.json`. Usa `data/contracting-authorities.example.json` como referencia.
5. Inicializa el submódulo e instala dependencias para desarrollo local:

   ```sh
   git submodule update --init --recursive
   cd adjudica
   pnpm install
   ADJUDICA_INSTANCE_ROOT=.. ADJUDICA_INSTANCE_DB_PATH=../data/contracts.db pnpm prepare:instance
   pnpm dev
   ```

   El repositorio ya incluye `data/contracts.db` con el esquema vacío; no hace falta crear la base manualmente.

6. Configura `DNI_SALT` como secreto de Actions del repositorio nuevo y como variable de entorno de producción en su proyecto de Vercel. La aplicación y los flujos lo usan para seudonimizar identificadores personales; ambos entornos deben compartir el mismo valor estable.
7. En Vercel, conecta el repositorio nuevo y conserva la raíz del proyecto en `.`. El comando de compilación prepara el submódulo con `site.config.json`, `public/logo.svg` y `data/contracts.db` de esta instancia.

Cuando la configuración esté en el repositorio, ejecuta manualmente el flujo `update-contracts` para cargar los primeros contratos. Después, las actualizaciones programadas guardarán los cambios SQLite aquí.

La instancia conserva aquí sus datos y configuración. Los cambios de funcionalidad se realizan en el repositorio `adjudica`.
