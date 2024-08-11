# Оркестрация и контейнеризация

## Базы данных

### Postgres
Чтобы создать контейнер postgres  
```cmd 
docker run --name postgres -p 5439:5432 -e POSTGRES_PASSWORD=12345 -d postgres
 ```
И во вкладке Inspect определить порт  

Для добавления в оркестрацию необходим следующий код

```yaml
services:
  postgres:
    image: 'postgres:latest'
    environment:
      - 'POSTGRES_DB=postgres'
      - 'POSTGRES_PASSWORD=12345'
      - 'POSTGRES_USER=postgres'
    ports:
      - '5439:5432'
```
Для сборки докер файла:
```cmd
docker build -t image_name .
```
Для запуска контейнера из образа:
```cmd
docker run -p 8080:8080 --name container_name image_name
```
Для сборки docker compose:
```cmd
docker compose up --build
```
Просмотреть запущенные контейнеры:
```cmd
docker ps
```
Просмотреть все контейнеры:
```cmd
docker ps -a
```
Удалить контейнеры:
```cmd
docker rm container_name
```
Просмотреть все образы:
```cmd
docker images
```
Удалить образы:
```cmd
docker rmi image_name
```
