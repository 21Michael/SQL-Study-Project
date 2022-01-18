# Data Mapper pattern:

**The Data Mapper** is a layer of software that separates the in-memory objects from the 
database. Its responsibility is to transfer data between the two and also to isolate them 
from each other. With Data Mapper the in-memory objects needn't know even that there's a 
database present; they need no SQL interface code, and certainly no knowledge of the database 
schema. (The database schema is always ignorant of the objects that use it.) Since it's a form 
of Mapper (473), Data Mapper itself is even unknown to the domain layer.

![link](https://drive.google.com/uc?id=1Sa2xqGL_cSq-cC1Rztp8IOhf_-fC4gpb)