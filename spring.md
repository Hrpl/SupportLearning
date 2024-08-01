# Spring-framework

## Базовые концепции
Когда говорят про Spring, говорят о экосистеме фреймворков таких как:

* Spring Core - это фундаментальная
функциональная возможность, благодаря которой Spring может управлять
экземплярами приложения. Также частью функционала Spring Core являются аспекты Spring.
 С ними Spring может перехватывать определенные в приложении методы и манипулировать ими

* Spring MVC (model-view-controller, «модель — представление — контроллер»). Эта часть фреймворка Spring позволяет создавать веб-приложения,
обрабатывающие HTTP-запросы
* Spring Data Access — еще одна базовая часть Spring. Она предоставляет
основные инструменты для соединения с базами данных SQL, что позволяет
реализовать уровень доступа к данным в приложении.
* Spring Testing. Эта часть фреймворка включает в себя инструменты, позволяющие писать тесты для Spring-приложения
* Spring Boot - Главная идея этой концепции состоит
в следующем. Вместо того чтобы описывать все параметры конфигурации в самом
фреймворке, Spring Boot предлагает некую конфигурацию по умолчанию, которую
можно изменять по мере необходимости  

Но основной частью является Spring Core. Spring работает по принципу
инверсии управления (inversion of control, IoC): вместо того чтобы приложение
само контролировало свое выполнение, управление передается некоторому
другому программному обеспечению — в данном случае фреймворку Spring.  

Благодаря контейнеру IoC, который часто называют контекстом Spring, объекты
становятся видимыми для Spring, и фреймворк может их использовать в соответствии с заданной вами конфигурацией.  


Нам необходимо включать бины в контекст Spring, потому что
именно так мы сообщаем Spring, какими экземплярами объектов приложения
должен управлять фреймворк

Существуют следующие способы включить бин в контекст (далее
мы рассмотрим их подробнее):
* посредством аннотации @Bean;
* посредством стереотипных аннотаций;
* программно
### @Bean
Добавление зависимости 
```xml
<dependencies>
 <dependency>
 <groupId>org.Springframework</groupId>
 <artifactId>Spring-context</artifactId>
 <version>5.2.6.RELEASE</version>
 </dependency>
 </dependencies>
```

Создание экземпляра зависимости 
```java
public class main {
 public static void main(String[] args) {
 var context =
 new AnnotationConfigApplicationContext();
 Parrot p = new Parrot();
 }
}
```
Для добавления экземпляра класса в контекст Spring необходимо

1. Определение конфигурационного класса в проекте
если необходимо, чтобы Spring управлял этим объектом и мог расширить
его возможности за счет своего функционала. Если объект не нуждается
в возможностях, предоставляемых фреймворком, то не следует делать
его бином.
 * Если нужно сделать объект бином и разместить его в контексте Spring,
то бин должен быть одиночным только в случае, если он неизменяемый.
Постарайтесь не создавать изменяемые одиночные бины.
 * Если бин все же должен быть изменяемым, лучше использовать прототипную
область видимости.
```java
@Configuration
public class ProjectConfig {
}
```
2.Определение метода @Bean
```java
@Configuration
public class ProjectConfig {
 @Bean
 Parrot parrot() {
 var p = new Parrot();
 p.setName("Koko");
 return p;
 }
}
```
Класс конфигурации позволяет, в частности, добавлять бины в контекст
Spring. Для этого нужно определить метод, возвращающий экземпляр объекта, который мы хотим добавить в контекст, и снабдить этот метод аннотацией
@Bean. Она сообщит Spring о том, что при инициализации контекста нужно
вызвать данный метод и добавить возвращенное им значение в контекст.

Инициализация контекста Spring на основании созданного класса конфигурации и обращение к экземпляру Parrot из контекста
 ```java
public class main {
 public static void main(String[] args) {
 var context =
 new AnnotationConfigApplicationContext(
 ProjectConfig.class);
 Parrot p = context.getBean("parrot2", Parrot.class);
 System.out.println(p.getName());
 }
}
```

Что бы изменить имя бина
* @Bean(name = "miki");
* @Bean(value = "miki");
* @Bean("miki").

Если будет несколько бинов одного типа то, чтобы сделать бин по умолчанию необходимо указать @Primary  


### Стереотипные аннотации

Применение стереотипной аннотации к классу Parrot
```java
@Component
public class Parrot {
 private String name;
 public String getName() {
 return name;
 }
 public void setName(String name) {
 this.name = name;
 }
}

```
Использование аннотации @ComponentScan, чтобы сообщить Spring,
где находятся классы со стереотипными аннотациями

```java
@Configuration
@ComponentScan(basePackages = "main")
public class ProjectConfig {
}

```
В программе пустой конфигурационный файл, при этом Spring сам добавляет бины в контекст самостоятельно, поэтому возможен только один экземпляр
### Программное добавление бина

