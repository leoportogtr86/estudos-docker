### Comandos Úteis para Monitoramento de Containers Docker

Monitorar containers Docker é essencial para garantir que suas aplicações estejam funcionando corretamente e para identificar e resolver problemas rapidamente. Docker oferece uma variedade de comandos para monitorar containers em tempo real, verificar logs, inspecionar containers e obter informações detalhadas sobre o uso de recursos. Este artigo explora os comandos úteis para monitorar containers Docker.

#### 1. `docker ps`

O comando `docker ps` lista todos os containers em execução, fornecendo informações básicas como o ID do container, a imagem usada, o status, e as portas expostas.

```sh
docker ps
```

Para listar todos os containers, incluindo os que estão parados, use a opção `-a`:

```sh
docker ps -a
```

#### 2. `docker stats`

O comando `docker stats` exibe o uso de recursos dos containers em tempo real, incluindo CPU, memória, uso de rede e uso de disco.

```sh
docker stats
```

Para monitorar containers específicos, passe os IDs ou nomes dos containers como argumentos:

```sh
docker stats container1 container2
```

#### 3. `docker top`

O comando `docker top` exibe os processos em execução dentro de um container, semelhante ao comando `top` no Linux.

```sh
docker top <nome-ou-id-do-container>
```

Por exemplo:

```sh
docker top meu-container
```

#### 4. `docker logs`

O comando `docker logs` exibe os logs gerados por um container. Este comando é essencial para depuração e monitoramento de atividades do container.

```sh
docker logs <nome-ou-id-do-container>
```

Para seguir os logs em tempo real, use a opção `-f` (follow):

```sh
docker logs -f meu-container
```

Para exibir um número específico de linhas de log, use a opção `--tail`:

```sh
docker logs --tail 100 meu-container
```

#### 5. `docker inspect`

O comando `docker inspect` fornece informações detalhadas sobre um container, incluindo configurações de rede, volumes montados, variáveis de ambiente e muito mais.

```sh
docker inspect <nome-ou-id-do-container>
```

Para extrair informações específicas usando filtros, use a opção `-f`:

```sh
docker inspect -f '{{.NetworkSettings.IPAddress}}' meu-container
```

#### 6. `docker events`

O comando `docker events` exibe eventos em tempo real do Docker, incluindo criação, inicialização, parada e remoção de containers, além de eventos de rede e volume.

```sh
docker events
```

Para monitorar eventos específicos, use filtros:

```sh
docker events --filter 'event=start' --filter 'event=stop'
```

#### 7. `docker diff`

O comando `docker diff` exibe as alterações feitas no sistema de arquivos de um container em comparação com a imagem original.

```sh
docker diff <nome-ou-id-do-container>
```

Por exemplo:

```sh
docker diff meu-container
```

#### 8. `docker stats` com formatação personalizada

Você pode personalizar a saída do comando `docker stats` para mostrar apenas as colunas desejadas:

```sh
docker stats --format "table {{.Container}}\t{{.CPUPerc}}\t{{.MemUsage}}"
```

#### 9. `docker system df`

O comando `docker system df` fornece uma visão geral do espaço em disco usado pelo Docker, incluindo imagens, containers, volumes e dados de cache.

```sh
docker system df
```

#### 10. `docker container cp`

O comando `docker container cp` copia arquivos entre o sistema de arquivos do host e o container. Isso pode ser útil para inspecionar arquivos de log ou outros dados gerados pelo container.

```sh
docker container cp <nome-ou-id-do-container>:<caminho-no-container> <caminho-no-host>
```

Por exemplo, para copiar um arquivo de log de um container para o host:

```sh
docker container cp meu-container:/var/log/nginx/access.log ./access.log
```

#### Exemplos Práticos

##### Exemplo 1: Monitorar Uso de Recursos de Containers

1. Inicie dois containers `nginx`:

```sh
docker run -d --name web1 nginx
docker run -d --name web2 nginx
```

2. Monitore o uso de recursos dos containers:

```sh
docker stats web1 web2
```

##### Exemplo 2: Verificar Logs de um Container

1. Inicie um container `nginx`:

```sh
docker run -d --name meu-nginx nginx
```

2. Exiba os logs do container:

```sh
docker logs meu-nginx
```

##### Exemplo 3: Inspecionar um Container

1. Inicie um container `nginx`:

```sh
docker run -d --name meu-nginx nginx
```

2. Inspecione o container para obter detalhes sobre a rede:

```sh
docker inspect -f '{{.NetworkSettings.IPAddress}}' meu-nginx
```

##### Exemplo 4: Monitorar Eventos do Docker

1. Inicie o monitoramento de eventos:

```sh
docker events
```

2. Em outra janela de terminal, inicie e pare alguns containers para observar os eventos gerados:

```sh
docker run -d --name container1 nginx
docker stop container1
docker rm container1
```

#### Conclusão

Monitorar containers Docker é crucial para garantir que suas aplicações estejam funcionando corretamente e para resolver problemas rapidamente. Utilizando os comandos abordados neste artigo, você pode monitorar o uso de recursos, inspecionar containers, verificar logs e obter informações detalhadas sobre a atividade do Docker. Esses comandos são ferramentas poderosas que permitem gerenciar seus containers de forma eficiente e eficaz.

---

Este artigo cobriu os principais comandos úteis para monitoramento de containers Docker, fornecendo uma base sólida para o uso eficaz dessas ferramentas. Compreender e utilizar esses comandos permitirá a você monitorar e gerenciar seu ambiente Docker com confiança, melhorando a estabilidade e a performance de suas aplicações.