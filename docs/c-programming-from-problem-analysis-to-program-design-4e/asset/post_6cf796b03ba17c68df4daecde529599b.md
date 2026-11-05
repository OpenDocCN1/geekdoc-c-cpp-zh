
real-world entities. The C# language was designed to take advantage of the benefits of the object-oriented methodology.

With **object-oriented analysis, design, and programming**, the focus is on determining the objects you want to manipulate rather than the processes or logic required to manipulate the data. Remember that the procedural approach focuses on processes. One of the underlying assumptions of the object-oriented methodology is that the world contains a number of entities that can be identified and described. An **entity** is often defined as a person, place, or thing. It is normally a noun. By **abstracting out the attributes** (data) and the **behaviors** (processes on the data), you can divide complex phenomena into understandable entities. An **abstraction** is simply a description of the essential, relevant properties of an entity. For example, you should easily be able to picture in your mind, or conceptualize, the entities of people, school personnel, faculty, student, undergraduate student, graduate student, vehicle, car, book, school, animal, dog, and poodle by describing **characteristics** or attributes, and **behaviors** or actions, about each of these.

Consider the case of a student. A student has these characteristics or attributes: student ID, name, age, GPA, major, and hometown. The characteristics can be further described by identifying what type or kind of data might exist in each of them. For example, alphabetic characters would be found in the name attribute. Whole numbers without a decimal would be found in the age attribute, and numbers with a decimal would be in the GPA attribute.

In addition to abstracting the data properties, you should also be able to think about some of the actions or behaviors of each of the entities identified in the previous paragraph. Behaviors associated with a student include actions such as Apply for Admission, Enroll as Student, Get Final Grade, Change Name, and Determine GPA. Using the object-oriented methodology, these attributes and actions (or characteristics and behaviors) are **encapsulated**, which means that they are combined together to form a class.

A **class diagram** is one of the primary modeling tools used by object-oriented programmers. Figure 1-9 illustrates the Student class diagram using the Unified Modeling Language (UML) notation. The top portion of the diagram identifies the name of the class, which is Student. The section in the center contains the data members and the type of data that would be found in each data member. **Information hiding** is an important component of object-oriented programming. The minus symbol (–) to the left of the data member’s name refers to the access modifier and indicates the member is private and accessible to that class only. The bottom portion of the diagram in Figure 1-9 shows actions, or methods, of the Student class. The plus symbol (+) access modifier indicates that the behaviors are public and available outside of the class. You will read more about class diagrams in upcoming chapters. This UML notation is used throughout the book for creating class diagrams.

![](img/36e48639a06772bcb0fa1ea2525b33a3_57_0.png)
**FIGURE 1-9** Student class diagram

A class is like a template. It is similar to a blueprint for a house. Even though you define all the characteristics of a house in the blueprint, the house does not exist until one is built using that template. Many houses can be created using the same template. In object-oriented terminology, the constructed house is one instance (object) of the blueprint or template. You **instantiate** the blueprint by building a house using that template. Many objects of a particular class can be instantiated. Thus, an **object** is an **instance** of the class.

Examine the expanded example of a student with the following data members:

- Student number: 122223
- Student name: Justin Howard
- Age: 18
- GPA: 3.80
- Major: CS
- Hometown: Winchester, Kentucky

When these data members are associated with the class, an object is created or **constructed**. A second object could be instantiated from that class by giving values to its members (e.g., 228221, Elizabeth Czerwinski, 21, 4.0, ENG, Reno, Nevada).

The object-oriented methodology facilitates designing components, which contain code that can be reused by packaging together the attributes of a data type along with the actions of that type. In Chapter 4 you will create your own classes that you instantiate.

Through inheritance, it is possible to define subclasses of data objects that share some or all of the parent’s class characteristics. This is what enables reuse of code. For example, you should be able to visualize that Student is a subset of Person, just as Teacher is a subset of Person. Using object-oriented design, you could abstract out the common characteristics of all people and place them in a superclass. Through inheritance, Student and Teacher can use the characteristics of Person and add their own unique members.

Another important object-oriented concept is polymorphism. Behaviors or methods of parent and subclasses can have the same name, but offer different functionality. Through polymorphism, you are able to invoke methods of the same name on objects of different classes and have the correct method executed. For example, you might have subclasses of UndergraduateStudent and GraduateStudent. They could both inherit characteristics from the Student class. Both of the subclasses might have their own method that contains details about how to determine their cost of tuition. Both subclasses might name their method DetermineTuitionCosts(). Through polymorphism, the correct method is executed based on which object invoked it. When an object of the UndergraduateStudent class is used, the DetermineTuitionCosts() method of the UndergraduateStudent class is used. When an object of the GraduateStudent class is used, the DetermineTuitionCosts() method of the GraduateStudent class is used. You will read much more about object-oriented features in upcoming chapters. In Chapter 11 you will read about advanced object-oriented programming features including inheritance and polymorphism. In that chapter you will write multiclass solutions.

The object-oriented principles are of particular importance when writing software using C#. No program can be written that does not include at least one class. All program statements written using the C# language are placed in a class.

Whether you are using a procedural or object-oriented approach, you should follow the five steps to program development. As with the procedural approach, the object-oriented development process is iterative. During design and subsequent phases, do not hesitate to reconsider analysis and design decisions.

## Evolution of C# and .NET

### Programming Languages

In the 1940s, programmers toggled switches on the front of computers to enter programs and data into memory. That is how some of the early programming began. Even when they moved to punching 0s and 1s on cards and reading the cards into memory, it could not have been much fun to be a programmer. Coding was very tedious and prone to error. In the 1950s, assembly languages replaced the binary notation by using mnemonic symbols to represent the instructions for the computer. Symbols such as MV were used to represent moving the contents of one value in memory to another memory location. Assembly languages were designed to make the programmer’s job easier by using these mnemonic symbols instead of binary numbers. However, the instructions depended on the particular CPU architecture. Statements to perform the same task differed from computer to computer. Assembly languages are still considered **low-level programming languages**. As you can see from Figure 1-10, these types of instructions are not easy to read or understand. They are not considered close to the English language, as high-level programming languages such as C# and Java are.

![](img/36e48639a06772bcb0fa1ea2525b33a3_59_0.png)
**FIGURE 1-10** Assembly language instruction to add two values

High-level languages came into existence in the late 1950s with **FORTRAN** (Formula Translator) and later **COBOL** (Common Business Oriented Language). These languages were considered **high-level languages** because they were designed to be accessible to humans, easy to read and write, and close to the English language. Since then, more than 2000 high-level languages have come into existence. Some have gone by the wayside, while others have evolved and are still widely used today.

Some of the more noteworthy high-level programming languages are C, C++, Visual Basic, Java, and now C#. **C++** is an extension of C, which actually evolved from BCPL and B in 1973. Dennis Ritchie is credited with developing the C programming language; Bjarne Stroustrup at Bell Labs is considered the father of C++ for his design work in the early 1980s. C++ includes features that enabled programmers to perform object-oriented programming. C++ is used heavily in the computer industry today.

Smalltalk, considered a pure object-oriented language, was developed at the Xerox Palo Alto Research Center (PARC). Visual Basic, introduced in 1991, derived from the BASIC (Beginners All Purpose Symbolic Code) programming language, a language developed in the 1960s. The earlier versions of Visual Basic did not facilitate development using an object-oriented approach. Earlier versions of Visual Basic did, however, facilitate easy creation of Windows-based graphical user interfaces (GUIs). Visual Basic has been used for a great deal of application development because of this.
