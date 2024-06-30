### Exercícios Práticos sobre Comandos para Gerenciar Volumes Docker

Aqui estão 20 exercícios práticos para ajudar a solidificar seu entendimento sobre os comandos de gerenciamento de volumes Docker. Esses exercícios abrangem desde a criação e inspeção de volumes até a montagem e remoção, passando por operações avançadas e situações do mundo real.

#### Exercício 1: Listar Volumes Docker

1. Liste todos os volumes Docker presentes no seu sistema.
2. Anote os nomes dos volumes listados.

```sh
docker volume ls
```

#### Exercício 2: Criar um Volume Docker

1. Crie um volume chamado `dados-app`.
2. Verifique se o volume foi criado listando todos os volumes novamente.

```sh
docker volume create dados-app
docker volume ls
```

#### Exercício 3: Inspecionar um Volume Docker

1. Inspecione o volume `dados-app`.
2. Anote o ponto de montagem e as labels (se houver) do volume.

```sh
docker volume inspect dados-app
```

#### Exercício 4: Montar um Volume em um Container

1. Inicie um container `nginx` montando o volume `dados-app` no diretório `/usr/share/nginx/html`.
2. Verifique se o container está em execução.

```sh
docker run -d -v dados-app:/usr/share/nginx/html --name nginx-container nginx
docker ps
```

#### Exercício 5: Adicionar um Arquivo a um Volume

1. Adicione um arquivo `index.html` com o conteúdo "Hello, Docker!" ao volume `dados-app`.
2. Verifique o conteúdo do arquivo dentro do container `nginx`.

```sh
echo "Hello, Docker!" > /var/lib/docker/volumes/dados-app/_data/index.html
docker exec -it nginx-container cat /usr/share/nginx/html/index.html
```

#### Exercício 6: Remover um Volume Docker

1. Pare e remova o container `nginx-container`.
2. Remova o volume `dados-app`.
3. Verifique se o volume foi removido listando todos os volumes novamente.

```sh
docker stop nginx-container
docker rm nginx-container
docker volume rm dados-app
docker volume ls
```

#### Exercício 7: Remover Volumes Órfãos

1. Crie e remova alguns volumes para garantir que há volumes órfãos no sistema.
2. Remova todos os volumes órfãos utilizando o comando `docker volume prune`.

```sh
docker volume create volume1
docker volume create volume2
docker volume rm volume1
docker volume prune
```

#### Exercício 8: Montar Múltiplos Volumes em um Container

1. Crie dois volumes chamados `config` e `logs`.
2. Inicie um container `nginx` montando os volumes `config` em `/app/config` e `logs` em `/app/logs`.
3. Verifique se os volumes foram montados corretamente no container.

```sh
docker volume create config
docker volume create logs
docker run -d -v config:/app/config -v logs:/app/logs --name multi-volume-container nginx
docker exec -it multi-volume-container ls /app
```

#### Exercício 9: Copiar Arquivos para um Volume

1. Crie um arquivo `config.json` no seu sistema host com algum conteúdo de configuração.
2. Copie o arquivo para o volume `config` montado no container `multi-volume-container`.

```sh
echo '{ "setting": "value" }' > config.json
docker cp config.json multi-volume-container:/app/config/config.json
docker exec -it multi-volume-container cat /app/config/config.json
```

#### Exercício 10: Montar Volumes com `--mount`

1. Crie um volume chamado `data`.
2. Inicie um container `nginx` montando o volume `data` no diretório `/data` usando a opção `--mount`.

```sh
docker volume create data
docker run -d --mount source=data,target=/data --name mount-test-container nginx
```

#### Exercício 11: Verificar o Uso de Espaço em Volumes

1. Inicie um container `ubuntu` com um volume montado em `/data`.
2. Dentro do container, verifique o uso de espaço no volume.

```sh
docker run -it -v data:/data --name space-check-container ubuntu
docker exec -it space-check-container df -h /data
```

#### Exercício 12: Persistir Dados com Volumes

1. Inicie um container `mysql` com um volume montado para armazenar os dados do banco de dados.
2. Crie uma tabela e insira alguns dados no banco.
3. Pare e remova o container.
4. Inicie um novo container `mysql` utilizando o mesmo volume e verifique se os dados ainda estão presentes.

