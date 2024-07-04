### Comandos para Gerenciar Redes Docker

Gerenciar redes Docker é essencial para conectar containers de forma eficiente e segura. Docker oferece várias opções de redes que permitem configurar ambientes de rede de acordo com as necessidades da aplicação. Este artigo explora os comandos essenciais para gerenciar redes Docker, desde a criação até a inspeção e remoção.

#### O que são Redes Docker?

Redes Docker permitem que containers se comuniquem entre si e com o mundo externo. Existem vários tipos de redes Docker, cada uma com suas características e casos de uso:

- **Bridge**: Rede padrão criada automaticamente pelo Docker. Ideal para comunicação entre containers no mesmo host.
- **Host**: Containers compartilham a pilha de rede do host. Utilizado para melhorar a performance.
- **Overlay**: Rede que permite comunicação entre containers em diferentes hosts. Usado em clusters de Docker Swarm.
- **Macvlan**: Atribui um endereço MAC a cada container, tornando-o visível na rede física.
- **None**: Desconecta o container de qualquer rede.

#### Comandos Básicos para Gerenciamento de Redes Docker

##### 1. Listar Redes Docker

Para listar todas as redes Docker no sistema, utilize o comando:

```sh
docker network ls
```

Este comando exibe uma lista de redes, incluindo seus nomes, IDs, drivers e escopos.

##### 2. Criar uma Rede Docker

Para criar uma nova rede Docker, utilize o comando:

```sh
docker network create --driver <driver> <nome-da-rede>
```

Por exemplo, para criar uma rede bridge chamada `minha-rede`:

```sh
docker network create --driver bridge minha-rede
```

##### 3. Inspecionar uma Rede Docker

Para obter detalhes sobre uma rede específica, utilize o comando:

```sh
docker network inspect <nome-da-rede>
```

Por exemplo:

```sh
docker network inspect minha-rede
```

##### 4. Conectar um Container a uma Rede

Para conectar um container existente a uma rede, utilize o comando:

```sh
docker network connect <nome-da-rede> <nome-do-container>
```

Por exemplo:

```sh
docker run -d --name meu-container nginx
docker network connect minha-rede meu-container
```

##### 5. Desconectar um Container de uma Rede

Para desconectar um container de uma rede, utilize o comando:

```sh
docker network disconnect <nome-da-rede> <nome-do-container>
```

Por exemplo:

```sh
docker network disconnect minha-rede meu-container
```

##### 6. Remover uma Rede Docker

Para remover uma rede Docker que não está em uso por nenhum container, utilize o comando:

```sh
docker network rm <nome-da-rede>
```

Por exemplo:

```sh
docker network rm minha-rede
```

#### Exemplos Práticos

##### Exemplo 1: Criar e Conectar Containers a uma Rede Bridge

1. **Criar uma rede bridge:**

```sh
docker network create --driver bridge minha-rede
```

2. **Iniciar dois containers e conectá-los à rede `minha-rede`:**

```sh
docker run -d --name container1 --network minha-rede nginx
docker run -d --name container2 --network minha-rede nginx
```

3. **Verificar a conectividade entre os containers:**

```sh
docker exec -it container1 ping container2
```

##### Exemplo 2: Utilizar a Rede Host

1. **Iniciar um container usando a rede host:**

```sh
docker run -d --name host-container --network host nginx
```

2. **Verificar a conectividade utilizando a rede do host:**

```sh
curl localhost
```

##### Exemplo 3: Criar e Usar uma Rede Overlay

Para usar redes overlay, você precisa estar em um modo de swarm. Primeiro, inicialize o swarm:

```sh
docker swarm init
```

1. **Criar uma rede overlay:**

```sh
docker network create --driver overlay minha-overlay
```

2. **Iniciar um serviço no swarm conectado à rede overlay:**

```sh
docker service create --name overlay-service --network minha-overlay nginx
```

3. **Verificar os detalhes da rede overlay:**

```sh
docker network inspect minha-overlay
```

#### Comandos Avançados

##### 1. Adicionar Sub-rede e Gateway

Ao criar uma rede, você pode especificar uma sub-rede e um gateway:

```sh
docker network create --driver bridge --subnet 192.168.1.0/24 --gateway 192.168.1.1 minha-rede
```

##### 2. Usar Rede Macvlan

Para criar e utilizar uma rede Macvlan:

```sh
docker network create -d macvlan \
    --subnet=192.168.1.0/24 \
    --gateway=192.168.1.1 \
    -o parent=eth0 minha-macvlan

docker run -d --name macvlan-container --network minha-macvlan --ip 192.168.1.100 nginx
```

#### Conclusão

Gerenciar redes Docker é crucial para conectar containers de forma eficiente e segura. Docker oferece várias opções de redes, desde redes bridge padrão até redes overlay avançadas para clusters. Com a prática e o uso adequado dos comandos para criar, inspecionar, conectar e remover redes, você pode otimizar a comunicação entre seus containers e melhorar a configuração da rede em suas aplicações Docker.

---

Este artigo cobriu os principais comandos para gerenciar redes Docker, fornecendo uma base sólida para o uso eficaz dessa funcionalidade. Compreender e utilizar esses comandos permitirá a você gerenciar redes Docker com confiança, melhorando seu processo de desenvolvimento e deployment de aplicações.