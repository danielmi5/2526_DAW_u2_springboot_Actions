# Documentación del despliegue

Enlace al repositorio en Docker Hub: [repositorio](https://hub.docker.com/repository/docker/dmon5/despliegueactions/general)

## Construcción y publicación de la imagen en Docker Hub

https://github.com/danielmi5/2526_DAW_u2_springboot_Actions/blob/14684b150e0b707d56e39fb85770e1e36a39a951/.github/workflows/cd.yml#L1-L16

- **name:** Nombre del actions.
- **on:** El action se ejecuta cuando se hace push a la rama master o se hace manualmente desde `Actions`. 
- **jobs:** Subir la imagen a docker hub, se ejecuta en Ubuntu 22.04, y tiene permisos de escritura (packages, attestations e id-token) y lectura (contents).

https://github.com/danielmi5/2526_DAW_u2_springboot_Actions/blob/14684b150e0b707d56e39fb85770e1e36a39a951/.github/workflows/cd.yml#L17C5-L43

- **steps del job:**
      1. Obtiene el repositorio.  
      2. Inicia sesión en Docker Hub a partir del action `docker/login-action` y se utiliza con el with para el usuario y contraseña los secretos de github.  
      3. Extrae los tags y labels para Docker a partir del action `docker/metadata-action` y se define con with el nombre de estos y el de la imagen.  
      4. Construir y subir la imagen, mediante el action `docker/build-push-action` `y se define con el with el contexto de la imagen (raíz del repositorio), la ruta del archivo Dockerfile, push cuando se cree la imagen correctamente y la metadata definida en el anterior paso.  

    
## Estado Final

La imagen se crea y se publica en Docker Hub. Pero a la hora de hacer el despliegue, no funciona la conexión.
