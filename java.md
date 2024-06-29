# Java
Для работы с Java необходимы JDK (Java Development Kit) - OpenJDK и OracelJDK

## Основы

Основным строительным блоком программы на языке Java являются инструкции (statement).

Для объявление переменных используют тип_данных название_переменной, либо var. Константа объявляется также, как и переменная, только вначале идет ключевое слово final: final int LIMIT = 5;  

Ввод с консоли:  
```java
  Scanner in = new Scanner(System.in);  
  System.out.print("Input a number: ");  
  int num = in.nextInt();  
  ```
