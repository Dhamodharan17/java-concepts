 Allows you to create families of related objects without directly specifying their concrete implementations.

Imagine that you’re creating a furniture shop simulator. Your code consists of classes that represent:

A family of related products, say: Chair + Sofa + CoffeeTable.

![image](https://github.com/Dhamodharan17/java-concepts/assets/30789057/c12b43a9-7444-43ed-92e1-8dafa1c21b76)

In the client code, we create instances of the concrete factories (WindowsFactory and MacOSFactory) and use them to create buttons without knowing the concrete button implementation.

**We create Object only for Windows Factory internally it creates object of button and checkbox and give us methods inside it.**
```
// Abstract product interfaces
interface Button {
    void click();
}

interface Checkbox {
    void check();
}

// Abstract factory
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// Concrete product implementations for Windows
class WindowsButton implements Button {
    @Override
    public void click() {
        System.out.println("Windows Button clicked");
    }
}

class WindowsCheckbox implements Checkbox {
    @Override
    public void check() {
        System.out.println("Windows Checkbox checked");
    }
}

// Concrete product implementations for MacOS
class MacOSButton implements Button {
    @Override
    public void click() {
        System.out.println("MacOS Button clicked");
    }
}

class MacOSCheckbox implements Checkbox {
    @Override
    public void check() {
        System.out.println("MacOS Checkbox checked");
    }
}

// Concrete factory implementations
class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

class MacOSFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacOSButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new MacOSCheckbox();
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        // Create Windows GUI components
        GUIFactory windowsFactory = new WindowsFactory();
        Button windowsButton = windowsFactory.createButton();
        Checkbox windowsCheckbox = windowsFactory.createCheckbox();
        windowsButton.click(); // Windows Button clicked
        windowsCheckbox.check(); // Windows Checkbox checked
        
        // Create MacOS GUI components
        GUIFactory macOSFactory = new MacOSFactory();
        Button macOSButton = macOSFactory.createButton();
        Checkbox macOSCheckbox = macOSFactory.createCheckbox();
        macOSButton.click(); // MacOS Button clicked
        macOSCheckbox.check(); // MacOS Checkbox checked
    }
}

```
