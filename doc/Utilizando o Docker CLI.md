### Utilizando o Docker CLI

O Docker CLI (Command Line Interface) é a ferramenta principal para interagir com o Docker, permitindo que você crie, gerencie e monitore containers, imagens, volumes e redes. Este artigo fornece uma visão geral abrangente de como utilizar o Docker CLI para realizar várias tarefas essenciais.

#### Introdução ao Docker CLI

O Docker CLI é a interface de linha de comando do Docker. Com ela, você pode executar comandos para gerenciar todos os aspectos do Docker. A estrutura básica de um comando Docker é:

```sh
docker [comando] [opções]
```

#### Comandos Básicos do Docker CLI

##### 1. `docker run`

O comando `docker run` cria e inicia um novo container a partir de uma imagem Docker. Exemplo:

```sh
docker run -d --name meu-container nginx
```

Opções:
- `-d`: Executa o container em segundo plano (detached mode).
- `--name`: Dá um nome ao container.

##### 2. `docker ps`

O comando `docker ps` lista todos os containers em execução. Para listar todos os containers, incluindo os que estão parados, use `-a`:

```sh
docker ps -a
```

##### 3. `docker images`

O comando `docker images` lista todas as imagens Docker armazenadas localmente:

```sh
docker images
```

##### 4. `docker pull`

O comando `docker pull` baixa uma imagem do Docker Hub ou de outro repositório Docker:

```sh
docker pull nginx
```

##### 5. `docker push`

O comando `docker push` envia uma imagem para um repositório Docker, como o Docker Hub:

```sh
docker push meu-usuario/meu-repositorio:tag
```

##### 6. `docker build`

O comando `docker build` cria uma nova imagem Docker a partir de um Dockerfile:

```sh
docker build -t minha-imagem:tag .
```

##### 7. `docker stop`

O comando `docker stop` para um container em execução:

```sh
docker stop meu-container
```

##### 8. `docker rm`

O comando `docker rm` remove um container que está parado:

```sh
docker rm meu-container
```

##### 9. `docker rmi`

O comando `docker rmi` remove uma imagem Docker:

```sh
docker rmi minha-imagem:tag
```

##### 10. `docker exec`

O comando `docker exec` executa um comando em um container em execução:

```sh
docker exec -it meu-container /bin/bash
```

Opções:
- `-i`: Modo interativo.
- `-t`: Aloca um pseudo-terminal.

#### Gerenciamento de Volumes com Docker CLI

##### 1. `docker volume create`

O comando `docker volume create` cria um novo volume:

```sh
docker volume create meu-volume
```

##### 2. `docker volume ls`

O comando `docker volume ls` lista todos os volumes Docker:

```sh
docker volume ls
```

##### 3. `docker volume inspect`

O comando `docker volume inspect` exibe detalhes sobre um volume:

```sh
docker volume inspect meu-volume
```

##### 4. `docker volume rm`

O comando `docker volume rm` remove um volume:

```sh
docker volume rm meu-volume
```

#### Gerenciamento de Redes com Docker CLI

##### 1. `docker network create`

O comando `docker network create` cria uma nova rede Docker:

```sh
docker network create --driver bridge minha-rede
```

##### 2. `docker network ls`

O comando `docker network ls` lista todas as redes Docker:

```sh
docker network ls
```

##### 3. `docker network inspect`

O comando `docker network inspect` exibe detalhes sobre uma rede:

```sh
docker network inspect minha-rede
```

##### 4. `docker network connect`

O comando `docker network connect` conecta um container a uma rede:

```sh
docker network connect minha-rede meu-container
```

##### 5. `docker network disconnect`

O comando `docker network disconnect` desconecta um container de uma rede:

```sh
docker network disconnect minha-rede meu-container
```

##### 6. `docker network rm`

O comando `docker network rm` remove uma rede:

```sh
docker network rm minha-rede
```

#### Monitoramento e Logs com Docker CLI

##### 1. `docker logs`

O comando `docker logs` exibe os logs de um container:

```sh
docker logs meu-container
```

##### 2. `docker stats`

O comando `docker stats` exibe o uso de recursos de containers em tempo real:

```sh
docker stats
```

##### 3. `docker top`

O comando `docker top` exibe os processos em execução em um container:

```sh
docker top meu-container
```

##### 4. `docker inspect`

O comando `docker inspect` exibe informações detalhadas sobre um container ou uma imagem:

```sh
docker inspect meu-container
```

#### Comandos de Utilidade

##### 1. `docker login`

O comando `docker login` faz login em um repositório Docker, como o Docker Hub:

```sh
docker login
```

##### 2. `docker logout`

O comando `docker logout` faz logout de um repositório Docker:

```sh
docker logout
```

##### 3. `docker info`

O comando `docker info` exibe informações detalhadas sobre a instalação do Docker:

```sh
docker info
```

##### 4. `docker system prune`

O comando `docker system prune` remove todos os containers, imagens, volumes e redes não utilizados:

```sh
docker system prune
```

#### Exemplos Práticos

##### Exemplo 1: Criar e Iniciar um Container

1. Puxe a imagem `nginx` do Docker Hub:

```sh
docker pull nginx
```

2. Inicie um container a partir da imagem `nginx`:

```sh
docker run -d --name meu-nginx -p 80:80 nginx
```

##### Exemplo 2: Construir uma Imagem a partir de um Dockerfile

1. Crie um arquivo `Dockerfile` com o seguinte conteúdo:

```Dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y nginx
CMD ["nginx", "-g", "daemon off;"]
EXPOSE 80
```

2. Construa a imagem:

```sh
docker build -t minha-imagem-nginx:latest .
```

3. Inicie um container a partir da imagem criada:

```sh
docker run -d --name meu-nginx-personalizado -p 80:80 minha-imagem-nginx:latest
```

#### Conclusão

O Docker CLI é uma ferramenta poderosa que permite gerenciar todos os aspectos do Docker, desde a criação e gerenciamento de containers até a configuração de volumes e redes. Com a prática e o uso adequado dos comandos abordados neste artigo, você pode otimizar seu fluxo de trabalho de desenvolvimento e deployment, melhorando a eficiência e a portabilidade de suas aplicações.

---

Este artigo cobriu os principais comandos do Docker CLI, fornecendo uma base sólida para o uso eficaz dessa ferramenta essencial. Compreender e utilizar esses comandos permitirá a você gerenciar seu ambiente Docker com confiança, melhorando seu processo de desenvolvimento e deployment de aplicações.