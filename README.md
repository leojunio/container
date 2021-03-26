# Comandos úteis para gerenciamento de container

## Executar um container novo e dar um nome para a imagem
	  docker container run --name <novo nome do container> <nome atual do container>

## Visualizar os containers atuais
	  docker ps -a
	  docker ls -a

## Iniciar o container
	  docker container start -ai <nome do container>
	  docker container run -h <nome do container>

## Parar o container
	  docker container stop <nome do container>

# Reiniciar o container
	  docker container restart <nome do container>

## Mapear portas do container
	  docker container run -p <porta destino>:<porta origem> <nome da imagem>

## Mapear diretórios no container
  1. criar uma pasta ou arquivo local
  2. criar um container com os seguintes passos, mapeando a porta e volume
  
  		docker container run -p <porta destino>:<porta origem> -v $(pwd)/pasta local:/<caminho da pasta do container> <nome da imagem> 
	
  ### ex

	docker container run -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html nginx

  ### Rodar o container em modo deamon (background)
    docker container run -d --name <nome do novo container> <nome da imagem do container>

## Acessar o log do container
    docker container logs <nome do container>

## Inspecionar o container
	docker container inspect <nome do container> 
  ### ex:
    	docker inspect <nome do container>

  ### com filtro
  	docker inspect <nome do container> | grep "IPAddress"

  ### com filtro do nome do host
  	docker container inspect <nome do container> | grep "Hostname"

## Executar um comando no container com modo interativo
  	docker container exec -it <nome do container> uname -or
  	docker container exec -it <nome do container> ifconfig

## Remover um container, forçando a deleção
	docker container rm <nome do container> -f

## Remover a imagem do container
	docker image rm <nome da imagem>

## Verificar as redes
	docker network ls

## Iniciar um container informando o tipo de rede
	  docker container run --net none <nome do container>

## Verificar no Ubuntu a rede do docker
	  sudo ip addr show docker0

## Criar uma nova rede
	  docker network create --driver <nome do driver> <nome da nova rede>
  ### ex:
	docker network create --driver bridge rede_nova

## Executar um container atribuindo uma nova rede com o modo deamon
	  docker container run -d --name <nome do container> --net <nome da rede> <imagem base>

## Remover uma rede do container
	  docker network disconnect <nome da rede> <nome do container>

## Instalar o mongodb atribuindo usuário e senha
	  docker run --name mongodb -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=balta -e MONGO_INITDB_ROOT_PASSWORD=e296cd9f mongo
  
  
