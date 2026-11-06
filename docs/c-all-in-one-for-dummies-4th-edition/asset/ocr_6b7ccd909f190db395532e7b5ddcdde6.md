+   - **Class definition:** The class definition describes the class. It starts with the word *class*, and then has the name of the class, followed by an open brace and closing brace. Inside the braces are the members of the class.
+   - **Property:** A *property* is a characteristic in a class, such as a color, style, or other descriptive element. You list the properties inside the class (normally before any methods, but there is no rule that says you must do so). Each instance of the class gets its own copy of each property.
+   - **Method:** A *method* is a capability of a class — some task that the class can perform. As with properties, you list methods inside the class. When you call a method for a particular instance, the method accesses the properties for the instance.

When you divide the class, you put part in the header file and part in the source code file. The following list describes what goes where:

+   - **Header file:** Put the class definition in the header file. Properties appear as part of the class definition within the header. You can include the method code inside the class definition if it's a short method. Most people prefer not to put any method code longer than a line or two in the header — in fact, many don't put any method code at all in the header. You may want to name the header file the same as the class but with an .h or .hpp extension. Thus, the class Pen, for instance, might be in the file Pen.h.
+   - **Source file:** If your class has methods, and you didn't put the code in the class definition, you need to put the code in a source file. When you do, precede the function name with the class name and the scope resolution operator (::). If you named the header file the same as the class, you probably want to name the source file the same as the class as well but with a .cpp extension.

# Working with a Class

Many handy tricks are available for working with classes. In this section, you explore several clever ways of working with classes, starting with the way you can hide certain parts of your class from other functions that are accessing them.

# Accessing members

When you work with an object in real life, there are often parts of the object that you interact with and other parts that you don't. For example, when you use the computer, you type on the keyboard but don't open the box and poke around with