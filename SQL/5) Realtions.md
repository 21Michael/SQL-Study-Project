#5) Relations between tables:

---

## - Concepts: ONE TO MANY / MANY TO ONE:
![link](https://drive.google.com/uc?id=1Hk3QN_KgQsuucXoiz8sS_eSm1rrLmqVB)

## - Create tables with relation (PRIMARY KEY, REFERENCES):
 ```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50)
);

INSERT INTO users (username)
VALUES
	('monahan93'),
  ('pferrer'),
  ('si93onis'),
  ('99stroman');

CREATE TABLE photos (
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id)
);

INSERT INTO photos (url, user_id)
VALUES
	('http://two.jpg', 1),
  ('http://25.jpg', 1),
  ('http://36.jpg', 1),
  ('http://754.jpg', 2),
  ('http://35.jpg', 3),
  ('http://256.jpg', 4);
 ```
Result: 
 1) users

| id   | username  |
|------|-----------|
| 1    | monahan93 |
| 2    | pferrer   |
| 3    | si93onis  |
| 4    | 99stroman |

2) photos

 | id   | url               | user_id  |
 |------|-------------------|----------|
 | 1    | http://two.jpg    | 1        |
 | 2    | http://25.jpg     | 3        |
 | 3    | http://36.jpg     | 4        |
 | 4    | http://754.jpg    | 2        |
 | 5    | http://35.jpg     | 2        |
 | 6    | http://256.jpg    | 2        |
 
![link](https://drive.google.com/uc?id=1T0fglgZVUTgzWr7az4EuvhgpzBP9VfZI)


# 5.1) Select data from joined tables (JOIN ON):  

---

 - **Basic:**
 ```sql
 SELECT url, username FROM photos
 JOIN users ON users.id = photos.user_id;
 ```
Result:

 | url               | username  |
 |-------------------|-----------|
 | http://two.jpg    | monahan93 |
 | http://754.jpg    | pferrer   |
 | http://35.jpg     | pferrer   |
 | http://256.jpg    | pferrer   |
 | http://25.jpg     | si93onis  |
 | http://36.jpg     | 99stroman |
 
 - **If id of table1 doesn't exist in table2:**  
 ```sql
 SELECT * FROM photos
 ```
1) users

 | id   | username  |
 |------|-----------|
 | 1    | monahan93 |

2) photos

 | id   | url               | user_id  |
 |------|-------------------|----------|
 | 1    | http://two.jpg    | 2686     |
 
Result: **Error**    
 - **If id of table1 doesn't exist in table2 (id: NULL):**  
1) users

 | id   | username  |
 |------|-----------|
 | 1    | monahan93 |

2) photos

 | id   | url               | user_id  |
 |------|-------------------|----------|
 | 1    | http://two.jpg    | null     | 
 
Result:

 | id   | url               | user_id  |
 |------|-------------------|----------|
 | 1    | http://two.jpg    | null     |

 - **If column with same name repeated in both tables (table.column):**
 ```sql
SELECT photos.id FROM photos
JOIN users ON users.id = photos.user_id;
 ```
![link](https://drive.google.com/uc?id=1Ruokio9nZ2kiyAZgouDzGpNQ-f6PdATz)

 - **If some of the rows doesn't have relation (JOIN TYPES):**  

![link](https://drive.google.com/uc?id=1JvMmO2aZzxLMbyT3_6KEfhcNN014CV4a)

 - **Filter joined data (JOIN + WHERE):**
 ```sql
SELECT url, contents
FROM comments
JOIN photos ON photos.id = comments.photo_id;
WHERE comments.user_id = photos.user_id;
 ```
![link](https://drive.google.com/uc?id=10jVMi3Z_JRnBeFJhTAzgmRkgKtsHTQ5T)

 - **Join 3 tables (JOIN ON):**
 ```sql
SELECT contents, url, username
FROM comments
JOIN photos ON photos.id = comments.photo_id;
JOIN users ON users.id = photos.user_id AND users.id = comments.user_id
 ```
![link](https://drive.google.com/uc?id=1Io8I2dBaQszIkWCqsgRBfsQ8Gpu6EqfA)

# - Delete joined data (ON DELETE):  
 - **Basic:**
 ```sql
DELETE FROM users WHERE id = 1;
 ```
result: **Error**    
 - **Cascade:**
 ```sql
CREATE TABLE photos (
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id)
  ON DELETE CASCADE
);

DELETE FROM users WHERE id = 1;
 ```
result:

| id   | url               | user_id  |
|------|-------------------|----------|
| 2    | http://25.jpg     | 3        |
| 3    | http://36.jpg     | 4        |
| 4    | http://754.jpg    | 2        |
| 5    | http://35.jpg     | 2        |
| 6    | http://256.jpg    | 2        |

 - **Set null:**
 ```sql
CREATE TABLE photos (
  id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id)
  ON DELETE SET NULL
);

DELETE FROM users WHERE id = 1;
 ```
result:

| id   | url               | user_id  |
|------|-------------------|----------|
| 1    | http://two.jpg    | null     |
| 2    | http://25.jpg     | 3        |
| 3    | http://36.jpg     | 4        |
| 4    | http://754.jpg    | 2        |
| 5    | http://35.jpg     | 2        |
| 6    | http://256.jpg    | 2        |

![link](https://drive.google.com/uc?id=1JyxYvcPwbZIWnjYBVBrqJzn4e9hw6UJh)