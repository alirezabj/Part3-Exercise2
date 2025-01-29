# Part3-Exercise2




#### A)
Inheritance and polymorphism are demonstrated in this code through the handling of the exception  and the structure of the class hierarchy. The Problem class extends Exception, and its subclasses, WeirdProblem and TrickyProblem, inherit from Problem, allowing them to be treated as Problem instances. This inheritance structure enables Experiment to explicitly declare that it throws either WeirdProblem or TrickyProblem, while Experiment2 generalizes this by declaring throws Problem, allowing any subclass of Problem to be thrown. Polymorphism is applied in the main() method’s try-catch structure, where exceptions are caught based on their actual type at runtime. The catch blocks are ordered correctly, handling the specific exceptions WeirdProblem and TrickyProblem first, before catching the more general Problem, which ensures that all exceptions are processed appropriately. 

#### B)
Printer1 and Printer2 both implement the Printer interface and use a decorator to modify how the output is displayed, but they are different in their approach to reuse. Printer1 uses inheritance, since it extends Fancy, meaning it directly inherits the decorate() method. This makes the code simpler but also less flexible, since it's directly tied to Fancy and can't easily switch to a different decoration style. On the other hand, Printer2 uses composition, meaning instead of inheriting from Fancy, it holds a reference to a Decorator instance, which it initializes through generateDecorator(). This approach allows greater flexibility, as the decorator can be dynamically assigned or changed without modifying the class itself. Thus, in generall, Printer1 is less flexible but simpler but Printer2 is more adaptable


To extend the previous Printer functionality in Printer3, we need to modify the decoration method so that instead of just using Fancy's == decoration, it also adds -- at both the beginning and end of the string. This means that Printer3 should wrap the existing decoration with -- on each side, resulting in an output like --== main ==--. The best way to implement this is to use composition rather than inheritance, meaning Printer3 would contain a Decorator instance (such as Fancy) and apply its additional formatting on top of it. This makes the class more flexible and reusable.

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

```java

interface Decorator {
    String decorate(String input);
    int getDecorationSize();
}

class CustomDecorator implements Decorator {
    private final Decorator baseDecorator;

    CustomDecorator(Decorator baseDecorator) {
        this.baseDecorator = baseDecorator;
    }

    @Override
    public String decorate(String input) {
        int size = getDecorationSize();
        String prefixSuffix = "-".repeat(size);
        return prefixSuffix + baseDecorator.decorate(input) + prefixSuffix;
    }

    @Override
    public int getDecorationSize() {
        return 2; 
    }
}

```

However, if the number of -- characters was defined in the Printer interface, it would shift the responsibility of defining the decoration style from decorators to printers. This means every class that implements Printer would need to specify how many -- characters should be used even if not all printers require this feature.




