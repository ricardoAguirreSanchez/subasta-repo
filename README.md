# Subasta Ping Pong

## Seguridad: Firebase API key

Este proyecto hace uso de **GitHub Secrets** y **GitHub Actions** para no persistir la API key de Firebase en el repositorio.

- Se utiliza un placeholder (`__FIREBASE_CONFIG_PLACEHOLDER__`) en `index.html` en lugar de la configuración real.
- El secret `FIREBASE_CONFIG` de GitHub contiene el objeto de configuración de Firebase (incluyendo apiKey, databaseURL, etc.) como JSON.
- El workflow `.github/workflows/deploy-pages.yml` reemplaza el placeholder por el valor del secret durante el deploy a GitHub Pages.

De esta forma, la API key nunca queda almacenada en el código del repo.

### Configuración del secret FIREBASE_CONFIG

Para que el deploy funcione, necesitás crear el secret en GitHub:

1. **Crear el secret**
   - Repo → Settings → Secrets and variables → Actions
   - New repository secret
   - Nombre: `FIREBASE_CONFIG`
   - Valor: el objeto de config de Firebase como JSON (una sola línea)

2. **Cambiar la fuente de Pages**
   - Repo → Settings → Pages
   - En "Build and deployment", cambiar Source de "Deploy from a branch" a **GitHub Actions**

3. Hacer push y el workflow hará el deploy automáticamente.