```sh
docker run -d -v mysql-data:/var/lib/mysql --name mysql-container -e MYSQL_ROOT_PASSWORD=root mysql
docker exec -it mysql-container mysql -uroot -proot -e "CREATE DATABASE testdb; USE testdb; CREATE TABLE testtable (id INT, name VARCHAR(50)); INSERT INTO testtable VALUES (1, 'Docker');"
docker stop mysql-container
docker rm mysql-container
docker run -d -v mysql-data:/var/lib/mysql --name mysql-container-new -e MYSQL_ROOT_PASSWORD=root mysql
docker exec -it mysql-container-new mysql -uroot -proot -e "USE testdb; SELECT * FROM testtable;"
```

#### Exercício 13: Criar um Volume com Labels

1. Crie um volume chamado `volume-labeled` com a label `env=dev`.
2. Inspecione o volume para verificar se a label foi aplicada corretamente.

```sh
docker volume create --label env=dev volume-labeled
docker volume inspect volume-labeled
```

#### Exercício 14: Utilizar Volumes Anônimos

1. Inicie um container `nginx` com um volume anônimo montado em `/usr/share/nginx/html`.
2. Verifique a criação do volume anônimo.

```sh
docker run -d -v /usr/share/nginx/html --name anonymous-volume-container nginx
docker volume ls
```

#### Exercício 15: Backupar Dados de um Volume

1. Crie e inicie um container `busybox` com um volume montado em `/data`.
2. Adicione alguns arquivos ao volume.
3. Utilize o comando `docker cp` para copiar os arquivos do volume para o host.

```sh
docker run -it -v backup-data:/data --name backup-container busybox
docker exec -it backup-container sh -c "echo 'Backup file' > /data/backup.txt"
docker cp backup-container:/data/backup.txt ./backup.txt
```

#### Exercício 16: Restaurar Dados para um Volume

1. Crie um novo volume chamado `restore-data`.
2. Copie os arquivos de backup do host para o volume montado em um novo container.

```sh
docker volume create restore-data
docker run -it -v restore-data:/data --name restore-container busybox
docker cp ./backup.txt restore-container:/data/backup.txt
docker exec -it restore-container cat /data/backup.txt
```

#### Exercício 17: Automatizar a Limpeza de Volumes

1. Utilize um script Bash para listar e remover volumes que não estão sendo utilizados.

```bash
#!/bin/bash
docker volume prune -f
```

#### Exercício 18: Monitorar o Tamanho de um Volume

1. Crie um volume e monte-o em um container.
2. Adicione dados ao volume e monitore seu tamanho utilizando `docker system df`.

```sh
docker volume create monitor-volume
docker run -d -v monitor-volume:/data --name monitor-container busybox
docker exec -it monitor-container sh -c "dd if=/dev/zero of=/data/testfile bs=1M count=50"
docker system df -v
```

#### Exercício 19: Gerenciar Permissões de Volumes

1. Monte um volume em um container `ubuntu` e altere as permissões de um arquivo dentro do volume.
2. Verifique as permissões alteradas.

```sh
docker volume create permission-volume
docker run -it -v permission-volume:/data --name permission-container ubuntu
docker exec -it permission-container bash -c "echo 'Permission test' > /data/testfile && chmod 777 /data/testfile && ls -l /data"
```

#### Exercício 20: Montar Volumes Somente para Leitura

1. Crie um volume chamado `readonly-volume`.
2. Inicie um container `nginx` montando o volume `readonly-volume` em `/data` com permissão somente para leitura.
3. Tente criar um arquivo no volume montado dentro do container.

```sh
docker volume create readonly-volume
docker run -d -v readonly-volume:/data:ro --name readonly-container nginx
docker exec -it readonly-container sh -c "echo 'This should fail' > /data/testfile"
```

### Conclusão

Esses exercícios práticos cobrem uma ampla gama de comandos e cenários de uso para volumes Docker. Ao completá-los, você desenvolverá uma compreensão sólida de como criar, montar, inspecionar, remover e gerenciar volumes Docker, além de aplicar essas habilidades em situações do mundo real.