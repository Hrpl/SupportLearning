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
* (next(): считывает введенную строку до первого пробела
* nextLine(): считывает всю введенную строку
* nextInt(): считывает введенное число int
* nextDouble(): считывает введенное число double
* nextBoolean(): считывает значение boolean
* nextByte(): считывает введенное число byte
* nextFloat(): считывает введенное число float
* nextShort(): считывает введенное число short
