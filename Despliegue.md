# Documentación del despliegue

Enlace al repositorio en Docker Hub: [repositorio](https://hub.docker.com/repository/docker/dmon5/despliegueactions/general)

## Construcción y publicación de la imagen en Docker Hub

https://github.com/danielmi5/2526_DAW_u2_springboot_Actions/blob/14684b150e0b707d56e39fb85770e1e36a39a951/.github/workflows/cd.yml#L1-L16

- **name:** Nombre del actions.
- **on:** El action se ejecuta cuando se hace push a la rama master o se hace manualmente desde `Actions`. 
- **jobs:** Subir la imagen a docker hub, se ejecuta en Ubuntu 22.04, y tiene permisos de escritura (packages, attestations e id-token) y lectura (contents).

https://github.com/danielmi5/2526_DAW_u2_springboot_Actions/blob/14684b150e0b707d56e39fb85770e1e36a39a951/.github/workflows/cd.yml#L17-L43

- **steps del job:**  
      1. Obtiene el repositorio.  
      2. Inicia sesión en Docker Hub a partir del action `docker/login-action` y se utiliza con el with para el usuario y contraseña los secretos de github. Logs del login:
```
Run docker/login-action@f4ef78c080cd8ba55a85445d5b36e214a81df20a
Logging into Docker Hub...
Login Succeeded!
```
3. Extrae los tags y labels para Docker a partir del action `docker/metadata-action` y se define con with el nombre de estos y el de la imagen. Logs:
```
Run docker/metadata-action@9ec57ed1fcdbf14dcef7dfbe97b2010124a938b7
Context info
Processing images input
Processing tags input
Processing flavor input
Docker image version
Docker tags
Docker labels
JSON output
Bake file definition
```
4. Construir y subir la imagen, mediante el action `docker/build-push-action` `y se define con el with el contexto de la imagen (raíz del repositorio), la ruta del archivo Dockerfile, push cuando se cree la imagen correctamente y la metadata definida en el anterior paso. Logs:

```
Run docker/build-push-action@3b5e8027fcad23fda98b2e3ac259d8d67585f671
GitHub Actions runtime token access controls
Docker info
Buildx version
/usr/bin/docker buildx build --file ./Dockerfile --iidfile /tmp/docker-build-push-C9p5Nx/iidfile --label org.opencontainers.image.title=2526_DAW_u2_springboot_Actions --label org.opencontainers.image.description=Despliegue de una aplicación spring boot en docker con github Actions. --label org.opencontainers.image.url=https://github.com/***/2526_DAW_u2_springboot_Actions --label org.opencontainers.image.source=https://github.com/***/2526_DAW_u2_springboot_Actions --label org.opencontainers.image.version=latest --label org.opencontainers.image.created=2025-12-04T08:59:25.750Z --label org.opencontainers.image.revision=b85b3695c49a6a4ca62caf8051e2c395de283822 --label org.opencontainers.image.licenses= --tag ***/despliegueactions:latest --metadata-file /tmp/docker-build-push-C9p5Nx/metadata-file --push .
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 1.17kB done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/gradle:8.5-jdk17
#2 ...

#3 [auth] library/tomcat:pull token for registry-1.docker.io
#3 DONE 0.0s

#4 [auth] library/gradle:pull token for registry-1.docker.io
#4 DONE 0.0s

#5 [internal] load metadata for docker.io/library/tomcat:10.1-jdk17
#5 DONE 1.0s

#2 [internal] load metadata for docker.io/library/gradle:8.5-jdk17
#2 DONE 1.0s

#6 [internal] load .dockerignore
#6 transferring context: 362B done
#6 DONE 0.0s

#7 [internal] load build context
#7 transferring context: 77.45kB done
#7 DONE 0.0s

#8 [builder 1/6] FROM docker.io/library/gradle:8.5-jdk17@sha256:7704366590930c03de7e514008ba3d7b7031b92591bd5a74fae79c16f3a17726
#8 resolve docker.io/library/gradle:8.5-jdk17@sha256:7704366590930c03de7e514008ba3d7b7031b92591bd5a74fae79c16f3a17726 done
#8 sha256:7704366590930c03de7e514008ba3d7b7031b92591bd5a74fae79c16f3a17726 1.21kB / 1.21kB done
#8 sha256:f59836e46ad7a565813de06768ff2884700d12b7ceedacb1701a2983dc859010 2.21kB / 2.21kB done
#8 sha256:31bd5f451a847d651a0996256753a9b22a6ea8c65fefb010e77ea9c839fe2fac 0B / 30.45MB 0.1s
#8 sha256:26611c45681a8966387aee7b2e1494405e20bc5a46dc5da0af9228c45f8e8ec4 0B / 17.46MB 0.1s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 0B / 144.90MB 0.1s
#8 sha256:521f64de188a3ae1cdf32821464b44693cf9b19cbba5f652a72eb8898353eb88 10.44kB / 10.44kB done
#8 sha256:31bd5f451a847d651a0996256753a9b22a6ea8c65fefb010e77ea9c839fe2fac 6.29MB / 30.45MB 0.5s
#8 sha256:26611c45681a8966387aee7b2e1494405e20bc5a46dc5da0af9228c45f8e8ec4 4.19MB / 17.46MB 0.5s
#8 sha256:31bd5f451a847d651a0996256753a9b22a6ea8c65fefb010e77ea9c839fe2fac 13.63MB / 30.45MB 0.6s
#8 sha256:26611c45681a8966387aee7b2e1494405e20bc5a46dc5da0af9228c45f8e8ec4 7.87MB / 17.46MB 0.6s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 11.53MB / 144.90MB 0.6s
#8 sha256:31bd5f451a847d651a0996256753a9b22a6ea8c65fefb010e77ea9c839fe2fac 30.45MB / 30.45MB 0.8s done
#8 sha256:26611c45681a8966387aee7b2e1494405e20bc5a46dc5da0af9228c45f8e8ec4 15.73MB / 17.46MB 0.8s
#8 sha256:26611c45681a8966387aee7b2e1494405e20bc5a46dc5da0af9228c45f8e8ec4 17.46MB / 17.46MB 0.9s done
#8 extracting sha256:31bd5f451a847d651a0996256753a9b22a6ea8c65fefb010e77ea9c839fe2fac 0.1s
#8 sha256:a36c85a96a6da44b1c1559a390715fd929fae60db504c8b9c745897d737ca485 0B / 173B 0.9s
#8 sha256:30d3df2ee4d87245e77cfd06e96a597422956e0194064b0b71152e77d117ff54 0B / 733B 0.9s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 22.02MB / 144.90MB 1.0s
#8 sha256:a36c85a96a6da44b1c1559a390715fd929fae60db504c8b9c745897d737ca485 173B / 173B 1.0s done
#8 sha256:d07f8a99f32569a5ebfa8e9c3f4da0166c21ab862fab70f288cac5905e4d76f4 0B / 4.36kB 1.0s
#8 sha256:30d3df2ee4d87245e77cfd06e96a597422956e0194064b0b71152e77d117ff54 733B / 733B 1.1s done
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 0B / 51.55MB 1.1s
#8 sha256:d07f8a99f32569a5ebfa8e9c3f4da0166c21ab862fab70f288cac5905e4d76f4 4.36kB / 4.36kB 1.2s done
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 0B / 132.54MB 1.2s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 39.85MB / 144.90MB 1.4s
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 5.24MB / 51.55MB 1.4s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 54.53MB / 144.90MB 1.7s
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 15.73MB / 51.55MB 1.7s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 9.44MB / 132.54MB 1.7s
#8 extracting sha256:31bd5f451a847d651a0996256753a9b22a6ea8c65fefb010e77ea9c839fe2fac 1.0s done
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 23.07MB / 51.55MB 1.8s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 63.96MB / 144.90MB 1.9s
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 32.51MB / 51.55MB 1.9s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 18.87MB / 132.54MB 1.9s
#8 extracting sha256:26611c45681a8966387aee7b2e1494405e20bc5a46dc5da0af9228c45f8e8ec4 0.1s
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 36.70MB / 51.55MB 2.0s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 71.30MB / 144.90MB 2.1s
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 39.85MB / 51.55MB 2.1s
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 47.19MB / 51.55MB 2.2s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 26.21MB / 132.54MB 2.2s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 84.93MB / 144.90MB 2.3s
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 50.33MB / 51.55MB 2.3s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 95.42MB / 144.90MB 2.5s
#8 sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 51.55MB / 51.55MB 2.3s done
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 34.60MB / 132.54MB 2.5s
#8 sha256:f43bfc2819ff808463a651fd1b0d4343062dcbc80dffcd07fb360ca66f98626b 0B / 170B 2.5s
#8 sha256:f43bfc2819ff808463a651fd1b0d4343062dcbc80dffcd07fb360ca66f98626b 170B / 170B 2.5s done
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 115.34MB / 144.90MB 2.8s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 45.09MB / 132.54MB 2.8s
#8 extracting sha256:26611c45681a8966387aee7b2e1494405e20bc5a46dc5da0af9228c45f8e8ec4 1.0s done
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 130.02MB / 144.90MB 3.1s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 56.62MB / 132.54MB 3.1s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 138.41MB / 144.90MB 3.4s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 63.96MB / 132.54MB 3.4s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 77.59MB / 132.54MB 3.7s
#8 sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 144.90MB / 144.90MB 3.8s done
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 85.98MB / 132.54MB 3.9s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 93.32MB / 132.54MB 4.2s
#8 extracting sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 102.76MB / 132.54MB 4.5s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 113.25MB / 132.54MB 4.8s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 121.63MB / 132.54MB 5.0s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 132.54MB / 132.54MB 5.2s
#8 sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 132.54MB / 132.54MB 5.2s done
#8 extracting sha256:0a1f4ac6e69541680073b21e32dd3de17885de514e36838468fe84707c7b5acf 1.7s done
#8 extracting sha256:a36c85a96a6da44b1c1559a390715fd929fae60db504c8b9c745897d737ca485
#8 extracting sha256:a36c85a96a6da44b1c1559a390715fd929fae60db504c8b9c745897d737ca485 done
#8 extracting sha256:30d3df2ee4d87245e77cfd06e96a597422956e0194064b0b71152e77d117ff54 done
#8 extracting sha256:d07f8a99f32569a5ebfa8e9c3f4da0166c21ab862fab70f288cac5905e4d76f4 done
#8 extracting sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c
#8 ...

#9 [stage-1 1/4] FROM docker.io/library/tomcat:10.1-jdk17@sha256:d2cd0027e6b828ad8a5ff7693a20d972f16af0139f7fcecafa0797b31809863e
#9 resolve docker.io/library/tomcat:10.1-jdk17@sha256:d2cd0027e6b828ad8a5ff7693a20d972f16af0139f7fcecafa0797b31809863e done
#9 sha256:d2cd0027e6b828ad8a5ff7693a20d972f16af0139f7fcecafa0797b31809863e 7.97kB / 7.97kB done
#9 sha256:d7e557a209e888a501219479852f290c330a1621b70dfd293cda06f75601789b 13.03kB / 13.03kB done
#9 sha256:5555010508e0938564d9a2fc6d7c0c3386c896743c142c207014f9b4d1a05a5b 2.72kB / 2.72kB done
#9 sha256:20043066d3d5c78b45520c5707319835ac7d1f3d7f0dded0138ea0897d6a3188 29.72MB / 29.72MB 3.5s done
#9 extracting sha256:20043066d3d5c78b45520c5707319835ac7d1f3d7f0dded0138ea0897d6a3188 1.3s done
#9 sha256:077c4ca28173a06771936e7d2dd6254602c0fa1edee45debed984b4b382915de 22.96MB / 22.96MB 4.3s done
#9 sha256:b88b6ae1b108522b13f2cdc7912b1e5784e2a63268ea6d6d967b4e562b803b6f 144.85MB / 144.85MB 5.6s done
#9 sha256:67cf99ea3a756f77f1989a181feed90c517d46369d9430b6d37e86797f650a47 159B / 159B 4.5s done
#9 sha256:02d80376fd82870628b01ae6f01bd27552bc9aa3a4cd5be88515f79fe298a87a 2.28kB / 2.28kB 4.6s done
#9 sha256:ba09cd1b52686ac9e9dbb220adb4ab688596c111fa8403f9fb633cbfbdee0eee 139B / 139B 4.8s done
#9 sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1 32B / 32B 5.0s done
#9 sha256:6431d88ca8c2ceaed69970f6c943b1b6f48e0a66b8750f8654bd2bf0c977be68 14.34MB / 14.34MB 5.4s done
#9 extracting sha256:077c4ca28173a06771936e7d2dd6254602c0fa1edee45debed984b4b382915de 1.4s done
#9 extracting sha256:b88b6ae1b108522b13f2cdc7912b1e5784e2a63268ea6d6d967b4e562b803b6f 1.4s done
#9 extracting sha256:67cf99ea3a756f77f1989a181feed90c517d46369d9430b6d37e86797f650a47 done
#9 extracting sha256:02d80376fd82870628b01ae6f01bd27552bc9aa3a4cd5be88515f79fe298a87a done
#9 extracting sha256:ba09cd1b52686ac9e9dbb220adb4ab688596c111fa8403f9fb633cbfbdee0eee done
#9 extracting sha256:4f4fb700ef54461cfa02571ae0db9a0dc1e0cdb5577484a6d75e68dc38e8acc1 done
#9 extracting sha256:6431d88ca8c2ceaed69970f6c943b1b6f48e0a66b8750f8654bd2bf0c977be68 0.3s done
#9 DONE 9.5s

#8 [builder 1/6] FROM docker.io/library/gradle:8.5-jdk17@sha256:7704366590930c03de7e514008ba3d7b7031b92591bd5a74fae79c16f3a17726
#8 extracting sha256:aad08408064ed46f64df063070cbdca2e9c201ef791fca8b24f281c176dd595c 2.8s done
#8 ...

#10 [stage-1 2/4] RUN mkdir -p /app/data
#10 DONE 0.2s

#11 [stage-1 3/4] RUN rm -rf /usr/local/tomcat/webapps/*
#11 DONE 0.2s

#8 [builder 1/6] FROM docker.io/library/gradle:8.5-jdk17@sha256:7704366590930c03de7e514008ba3d7b7031b92591bd5a74fae79c16f3a17726
#8 extracting sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b
#8 extracting sha256:f5b1cf504e03486f25a93789e25d170596a30a0bcddc7396219539ae4d3a3e3b 0.7s done
#8 extracting sha256:f43bfc2819ff808463a651fd1b0d4343062dcbc80dffcd07fb360ca66f98626b
#8 extracting sha256:f43bfc2819ff808463a651fd1b0d4343062dcbc80dffcd07fb360ca66f98626b done
#8 DONE 10.5s

#12 [builder 2/6] WORKDIR /app
#12 DONE 0.0s

#13 [builder 3/6] COPY build.gradle settings.gradle gradlew ./
#13 DONE 0.0s

#14 [builder 4/6] COPY gradle ./gradle
#14 DONE 0.0s

#15 [builder 5/6] COPY src ./src
#15 DONE 0.0s

#16 [builder 6/6] RUN chmod +x gradlew && ./gradlew bootWar --no-daemon
#16 0.186 Downloading https://services.gradle.org/distributions/gradle-8.14.3-bin.zip
#16 0.850 .............10%.............20%.............30%.............40%.............50%.............60%.............70%.............80%.............90%..............100%
#16 3.136 
#16 3.136 Welcome to Gradle 8.14.3!
#16 3.136 
#16 3.136 Here are the highlights of this release:
#16 3.136  - Java 24 support
#16 3.137  - GraalVM Native Image toolchain selection
#16 3.137  - Enhancements to test reporting
#16 3.137  - Build Authoring improvements
#16 3.137 
#16 3.137 For more details see https://docs.gradle.org/8.14.3/release-notes.html
#16 3.137 
#16 3.236 To honour the JVM settings for this build a single-use Daemon process will be forked. For more on this, please refer to https://docs.gradle.org/8.14.3/userguide/gradle_daemon.html#sec:disabling_the_daemon in the Gradle documentation.
#16 4.335 Daemon will be stopped at the end of the build 
#16 25.24 > Task :compileJava
#16 25.24 > Task :processResources
#16 25.24 > Task :classes
#16 25.24 > Task :resolveMainClassName
#16 26.03 > Task :bootWar
#16 26.10 
#16 26.10 BUILD SUCCESSFUL in 25s
#16 26.10 4 actionable tasks: 4 executed
#16 DONE 26.3s

#17 [stage-1 4/4] COPY --from=builder /app/build/libs/*.war /usr/local/tomcat/webapps/ROOT.war
#17 DONE 0.0s

#18 exporting to image
#18 exporting layers
#18 exporting layers 0.4s done
#18 writing image sha256:259aef697dd01045e6e9b3f0f28b4df45c429da84b69f04880347c45c9ecb607 done
#18 naming to docker.io/***/despliegueactions:latest done
#18 DONE 0.4s

#19 resolving provenance for metadata file
#19 DONE 0.0s

#20 pushing ***/despliegueactions:latest with docker
#20 pushing layer 5d232dab336b
#20 pushing layer 5f70bf18a086
#20 pushing layer 88fd090a1900
#20 pushing layer 1cebd62ceefc
#20 pushing layer bb3ea38bfd9c
#20 pushing layer db1688142012
#20 pushing layer d03939930dac
#20 pushing layer 35c0b8fb11b1
#20 pushing layer d7ef4463791e
#20 pushing layer e8bce0aabd68
#20 pushing layer 5d232dab336b 1.61MB / 22.56MB 1.0s
#20 pushing layer 5d232dab336b 4.13MB / 22.56MB 1.2s
#20 pushing layer 5d232dab336b 8.03MB / 22.56MB 1.3s
#20 pushing layer 5d232dab336b 11.47MB / 22.56MB 1.4s
#20 pushing layer 5d232dab336b 15.37MB / 22.56MB 1.5s
#20 pushing layer 5d232dab336b 19.27MB / 22.56MB 1.6s
#20 pushing layer 5d232dab336b 22.25MB / 22.56MB 1.7s
#20 pushing layer 88fd090a1900 2.2s done
#20 pushing layer 5d232dab336b 3.5s done
#20 pushing layer d7ef4463791e 7.7s done
#20 pushing layer 5f70bf18a086 7.7s done
#20 pushing layer 1cebd62ceefc 7.7s done
#20 pushing layer bb3ea38bfd9c 7.7s done
#20 pushing layer db1688142012 7.7s done
#20 pushing layer d03939930dac 7.7s done
#20 pushing layer 35c0b8fb11b1 7.7s done
#20 pushing layer e8bce0aabd68 7.7s done
#20 DONE 7.9s
ImageID
Digest
Metadata
```

    
## Estado Final

La imagen se crea y se publica en Docker Hub correctamente. Pero al hacer el despliegue, pero no hay acceso al intentar acceder.
