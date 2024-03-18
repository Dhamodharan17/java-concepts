![image](https://github.com/Dhamodharan17/java-concepts/assets/30789057/bb1aaaf8-1d46-4e9c-9aa7-e21dd4839625)### Allows objects with incompatible interfaces to collaborate.
![image](https://github.com/Dhamodharan17/java-concepts/assets/30789057/8a2b65a8-abe4-4569-b505-a9920c675432)

Modern shape cannot call Legacy shape directly.
So,Modern Shape calls Shape Adpater calls Legacy Shape ** legacyShape.display();**
```
package javaconcepts;

// Legacy interface
interface LegacyShape {
    void display();
}

// Legacy class implementing the legacy interface
class LegacyRectangle implements LegacyShape {
    @Override
    public void display() {
        System.out.println("LegacyRectangle: Displaying");
    }
}

// Modern interface
interface ModernShape {
    void draw();
}

// Adapter class implementing the modern interface
class ShapeAdapter implements ModernShape {
    private LegacyShape legacyShape;

    public ShapeAdapter(LegacyShape legacyShape) {
        this.legacyShape = legacyShape;
    }

    @Override
    public void draw() {
        // Call the legacy interface method from the adapter
        legacyShape.display();
    }
}

// Client code using the modern interface
public class Client {
    public static void main(String[] args) {
        // Create a legacy shape object
        LegacyShape legacyShape = new LegacyRectangle();

        // Create an adapter object and pass the legacy shape to it
        ModernShape modernShape = new ShapeAdapter(legacyShape);

        // Use the adapter to call the modern interface method
        modernShape.draw(); // Output: LegacyRectangle: Displaying
    }
}
```
