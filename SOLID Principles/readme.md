<details> <summary> <h2> Introduction </h2> </summary> 

The SOLID Principle was introduced by Robert C. Martin, also known as Uncle Bob.


SOLID Principles are the 05 principles of Object-Oriented Design(OOD). They are the rules and best practices to follow while designing a class structure.
SOLID is the acronym for the below 05 principles:-


<br>

S: Single Responsibility Principle(SRP)

O: Open/Closed Principle 

L: Liskov Substitution Principle(LSP)

I: 

D: 

## Advantages of following the SOLID Principles:-


1. Reduce code ``redundancy``(i.e. duplication of code).
2. Results in loose ``coupling``.
3. Makes software ``flexible``.
4. Reduces ``complexity``.
5. Easy to ``understand``.
6. Easy to ``maintain``.


> What is coupling?

It is the degree of interdependence of modules or classes.


Tight Coupled: Modules/Classes are called tightly coupled if they are highly dependent on each other. It should be avoided, because, if we make changes in one module/class it will affect the others' dependent 
modules/classes.


Loose Coupled: Modules/Classes are called loosely coupled if they are independent of each other. A loosely coupled code is considered better because changes in one module/class won't affect any other modules/classes.
Therefore, it makes our code flexible, stable, maintainable, and reusable.

</details>


<details> <summary> <h2> Single Responsibility Principle </h2></summary>

It states that:-

1. A Module should have **only ONE reason to change**.
2. A Module should have **only ONE responsibility**. 

        MODULE: here module refers to class or method or package. 

NOTE: It means it should focused/concerned with ONLY one SPECIFIC task.

- According to SRP, whenever we have n number of reasons for a class to change then, there must be n different classes to handle each responsibilities, so that whenever we need to make a 
change then it can be done in an organised manner and without affecting other modules.


### EXAMPLE-1

```java

class Invoice{
    public calculateInvoice(){
        // logic to find out invoice
        int total = price * quantity;
        return total;
    }

    public void printInvoice(){
        // print the invoice
    }

    public void saveToDB(){
        // save the invoice to db
    }
}


```

In the above example, we can see that there are 03 reasons for the class to change, i.e.:-

1. If in the future we come up with a different logic to calculate the invoice, like if we introduce tax in its calculation, then our business logic will change.
2. If we change the printing logic.
3. If we want to save the invoice in the file instead of a db.

So we can see that there are 3 reasons for the class to change and hence it doesn't have a single responsibility, so we need to re-write it such that it follows the SRP.

### Code following SRP

In the below code, each of the classes has only ONE ``responsibility`` and only ``ONE reason to change``, hence it follows SRP.



```java

class InvoiceCalculator{
    public int calculateInvoice(){
        // logic to calculate invoice    
    }
}


class InvoicePrinter{
    public void printInvoice(){
        // logic to print invoice
    }
}


class InvoiceSaver{
    public void saveToDB(){
        // saves invoice to db
    }
}


```


<br>

### Why to follow SRP?

If we have a class that handles many responsibilities then it will have many reasons to change, and if we make a change in the logic of any of the methods then it might affect the other methods. Additionally, it becomes very complex, and difficult to understand and maintain, if all the logic is written inside a single class. 



### EXAMPLE-2

Let's say we have a class and it is sending a message to the server. Now, below are the possible reasons for the class to change.

|    |  Reasons  | Earlier   | Now   |
| ------- | -----   | --------   | ----------   |
| 1.   |  Protocol change |  HTTP  | HTTPS   |
| 2.   |  Message format | JSON   |  HTML  |
| 3.   |  Communication Security Change  |  no authentication  | authentication required   |

Now, the above class has 03 reasons to change, so it is not following SRP. We must write individual classes for each tasks, in-order to make it follow SRP.


</details>

<br>

  
<details>  <summary>  <h2>  Open-Close Principle  </h2>  </summary>  

It states that a class should be ``OPEN for Extension`` but ``CLOSED for Modification``.

Modification: It means to make changes in the existing code.

