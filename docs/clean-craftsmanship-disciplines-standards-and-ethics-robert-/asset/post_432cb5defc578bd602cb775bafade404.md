
## 4 Test Design

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_172_0.png)

If you look at the three laws of test-driven development (TDD), presented in Chapter 2, “Test-Driven Development,” you could come to the conclusion that TDD is a shallow skill: Follow the three laws, and you are done. This is far from the truth. TDD is a deep skill. There are many layers to it; and they take months, if not years, to master.

In this section, we delve into just a few of those layers, ranging from various testing conundrums, such as databases and graphical user interfaces (GUIs), to the design principles that drive good test design, to patterns of testing, and to some interesting and profound theoretical possibilities.

### Testing Databases

The first rule of testing databases is: *Don’t test databases.* You don’t need to test the database. You can assume that the database works. You’ll find out soon enough if it doesn’t.

What you really want to test are queries. Or, rather, you want to test that the commands that you send to the database are properly formed. If you write SQL directly, you are going to want to test that your SQL statements work as intended. If you use an object-relational mapping (ORM) framework, such as Hibernate, you are going to want to test that Hibernate operates the database the way you intended. If you use a NoSQL database, you are going to want to test that all your database accesses behave as you intended.

None of these tests require you to test business rules; they are only about the queries themselves. So, the second rule of testing databases is: *Decouple the database from the business rules.*

We decouple them by creating an interface, which I have called `Gateway`¹ in the diagram in [Figure 4.1]. Within the `Gateway` interface, we create one method for every kind of query we wish to perform. Those methods can take arguments that modify the query. For example, in order to fetch all the `Employees` from the database whose hiring date was after 2001, we might call the `Gateway` method `getEmployeesHiredAfter(2001)`.

- 1. Martin Fowler, *Patterns of Enterprise Application Architecture* (Addison-Wesley, 2003), 466.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_174_0.png)

Every query, update, delete, or add we want to perform in the database will have a corresponding method in a `Gateway` interface. There can, of course, be many `Gateways`, depending on how we want to partition the database.

The `GatewayImpl` class implements the gateway and directs the actual database to perform the functions required. If this is a SQL database, then all the SQL is created within the `GatewayImpl` class. If you are using ORM, the ORM framework is manipulated by the `GatewayImpl` class. Neither SQL nor the ORM framework nor the database API is known above the architectural boundary that separates the `Gateway` from the `GatewayImpl`¹.

Indeed, we don’t even want the schema of the database known above that boundary. The `GatewayImpl` should unpack the rows, or data elements, retrieved from the database and use that data to construct appropriate business objects to pass across the boundary to the business rules.

And now testing the database is trivial. You create a suitably simple test database, and then you call each query function of the `GatewayImpl` from your tests and ensure that it has the desired effect on that test database. Make sure that each query function returns a properly loaded set of business objects.

window. The presenter does as much as possible toward that end, allowing us to make the GUI absurdly small.

So, for example, the presenter is the module that determines the state of every button and menu item. It specifies their names and whether or not they should be grayed out. If the name of a button changes based on the state of a window, it is the presenter that knows that state and changes that name. If a grid of numbers should appear on the screen, it is the presenter that creates a table of strings, all properly formatted and arranged. If there are fields that should have special colors or fonts, it is the presenter that determines those colors and fonts.

The presenter takes care of all of that detailed formatting and arrangement and produces a simple data structure full of strings and flags that the GUI can use to build the commands that get sent to the screen. And, of course, that makes the GUI very small indeed.

The data structure created by the presenter is often called a *view model*.

In the diagram in Figure 4.2, the interactor is responsible for telling the presenter what data should be presented to the screen. This communication will be in the form of one or more data structures passed to the presenter through a set of functions. The actual presenter is shielded from the interactor by the presenter interface. This prevents the high-level interactor from depending on the implementation of the lower-level presenter.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_176_0.png)

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_178_0.png)

**Figure 4.3 Testing the GUI**

The GUI framework communicates with a controller through an `EventHandler` interface. This makes sure that the controller has no transitive source code dependency on the GUI framework. The job of the controller is to gather the necessary events from the GUI framework into a pure data structure that I have here called the `RequestModel`.

Once the `RequestModel` is complete, the controller passes it through the `InputBoundary` interface to the interactor. Again, the interface is there to ensure that the source code dependencies point in an architecturally sound direction.

Testing the interactor is trivial; our tests simply create appropriate request models and hand them to the interactor. We can either check the results directly or use spies to check them. Testing the controller is also trivial—our tests simply invoke events through the event handler interface and then make sure that the controller builds the right request model.

### Test Patterns

There are many different design patterns for testing, and there are several books that have documented them: *XUnit Test Patterns*⁴ by Gerard Meszaros and *JUnit Recipes*⁵ by J. B. Rainsberger and Scott Stirling, to mention just two of them.

- 4. Gerard Meszaros, *XUnit Test Patterns: Refactoring Test Code* (Addison-Wesley, 2012).
- 5. J. B. Rainsberger and Scott Stirling, *JUnit Recipes: Practical Methods for Programmer Testing* (Manning, 2006).

It is not my intention to try to document all those patterns and recipes here. I just want to mention the three that I have found most useful over the years.

#### Test-Specific Subclass

This pattern is primarily used as a safety mechanism. For example, let’s say that you want to test the `align` method of the `XRay` class. However, the `align` method invokes the `turnOn` method. You probably don’t want x-rays turned on every time you run the tests.

The solution, as shown in Figure 4.4, is to create a *test-specific subclass* of the `XRay` class that overrides the `turnOn` method to do nothing. The test creates an instance of the `SafeXRay` class and then calls the `align` method, without having to worry that the x-ray machine will actually be turned on.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_179_0.png)

**Figure 4.4** Test-Specific-Subclass pattern

It is often helpful to make the test-specific subclass a spy so that the test can interrogate the safe object about whether the unsafe method was actually called or not.

In the example, if `SafeXRay` were a spy, then the `turnOn` method would record its invocation, and the test method in the `XRayTest` class could interrogate that record to ensure that `turnOn` was actually called.

Sometimes the *Test-Specific Subclass* pattern is used for convenience and throughput rather than safety. For example, you may not wish the method being tested to start a new process or perform an expensive computation.

It is not at all uncommon for the dangerous, inconvenient, or slow operations to be extracted into new methods for the express purpose of overriding them in a test-specific subclass. This is just one of the ways that tests impact the design of the code.

#### Self-Shunt

A variation on that theme is the *Self-Shunt* pattern. Because the test class *is* a class, it is often convenient for the test class to become the test-specific subclass, as shown in Figure 4.5.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_180_0.png)

**Figure 4.5** Self-Shunt pattern
