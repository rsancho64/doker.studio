[install](https://docs.docker.com/engine/install/ubuntu/) 

## sheets: https://dockerlabs.collabnix.com/docker/cheatsheet/

got here: https://dockerlabs.collabnix.com/docker/cheatsheet/

## clean:

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

*docker.io*
*docker-doc* 
*docker-compose* 
*docker-compose-v2* 
*podman-docker* 
*containerd runc*

## setup docker repo

```bash
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

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## use as no-sudoer [link](https://cloudyuga.guru/blogs/manage-docker-as-non-root-user/)

## uses 101

sudo docker run hello-world # ... descarga
sudo docker images
sudo docker run hello-world # no descarga (ya en local)
sudo docker run alpine # ... descarga
sudo docker images 
sudo docker ps  ## lista vacia ??
sudo docker run alpine  ## el comando termina... ??
sudo docker ps

## no bash?

Un ejemplo de instalacion en alpine [aqui](https://www.baeldung.com/linux/bash-alpine-docker-images)

`docker pull openjdk:8-jdk-alpine`
`docker run -it a3562aa0b991 /bin/bash`  # error: no bash in image
`docker run -it a3562aa0b991 /bin/sh`    # sh si esta ...
`/ # apk add --no-cache bash`

## limpio todas las imagenes

sudo docker prune # no es la api moderna
sudo docker images
...
sudo docker rmi -f d2 ...  # ok
sudo docker rmi -f 05 ...  # ok

// no images

## instalo ubuntu (:latest) y la lanzo y hablo con su shell

`sudo docker pull ubuntu`
`sudo docker images`
`sudo docker run xx` ...  # termina (sudo docker ps -> vacio)
`sudo docker run -it fd /bin/bash` # -> prompt `root@ce4fa3c2b6c0:/#`
`sudo docker run -it fd /bin/sh` # -> prompt `#`