Extension: It means adding new functionalities without altering/touching the existing code.

- Open for Extension: extend existing behaviour.

- Closed for Modification: existing code remains unchanged

Example:- 

If we have a class InvoiceSaver that currently saves the data in the DB, but now we want to save the data in the file as well. So, we have modified the InvoiceSaver class by adding the method saveToFile that saves the data to a file, as shown below👇But is this a good approach🤔? The answer is NO❌. 

| Before Modification  | After Modification |
|  ----  |  ----  |
|  ![image](https://github.com/Shweta2024/LLD/assets/75883328/25f925ef-adad-49fa-98a1-0e8c87555c77) |  ![image](https://github.com/Shweta2024/LLD/assets/75883328/45b2c9bf-5430-4791-a91b-cd911b22f1e9)   |




> Why follow the Open/Close principle?

In real-life scenarios, the code that we deal with is tested, reliable, and live i.e. on production, so it is always a better approach to EXTEND the functionalities instead of making modifications in the existing code because it makes our code subjected to potential bugs. Below is the updated code that follows the Open/Close Principle:-





> How are we going to add new functionality without touching the existing code?

We'll achieve that by using ``Interfaces`` and ``Abstract classes``.


## Code following Open/Close Principle

```java

// interface
interface InvoiceSaver{
    public void saveInvoice();
} 


class SaveInvoiceToDB implements InvoiceSaver{

    @override
    public void saveInvoice(){
        // logic to save to DB
    }     
}


class SaveInvoiceToFile implements InvoiceSaver{

    @override
    public void saveInvoice(){
        // logic to save to File
    }
}


```

So, whenever we'll have a new functionality we'll just extend it:-

```
                  
                      InvoiceSaver
        /             |                \        \
SaveInvoiceToDB    SaveInvoiceToFile    X       Y.....(any new functionality/extension)

```

</details>



<details>   <summary>      <h2> Liskov Substitution Principle(LSP) </h2>        </summary>        

- We should be able to substitute the object of the base/parent class with the object of the child class, without breaking the behaviour of thr program.
- Eg.: If Class B is a subclass of Class A, then we should be able to replace the object of Class A with the object of Class B, without breaking the behaviour of the program.
- So, it basically means that if the object of the parent class was providing a certain behaviour, then on substituting the object with that of the child class must not alter the behaviour. So, whatever is expected to happen should happen even if we change the base class object with the child class object. 

          NOTE: Subclass should extend the funtionalities of the parent class not narrow it down. 


### EXAMPLE:-

```java


interface Vehicle{
    void turnOnEngine();
    void accelerate();
}


class Bike implements Vehicle{
    
    boolean isEngineOn;
    int speed;

    public void turnOnEngine(){
        // logic to turn on the engine
        isEngineOn = true;
    }
    
    public void accelerate(){
        speed = speed + 20;
    }
}


class Cycle implements Vehicle{
    
    int speed;

    // this method throws an error 
    public void turnOnEngine(){
        throw new AssertionError(detailMessage: "there is no engine");
    }
    
    public void accelerate(){
        // logic for accelerating
    }
}


```

- The two classes Bike and Cycle implements the Vehicle interface.
- If we have an object of the Vehicle class, then we can replace it with the object of the Bike class, without any issues. The reason being, with the object of Bike class we'll be able to implement both the functionalities of the parent class, so we are following LSP in the Bike class.
- However, if we use the object of the Cycle class, then we won't be able to access both the functionalities, it is because in case of Cycle the ``turnOnEngine()`` method throws an error, because a Cyle doesn't has an engine because of which we won't require this method at all. Hence, we are narrowing down the capabilities of the parent class(i.e. Vehicle in this case), so it is not following LSP, because we can't replace the object of Vehicle class with that of Cycle class.


                                 Parent
                      /     /      |      \      \
                  child1  child2  child3  child4 ...

  - So accroding to LSP, we should be able to substitute the object of the parent class with its child class without breaking the behaviour of the program.
    
 
</details>
