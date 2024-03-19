## Introduction to SOLID Principles

S – Single-responsibility principle
O – Open-closed principle
L – Liskov substitution principle
I – Interface segregation principle
D – Dependency Inversion Principle

**1. Single Responsibility Principle (SRP):**

Nutshell : put objects and method in separate class

- Single responsibility principle states that, each class should have only one responsibility or a one purpose
- we want to keep classes so simple that we wont modify the class unless we require to update that one responsibility which class performs.

```
public class Employee {
	private String employeeId;
	private String employeeName;
	private String address;
	private Date dateOfJoining;

public boolean isPromotionDueThisYear() {
		// promotion logic implementation
		return true;
	}
	public Double calcIncomeTaxForCurrentYear() {
		// income tax logic implementation
		Double incometax= 20000.78;
		return incometax;
	}

}
```
the class name is Employee, so it should only store and handle basic attributes of Employee class. 
But in this class , apart from getter setter methods of Employee there are 2 business logics i.e deciding promotion of employee and calculating income tax for the year. 
So this class has more than one reasons to modify. Hence it is a best candidate to refactor 

```
public class Employee {
    private String employeeId;
    private String employeeName;
    private String address; 
    private Date dateOfJoining;
}

public class HRPromotions {
    public boolean isPromotionDueThisYear(Employee emp){
       //some logic to decide promotion factor 
        return false;     
    }
  }

public class IncomeTaxCalculator {
    public Double calcIncomeTaxForCurrentYear(){
        //income tax logic implementation
        
        return 10000.78;
      }
}
```
**Hence to apply SRP principle we should understand:**
- Responsibility of each class and decide scope of each class
- We must understand problem domain, the business need and also architecture of the application

**Open Closed Principle(OCP)**

Nutshell : override , don't touch the class.

