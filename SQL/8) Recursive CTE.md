---
# **7.1) Recursive Table Expression (WITH RECURSIVE ... UNION ...):**
---
#Uses for selecting data from tree, graph data structures:  
#1) Graph:  
![link](https://www.geeksforgeeks.org/wp-content/uploads/undirectedgraph.png)

#2) Tree:  
![link](https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png)

#  **- Example:**
#Selecting data-structure:  
![link](https://drive.google.com/uc?id=10NuwlES_8xGNwylOC1SKcev48vwh3Ub6)

#Existing tables:
![link](https://drive.google.com/uc?id=1wekoVSPF3eOnguG2vlRGZJuYs2opKuzK)

#Code:  
 ```sql
WITH RECURSIVE related_followers(follower_id, user_id, depth) AS (
    SELECT follower_id, user_id, 1 AS depth
    FROM followers
    WHERE follower_id = 9
  UNION
    SELECT followers.follower_id, followers.user_id, depth + 1
    FROM followers
    JOIN related_followers ON related_followers.user_id = followers.follower_id
    WHERE depth <  3
)
SELECT DISTINCT users.id, users.name
FROM related_followers
JOIN users ON users.id = related_followers.user_id
WHERE depth = 2
 ```
#Code flow:
## 1) First query computation:
 ```sql
    SELECT follower_id, user_id, 1 AS depth
    FROM followers
    WHERE follower_id = 9
 ```
![link](https://drive.google.com/uc?id=1ijYyIsbp0AAJhRNUg7CCLuHTGggKvt24)
## 2) Recursion query computations (select from joined tables: first query computation table and followers table) till depth < 3:
 ```sql
    SELECT followers.follower_id, followers.user_id, depth + 1
    FROM followers
    JOIN related_followers ON related_followers.user_id = followers.follower_id
    WHERE depth <  3
 ```
Process:  
![link](https://drive.google.com/uc?id=1xb30o0lBSX27_dUgBmS-j5pJNMwa8QEO)
   
Result:  
![link](https://drive.google.com/uc?id=1R1txYMx_aHWD36TSmTgX8NJ658xL-t-D)

## 3) join users tables with related_followers table:  
 ```sql
    JOIN users ON users.id = related_followers.user_id
    WHERE depth = 2
 ```
![link](https://drive.google.com/uc?id=113qoUIq1pGxy7YCanlxvK4chiTQv4YiP)
   
## 4) Result:  
 ```sql
  SELECT DISTINCT users.id, users.name
  FROM related_followers
  JOIN users ON users.id = related_followers.user_id
  WHERE depth = 2
 ```
![link](https://drive.google.com/uc?id=1tr8ihBQe84xi9vb5VTsgMQWcr97rzfr0)
