### Comandos para Gerenciar Imagens Docker

Docker é uma ferramenta poderosa para criar, distribuir e executar aplicações em containers. Um dos aspectos
fundamentais do Docker é o gerenciamento de imagens Docker, que são os templates a partir dos quais os containers são
criados. Este artigo explora os comandos essenciais para gerenciar imagens Docker, desde a criação até a remoção.

#### O que são Imagens Docker?

Imagens Docker são snapshots imutáveis que contêm tudo o que uma aplicação precisa para ser executada: código, runtime,
bibliotecas e configurações. Elas são construídas a partir de arquivos Dockerfile e armazenadas em registries, como o
Docker Hub, para serem reutilizadas e compartilhadas.

#### Comandos Básicos para Gerenciamento de Imagens Docker

##### 1. Listar Imagens Docker

Para listar todas as imagens Docker armazenadas localmente, utilize o comando:

```sh
docker images
```

Este comando exibe informações como REPOSITORY, TAG, IMAGE ID, CREATED e SIZE.

##### 2. Buscar Imagens no Docker Hub

Para procurar imagens no Docker Hub, use o comando:

```sh
docker search <nome-da-imagem>
```

Por exemplo, para procurar uma imagem do nginx:

```sh
docker search nginx
```

##### 3. Baixar Imagens do Docker Hub

Para baixar uma imagem do Docker Hub para sua máquina local, utilize:

```sh
docker pull <nome-da-imagem>:<tag>
```

Se a tag não for especificada, o Docker baixará a imagem com a tag `latest`. Por exemplo:

```sh
docker pull nginx
```

##### 4. Construir Imagens a partir de Dockerfile

Para construir uma imagem a partir de um Dockerfile, navegue até o diretório contendo o Dockerfile e execute:

```sh
docker build -t <nome-da-imagem>:<tag> .
```

O ponto final (`.`) indica o diretório atual. Exemplo:

```sh
docker build -t minha-aplicacao:v1.0 .
```

##### 5. Exibir Histórico de uma Imagem

Para ver o histórico das camadas de uma imagem Docker, utilize:

```sh
docker history <nome-da-imagem>:<tag>
```

Por exemplo:

```sh
docker history nginx
```

##### 6. Ver Detalhes de uma Imagem

Para ver informações detalhadas sobre uma imagem Docker, use:

```sh
docker inspect <nome-da-imagem>:<tag>
```

Por exemplo:

```sh
docker inspect nginx
```

##### 7. Renomear uma Imagem

Para renomear uma imagem Docker, utilize:

```sh
docker tag <imagem-existente>:<tag> <novo-nome>:<nova-tag>
```

Por exemplo:

```sh
docker tag minha-aplicacao:v1.0 minha-aplicacao:latest
```

##### 8. Remover Imagens

Para remover uma imagem Docker localmente, utilize:

```sh
docker rmi <nome-da-imagem>:<tag>
```

Se a imagem não estiver sendo usada por nenhum container, ela será removida. Por exemplo:

```sh
docker rmi nginx
```

##### 9. Exportar e Importar Imagens

Para exportar uma imagem Docker para um arquivo tar, utilize:

```sh
docker save -o <nome-do-arquivo>.tar <nome-da-imagem>:<tag>
```

Para importar uma imagem Docker de um arquivo tar, utilize:

```sh
docker load -i <nome-do-arquivo>.tar
```

##### 10. Enviar Imagens para o Docker Hub

Para enviar uma imagem para o Docker Hub, primeiro faça login:

```sh
docker login
```

Depois, envie a imagem utilizando:

```sh
docker push <nome-do-repositorio>/<nome-da-imagem>:<tag>
```

Por exemplo:

```sh
docker push meu-usuario/nginx:custom
```

#### Exemplos Práticos

##### Criando uma Imagem Personalizada

1. Crie um arquivo `Dockerfile` com o seguinte conteúdo:

```Dockerfile
FROM nginx:latest
COPY ./html /usr/share/nginx/html
```

2. Construa a imagem:

```sh
docker build -t meu-nginx:1.0 .
```

3. Execute um container usando a imagem criada:

```sh
docker run -d -p 8080:80 meu-nginx:1.0
```

##### Enviando uma Imagem para o Docker Hub

1. Faça login no Docker Hub:

```sh
docker login
```

2. Renomeie a imagem para o repositório Docker Hub:

```sh
docker tag meu-nginx:1.0 meu-usuario/meu-nginx:1.0
```

3. Envie a imagem:

```sh
docker push meu-usuario/meu-nginx:1.0
```

#### Conclusão

Gerenciar imagens Docker é uma habilidade essencial para qualquer desenvolvedor que trabalha com containers. Desde a
criação até a distribuição, Docker fornece uma gama completa de comandos para facilitar o gerenciamento eficiente de
imagens. Com a prática e o uso adequado desses comandos, você pode otimizar seus fluxos de trabalho e melhorar a
consistência e portabilidade de suas aplicações.

---

Este artigo cobriu os principais comandos para gerenciar imagens Docker, fornecendo uma base sólida para o uso eficaz
dessa tecnologia. Compreender e utilizar esses comandos permitirá a você gerenciar imagens Docker com confiança,
melhorando seu processo de desenvolvimento e deployment de aplicações.