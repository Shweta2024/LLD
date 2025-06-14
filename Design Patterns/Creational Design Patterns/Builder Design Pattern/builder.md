# Builder Design Patter
- Creational Design Pattern.
- Creates object step-by-step.

<details>
  <summary>
    <h2>When to use Builder design pattern?</h2>
  </summary>

  - ``Complex Object``: when an object has multiple components/parts and we want to provide a clear speration between its construction process and its actual
    representation.
  - Step by step process: when an object creation invloves step by step process, where different configurations need to be set at different stages.
  - Avoiding constructors with multiple parameters: when the number of parameters in a constructor is large.
</details>

<details>
  <summary>
    <h2>Components of Builder design Pattern</h2>
  </summary>

  - Product: it is the complex object that Builder pattern will construct.
    - it may have multiple components/parts.
    - it is typically a class with attributes, representing the different parts that the builder will construct.
     
  - Builder: it is an interface or abstract class, that declares the construction steps for building a Product(complex object).
    - it includes methods for constructing individual parts of a Product.
    - by defining an interface, it allows the creation of different concreteBuilder which can produce variations of the Product.
         
  - ConcreteBuilder: it implements the Builder, and provides specific implementations for building each part of the product.
    
  - Director: it manages the construction process of the Product(Complex object).
    - it collaboartes with the Builder, but is unaware about how each part of the Product(Complex object) is created.
      
  - Client: it initiates the construction of the Product(complex object).

            Note: here components/parts refers to the different attributes of the class.
    
</details>


<details>
<summary>
  <h2>Steps to implement Builder design pattern</h2>
</summary>

  - Create Product: define the complex object that needs to be built.
    
  - Create Builder: create methods to set different parts of the Product. Each method returns a builder itself to allow method chaining.
    
  - Add build() method: this method, assembles the Product(i.e. the components/parts of the complex object) and returns the final object.
    
  - Use Director(optional): if needed, create a Director class to control the building process and decide the order in which parts are constructed.
     
  - Client: it uses the builder to set the parts step by step and call the build() method to get the final product.
    
</details>

<details>
  <summary>
    <h2>When NOT to use builder design pattern?</h2>
  </summary>

  - Simple Object: when an object has few attributes and a straightforward creation process.
    
  - Performance Concern: in case of performance critical application, the extra method calls involved in the object creation process could impact the performance,
    especially when object creation is frequent.
    
  -  Increased Code Complexity: creating builder class for every complex object can lead to increase in code complexity.
    
  - Tight coupling with product: if builder class is tightly coupled with the Product, then any changes in thr product will require corresponding modifications
    in the builder, which reduces the flexibility and maintainibility of the code.

</details>
