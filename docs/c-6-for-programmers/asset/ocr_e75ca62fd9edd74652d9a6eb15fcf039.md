> > **Error-Prevention Tip 4.1**
> >
> > *Making a class's instance variables private and its methods (and as you'll see, properties) public and accessing those instance variables only through the class's methods and properties facilitates debugging, because problems with data manipulations are localized to the methods (and properties).*

> > **Common Programming Error 4.1**
> >
> > *An attempt by a method that's not a member of a particular class to access a private member of that class is a compilation error.*

# ### 4.3.7 Account UML Class Diagram

We'll often use UML class diagrams to summarize a class's attributes and operations. In industry, UML diagrams help systems designers specify systems in a concise, graphical, programming-language-independent manner, before programmers implement the systems in specific programming languages. Figure 4.3 presents a UML class diagram for class Account of Fig. 4.2.

![](bbox=[0.341, 0.44, 0.651, 0.532])

Fig. 4.3 | UML class diagram for class Account of Fig. 4.2.

*Top Compartment*

In the UML, each class is modeled in a class diagram as a rectangle with three compartments. In this diagram the top compartment contains the class name Account centered horizontally in boldface type.

*Middle Compartment*

The middle compartment contains the class's attribute names, which correspond to the instance variables of the same names in C#. The single instance variable name in Fig. 4.2 is private in C#, so the UML class diagram lists a minus sign (-) UML access modifier before the attribute's name. Following the attribute's name are a colon and the attribute type, in this case string.

*Bottom Compartment*

The bottom compartment contains the class's operations, SetName and GetName, which correspond to the methods of the same names in C#. The UML models operations by listing the operation name preceded by a UML access modifier, for example, + SetName. This plus sign (+) indicates that SetName is a public operation in the UML (because it's a public method in C#). Operation GetName is also a public operation.