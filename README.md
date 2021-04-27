# Crie uma Network no Docker
```bash
docker network create devtube
```

# Baixe o container MySQL

```bash
docker run -d -e MYSQL_ROOT_PASSWORD=root --network devtube --name devtube_mysql vinigracindo/pfa-chal1-mysql
```

Espere 30 segundos para o Mysql Subir e execute o comando abaixo para criar o bando de dados

```bash
docker exec -it devtube_mysql mysql -uroot -proot -e "source /mydata/database_create.sql"
```

# Aplicação
```bash
docker run -d --network devtube --name devtube_app vinigracindo/pfa-chal1-app
```

Execute o comando abaixo para carregar o arquivos estático da aplicação.

```bash
docker exec devtube_app python3 manage.py collectstatic --no-input
```

## Nginx
```bash
docker run -d -p 8080:80 --network devtube --name devtube_nginx vinigracindo/pfa-chal1-nginx
```

# Deployment
- Acesse http://localhost:8080

Página para cadastrar curso:
http://localhost:8080/admin (usuário: admin senha: admin)
