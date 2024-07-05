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

## Spring Web API

Для создания проекта необходимо добавить зависимости: Spring Web и Spring Boot DevTools

Что бы создать какой либо объект и внести его в контекст приложения Spring необходимо указать анотацию  
Для контроллера анотация является @RestController, а для конечной точки @GetMapping

### Пример API

Models
```java
package com.webapi.firstapi.models;

public record User(String name,
                   int age,
                   String Email)
{
}

```

Service
```java
package com.webapi.firstapi.services;

import com.webapi.firstapi.models.User;
import jakarta.annotation.PostConstruct;
import org.springframework.stereotype.Repository;
import org.springframework.stereotype.Service;

import java.util.*;

@Repository
public class UserService {
    private List<User> users = new ArrayList<>();

    public List<User> findAll(){
        return users;
    }

    @PostConstruct
    private void init(){
        users.add(new User("Andrey",
                18,
                "example@mail.ru")
        );
        users.add(new User("Oleg",
                20,
                "Oleg@example.com")
        );
    }
}
```

Controller
```java 
package com.webapi.firstapi.controller;

import com.webapi.firstapi.models.User;
import com.webapi.firstapi.services.UserService;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService){
        this.userService = userService;
    }

    @GetMapping("/Users")
    List<User> GetUsers(){
        return userService.findAll();
    }
}
```
