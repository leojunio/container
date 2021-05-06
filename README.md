# Instalação do Docker Container - CentOS
```shell
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo systemctl enable docker 
sudo systemctl start docker
sudo usermod -aG docker $USER
```
# Instalação do Docker Container - Ubuntu

- [Instalação do Docker no Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

# Instalação do Docker Compose no Ubuntu

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
- [Instalaçao do Docker Compose no Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04-pt)

# Comandos úteis para gerenciamento de container

## Executar um container novo e dar um nome para a imagem
```shell
docker container run --name <novo nome do container> <nome atual do container>
```

## Visualizar os containers atuais
```shell
docker ps -a
```
```shell
docker ls -a
```

## Iniciar o container
```shell
docker container start -ai <nome do container>
docker container run -h <nome do container>
```

## Parar o container
```shell
docker container stop <nome do container>
```

# Reiniciar o container
```shell
docker container restart <nome do container>
```

## Mapear portas do container
```shell
docker container run -p <porta destino>:<porta origem> <nome da imagem>
```

## Mapear diretórios no container
  1. criar uma pasta ou arquivo local
  2. criar um container com os seguintes passos, mapeando a porta e volume
  
```shell
docker container run -p <porta destino>:<porta origem> -v $(pwd)/pasta local:/<caminho da pasta do container> <nome da imagem> 
```
  ### ex
```shell
	docker container run -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html nginx
```
### Rodar o container em modo deamon (background)
```shell
docker container run -d --name <nome do novo container> <nome da imagem do container>
```

## Acessar o log do container
```shell
docker container logs <nome do container>
```

## Inspecionar o container
```shell
docker container inspect <nome do container> 
```
  ### ex:
```shell
docker inspect <nome do container>
```
  ### com filtro
```shell
docker inspect <nome do container> | grep "IPAddress"
```
  ### com filtro do nome do host
```shell
docker container inspect <nome do container> | grep "Hostname"
```

## Executar um comando no container com modo interativo
```shell
docker container exec -it <nome do container> uname -or
```
```shell
docker container exec -it <nome do container> ifconfig
```

## Remover um container, forçando a deleção
```shell
docker container rm <nome do container> -f
```

## Remover a imagem do container
```shell
docker image rm <nome da imagem>
```

## Verificar as redes
```shell
docker network ls
```

## Iniciar um container informando o tipo de rede
```shell
docker container run --net none <nome do container>
```

## Verificar no Ubuntu a rede do docker
```shell
sudo ip addr show docker0
```

## Criar uma nova rede
```shell
docker network create --driver <nome do driver> <nome da nova rede>
```
  ### ex:
```shell
docker network create --driver bridge rede_nova
```

## Executar um container atribuindo uma nova rede com o modo deamon
```shell
docker container run -d --name <nome do container> --net <nome da rede> <imagem base>
```

## Remover uma rede do container
```shell
docker network disconnect <nome da rede> <nome do container>
```

## Copiar arquivos de dentro do container para uma pasta local
```
docker cp <nome do container>:<caminho da pasta do container> <pasta local>
```
### ex:
```
docker cp yb-tserver-n1:/mnt/tserver/yb-data/tserver/logs ./logs_yugabyte
```

## Escalar uma aplicação em containers
```shell
docker compose up -d --scale worked=<quantidade>
```
### ex: 
```
docker compose up -d --scale worked=4
```

## Instalar o mongodb atribuindo usuário e senha
```shell
docker run --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=balta -e MONGO_INITDB_ROOT_PASSWORD=e296cd9f mongo
``` 
- [Post de Instalação Mongodb](https://balta.io/artigos/mongodb-docker)

## Instalar um cluster Yugabyte local e com persistência dos dados
```shell
docker run -d --name yugabyte  -p7000:7000 -p9000:9000 -p5433:5433 -p9042:9042\
 -v ~/yb_data:/home/yugabyte/var\
 yugabytedb/yugabyte:latest bin/yugabyted start\
 --daemon=false 
 ```
 - [Instalação do Yugabyte no Docker](https://docs.yugabyte.com/latest/quick-start/create-local-cluster/docker/)

## Instalar o Nifi
```shell
docker run --name nifi -p 8091:8080 -i -v ~/document/Nifi/shared-directory:/opt/nifi/nifi-current/ls-target apache/nifi
``` 
```shell
docker run --name nifi-registry -p 18080:18080 apache/nifi-registry
```
- [Instalação do NIFI](https://medium.com/analytics-vidhya/setting-apache-nifi-on-docker-containers-a00e862a8399)
