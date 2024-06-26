# SOLID Principle Simplified
In Object-oriented software development, SOLID is a popular design principle. Most software developers are implementing the SOLID design principle into their code.
## History
The SOLID principles were developed by Robert C. Martin in a 2000 essay, “Design Principles and Design Patterns,” although the acronym was coined later by Michael Feathers. In his essay, Martin acknowledged that successful software will change and develop. As it changes, it becomes increasingly complex. Without good design principles, Martin warns that software becomes rigid, fragile, immobile, and vicious. The SOLID principles were developed to combat these problematic design patterns.
## Goal
The broad goal of the SOLID principles is to reduce dependencies so that engineers change one area of software code without impacting others. Additionally, they’re intended to make designs easier to understand, maintain, and extend. Ultimately, using these design principles makes it easier for software engineers to avoid issues and build adaptive, effective, and agile software.
## SOLID Acronym
SOLID is an acronym that stands for five key design principles:

1. Single Responsibility Principle (SRP)

2. Open-Closed Principle (OCP)

3. Liskov Substitution Principle (LSP)

4. Interface Segregation Principle (ISP)

5. Dependency Inversion Principle (DIP)

All five are commonly used by software engineers and provide some important benefits for developers.
## Advantages of SOLID Principles
Achieve the reduction in complexity of the code
Increase readability, extensibility, and maintenance
Increase scalability, code flexibility, and readability
Achieve Better testability
Reduce tight coupling
Reduce error and implement Reusability
Increase Parallel development
## Single Responsibility Principle (SRP)
The Single Responsibility Principle states, "Each software module or class should have only one reason to change“. In other words, we can say that each module or class should have only one responsibility to do.

We must design the software in such a way that everything in a class or module is related to a single responsibility. That is not to say that your class should only have one method or property; you can have multiple members (methods or properties) as long as they are all related to a single responsibility or functionality. As a result of the Single Responsibility Principle, the classes become smaller and cleaner, making them easier to maintain.

<pre>
public class EmailSender
{
    public void SendEmail(string emailAddress, string subject, string message)
    {
        // Code to send an email
    }
}

public class Logger
{
    public void LogMessage(string message)
    {
        // Code to log a message
    }
}
</pre>

In this example, the EmailSender class has a single responsibility, which is to send an email. The Logger class has a single responsibility, which is to log messages. Both classes focus on a single, well-defined task and have only one reason to change. This makes the code easier to understand, maintain, and test.
## Open-Closed Principle (OCP)
The Open/Closed Principle is one of the SOLID principles of software design, which suggests that software entities such as classes, modules, and functions should be open for extension but closed for modification. This principle states that you should be able to add new functionality to a system without having to modify existing code.

In other words, you should be able to extend the behavior of a system without changing its existing codebase. This is important because modifying existing code can lead to unforeseen consequences and introduce bugs while extending the behavior of a system can improve its functionality without negatively affecting its existing code.

Let’s consider a C# example to illustrate the Open/Closed Principle. Suppose we have a basic logging system that can log messages to the console:

<pre>public class ConsoleLogger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
}</pre>
Now, imagine that we want to add the ability to log messages to a file, without modifying the existing code. To do this, we can create a new class that extends the ConsoleLogger class and overrides the Log method:
<pre>public class FileLogger : ConsoleLogger
{
    public void Log(string message, string fileName)
    {
        using (StreamWriter writer = new StreamWriter(fileName, true))
        {
            writer.WriteLine(message);
        }
    }
}</pre>
This new FileLogger class adds the ability to log messages to a file, but it does so by extending the ConsoleLogger class, rather than modifying it. This means that the ConsoleLogger class remains unchanged, and we can continue to use it in the same way as before.

Here’s an example of how we could use the FileLogger class to log messages to a file:
<pre>
static void Main(string[] args)
{
    ConsoleLogger logger = new ConsoleLogger();
    logger.Log("This is a console log message");

    FileLogger fileLogger = new FileLogger();
    fileLogger.Log("This is a file log message", "log.txt");
}
</pre>
As you can see, we can use the ConsoleLogger and FileLogger classes interchangeably, because they both have a Log method with the same signature. However, the FileLogger class adds new functionality by allowing us to specify a filename for the log messages.

