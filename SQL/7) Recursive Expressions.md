---
# **7) Recursive Table Expression (WITH RECURSIVE ... UNION ...):**
---
#Uses for selecting data from tree, graph data structures:  
#1) Graph:  
![link](https://www.geeksforgeeks.org/wp-content/uploads/undirectedgraph.png)

#2) Tree:  
![link](https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png)

#  **- Example:**  
#Existing tables:  
![link](https://drive.google.com/uc?id=1L3E-C_UqVILAxJy9IoaEkfysbeqmpYg5)
#Selecting data-structure:  
![link](https://drive.google.com/uc?id=10NuwlES_8xGNwylOC1SKcev48vwh3Ub6)
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
    WHERE depth < 3
)
SELECT DISTINCT users.id, users.name
FROM related_followers
JOIN users ON users.id = related_followers.user_id
WHERE depth > 1
 ```

1) related_followers:  
![link](https://drive.google.com/uc?id=10TmSEdsQf-fR_qP8v68xrxjPxPB3dJLU)
   
2) joined tables:  
![link](https://drive.google.com/uc?id=1aNdGli0NbknZ5rWIjRUMgkYarsmFvPWE)
   
3) result:  
![link](https://drive.google.com/uc?id=1kqz2iMNgS9GAeltinTZfAmuADWuKQF6d)