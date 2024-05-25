# PostgreSQL DOcker Container Keeping Data

## Instalar Docker

### Configurações necessárias:

1. Atualize a lista de pacotes do sistema:

```
sudo yum update
```

2. Instale as dependências necessárias:

```
sudo yum install -y yum-utils
```

3. Adicione o repositório oficial do Docker:

```
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

### Instalar Docker Engine

1. Instale o Docker Engine, o containerd e o Docker Compose:

```
sudo yum install docker-ce docker-ce-cli containerd.io --nobest --allowerasing
```

2. Depois de instalado, inicie e habilite o Docker:

```
sudo systemctl start docker
sudo systemctl enable docker
```

3. Verifique se o Docker foi instalado corretamente:

```
sudo docker --version
```

4. Teste o Docker executando um contêiner de exemplo, como o "Hello World":

```
sudo docker run hello-world
```

## Criar uma imagem do Postgresql

1. Crie um arquivo Dockerfile:

```
echo 'FROM postgres:latest' > Dockerfile
```

Edite o arquivo Dockerfile, :

```
sudo vi Dockerfile
```

- Dentro do arquivo Dockerfile:


```
# imagem oficial do PostgreSQL
FROM postgres:latest

# variáveis de ambiente
ENV POSTGRES_DB mydatabase
ENV POSTGRES_USER myuser
ENV POSTGRES_PASSWORD mypassword

# Crie um diretório para persistir os dados
RUN mkdir -p /var/lib/postgresql/pgdata

# Defina o diretório de dados como um volume
VOLUME /var/lib/postgresql/pgdata
```

- Para Salvar o arquivo Esc :wq


### Construir a imagem:

- Substitua my-postgres-image pelo o nome que você deseja

```
docker buildx build -t my-postgres-image .
```

- Verifique se a imagem foi criada usando o comando:


```
sudo docker images
```

### Execute um Container:

- Depois que criou a imagem, pode executar um container com base nela.

```
sudo docker run -d --name my-postgres-container my-postgres-image
```
*Substitua my-postgres-container pelo o nome que deseja, e certifique de usar o mesmo nome que usou na imagem, my-postgres-image*

- Para verificar se o container foi executado:

```
sudo docker ps
```

### Acesse o PostgreSQL


```
sudo docker exec -it my-postgres-container psql -U myuser mydatabase
```

- Substitua os valores myuser e mydatabase pelos valores que você definiu nas variáveis de ambiente do Dckerfile
