### Exercícios Práticos sobre Comandos para Gerenciar Containers Docker

Aqui estão 10 exercícios práticos para ajudar a solidificar seu entendimento sobre os comandos de gerenciamento de
containers Docker. Esses exercícios abrangem desde a criação até a remoção de containers, passando pela execução de
comandos e cópia de arquivos.

#### Exercício 1: Listar Containers em Execução

1. Liste todos os containers em execução no seu sistema.
2. Anote o ID e o nome de cada container.

```sh
docker ps
```

#### Exercício 2: Iniciar um Container

1. Inicie um container a partir da imagem `nginx` e nomeie-o como `meu-nginx`.
2. Verifique se o container está em execução.

```sh
docker run -d --name meu-nginx nginx
docker ps
```

#### Exercício 3: Parar um Container

1. Pare o container `meu-nginx` que você criou no exercício anterior.
2. Verifique se o container foi parado com sucesso.

```sh
docker stop meu-nginx
docker ps -a
```

#### Exercício 4: Reiniciar um Container

1. Reinicie o container `meu-nginx`.
2. Verifique se o container está novamente em execução.

```sh
docker restart meu-nginx
docker ps
```

#### Exercício 5: Remover um Container

1. Pare o container `meu-nginx` se ele estiver em execução.
2. Remova o container `meu-nginx`.
3. Verifique se o container foi removido com sucesso.

```sh
docker stop meu-nginx
docker rm meu-nginx
docker ps -a
```

#### Exercício 6: Ver Logs de um Container

1. Crie e execute um container a partir da imagem `redis` e nomeie-o como `meu-redis`.
2. Visualize os logs do container `meu-redis`.

```sh
docker run -d --name meu-redis redis
docker logs meu-redis
```

#### Exercício 7: Executar um Comando em um Container

1. Inicie um container `ubuntu` em segundo plano e nomeie-o como `meu-ubuntu`.
2. Execute o comando `ls /` dentro do container `meu-ubuntu`.

```sh
docker run -d --name meu-ubuntu ubuntu sleep infinity
docker exec -it meu-ubuntu ls /
```

#### Exercício 8: Inspecionar um Container

1. Inspecione o container `meu-ubuntu` e anote as informações sobre a rede e os volumes.
2. Verifique as informações detalhadas sobre o estado do container.

```sh
docker inspect meu-ubuntu
```

#### Exercício 9: Ver Estatísticas de um Container

1. Inicie um container a partir da imagem `nginx` e nomeie-o como `nginx-stats`.
2. Verifique as estatísticas de uso de recursos do container `nginx-stats`.

```sh
docker run -d --name nginx-stats nginx
docker stats nginx-stats
```

#### Exercício 10: Copiar Arquivos de/Ao Container

1. Crie um arquivo `index.html` no seu sistema host com algum conteúdo.
2. Inicie um container `nginx` e nomeie-o como `nginx-copy`.
3. Copie o arquivo `index.html` do host para o container `nginx-copy` no diretório `/usr/share/nginx/html`.
4. Verifique se o arquivo foi copiado com sucesso.

```sh
echo "Hello, Docker!" > index.html
docker run -d --name nginx-copy nginx
docker cp index.html nginx-copy:/usr/share/nginx/html/index.html
docker exec -it nginx-copy ls /usr/share/nginx/html
```

### Conclusão

Esses exercícios práticos cobrem os principais comandos para gerenciar containers Docker. Ao completá-los, você terá uma
compreensão sólida de como criar, iniciar, parar, reiniciar, remover, inspecionar, executar comandos dentro de
containers, visualizar logs e copiar arquivos de e para containers Docker. Essas habilidades são essenciais para
qualquer desenvolvedor que trabalha com Docker.