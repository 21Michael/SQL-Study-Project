# Active Record pattern:
**Active Record** обеспечивает объектно-ориентированный интерфейс для доступа и манипулирования данными,
хранящимися в базах данных. Класс Active Record соответствует таблице в базе данных, 
объект Active Record соответствует строке этой таблицы, а атрибут объекта Active Record представляет 
собой значение отдельного столбца строки. Вместо непосредственного написания SQL-выражений вы сможете
получать доступ к атрибутам Active Record и вызывать методы Active Record для доступа и манипулирования
данными, хранящимися в таблицах базы данных.

![link](https://habrastorage.org/r/w1560/getpro/habr/post_images/df2/419/56b/df241956b214111c8f04421c275e4037.png)

## Example:

![link](https://drive.google.com/uc?id=1WUWCiErL623bMI9gQaPvCzmrfogvb-gf)

## Usage:
```js
    // Service Citie built as active record:
    class Citie {
      constructor({ db, name, population, area, mayor }) {
        this.db = db;
        this.name = name;
        this.population = population; 
        this.area = area; 
        this.mayor = mayor;
      }
      save() {
        this.db.query(`
            INSERT INTO cities
            SET (population, name, area, mayor)
            VALUES (${this.population}, ${this.name}, ${this.area}, ${this.mayor})
        `)
      }
      // DB logic methods... + buisness logic methods...
    }
    
    // Usage:
    const citie = new Citie({ db, name, population, area, mayor });
    citie.save();
```

## Pros:
  - Self-descriptive
  - Good choice for domain logic that isn’t too complex, such as creates, reads, updates, and deletes.
    Derivations and validations based on a single record work well in this structure.
  - Easy to implement;
## Cons: 
  - On its own, the pattern encourages tight coupling between domain objects and your database. 
    Every domain object knows about the database, tables, and schemas. This statement also implies 
    that the pattern **violates the single responsibility principle.**
  - Because the domain objects are mapped to the database schema, project **refactoring becomes more 
    difficult** as changes in one, either domain or database design, will force you to adjust the other.
  - It also **increases the complexity of the logic in your domain objects as they will have to deal 
    with both business logic concerns as well as database access (persistence concerns).** A lot of 
    relationships, inheritance, sophisticated entities and complex queries may make your code quite 
    messy if you do not adapt patterns to tackle those problems.
