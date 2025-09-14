## Singleton Design pattern

> It allows us to create ONLY ONE INSTANCE of a class.

<details>
  <summary>
    <h2>Problems</h2>
  </summary>


  1. ``Logger``
     
     Logger writes the details to a file. Lets say we have three classes: Class A, Class B and Class C. If we create a new instance of Logger class in all
     the three classes, then for all of them it will write logs to three different files, i.e. one file for each class will be created. Which is not expected,
     as we would want to see the entire log in one place.

  2. ``DB Connection``

     Maintaining multiple DB connections unnecessarily is resource heavy.

     Establishing a connection involves network handshake, authentication, allocating server resources, etc. If every requests opens a new DB connection and closes
     it immediately, the system spends more time connecting than actually querying.

  3. ``Thread pool`` ---- @TODO need to get a better understanding from gogu

  4. ``Cache manager``

     Cache manager: it stores data in memory(key-value format, like a dictionary/map).

     If every component of an application created its own cache then: we would have multiple, inconsistent copies of data, as updates in one cahce would not be
     reflected on the other. Memory would skyrocket.

     ``Why use singleton cache?``

     All parts of the system talk to the same cache. Data consistency, and memory efficiency are maintained.

  5. ``Configuration manager``

     App wide settings like: DB connection strings, API keys, feature flags etc. should be consistent throught the app. A singleton config manager ensures every
     part of the app uses the same config without reloading or duplicating.

     
</details>


<details>
  <summary>
    <h2>
      When to use singleton design pattern?
    </h2>
  </summary>

1.  Shared Resources
2.  Single source of truth/Consistency
3.  Creating multiple instances is resource intensive.
  
</details>



<details>
  <summary>
    <h2> Implemetation steps</h2>
  </summary>

  - How can we create a class, s/t no other classes can create an instance of it/no objects can be created for it?

    We can mark its constructor as ``private``, because in order to create an object the constructor gets called.

    Now, we have successfully prevented the creation of object/instance of this class by ``Constructor hiding``.

    ```java

    public class Database{
      private Database(){
      }
    }
    
    ```

    The above code restricts the initialization of the Database class. Now, we need to create a ``Global access point`` to get the instance of the Database
    class. We can do this by creating a static method(i.e Static initializer) that returns the instance of the class. If instance does not exists, it should
    create an instance and then return it.
    
    ``Static Initializer``: a static method which creates an instance/object of a class. This is static method is also known as a ``Global access point``.

- ``Why to use a static method?``
      If this is a non-static method, then in order to call it, we would need an object of a class. However, we don't have the object of the class and our goal
      here is to create that/get the instance, using the static initializer itself.

- ❌

  ```java

  public class Database{
      private Database(){
      }
    
      public static Database getInstance(){
          return new Database();
      }
  }

  ```

   - According to the above implementation, how many instances of the class be created?
   It will create multiple instances, as each time the static initializer will be called, it'll create a new instance. So, this implementation violates the
  purpose of singleton.

- ✅ So how do we ensure only only instance is returned from the static initializer

``getInstance()``
    
- check if an object
  - if exists, then return it.
  - otherwise, create a new object
  
- save the object

- Now the question is, where to store this instance?
  
  We'll be storing the instance in a static attribute. Because:
  - ``Static belongs to the class, not the object``: in order to access a non-static attribute, we'll need the object of the class, but in singleton we want to
    create the object itself and make it globally available. If instance is stored in static field it is tied to the class itself(and not to any object).
  - ``Guarantees only one copy exists``: static variable exists only one per classholder, regardless of the number of time we access it. If it was non-static,
    then every call to the static initializer would create a new instance --- which violates the singleton rule                

## STEPS

1. Constructor hiding
2. Creating a Global access point(static initializer/static method which creates object of the class)
3. Static attribute (to store the instance of the class)
4. Logic: if instance ----> return it; otherwise create an instance and store it and then return.

</details>











### miscellaneous

- every object that spring creates is singleton -- and it is called Beans. @TODO ---- understand this from gogu
  
