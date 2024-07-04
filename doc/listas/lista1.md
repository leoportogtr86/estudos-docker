### Exercícios Práticos sobre Comandos para Gerenciar Imagens Docker

Aqui estão 10 exercícios práticos para ajudar a solidificar seu entendimento sobre os comandos de gerenciamento de
imagens Docker. Esses exercícios abrangem desde a busca e download de imagens até a criação, inspeção e remoção de
imagens.

#### Exercício 1: Listar Imagens Docker

1. Execute o comando para listar todas as imagens Docker armazenadas localmente.
2. Verifique as informações exibidas, como REPOSITORY, TAG, IMAGE ID, CREATED e SIZE.

```sh
docker images
```

#### Exercício 2: Buscar Imagens no Docker Hub

1. Utilize o comando para buscar a imagem oficial do MySQL no Docker Hub.
2. Anote o número de estrelas e descrições das imagens encontradas.

```sh
docker search mysql
```

#### Exercício 3: Baixar uma Imagem do Docker Hub

1. Baixe a imagem do Redis utilizando o comando `docker pull`.
2. Verifique se a imagem foi baixada corretamente listando as imagens locais.

```sh
docker pull redis
docker images
```

#### Exercício 4: Construir uma Imagem a partir de um Dockerfile

1. Crie um arquivo `Dockerfile` com o seguinte conteúdo para uma aplicação Node.js simples:

```Dockerfile
FROM node:14
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "app.js"]
EXPOSE 3000
```

2. Construa a imagem utilizando o comando `docker build` e nomeie-a como `meu-node-app:v1`.

```sh
docker build -t meu-node-app:v1 .
```

#### Exercício 5: Exibir Histórico de uma Imagem

1. Exiba o histórico de camadas da imagem `nginx` utilizando o comando `docker history`.

```sh
docker history nginx
```

#### Exercício 6: Inspecionar uma Imagem

1. Inspecione a imagem `redis` utilizando o comando `docker inspect`.
2. Verifique informações detalhadas como o tamanho da imagem, camadas e variáveis de ambiente.

```sh
docker inspect redis
```

#### Exercício 7: Renomear uma Imagem

1. Renomeie a imagem `meu-node-app:v1` para `meu-node-app:latest` utilizando o comando `docker tag`.

```sh
docker tag meu-node-app:v1 meu-node-app:latest
```

#### Exercício 8: Remover uma Imagem Docker

1. Remova a imagem `redis` utilizando o comando `docker rmi`.
2. Verifique se a imagem foi removida corretamente.

```sh
docker rmi redis
docker images
```

#### Exercício 9: Exportar e Importar uma Imagem Docker

1. Exporte a imagem `meu-node-app:latest` para um arquivo tar utilizando o comando `docker save`.
2. Remova a imagem localmente e depois importe-a novamente utilizando os comandos `docker rmi` e `docker load`.

```sh
docker save -o meu-node-app.tar meu-node-app:latest
docker rmi meu-node-app:latest
docker load -i meu-node-app.tar
```

#### Exercício 10: Enviar uma Imagem para o Docker Hub

1. Faça login no Docker Hub utilizando o comando `docker login`.
2. Renomeie a imagem `meu-node-app:latest` para o repositório do Docker Hub.
3. Envie a imagem utilizando o comando `docker push`.

```sh
docker login
docker tag meu-node-app:latest meu-usuario/meu-node-app:latest
docker push meu-usuario/meu-node-app:latest
```

### Conclusão

Esses exercícios práticos cobrem os principais comandos para gerenciar imagens Docker. Ao completá-los, você terá uma
compreensão sólida de como buscar, baixar, construir, inspecionar, renomear, remover, exportar, importar e enviar
imagens Docker. Essas habilidades são essenciais para qualquer desenvolvedor que trabalha com Docker.