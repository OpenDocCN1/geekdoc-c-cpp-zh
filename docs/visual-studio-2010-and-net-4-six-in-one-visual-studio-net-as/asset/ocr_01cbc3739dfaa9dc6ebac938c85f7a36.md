The situation gets more and complex if you have several configurations of the application that should be deployed differently to client machines. From the efforts point of view, it means that developers spend approximately 20 percent of their effort developing the original application and about 80 percent maintaining it through the years. You could turn a least of that painful 80 percent into something more useful (for example, investing in creating better business value or an improved user experience), both your customers and your boss would be happy, and you would be better paid. That is where MEF comes into the picture.

# Dynamic Composition

Why is dynamic composition so important? If you create applications from smaller independent components, you can architect the application so that responsibilities are better divided, and boundaries are more obvious. According to these responsibilities, you can test your components separately, find bugs, and correct them. It is easier to handle these small parts individually than it is to maintain them. However, the question is how do you roll these individual parts to form an entire application?

Well, this is what MEF does — parts declare their intention to work together with other parts, and MEF pulls all of them together for the application. Instead of a monolithic and statically compiled piece of software, you could have a dynamically composed one, where you could even have the possibility to “drop into” a new part (as inserting a new LEGO brick to an existing composition). One of the first Microsoft applications that utilizes MEF is Visual Studio 2010, where the code editor is actually built with MEF.

# The Open/Closed Principle

You may think the design methodologies of dynamically composed and statically compiled applications are very different. You cannot say one is easier while the other is more complex. They are simply different. However, there is a primary design principle from the aspect of dynamism that will be your guiding star.

This is the Open/Closed Principle that is credited to Bertrand Meyer in his book *Object Oriented Software Construction* (Upper Saddle, New Jersey: Prentice-Hall, 2000). This principle says that you should create your software entities (components) so that they are open for extensibility, but closed for modifications. It can be translated so that if you create software entities, you should create objects that possess the opportunity to be extended without changing their source code.

One example of this principle is when you create a base class with virtual methods for extensibility points. When it’s time to modify the behavior, you keep the base class untouched, and write a derived class overriding the virtual methods.

The reason behind this principle is that modifying the source code of an existing (even tested) component introduces risks with a relatively high mitigation cost. You can introduce new bugs, change the expected logic, or even break existing interfaces. The Open/Closed Principle actually says that you can modify a system without changing existing code. Instead, you add new (and, of course, tested) code.