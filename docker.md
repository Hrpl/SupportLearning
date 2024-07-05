# Оркестрация и контейнеризация

## Базы данных

### Postgres
Чтобы создать контейнер postgres  
```cmd docker run --name postgres -p 5439:5432 -e POSTGRES_PASSWORD=12345 -d postgres  ```
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
