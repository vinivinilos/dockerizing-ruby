# dockerizing-ruby
A Ruby docker image

Creamos el dockerfile con la etiqueta que hemos sacado de [https://hub.docker.com/_/ruby](https://hub.docker.com/_/ruby)
Vamos a utilizar una version con Alpine puesto que es un linux que ocupa muy poco.
Se pone el tag que nos diga la web.
En el Dockerfile:
FROM imagen ruby con alpine
ARG variables que se generan a la hora de construir la imagen. User y group concidiran con host y docker container.
RUN ejecuta comandos dentro del contenedor. En nuestro archivo creamos un usuario y un grupo y luego se isntalan las gemas de Rails.
```
    --gid ID
              Cuando se crea un grupo, esta opción fuerza el nuevo GID al número dado. Cuando  se
              crea un usuario la opción añade el usuario a ese grupo.
    --gecos GECOS
              Especifica  el  nuevo  campo  gecos para la entrada generada. adduser no solicitará
              esta información si se proporciona esta opción.
    The --disabled-password option will  not  set  a  password,  but  login  is  still possible  
    (for  example with SSH RSA keys).
```
ENV Define variables de entorno.
WORKDIR cambia el directorio de trabajo dentro del contenedor
USER Cambia el usuario activo al del argumento que hemos pasado antes
CMD Define que programa se ejecutara al iniciar el contenedor.

# Crear la imagen

```
    docker build -t rails-toolbox \
       --build-arg USER_ID=$(id -u)  \
       --build-arg GROUP_ID=$(id -g) \
       -f Dockerfile .
```
# Crear un proyecto
```
    $ docker run -it \
    -v $PWD:/opt/app \
    rails-toolbox rails new --skip-bundle drkiq
```