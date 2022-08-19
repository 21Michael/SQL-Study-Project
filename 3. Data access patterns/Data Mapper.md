# Data Mapper pattern:

**The Data Mapper** is a layer of software that separates the in-memory objects from the 
database. Its responsibility is to transfer data between the two and also to isolate them 
from each other. With Data Mapper the in-memory objects needn't know even that there's a 
database present; they need no SQL interface code, and certainly no knowledge of the database 
schema. (The database schema is always ignorant of the objects that use it.) Since it's a form 
of Mapper (473), Data Mapper itself is even unknown to the domain layer.

## Example:
![link](https://drive.google.com/uc?id=1Sa2xqGL_cSq-cC1Rztp8IOhf_-fC4gpb)

## Usage:
```js
    // Service Citie:
    class Citie {
      constructor({ name, population, area, mayor }) {
        this.name = name;
        this.population = population; 
        this.area = area; 
        this.mayor = mayor;
      }
      // buisness logic methods...
    }
    
    // Service Citie built as data mapper:
    class CitieDAO {
      constructor({ db }) {
        this.db = db;
      }
      save({ name, population, area, mayor }) {
        this.db.query(`
            INSERT INTO cities
            SET (population, name, area, mayor)
            VALUES (${population}, ${name}, ${area}, ${mayor})
        `)
      }
      // DB logic methods...
    }
    
    // Usage:
    const citie = new Citie({ name, population, area, mayor });
    const citieDAO = new CitieDAO({ db });
    
    citieDAO.save({ 
      name: citie.name, 
      population: citie.population, 
      area: citie.area, 
      mayor: citie.mayor 
    });
```

## Pros:
  - Каждый объект имеет свою зону ответственности, тем самым следую принципам SOLID и 
    сохраняя каждый объект простым и по существу.
  - Бизнес-логика и сохранение данных связаны слабо, и если вы хотите сохранять данные в 
    XML-файл или какой-нибудь другой формат, вы можете просто написать новый Mapper, не
    притрагиваясь к доменному объекту.
## Cons:
  - Вам придется гораздо больше думать, перед тем как написать код.
  - В итоге у вас больше объектов в управлении, что немного усложняет код и его отладку.
