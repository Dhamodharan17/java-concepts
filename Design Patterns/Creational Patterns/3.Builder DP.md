Builder is a creational design pattern that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.

Imagine a complex object that requires laborious, step-by-step initialization of many fields and nested objects. 
Such initialization code is usually buried inside a **monstrous constructor with lots of parameters**. Or even worse: scattered all over the client code.

![image](https://github.com/Dhamodharan17/java-concepts/assets/30789057/40b2e496-e6bf-4eea-ac2e-a411b5e1bd72)

In most cases most of the parameters will be unused, making the constructor calls pretty ugly. 
For instance, only a fraction of houses have swimming pools, so the parameters related to swimming pools will be useless nine times out of ten.

![image](https://github.com/Dhamodharan17/java-concepts/assets/30789057/6bd94c6a-168d-4799-8f08-db46cb51e23e)

The Builder pattern suggests that you extract the object construction code out of its own class and move it to separate objects called builders.

```
// Product class
class User {
    private final String name;
    private final int age;
    private final String email;
    private final String phoneNumber;

    private User(Builder builder) {
        this.name = builder.name;
        this.age = builder.age;
        this.email = builder.email;
        this.phoneNumber = builder.phoneNumber;
    }

    // Getter methods
    // (No setter methods to enforce immutability)

    // Builder class
    static class Builder {
        private final String name; // Required parameter
        private int age; // Optional parameter (default value 0)
        private String email = ""; // Optional parameter (default value "")
        private String phoneNumber = ""; // Optional parameter (default value "")

        // Constructor with required parameters
        Builder(String name) {
            this.name = name;
        }

        // Setter methods for optional parameters
        Builder age(int age) {
            this.age = age;
            return this;
        }

        Builder email(String email) {
            this.email = email;
            return this;
        }

        Builder phoneNumber(String phoneNumber) {
            this.phoneNumber = phoneNumber;
            return this;
        }

        // Build method to construct the final User object
        User build() {
            return new User(this);
        }
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        // Create a User object using the Builder pattern
        User user1 = new User.Builder("John")
                        .age(30)
                        .email("john@example.com")
                        .phoneNumber("1234567890")
                        .build();
        
        // Create another User object with minimal information
        User user2 = new User.Builder("Alice").build();
        
        // Print user details
        System.out.println("User 1: " + user1);
        System.out.println("User 2: " + user2);
    }
}

```
