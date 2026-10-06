
For example, suppose you are part of a programming team that has written an extensive customer database program. The program was initially designed so that a customer's name, address, and phone number were stored in String variables. Your job was to design several modules that accept these variables as arguments and perform operations on them. The software has been operating successfully for some time, but your team has been asked to update it by adding several new features. During the revision process, the senior programmer informs you that the customer's name, address, and phone number will no longer be stored in variables. Instead, they will be stored in a String array. This means that you will have to modify all of the modules that you have designed so they accept and work with a String array instead of the three variables. Making these extensive modifications is not only a great deal of work, but also opens the opportunity for errors to appear in your code.

Whereas procedural programming is centered on creating procedures (which are modules and functions), object-oriented programming is centered on creating objects. An object is a software entity that contains both data and procedures. The data contained in an object is known as the object's fields. Fields are simple variables, arrays, or other data structures that are stored in the object. The procedures that object performs are known as methods. An object's methods are nothing more than modules or functions. The object is, conceptually, a self-contained unit that consists of data (fields) and procedures (methods). This is illustrated in Figure 14-1.

# Figure 14-1 An object contains data and procedures

![](img/c939132f78787c7f339c6977b3fc8c85_546_0.png)

OOP addresses the problem of code/data separation through encapsulation and data hiding. Encapsulation refers to the combining of data and code into a single object. Data hiding refers to an object's ability to hide its data from code that is outside the object. Only the object's methods may then directly access and make changes to the object's data. An object typically hides its data, but allows outside code to access via its methods. As shown in Figure 14-2, the object's methods provide self-contained programming statements outside the object with indirect access to the object's data.

## 14.1 Procedural and Object-Oriented Programming

Figure 14-2 Code outside the object interacts with the object's methods

![](img/c939132f78787c7f339c6977b3fc8c85_547_0.png)

When an object's internal data is hidden from outside code and access to data is restricted to the object's methods, the data is protected from accidental corruption. In addition, the programming code outside the object does not need to know about the format or internal structure of the object's data. The code only needs to interact with the object's methods. When a programmer changes the structure of an object's internal data, he or she modifies the object's methods so that they may properly operate on the data. The way in which outside code interacts with the methods, however, does not change.

## Object Reusability

In addition to solving the problems of code/data separation, the use of OOP has been encouraged by the trend of object reusability. An object is not a stand-alone program, but used by programs that need its service. For example, Sharon is a programmer who has developed an object for rendering 3D images. She is a math whiz and knows all about computer graphics, so her object is coded to perform all the necessary 3D mathematical operations and handle the computer's hardware. Tom, who is writing a program for an architectural firm, needs his application to display 3D images of buildings. Because he is working under a tight deadline and does not possess a great deal of knowledge about computer graphics, he can use Sharon's object to perform the 3D rendering (for a small fee, of course).

## An Everyday Example of an Object

Think of your alarm clock as an object. It has the following fields:

- The current second (a value in the range of 0–59)
- The current minute (a value in the range of 0–59)
- The current hour (a value in the range of 1–12)
- The time alarm is set for (a valid hour and minute)
- Whether the alarm is on or off ("on" or "off")

As you can see, the fields are merely data values that define the state that the alarm clock is currently in. The user, of the alarm clock object, cannot directly manipulate these fields because they are private. To change a field value, you must use one of the object's methods. The following are some of the alarm clock object's methods:

- Set time
- Set alarm time
- Turn alarm on
- Turn alarm off

Each method manipulates one or more of the fields. For example, the Set time method allows you to set the alarm clock's time. You activate the method by pressing a button on top of the clock. By using another button, you can activate the Set alarm time method.

In addition, another button allows you to execute the Turn alarm on and Turn alarm off methods. Notice that all of these methods can be activated by you, who are outside of the alarm clock. Methods that can be accessed by entities outside the object are known as public methods.

The alarm clock also has private methods, which are part of the object's private, internal workings. External entities (such as you, the user of the alarm clock) do not have direct access to these methods. The following are the alarm clock's private methods:

- Increment the second
- Increment the minute
- Increment the hour
- Sound alarm

Every second, the Increment second method executes. This changes the value of the current second. If the current second is set to 59, it resets the current second to 0 and then causes the Increment minute method to execute. This adds 1 to the current minute, unless it is set to 59. In that case, it resets the current minute to 0 and causes the Increment hour method to execute. (Note that the Increment minute method compares the new time to the alarm time. If the two times match and the alarm is on, the Sound alarm method is executed.)

![](img/c939132f78787c7f339c6977b3fc8c85_548_0.png)

## Checkpoint

- 14.1 What is an object?
- 14.2 What is encapsulation?
- 14.3 Why is an object's internal data usually hidden from outside code?
- 14.4 What are public methods? What are private methods?

## 14.2 Classes

> **CONCEPT:** A class is a code that specifies the fields and methods for a particular object.

Now, let's discuss how objects are created in software. Before an object can be created, it must be designed by a programmer. The programmer determines the fields and methods that are necessary, and then creates a class. A class is code that specifies the fields and methods of a particular type of object. Think of a class as a "blueprint" that objects may be created from. It serves a similar purpose as the blueprint for a house. The blueprint itself is not a house, but a detailed description of a house. When we use the blueprint to build an actual house, we could say we are building an instance of the house described by the blueprint. If we so, we can build several identical houses from the same blueprint. Each house is a separate instance of the house described by the blueprint. This idea is illustrated in Figure 14-3.

**Figure 14-3** A blueprint and houses built from the blueprint

![](img/c939132f78787c7f339c6977b3fc8c85_549_0.png)

Another way of thinking about the difference between a class and an object is to think of the difference between a cookie cutter and a cookie. While a cookie cutter itself is not a cookie, it describes a cookie. The cookie cutter can be used to make several cookies, as shown in Figure 14-4. Think of a class as a cookie cutter and the objects created from the class as cookies.
