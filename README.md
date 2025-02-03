# Part3-Exercise2




#### A)
Inheritance and polymorphism are demonstrated in this code through the handling of the exception  and the structure of the class hierarchy. The Problem class extends Exception, and its subclasses, WeirdProblem and TrickyProblem, inherit from Problem, allowing them to be treated as Problem instances. This inheritance structure enables Experiment to explicitly declare that it throws either WeirdProblem or TrickyProblem, while Experiment2 generalizes this by declaring throws Problem, allowing any subclass of Problem to be thrown. 

Polymorphism is used in the try-catch structure because exceptions are handled based on their actual type when they occur. Even though WeirdProblem and TrickyProblem are both treated as Problem, Java automatically recognizes which specific exception is thrown at runtime. In Experiment2, the perform method is declared to throw a Problem, but in reality, it throws either WeirdProblem or TrickyProblem. This is an example of  polymorphism, where a general type (Problem) is used, but the actual object is one of its specific subclasses (WeirdProblem or TrickyProblem). 

Addtionaly, the catch block ordering in the code is correct because Java requires more specific exceptions to be caught before more general ones. Since WeirdProblem and TrickyProblem are subclasses of Problem, they must be caught first. Otherwise, placing catch (Problem w) before them would make the specific catch blocks unreachable, causing an error.









#### B)
Printer1 and Printer2 both implement the Printer interface and use a decorator to modify how the output is displayed, but they are different in their approach to reuse. Printer1 uses inheritance, since it extends Fancy, meaning it directly inherits the decorate() method. This makes the code simpler but also less flexible, since it's directly tied to Fancy and can't easily switch to a different decoration style. On the other hand, Printer2 uses composition, meaning instead of inheriting from Fancy, it holds a reference to a Decorator instance, which it initializes through generateDecorator(). This approach allows greater flexibility, as the decorator can be dynamically assigned or changed without modifying the class itself. Thus, in generall, Printer1 is less flexible but simpler but Printer2 is more adaptable


To extend the previous Printer functionality in Printer3, we would need to to add decoration at both the beginning and end of the string with additional "--" characters.  The best way to implement this is to use composition rather than inheritance, meaning Printer3 would contain a Decorator instance (such as Fancy) and apply its additional formatting on top of it. This makes the class more flexible and reusable.

```java
class Printer3 implements Decorator, Printer {
    private final Decorator decorator = new Fancy();

    @Override
    public String decorate(String input) {
        return "--" + decorator.decorate(input) + "--";
    }

    @Override
    public void print(String s) {
        System.out.println(s);
    }

    @Override
    public void run() {
        print(decorate("main"));
    }
}
```


If the number of -- characters wasn’t fixed at two per side and needed to be customizable, one approach would be to define this behavior in the Decorator interface. This would require adding a method to Decorator that returns the number of -- characters to apply, allowing each decorator to define its own style.


However, if the number of -- characters was defined in the Printer interface, it would shift the responsibility of defining the decoration style from decorators to printers. This means every class that implements Printer would need to specify how many -- characters should be used even if not all printers require this feature.




