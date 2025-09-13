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

  
