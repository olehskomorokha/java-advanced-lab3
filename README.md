# SQL queries creator for CRUD operations

## Автор
- **Скомороха Олег Ігорович**
- **Телеграм**: [@olegskomoroha](https://t.me/olegskomoroha)
- **Email**: [oleg.skomoroha1@gmail.com](mailto:oleg.skomoroha1@gmail.com)

## Група
ІО-25

## Опис проєкту
Цей проект демонструє динамічну генерацію SQL-запитів для роботи з базами даних за допомогою Java.
Він підтримує створення таблиць, вставку, оновлення, видалення та вибірку даних. 
У проекті використовується рефлексія та анотації для автоматизації SQL-операцій, 
а також ручні SQL-генератори для специфічних класів.

## Особливості

- **Динамічна генерація SQL**: Використання рефлексії для автоматичного створення запитів на основі анотацій Java-класів.
- **Генерація без рефлексії**: Окремі генератори для кожного класу з ручним створенням SQL-запитів.
- **CRUD-операції**: Підтримка операцій створення, вставки, вибірки, оновлення та видалення даних.

## Структура проєкту

### Анотації

#### `@Table`
Анотація для класу, що вказує відповідність між класом Java та таблицею бази даних.  
**Параметр:**
- `name` — назва таблиці.

#### `@Column`
Анотація для полів класу, що вказує відповідність між полем Java та колонкою таблиці.  
**Параметр:**
- `name` — назва колонки.

### SQL Генератори

#### `SqlGenerator<T>`
Універсальний клас для динамічної генерації SQL-запитів за допомогою рефлексії.  
**Методи:**
- `generateCreate()` — створює SQL-запит для створення таблиці.
- `generateInsert(T instance)` — створює SQL-запит для вставки даних.
- `generateUpdate(T instance, String condition)` — створює SQL-запит для оновлення даних.
- `generateDelete(String condition)` — створює SQL-запит для видалення даних.

#### `UserSQLGenerator`, `ProductSQLGenerator`, `OrderSQLGenerator`
Специфічні генератори для класів `User`, `Product`, `Order`. Вони створюють SQL-запити без використання рефлексії.  
**Методи:**
- `generateCreate()` — створює SQL-запит для створення таблиці.
- `generateInsert(Object instance)` — створює SQL-запит для вставки даних.
- `generateUpdate(Object instance, String condition)` — створює SQL-запит для оновлення даних.
- `generateDelete(String condition)` — створює SQL-запит для видалення даних.

### Класи

#### `User`
Користувач із полями:
- `id` (primary key)
- `name`
- `age`

#### `Product`
Продукт із полями:
- `id` (primary key)
- `title`
- `price`

#### `Order`
Замовлення із полями:
- `orderId` (primary key)
- `userId`
- `amount`

## Приклад використання

### Генерація SQL-запитів

```java
// Створення екземплярів
User user = new User(1, "John Doe", 30);
Product product = new Product(101, "Laptop", 1500.0);
Order order = new Order(5001, 1, 1500.0);

*/Генерація SQL із використанням специфічних генераторів
UserSQLGenerator userGenerator = new UserSQLGenerator();
System.out.println(userGenerator.generateCreate());
System.out.println(userGenerator.generateInsert(user));
System.out.println(userGenerator.generateUpdate(user, "id = 1"));
System.out.println(userGenerator.generateDelete("id = 1"));
```

## Очікувані результати
- Динамічна генерація SQL за допомогою рефлексії спрощує підтримку та автоматизацію.
- Генерація SQL без рефлексії забезпечує швидкість, але потребує більше коду.