In summary, the Open/Closed Principle is an important principle of software design that suggests that software entities should be open for extension but closed for modification. In the example above, we demonstrated how we can extend the behavior of a logging system by adding a new FileLogger class that extends the existing ConsoleLogger class, without modifying its existing codebase.
#### Liskov Substitution Principle (LSP)
The Liskov Substitution Principle (LSP) is a principle in object-oriented programming that states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. This means that a subclass should be a subtype of its superclass and that objects of the subclass should be able to be used wherever objects of the superclass are expected without introducing any new bugs or causing any existing functionality to break.

The LSP is important for creating maintainable and flexible code. If a subclass is not a proper subtype of its superclass, then using an object of the subclass in place of an object of the superclass can cause unexpected behavior, which can lead to bugs that are difficult to track down and fix.

To ensure that a subclass is a proper subtype of its superclass, it should fulfill the following requirements:

The subclass should have all the properties and methods of the superclass.
The subclass should not have any new properties or methods that are not in the superclass.
The subclass should not reduce the visibility of any properties or methods in the superclass.
The subclass should not change the behavior of any properties or methods in the superclass in a way that would break existing code that uses the superclass.
To illustrate the Liskov Substitution Principle, let’s consider a C# example. Suppose we have a Rectangle class that represents a rectangle with a width and height:

<pre>
public class Rectangle
{
    public int Width { get; set; }
    public int Height { get; set; }

    public int Area()
    {
        return Width * Height;
    }
}</pre>

Now, let’s say we want to create a Square class that represents a square with a side length. A square is a special case of a rectangle, where the width and height are always equal. We could define the Square class like this:

<pre>
public class Square : Rectangle
{
    public int Side { get; set; }

    public new int Width
    {
        get { return Side; }
        set { Side = value; }
    }

    public new int Height
    {
        get { return Side; }
        set { Side = value; }
    }
}
</pre>

In this implementation, we use the new keyword to shadow the Width and Height properties of the Rectangle class, and replace them with properties that get and set the Side property. This allows us to create a Square object and use it like a Rectangle object, since it inherits all of the properties and methods of the Rectangle class.

However, this implementation violates the Liskov Substitution Principle, because a Square object does not behave like a Rectangle object in all cases. For example, if we create a Rectangle object with a width of 5 and a height of 10, and then replace it with a Square object with a side length of 5, the area will be different:

<pre>
Rectangle rectangle = new Rectangle { Width = 5, Height = 10 };
int rectangleArea = rectangle.Area(); // returns 50

Square square = new Square { Side = 5 };
int squareArea = square.Area(); // returns 25

// This violates the Liskov Substitution Principle
rectangle = square;
int rectangleArea2 = rectangle.Area(); // returns 25, not 50</pre>

To fix this problem and adhere to the Liskov Substitution Principle, we need to change the design of the Square class. One way to do this is to use a separate Square class that does not inherit from Rectangle. This allows us to define a Square object in a way that does not interfere with the behavior of the Rectangle class:

<pre>
public class Square
{
    public int Side { get; set; }

    public int Area()
    {
        return Side * Side;
    }
}
</pre>

By using a separate Square class, we can ensure that a Square object can be substituted for a Rectangle object without violating the correctness of the program.

By following the LSP, we can create a flexible and maintainable codebase, where objects of different classes can be used interchangeably without causing any unexpected behavior. This makes it easier to extend and modify our code as needed, without introducing any new bugs.

#### Interface Segregation Principle (ISP)
It states that a client should not be forced to depend on interfaces that it does not use. In other words, it is better to have multiple smaller interfaces that are tailored to specific needs rather than a single large interface that tries to cover everything.

To illustrate the Interface Segregation Principle, let’s consider a C# example. Suppose we have an IPrinter interface that represents a printer, with methods to print and scan:

<pre>
public interface IPrinter
{
    void Print(string document);
    void Scan(string document);
}
</pre>

Now, let’s say we have two types of printers, a basic printer and a multi-function printer. The basic printer can only print, while the multi-function printer can both print and scan. We could define these classes like this:
<pre>
public class BasicPrinter : IPrinter
{
    public void Print(string document)
    {
        Console.WriteLine("Printing document: " + document);
    }

