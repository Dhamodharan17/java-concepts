## Factory Design Pattern
Factory Method is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to **alter the type of objects that will be created**.
- Clients only need to interact with the factory interface, **which shields them from the complexities of object creation**.

**Relating to SOLID Principles:**

- Single Responsibility Principle (SRP): The Factory Design Pattern follows SRP by encapsulating the **object creation logic** into a separate class.
This class is responsible for creating objects, adhering to the principle of separation of concerns. **Encapsulation**

- Open/Closed Principle (OCP): The Factory Design Pattern follows OCP by allowing the system to be **easily extended **with new types of objects **without modifying existing** client code.
You can add new types of objects by creating new concrete implementations of the factory interface. **Flexibility**

- Liskov Substitution Principle (LSP): The Factory Design Pattern supports LSP by **returning objects through a common interface**
Clients can treat these objects uniformly without needing to know their specific types, ensuring that substitutability is maintained.

![image](https://github.com/Dhamodharan17/java-concepts/assets/30789057/0d2702fd-7567-4824-aeeb-2d7c177c6b17)

### Code
```
// Shape interface
interface Shape {
    void draw();
}

// Concrete implementations of Shape interface
class Circle implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

class Square implements Shape {
    @Override
    public void draw() {
        System.out.println("Drawing Square");
    }
}

// Shape Factory
class ShapeFactory {
    // Factory method to create shapes
    public Shape createShape(String type) {
        if ("circle".equalsIgnoreCase(type)) {
            return new Circle();
        } else if ("square".equalsIgnoreCase(type)) {
            return new Square();
        } else {
            throw new IllegalArgumentException("Invalid shape type: " + type);
        }
    }
}

// Client code using the factory
public class Main {
    public static void main(String[] args) {
        ShapeFactory factory = new ShapeFactory();
        Shape circle = factory.createShape("circle");
        Shape square = factory.createShape("square");

        circle.draw(); // Output: Drawing Circle
        square.draw(); // Output: Drawing Square
    }
}
```
 
In simpler terms, it's like a **factory that produces different types of objects based on certain conditions or parameters.**
