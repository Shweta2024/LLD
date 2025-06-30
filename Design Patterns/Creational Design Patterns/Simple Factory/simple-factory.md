## Simple Factory

- Creational design pattern.
- Object is created based on some Condition.(eg:- if condition1 satisfied create Object1, if condition2 is satisfied create Object2 and so on)

### UML Diagram

![image](https://github.com/user-attachments/assets/c695124e-14b4-4d9c-9554-1ae2cee9c19e)

<details>
  <summary>
    <h2>Example</h2>
  </summary>

- Product Interface
```java
public interface Shape{
    void draw();
}
```

- Implementation Classes
```java
public class Square implements Shape{
    @override
    public void draw(){
        System.out.println("Square");
    }
}
```

```java
public class Circle implements Shape{
    @override
    public void draw(){
        System.out.println("Circle");
    }
}
```

- Factory Class
```java
public class ShapeFactory{
    Shape getShape(string input){

        switch(input){
            case "Circle":
                return new Circle();
            case "Square":
                return new Square();
            default:
                return null;
        }
    }
}
```

- Client
```java
public class Main{
	public static void main(String[] args) {
	    ShapeFactory shapeFactory = new ShapeFactory();
	    Shape shapeObj = shapeFactory.getShape("Circle");
	    shapeObj.draw();
	}
}
```

</details>
