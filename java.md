# Java
Для работы с Java необходимы JDK (Java Development Kit) - OpenJDK и OracelJDK

## Основы

Основным строительным блоком программы на языке Java являются инструкции (statement).

Для объявление переменных используют тип_данных название_переменной, либо var. Константа объявляется также, как и переменная, только вначале идет ключевое слово final: final int LIMIT = 5;  

Ввод с консоли:  
```java
  import java.util.Scanner;

  Scanner in = new Scanner(System.in);  
  System.out.print("Input a number: ");  
  int num = in.nextInt();  
  ```
Класс Scanner имеет еще ряд методов, которые позволяют получить введенные пользователем значения:
* next(): считывает введенную строку до первого пробела
* nextLine(): считывает всю введенную строку
* nextInt(): считывает введенное число int
* nextDouble(): считывает введенное число double
* nextBoolean(): считывает значение boolean
* nextByte(): считывает введенное число byte
* nextFloat(): считывает введенное число float
* nextShort(): считывает введенное число short  

Аналогом LINQ служит Stream API  
При работе с ним, мы можем столкнуться с тем, что запрос ничего не вернёт и метод get() ничего не вернёт. Т.к. get() просто переводит результат из Optional<T>(аналог Task<T>) -> T, мы можем использовать методы объекта Optional для проверки результата

## Spring Web API

Для создания проекта необходимо добавить зависимости: Spring Web и Spring Boot DevTools

Что бы создать какой либо объект и внести его в контекст приложения Spring необходимо указать анотацию  
Для контроллера анотация является @RestController, а для конечной точки @GetMapping

### Пример API

Models
```java
public record User(int id,
                   String name,
                   int age,
                   String Email){}
```

Service
```java
package com.webapi.firstapi.services;

import com.webapi.firstapi.models.User;
import jakarta.annotation.PostConstruct;
import org.springframework.stereotype.Repository;
import java.util.*;

@Repository
public class UserService {
    private List<User> users = new ArrayList<>();

    public List<User> findAll(){
        return users;
    }

    public Optional<User> findById(int id){
        return users.stream().filter(w -> w.id() == id).findFirst();
    }


    @PostConstruct
    private void init(){
        users.add(new User( 1,
                "Andrey",
                18,
                "example@mail.ru")
        );
        users.add(new User(2,
                "Oleg",
                20,
                "Oleg@example.com")
        );
    }
}
```

Controller
```java 
package com.webapi.firstapi.controller;

@RestController
@RequestMapping("api/users/")
public class UserController {

    private final UserService userService;

    public UserController(UserService userService){
        this.userService = userService;
    }

    @GetMapping("")
    List<User> findAll(){
        return userService.findAll();
    }

    @GetMapping("/{id}")
    User findUserByid(@PathVariable int id){
        var user = userService.findById(id);
        if(user.isPresent()){
            return user.get();
        }
        else {
            throw new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found"); // Выводит статус код ошибки 404
        }
    }
}
```
### Валидация
Для валидации используется зависимость
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
