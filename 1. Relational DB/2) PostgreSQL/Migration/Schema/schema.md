# 1) Schema migration:

---

## Git review problem:
![link](https://drive.google.com/uc?id=1dZuhZmh72tDk-mdAzoCkgIyDM0Hm8BIg)

## Deployment db changes problem: 

**Problem:**  
![link](https://drive.google.com/uc?id=1sJfkpqeo7g23oJJTZX6coWg5GGiUFnoG)

**Solving:**
![link](https://drive.google.com/uc?id=1EXoRW5h3bTeYJqdMHEiDGaNd4NQUO9vx)

## Migration file structure:
![link](https://drive.google.com/uc?id=1fMszrinGO6mnuTn-8obhpKykILr5ImUy)
```js
exports.shorthand = undefined;

exports.up = pgm => {
  pgm.sql(`
    ALTER TABLE cities
    RENAME COLUMN population to amount_of_citizen;
  `);
};

exports.down = pgm => {
  pgm.sql(`
    ALTER TABLE cities
    RENAME COLUMN amount_of_citizen to population;
  `);
};
```
## Packages:  
![link](https://drive.google.com/uc?id=1ipzkP7RoKLow1_Ku5Zw7dkFk2bqbmfMc)

