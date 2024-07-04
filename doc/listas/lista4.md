### Exercícios Práticos sobre Comandos para Gerenciar Redes Docker

Aqui estão 20 exercícios práticos para ajudar a solidificar seu entendimento sobre os comandos de gerenciamento de redes Docker. Esses exercícios abrangem desde a criação e inspeção de redes até a conexão e desconexão de containers, passando por operações avançadas e configurações específicas de redes.

#### Exercício 1: Listar Redes Docker

1. Liste todas as redes Docker no seu sistema.
2. Anote os nomes, IDs, drivers e escopos das redes listadas.

```sh
docker network ls
```

#### Exercício 2: Criar uma Rede Bridge

1. Crie uma rede bridge chamada `minha-rede`.
2. Verifique se a rede foi criada listando todas as redes novamente.

```sh
docker network create --driver bridge minha-rede
docker network ls
```

#### Exercício 3: Inspecionar uma Rede Docker

1. Inspecione a rede `minha-rede`.
2. Anote os detalhes da rede, como ID, driver e sub-rede.

```sh
docker network inspect minha-rede
```

#### Exercício 4: Conectar um Container a uma Rede

1. Inicie um container `nginx` e conecte-o à rede `minha-rede`.
2. Verifique se o container está conectado à rede inspecionando o container.

```sh
docker run -d --name meu-container --network minha-rede nginx
docker inspect meu-container
```

#### Exercício 5: Desconectar um Container de uma Rede

1. Desconecte o container `meu-container` da rede `minha-rede`.
2. Verifique se o container foi desconectado da rede.

```sh
docker network disconnect minha-rede meu-container
docker inspect meu-container
```

#### Exercício 6: Remover uma Rede Docker

1. Pare e remova todos os containers conectados à rede `minha-rede`.
2. Remova a rede `minha-rede`.
3. Verifique se a rede foi removida listando todas as redes novamente.

```sh
docker stop meu-container
docker rm meu-container
docker network rm minha-rede
docker network ls
```

#### Exercício 7: Criar e Usar uma Rede Host

1. Inicie um container `nginx` usando a rede host.
2. Verifique a conectividade utilizando a rede do host.

```sh
docker run -d --name host-container --network host nginx
curl localhost
```

#### Exercício 8: Criar e Usar uma Rede Overlay

1. Inicialize o swarm no seu sistema.
2. Crie uma rede overlay chamada `minha-overlay`.
3. Inicie um serviço `nginx` no swarm conectado à rede `minha-overlay`.

```sh
docker swarm init
docker network create --driver overlay minha-overlay
docker service create --name overlay-service --network minha-overlay nginx
```

#### Exercício 9: Conectar um Container a Múltiplas Redes

1. Crie duas redes bridge chamadas `rede1` e `rede2`.
2. Inicie um container `nginx` e conecte-o às redes `rede1` e `rede2`.
3. Verifique as conexões inspecionando o container.

```sh
docker network create --driver bridge rede1
docker network create --driver bridge rede2
docker run -d --name multi-net-container --network rede1 nginx
docker network connect rede2 multi-net-container
docker inspect multi-net-container
```

#### Exercício 10: Adicionar Sub-rede e Gateway

1. Crie uma rede bridge chamada `minha-rede-subnet` com uma sub-rede específica `192.168.1.0/24` e gateway `192.168.1.1`.
2. Verifique as configurações da rede inspecionando-a.

```sh
docker network create --driver bridge --subnet 192.168.1.0/24 --gateway 192.168.1.1 minha-rede-subnet
docker network inspect minha-rede-subnet
```

#### Exercício 11: Usar Rede Macvlan

1. Crie uma rede Macvlan chamada `minha-macvlan` com a sub-rede `192.168.1.0/24` e gateway `192.168.1.1`.
2. Inicie um container `nginx` com um endereço IP específico `192.168.1.100` na rede `minha-macvlan`.