```java
public static void main(String[] args) {
 var context =
 new AnnotationConfigApplicationContext(
 ProjectConfig.class);
 Parrot x = new Parrot();
 x.setName("Kiki");
 Supplier<Parrot> parrotSupplier = () -> x; // функциональный интерфейс, для того чтобы возращать значения
 context.registerBean("parrot1",
 Parrot.class, parrotSupplier)
}
```

### Когда использовать @Component, а когда @Bean?

@Component лучше использовать в случаях, когда мы можем изменить класс и он принадлежит проекту (является его частью), а иначе @Bean

### Создание связей между бинами
Применение аннотации @Qualifier

```java
@Configuration
public class ProjectConfig {
 @Bean
 public Parrot parrot1() {
 Parrot p = new Parrot();
 p.setName("Koko");
 return p;
 }
 @Bean
 public Parrot parrot2() {
 Parrot p = new Parrot();
 p.setName("Miki");
 return p;
 }
 @Bean
 public Person person(
 @Qualifier("parrot2") Parrot parrot) {
 Person p = new Person();
 p.setName("Ella");
 p.setParrot(parrot);
 return p;
 }
}
```
Если при внедрении бина, в контексте будет несколько бинов одного типа, то конструктор выберет бин, чьё имя будет совпадать с параметром

```java
@Configuration
public class ProjectConfig {
 @Bean
 public Parrot parrot1() {
 Parrot p = new Parrot();
 p.setName("Koko");
 return p;
 }
 @Bean
 public Parrot parrot2() {
 Parrot p = new Parrot();
 p.setName("Miki");
 return p;
 }
 @Bean
 public Person person(
 @Qualifier("parrot2") Parrot parrot) {
 Person p = new Person();
 p.setName("Ella");
 p.setParrot(parrot);
 return p;
 }
}
```
### Нужен ли объетк в контексте Spring?

DI - Объект, нужный нам для добавления в контекст Spring,
либо имеет зависимость, которую мы хотим внедрить из контекста, либо сам является такой зависимостью.

### Как выбрать одну реализацию интерфеса, если их несколько

```java
@Component
@Qualifier("PUSH") // С помощью аннотации @Qualifier присваиваем реализации имя PUSH
public class CommentPushNotificationProxy
 implements CommentNotificationProxy {
 // код класса
}

@Component
@Qualifier("EMAIL") // С помощью аннотации @Qualifier присваиваем реализации имя EMAIL
public class EmailCommentNotificationProxy
 implements CommentNotificationProxy {
 // код класса
}


@Component
public class CommentService {
 private final CommentRepository commentRepository;
 private final CommentNotificationProxy commentNotificationProxy;
 public CommentService(
 CommentRepository commentRepository,
 @Qualifier("PUSH") CommentNotificationProx
commentNotificationProxy) {
 this.commentRepository = commentRepository;
 this.commentNotificationProxy = commentNotificationProxy;
 }
 // остальной код класса
}
```

### ТРИ ГЛАВНЫХ ПРАВИЛА ИСПОЛЬЗОВАНИЯ БИНОВ
 * Размещайте объект в контексте Spring в виде бина только в том случае,


### Немедленная и ленивая загрузка

При немедленной загрузке бины создаются во время инициализации и это является вариантом по умолчанию. Существует возможность, чтобы бины создавались при первом обращении к нему, для этого необходимо указать аннотацию @Lazy перед классом.

### Прототипная и одиночная область видимости 
Одиночный бин - «одиночный» означает уникальность имени, но не уникальность наличия в пределах приложения.
Прототипный бин - каждый раз, когда запрашивается
ссылка на прототипный бин, Spring создает новый экземпляр объекта.Что бы бин сделать прототипным, надо указать @Scope(BeanDefinition.SCOPE_PROTOTYPE)


## Аспектно-ориентированное программировани

Аспект — это просто часть логики, которую фреймворк реализует, вызывая
определенные, выбранные вами методы.  
При разработке аспекта нужно определить следующее:
* какой код должен выполнять Spring при вызове данных методов. Именно
это и называется аспектом;
* когда приложение должно выполнять логику аспекта (например, перед, после
или вместо вызова метода). Это называется советом;
* выполнение каких методов должен перехватывать фреймворк и реализовывать аспект. Это называется срезом.

## Разработка Web-приложений

Сервлет — точка входа в логику приложения, компонент, с которым напрямую взаимодействует контейнер сервлетов (в данном случае Tomcat). Когда контейнер получает HTTP-запрос, он вызывает метод
объекта сервлета, которому передает этот запрос в виде параметра

## Транзакции

Транзакция — это определенный набор изменяющих операций, которые либо выполняются корректно все, либо не выполняются вообще. Подобное явление называется атомарностью. Транзакции —
необходимая часть приложений, они гарантируют согласованность данных
в случае, если один из этапов сценария использования, выполняемый после
изменения данных, завершится неудачно. 