    public void Scan(string document)
    {
        throw new NotImplementedException();
    }
}

public class MultiFunctionPrinter : IPrinter
{
    public void Print(string document)
    {
        Console.WriteLine("Printing document: " + document);
    }

    public void Scan(string document)
    {
        Console.WriteLine("Scanning document: " + document);
    }
}
</pre>

In this implementation, we have implemented the IPrinter interface in both BasicPrinter and MultiFunctionPrinter classes. However, this violates the Interface Segregation Principle, because the BasicPrinter class is forced to implement the Scan method, even though it does not support scanning. This is not ideal, as it creates unnecessary coupling and can lead to confusing or unexpected behavior.

To adhere to the Interface Segregation Principle, we can split the IPrinter interface into two smaller interfaces, one for printing and one for scanning:

<pre>
public interface IPrinter
{
    void Print(string document);
}

public interface IScanner
{
    void Scan(string document);
}
</pre>

Now, we can define the BasicPrinter and MultiFunctionPrinter classes to implement only the interface(s) that they actually use:

<pre>
public class BasicPrinter : IPrinter
{
    public void Print(string document)
    {
        Console.WriteLine("Printing document: " + document);
    }
}

public class MultiFunctionPrinter : IPrinter, IScanner
{
    public void Print(string document)
    {
        Console.WriteLine("Printing document: " + document);
    }

    public void Scan(string document)
    {
        Console.WriteLine("Scanning document: " + document);
    }
}
</pre>

In this new implementation, the BasicPrinter class only needs to implement the IPrinter interface, and the MultiFunctionPrinter class can implement both IPrinter and IScanner interfaces. This adheres to the Interface Segregation Principle, as each class is only dependent on the interfaces that it actually uses.

The Interface Segregation Principle is an important principle of software design that encourages the use of smaller, more focused interfaces instead of large, monolithic ones. In the C# example above, we demonstrated how to refactor the IPrinter interface to adhere to the Interface Segregation Principle and avoid unnecessary coupling and unexpected behavior.

#### Dependency Inversion Principle (DIP)
It states that high-level modules should not depend on low-level modules. Instead, both should depend on abstractions. This promotes loose coupling and flexibility, making it easier to make changes without affecting other parts of the system.

To illustrate the Dependency Inversion Principle, let’s consider a C# example. Suppose we have a Car class that needs to use a FuelInjector class to inject fuel into the engine. In this example, the Car class represents a high-level module, and the FuelInjector class represents a low-level module.

<pre>
public class Car
{
    private readonly FuelInjector _fuelInjector;

    public Car()
    {
        _fuelInjector = new FuelInjector();
    }

    public void Start()
    {
        _fuelInjector.InjectFuel();
        // other code to start the car
    }
}

public class FuelInjector
{
    public void InjectFuel()
    {
        Console.WriteLine("Injecting fuel into engine.");
    }
}
</pre>

In this implementation, the Car class directly instantiates a FuelInjector object in its constructor. This violates the Dependency Inversion Principle because the Car class is dependent on a low-level module, making it inflexible and tightly coupled.

To adhere to the Dependency Inversion Principle, we can use an abstraction, such as an interface or an abstract class, to decouple the Car class from the FuelInjector class. We can define an IFuelInjector interface to represent the fuel injection behavior, and then inject an instance of this interface into the Car class:

<pre>
public interface IFuelInjector
{
    void InjectFuel();
}

public class Car
{
    private readonly IFuelInjector _fuelInjector;

    public Car(IFuelInjector fuelInjector)
    {
        _fuelInjector = fuelInjector;
    }

    public void Start()
    {
        _fuelInjector.InjectFuel();
        // other code to start the car
    }
}

public class FuelInjector : IFuelInjector
{
    public void InjectFuel()
    {
        Console.WriteLine("Injecting fuel into engine.");
    }
}
</pre>

In this new implementation, the Car class is no longer dependent on the FuelInjector class, but rather on the IFuelInjector interface. We can now create multiple implementations of the IFuelInjector interface, which can be used to inject fuel into the engine in different ways. This makes the Car class more flexible and easier to change, as it is no longer tightly coupled to the FuelInjector class.