```sh
docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 minha-macvlan
docker run -d --name macvlan-container --network minha-macvlan --ip 192.168.1.100 nginx
```

#### Exercício 12: Usar Rede None

1. Inicie um container `nginx` usando a rede `none`.
2. Verifique se o container está desconectado de todas as redes.

```sh
docker run -d --name no-net-container --network none nginx
docker inspect no-net-container
```

#### Exercício 13: Verificar a Conectividade entre Containers

1. Crie uma rede bridge chamada `conectividade-rede`.
2. Inicie dois containers `nginx` conectados à rede `conectividade-rede`.
3. Verifique a conectividade entre os containers usando o comando `ping`.

```sh
docker network create --driver bridge conectividade-rede
docker run -d --name container1 --network conectividade-rede nginx
docker run -d --name container2 --network conectividade-rede nginx
docker exec -it container1 ping container2
```

#### Exercício 14: Remover Redes Inativas

1. Liste todas as redes no sistema.
2. Remova todas as redes que não estão em uso por nenhum container.

```sh
docker network ls
docker network prune
```

#### Exercício 15: Adicionar e Remover Alias de Rede

1. Inicie um container `nginx` com um alias de rede `web`.
2. Verifique o alias inspecionando o container.
3. Remova o alias de rede do container.

```sh
docker run -d --name alias-container --network minha-rede --network-alias web nginx
docker inspect alias-container
docker network disconnect minha-rede alias-container
docker network connect minha-rede alias-container
```

#### Exercício 16: Gerenciar Redes com Compose

1. Crie um arquivo `docker-compose.yml` com duas redes personalizadas.
2. Inicie os serviços definidos no arquivo Compose e verifique as redes criadas.

```yaml
version: '3.7'
services:
  web:
    image: nginx
    networks:
      - frontend
      - backend
  db:
    image: mysql
    networks:
      - backend
networks:
  frontend:
  backend:
```

```sh
docker-compose up -d
docker network ls
```

#### Exercício 17: Criar Rede com Opções Avançadas

1. Crie uma rede bridge chamada `avancada-rede` com opções avançadas, como MTU e opções de driver.
2. Verifique as opções configuradas inspecionando a rede.

```sh
docker network create --driver bridge --opt com.docker.network.driver.mtu=1200 avancada-rede
docker network inspect avancada-rede
```

#### Exercício 18: Monitorar Tráfego de Rede

1. Inicie dois containers `nginx` conectados à mesma rede.
2. Use o comando `docker stats` para monitorar o tráfego de rede dos containers.

```sh
docker network create --driver bridge monitoramento-rede
docker run -d --name monitor-container1 --network monitoramento-rede nginx
docker run -d --name monitor-container2 --network monitoramento-rede nginx
docker stats monitor-container1 monitor-container2
```

#### Exercício 19: Usar Endpoints Estáticos

1. Crie uma rede bridge chamada `static-endpoints-rede`.
2. Inicie um container `nginx` e configure um endpoint IP estático na rede `static-endpoints-rede`.

```sh
docker network create --driver bridge static-endpoints-rede
docker run -d --name static-endpoint-container --network static-endpoints-rede --ip 172.18.0.10 nginx
```

#### Exercício 20: Criar Rede com Sub-rede IPv6

1. Crie uma rede bridge chamada `ipv6-rede` com sub-rede IPv6 `2001:db8::/64`.
2. Inicie um container `nginx` e verifique a conectividade IPv6.

```sh
docker network create --driver bridge --subnet 2001:db8::/64 ipv6-rede
docker run -d --name ipv6-container --network ipv6-rede nginx
docker exec -it ipv6-container ping6 google.com
```

### Conclusão

Esses exercícios práticos cobrem uma ampla gama de comandos e cenários de uso para redes Docker. Ao completá-los, você desenvolverá uma compreensão sólida de como criar, conectar, inspecionar, remover e gerenciar redes Docker, além de aplicar essas habilidades em situações do mundo real.