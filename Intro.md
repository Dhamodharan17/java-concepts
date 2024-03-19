## Introduction to SOLID Principles

S – Single-responsibility principle
O – Open-closed principle
L – Liskov substitution principle
I – Interface segregation principle
D – Dependency Inversion Principle

**1. Single Responsibility Principle:**

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

  















