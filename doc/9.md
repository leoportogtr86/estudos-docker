### Comandos para Gerenciar Containers Docker

Docker é uma plataforma poderosa para criar, distribuir e executar aplicações em containers. Um aspecto fundamental do
uso de Docker é a gestão de containers, que são as instâncias em execução das imagens Docker. Este artigo explora os
comandos essenciais para gerenciar containers Docker, desde a criação até a remoção.

#### O que são Containers Docker?

Containers Docker são unidades portáteis e leves que incluem tudo o que uma aplicação precisa para ser executada,
incluindo o código, runtime, bibliotecas e dependências. Eles são criados a partir de imagens Docker e oferecem um
ambiente isolado para a execução de aplicações.

#### Comandos Básicos para Gerenciamento de Containers Docker

##### 1. Listar Containers em Execução

Para listar todos os containers em execução, utilize o comando:

```sh
docker ps
```

Para listar todos os containers, incluindo os que estão parados, utilize:

```sh
docker ps -a
```

##### 2. Iniciar um Container

Para iniciar um container a partir de uma imagem Docker, utilize o comando `docker run`:

```sh
docker run -d --name meu-container nginx
```

Explicação:

- `-d`: Executa o container em segundo plano (detached mode).
- `--name`: Dá um nome ao container.
- `nginx`: Nome da imagem Docker.

##### 3. Parar um Container

Para parar um container em execução, utilize o comando:

```sh
docker stop <container-id ou nome>
```

Por exemplo:

```sh
docker stop meu-container
```

##### 4. Reiniciar um Container

Para reiniciar um container, utilize o comando:

```sh
docker restart <container-id ou nome>
```

Por exemplo:

```sh
docker restart meu-container
```

##### 5. Remover um Container

Para remover um container que está parado, utilize o comando:

```sh
docker rm <container-id ou nome>
```

Por exemplo:

```sh
docker rm meu-container
```

Para remover um container em execução, utilize o comando `docker rm` com a opção `-f` (force):

```sh
docker rm -f <container-id ou nome>
```

##### 6. Ver Logs de um Container

Para visualizar os logs de um container em execução, utilize o comando:

```sh
docker logs <container-id ou nome>
```

Por exemplo:

```sh
docker logs meu-container
```

##### 7. Executar um Comando em um Container em Execução

Para executar um comando em um container em execução, utilize o comando `docker exec`:

```sh
docker exec -it <container-id ou nome> <comando>
```

Por exemplo, para abrir um shell interativo no container:

```sh
docker exec -it meu-container /bin/bash
```

Explicação:

- `-i`: Modo interativo.
- `-t`: Aloca um pseudo-terminal.

##### 8. Inspecionar um Container

Para obter detalhes sobre a configuração e o estado de um container, utilize o comando:

```sh
docker inspect <container-id ou nome>
```

Por exemplo:

```sh
docker inspect meu-container
```

##### 9. Ver Estatísticas de um Container

Para monitorar o uso de recursos de um container em tempo real, utilize o comando:

```sh
docker stats <container-id ou nome>
```

Por exemplo:

```sh
docker stats meu-container
```

##### 10. Copiar Arquivos de/Ao Container

Para copiar arquivos do host para o container, utilize o comando:

```sh
docker cp <caminho-no-host> <container-id ou nome>:<caminho-no-container>
```

Por exemplo:

```sh
docker cp ./index.html meu-container:/usr/share/nginx/html
```

Para copiar arquivos do container para o host, utilize o comando:

```sh
docker cp <container-id ou nome>:<caminho-no-container> <caminho-no-host>
```

Por exemplo:

```sh
docker cp meu-container:/usr/share/nginx/html/index.html ./index.html
```

#### Exemplos Práticos

##### Criando e Gerenciando um Container Nginx

1. **Criar e executar um container Nginx:**

```sh
docker run -d --name nginx-container -p 8080:80 nginx
```

2. **Verificar os containers em execução:**

```sh
docker ps
```

3. **Visualizar os logs do container:**

```sh
docker logs nginx-container
```

4. **Executar um comando dentro do container (abrir um shell):**

```sh
docker exec -it nginx-container /bin/bash
```

5. **Parar o container:**

```sh
docker stop nginx-container
```

6. **Reiniciar o container:**

```sh
docker restart nginx-container
```

7. **Remover o container:**

```sh
docker rm nginx-container
```

#### Conclusão

Gerenciar containers Docker é uma habilidade essencial para qualquer desenvolvedor que trabalha com esta tecnologia.
Desde a criação até a remoção, Docker fornece uma gama completa de comandos para facilitar o gerenciamento eficiente de
containers. Com a prática e o uso adequado desses comandos, você pode otimizar seus fluxos de trabalho e melhorar a
consistência e portabilidade de suas aplicações.

---

Este artigo cobriu os principais comandos para gerenciar containers Docker, fornecendo uma base sólida para o uso eficaz
dessa tecnologia. Compreender e utilizar esses comandos permitirá a você gerenciar containers Docker com confiança,
melhorando seu processo de desenvolvimento e deployment de aplicações.