- Software entities should be open for extension, but closed for modification.
- It means when you have any new requirement in application or module, we should be **able to extend the functionality** but also **restrict modifying existing** entity for it.
- What we do in **polymorphism** is, we extend our parent class as per the need of child class and we restrict modifying the parent class.
- So if we need to add additional behaviors and attributes ,we simply extend it by inheriting new class from it.
- Our Parent class can be abstract class or interface, which is a base class and can be reused by adding more behaviors to it through inheritance.
- So the parent class is open for extension but closed for modification

  ![image](https://github.com/Dhamodharan17/java-concepts/assets/30789057/fd602539-42a5-4996-a71a-251fcdd44ef8)
**Why do we follow OCP principle?**
 - Many times the code changes introduce heavy risk. While modifying code we might end up breaking existing functionality.
 - Hence we can minimize the risk of breaking code by avoid modifying existing code and make sure to design it such way that we can extend it.
 - **Adding more responsibility to one class also violates the single responsibility principle.**

```
public class Shape {
	public double calculateAreaForSquare(double length) {
		return length * length;
	}


	public double calculateAreaForRectangle(double length, double breadth) {


		return length * breadth;
	}
	
	public double calculateAreaForCircle(double radius) {
		return Math.PI * radius * radius;
	}

}


public class AreaCalculatorClient {


	public static void main(String args[]) {
		Shape shape = new Shape();
  		System.out.println("Area of Square: " + 
shape.calculateAreaForSquare(10));
  		System.out.println("Area of Rectangle: " + shape.calculateAreaForRectangle(10, 5));
  		System.out.println("Area of Circle: " + shape.calculateAreaForCircle(10.5));
  	}

}
```
If we introduce more shapes, we will modify this class again to add method of that shape. 

```
public interface Shape {
    public double calculateArea();
}

public class Rectangle implements Shape {
	double length;
	double breadth;


	public Rectangle(double length, double breadth) {
		this.length = length;
		this.breadth = breadth;
	}


	public double calculateArea() {
		return length * breadth;
	}

}

public class Square implements Shape{
    double length;

    public Square(double length){
        this.length = length;
    }


    public double calculateArea(){
        System.out.println("Calculating area of square shape");
        return length * length;
    }
    
}

public class Circle implements Shape{
	double radius;

	public Circle(double radius) {
		this.radius = radius;
	}


	public double calculateArea() {
		return Math.PI * radius * radius;
	}

}

public class AreaCalculatorClient{


	public static void main(String args[]) {
		Shape shape = new Rectangle(10, 5);
		System.out.println("Rectangle Area: " + shape.calculateArea());


		shape = new Square(10);
		System.out.println("Square area: " + shape.calculateArea());
		
		shape = new Circle(10.5);
		System.out.println("Circle area: "+ shape.calculateArea());
	}
}
```
- We can extend as many shapes as possible from basic Shape interface here.

- If we need to introduce additional method in Rectangle class to calculate perimeter, we can simply do it by adding new method in Rectangle class alone. 

**3.Liskov Substitution Principle**

Nutshell : do inheritence in proper way

- Following this OCP principle alone, may not be enough to ensure that , change in one part of system wont break other parts of system. 
- To assure , that we are not breaking other parts of system while changing existing code, our code need to follow the Liskov Substitution Principle.
- We have seen that with the help of "polymorphism" we are able to invoke child class methods using a parent class reference variable at run time.
**Principle**
- if my parent class object is able to do something then all the child classes objects should also be also to do that thing.
- if child class is not able to do the thing which parent class do , then its not cirrect hierarchy and
- we cannot substitute child class for their parent class, this is called String Behabioral Subtyping.

**Violation Example**

```
public abstract class TransportationDevice{
	String name;
	double speed;
	public abstract void startEngine();
	public abstract void startMovement();
}

public class Car extends TransportationDevice{
	@Override
	public void startEngine() {
		System.out.println("Engine of car started");
	}


	@Override
	public void startMovement() {
		System.out.println("Movement of Car started");
	}
}

public class Bicycle extends TransportationDevice {
	@Override
	public void startEngine() {
		// cant implement this method as there is no Engine in bicycle
		// leave it without implementation or throw exception
	}


	public void startMovement() {
		System.out.println("Movement of bicycle started");
	}
}
```
- Bicycle class will simply have empty implementation of this method or may throw some exception as its unsupported functionality.
- Hence we need to fix it by making inheritance in better way
![image](https://github.com/Dhamodharan17/java-concepts/assets/30789057/f63ff6f5-9969-480c-939c-f795c1f628d7)

**4.Interface Segregation Principle**

- This principle relates to the problem of a fat interface which has too many attributes and behaviors.
- **“A Client should not be forced to implement an interface that it doesn’t use.”**

This means the one fat interface need to be split into many smaller and relevant interfaces so that clients can chose the most relevant interfaces for them . 


**ISP Violation**
```
public interface PrintTasks {
	boolean printContent(String content);


	boolean scanContent(String content);


	boolean faxContent(String content);


	boolean photoCopyContent(String content);
}
```
**Problem :** 
- Hp printer have fax feature but cannon don't have but still it has to implement it.
- when we add new feature all the child should override it which might be relevent too.

**Solution**
```
interface PrintScanContent{
	boolean printContent(String content);

	boolean scanContent(String content);

	boolean photoCopyContent(String content);
}


interface FaxContent{
	boolean faxContent(String content);
}


interface DuplexContent{
	boolean printDuplexContent(String content);
}
```
**5. Dependency Inversion Principle(DIP)**

Create objects for interface and use it.<br/>
In simple language DIP principle states to keep the dependent code i.e low-level module away from the main program i.e high-level module. 

So it suggests to eliminate direct dependency of low-level module with high-level module to reduce coupling. 

So the modules should rely on abstraction layer to interact with each other. This make sure any changes done in low-level module wont break the high-level module. 

This reduces the cost of maintenance and fragility of code.

**Violation**
```
public class EmailService{
	public void sendEmail() {
		// logic to send email
		System.out.println("Sending result through Email");
	}
}


public class SMSService {
	public void sendSMS() {
		// logic to send email
		System.out.println("Sending result through SMS");
	}
}

public class ResultPublisher {
	private SMSService smsService = new SMSService();
	private EmailService emailService = new EmailService();
	public void publishResult() {
		// need to publish result through email and sms both
		smsService.sendSMS();
		emailService.sendEmail();
	}
```

**Solution**
```
 public interface MessageService {

	public void sendMessage();
}

public class EmailServiceImpl implements MessageService {
	public void sendMessage() {
		// logic to send email
		System.out.println("Sending result through Email");
	}
}

public class SMSServiceImpl implements MessageService {


	public void sendMessage() {
		// logic to send SMS
		System.out.println("sending result through sms");
	}
}

public class ResultPublisher {

	private List<MessageService> messageServices;
	
	public ResultPublisher(List<MessageService> messageServices) {
		this.messageServices = messageServices;
	}
	
	public void publishResult() {
		messageServices.forEach(messageService->messageService.sendMessage());
	}
}

So based on the reference of concrete class into the parent reference, the required method will be invoked. Changes in low level module wont affect high level module here. Even if any new concrete class is introduced to send message like FaxService, it wont affect high level module as it will be accessed through abstraction in high level module.


```
