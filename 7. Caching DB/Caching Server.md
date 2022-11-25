# Caching Server:
**<ins>Caching</ins>** is the process of storing file copies in a cache server for quick
access. While a cache is any temporary storage location for data or files,
the term is commonly used when referring to internet technologies.

**<ins>DNS servers</ins>** are used to cache DNS records for easier lookup access, CDN server
cache content for reduced latency while web browsers cache JavaScript, HTML 
files, and images to ensure websites can load faster.

## Types of caching:
  - **<ins>Database caching:</ins>**   
    Database caching makes it possible for you to increase the throughput by 
    lowering latency in data retrieval when it comes to backend databases.
    You can apply a database cache in any type of database, including NoSQL 
    and relational databases. Common methods that can be used to load data 
    to a cache include write-through methods and lazy loading.
      - **Write-through strategy:**  
        The write-through strategy adds data or updates data in the cache
        whenever data is written to the database.  
        ![link](https://drive.google.com/uc?id=1N1wJxKEg9vTW_A6kMrXC47auHaKcnuAB)
     
      - **Lazy loading strategy:**  
        Lazy loading is a caching strategy that loads data into the cache 
        only when necessary.  
        --  
        Cache is an in-memory key-value store that sits between your 
        application and the data store (database) that it accesses. Whenever
        your application requests data, it first makes the request to the
        cache. If the data exists in the cache and is current, Cache returns
        the data to your application. If the data doesn't exist in the cache
        or has expired, your application requests the data from your data 
        store. Your data store then returns the data to your application. 
        Your application next writes the data received from the store to 
        the cache. This way, it can be more quickly retrieved the next time
        it's requested.  
        ![link](https://drive.google.com/uc?id=1xRmYj9o4f4WNXIp08vJ1Qy2QQ6lCFSz3)

  - **<ins>General cache:</ins>**  
    For use-cases that do not need disk-based durability or transactional
    data support, using in-memory key-value data storage as a standalone 
    database is an effective way of building high performance applications.  
    --  
    Apart from improved speeds, applications also record improved throughput
    at a lower price point. General cache can be used for referenceable 
    data like category listings, product grouping and profile information.  
    ![link](https://drive.google.com/uc?id=1w-X2iTwmqsCPCSBmgRbv4cU_Qzwum7Sc)

  - **<ins>CDN caching:</ins>**   
    A content delivery network or a CDN is a network that caches web content
    like videos, images or webpages in proxy servers located close to the 
    origin server being used by web users. Because of the proximity of the 
    proxy server to the user making the requests, a content delivery network
    delivers the content requested faster.  
    ![link](https://drive.google.com/uc?id=1rVW7AlsyAFZqptSUf00TiXiq6oxAZOiT)
