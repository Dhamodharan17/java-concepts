```
package javaconcepts;

import java.util.Map;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

public class FunctionalInterfaces {

    /*
    Functional Interface:
    1. Allow us to use "lambda expression and method reference" to provide concise and readable code for functional programming
    2. in functional programming , function is an independent entity
    3. to indicate an interface is a functional interface we can use @functionalInterface annotation

    Rules:
    1. can contain only one abstract method but any number of static and non-abstract methods.
    // abstract methods - needs implementation only while using
    2. @functionalInterface - not mandate

     */
    public static void main(String[] args) {
        // only one abstract method
        abstractImplementation();
        // static method
        MyFunctionalInterface  functionalInterface = MyClass::myStaticMethod;
        functionalInterface.doSomething();

        // Type 1 : Function - take one argument and produces result
            Function<Integer,Integer> square = x-> x*x;
            System.out.println(square.apply(5));

        // Type 2 : Predicate - boolean o/p
        // Methods - test,isEqual,and,or,negate
            Predicate<Integer> isEven=  x->x%2==0;
            System.out.println(isEven.test(6));
            Predicate<Integer> isEvener= x->x%2==0;
            System.out.println(isEven.and(isEvener));
            isEvener.negate();

        // Type 3 : Consumer - takes an argument and returns no result
            Consumer<String> printCaps = message-> System.out.println(message.toUpperCase());
            printCaps.accept("Hello");
            Consumer<String> printSmall = message-> System.out.println(message.toLowerCase());
            printCaps.andThen(printSmall).accept("Hello");

        // Type 4 : Supplier - Represents a supplier of results. Method present is : get()
            Supplier<Double> supplier = ()-> Math.random();
            System.out.println(supplier.get());
            // inbuilt interfaces - runnable, comparable, action listener, callable
    }

    public static void abstractImplementation() {
        // Rule 1
        MyFunctionalInterface myFunctionalInterface = () -> {
            System.out.println("Doing something...");
        };

        myFunctionalInterface.doSomething();
    }

}
class MyClass {
    static void myStaticMethod() {
        System.out.println("Static method called.");
    }
}

@FunctionalInterface
interface MyFunctionalInterface{
    void doSomething();
}

 class RunnableInterface {

    public static void main(String[] args) {

        Runnable task1 = ()->{
            System.out.println("Run thread 1");
        };

        Thread thread = new Thread(task1);
        thread.run();

    }
}

/* The Comparable interface in Java is used to define a natural ordering of objects of a class.
 compareTo() method returns a negative integer, zero, or a positive integer
 if the current object is less than, equal to, or greater than the specified object, respectively.

 -ve => current is less
 +ve => when current is more
 0 => both are equal

 */
```
