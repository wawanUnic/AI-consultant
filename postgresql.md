# PostgreSQL database

### Database - port 7756, Admin - port 7757

Work not as root

Create a folder for work
```
mkdir postgresql
cd postgresql
```

Create a docker-compose.yml file
```
# Use postgres/example user/password credentials
version: '3.9'
services:
  postgresql-server:
    image: postgres
    container_name: postgresql-server
    restart: always
    # set shared memory limit when using docker-compose
    shm_size: 128mb
    # or set shared memory limit when deploy via swarm stack
    #volumes:
    #  - type: tmpfs
    #    target: /dev/shm
    #    tmpfs:
    #      size: 134217728 # 128*2^20 bytes = 128Mb
    environment:
      POSTGRES_PASSWORD: example
    ports:
      - 7756:5432
  postgresql-adminer:
    image: adminer
    container_name: postgresql-adminer
    restart: always
    ports:
      - 7757:8080
networks:
  default:
    name: postgresql
```

Running container assembly
```
sudo docker-compose up -d
```

Using the adminer service (or the HeidiSQL program), log in
```
Движок - PostgreSQL
Сервер - postgresql-server
Имя пользователя - postgres
Пароль - example
База данных - 
```

Let's create a database and name it n8n_base
