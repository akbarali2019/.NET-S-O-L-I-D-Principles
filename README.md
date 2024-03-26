## SOLID Principle Simplified
In Object-oriented software development, SOLID is a popular design principle. Most software developers are implementing the SOLID design principle into their code.
#### History
The SOLID principles were developed by Robert C. Martin in a 2000 essay, “Design Principles and Design Patterns,” although the acronym was coined later by Michael Feathers. In his essay, Martin acknowledged that successful software will change and develop. As it changes, it becomes increasingly complex. Without good design principles, Martin warns that software becomes rigid, fragile, immobile, and vicious. The SOLID principles were developed to combat these problematic design patterns.
#### Goal
The broad goal of the SOLID principles is to reduce dependencies so that engineers change one area of software code without impacting others. Additionally, they’re intended to make designs easier to understand, maintain, and extend. Ultimately, using these design principles makes it easier for software engineers to avoid issues and build adaptive, effective, and agile software.
#### SOLID Acronym
SOLID is an acronym that stands for five key design principles:

1. Single Responsibility Principle (SRP)

2. Open-Closed Principle (OCP)

3. Liskov Substitution Principle (LSP)

4. Interface Segregation Principle (ISP)

5. Dependency Inversion Principle (DIP)

All five are commonly used by software engineers and provide some important benefits for developers.
#### Advantages of SOLID Principles
Achieve the reduction in complexity of the code
Increase readability, extensibility, and maintenance
Increase scalability, code flexibility, and readability
Achieve Better testability
Reduce tight coupling
Reduce error and implement Reusability
Increase Parallel development
#### Single Responsibility Principle (SRP)
The Single Responsibility Principle states, "Each software module or class should have only one reason to change“. In other words, we can say that each module or class should have only one responsibility to do.

We must design the software in such a way that everything in a class or module is related to a single responsibility. That is not to say that your class should only have one method or property; you can have multiple members (methods or properties) as long as they are all related to a single responsibility or functionality. As a result of the Single Responsibility Principle, the classes become smaller and cleaner, making them easier to maintain.

<pre>public class EmailSender
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
}</pre>

In this example, the EmailSender class has a single responsibility, which is to send an email. The Logger class has a single responsibility, which is to log messages. Both classes focus on a single, well-defined task and have only one reason to change. This makes the code easier to understand, maintain, and test.
#### Open-Closed Principle (OCP)
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
<pre>static void Main(string[] args)
{
    ConsoleLogger logger = new ConsoleLogger();
    logger.Log("This is a console log message");

    FileLogger fileLogger = new FileLogger();
    fileLogger.Log("This is a file log message", "log.txt");
}</pre>
As you can see, we can use the ConsoleLogger and FileLogger classes interchangeably, because they both have a Log method with the same signature. However, the FileLogger class adds new functionality by allowing us to specify a filename for the log messages.

In summary, the Open/Closed Principle is an important principle of software design that suggests that software entities should be open for extension but closed for modification. In the example above, we demonstrated how we can extend the behavior of a logging system by adding a new FileLogger class that extends the existing ConsoleLogger class, without modifying its existing codebase.
#### Liskov Substitution Principle (LSP)

#### Interface Segregation Principle (ISP)

#### Dependency Inversion Principle (DIP)

