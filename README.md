# docker studio 1 daw

## intro

[install](https://docs.docker.com/engine/install/ubuntu/) 

## sheets: https://dockerlabs.collabnix.com/docker/cheatsheet/

got here: https://dockerlabs.collabnix.com/docker/cheatsheet/

## clean:

`for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done`

? *docker.io*
? *docker-doc* 
? *docker-compose*  *docker-compose-v2* 
? *podman-docker* 
? *containerd runc*

## setup docker repo

```sh
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## latest

`sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

## use as no-sudoer [link](https://cloudyuga.guru/blogs/manage-docker-as-non-root-user/)

`sudo groupadd docker` 
`sudo usermod -aG docker ray`
`su - ray`

## usos 101

docker run hello-world # ... descarga
docker images
docker run hello-world # no descarga (ya en local)
docker run alpine # ... descarga
docker images 
docker ps  ## lista vacia ??
docker run alpine  ## el comando termina... ??
docker ps

## no bash?

Un ejemplo de instalacion en alpine [aqui](https://www.baeldung.com/linux/bash-alpine-docker-images)

`docker pull openjdk:8-jdk-alpine`
`docker run -it a3562aa0b991 /bin/bash`  # error: no bash in image
`docker run -it a3562aa0b991 /bin/sh`    # sh si esta ...
`/ # apk add --no-cache bash`

## limpio imagenes ..

docker prune # no es la api moderna
docker images
...
docker rmi -f d2 ...  # ok
docker rmi -f 05 ...  # ok

// no images

## instalo ubuntu (:latest) y la lanzo y hablo con su shell

`docker pull ubuntu`
`docker images`
`docker run xx` ...  # termina (sudo docker ps -> vacio)
`docker run -it fd /bin/bash` # -> prompt `root@ce4fa3c2b6c0:/#`
`docker run -it fd /bin/sh` # -> prompt `#`


## instalo contenedores mysql ...

aqui: https://hub.docker.com/_/mysql

lanzo `docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql`   (`:tag` no disponible)




```bash:
ray@daw1:~$ 
docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                 NAMES
0268fc4f2b0b   mysql     "docker-entrypoint.s…"   3 minutes ago    Up 3 minutes    3306/tcp, 33060/tcp   some-mysql
...
doker kill 02
ray@daw1:~$ 
docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                 NAMES
```

- Lanzo `docker run --name taustecontainer -it -e MYSQL_ROOT_PASSWORD=tauste -d mysql`
- Acceso al contenedor: `docker exec -it taustecontainer bash`
- Acceso al motor mysql dentro del contenedor: `mysql -u root -p`  ( pass: tauste )

mysql> 

## instancio una bd en el contenedor :

ver tb [howto](https://www.inmotionhosting.com/support/server/databases/create-a-mysql-database/) 

**mysql>** :

```sql:
show databases;
create database usuarios;
use usuarios;
create table usuarios(
  nombre varchar(20) NOT NULL,
  dni varchar(20) PRIMARY KEY
);
insert into usuarios (nombre, dni) values ("diego",1122);
insert into usuarios (nombre, dni) values ("marta",2233);
```
exit.. exit ...

```bash:
docker stop taustecontainer
docker start taustecontainer  
...
```

**y tiene persistencia ! (los datos estan)**

## limpio contenedores

`docker container prune`
