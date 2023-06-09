# Base de datos distribuida
Para simular que nuestra base de datos es distribuida,
hacemos uso de wsl sobre windows, sin embargo este procedimiento se puede
realizar tanto en contenedores de docker o bien en distintas computadoras, el unico
requisito es que estas tengan la misma version de postgres.

En ambas instancias de wsl usamos ubuntu.

## Configurando las computadoras
Para instalar la version más actual de postgres sql ejecutamos los comandos siguientes

 ``` shell
 su cluster

 sudo apt install wget ca-certificates
 wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

sudo apt update

 sudo apt install postgresql postgresql-contrib
 ```
Esto actualiza los repositorios y nos asegura que en ambas computadoras tendremos la ultima version de
 postgresql.

Se detiene el cluster creado por defecto
su postgres
``` shell
 sudo /etc/init.d/postgresql stop
```

creamos el directorio /var/run/postgresql y le damos permisos al usuario.


```shell
mkdir /var/run/postgresql
sudo chmod 777 /var/run/postgresql
```
Creamos los clusters, tanto el cluster como el standby.
 ```shell
 cd /usr/lib/postgresql/15/bin
 ./initdb -D ~/{nombre del cluster}/data
 ```
Una vez realizado esto, procedemos a configurar las instancias por separado.

## Configurando el cluster de postgresql

Modificamos el archivo [postgres.conf](cluster.postgres.conf)

# TODO: Explicacion de la configuracion--

posteriormente iniciamos el servidor
````shell
cd /usr/lib/postgresql/15/bin
./pg_ctl start -D ~/cluster/data
````
y creamos el usuario con el que se conectara el servidor standby
````shell
psql postgres -p 5555

create user repuser with login replication password 'contraseña secreta';
````
Y listo, por parte del cluster hemos acabado.

## Configurando el servidor standby
Nos dirigimos a ~/standby/data y borramos todo su contenido.
```shel
cd ~/standby/data && rm -rf *
```
en esta misma direccion ejecutamos 
```shell
pg_basebackup -Xs -d 'hostaddr=127.0.0.1 port=5555
 user=repuser password=contraseña secreta` -D . -v -Fp
 ```
Este comando nos sire para crear una copia de seguridad y almacenarla en el lugar proporcionado
por el parametro `-D` en este caso lo almacenamos en le directorio que nos encontramos

posteriormente modificamos el archivo [postgres.conf](standby.postgres.conf)

# TODO: explicar la configuracion del postgres.conf