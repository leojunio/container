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

## Instalar o mongodb atribuindo usuário e senha
```shell
docker run --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=balta -e MONGO_INITDB_ROOT_PASSWORD=e296cd9f mongo
```
  *Fonte:* https://balta.io/artigos/mongodb-docker
  
