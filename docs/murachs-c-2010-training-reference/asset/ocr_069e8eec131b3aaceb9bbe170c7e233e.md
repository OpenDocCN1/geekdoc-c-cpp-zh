# The code for the Product, Book, and Software classes

Figures 14-9 through 14-11 show the code for the Product base class and its two subclasses, Book and Software. You've seen portions of this code in previous figures, of which it should already be familiar to you.

The Product class, shown in figure 14-9, is the base class for the Book and Software classes. It's almost identical to the previous versions of the Product class that you saw in chapter 12. In fact, the only significant difference is that the GetDisplayText method specifies the virtual keyword. That way, this method can be overridden by the Book and Software classes.

The Book class, shown in figure 14-10, specifies the Product class as its base class. It declares a private instance variable to hold the value of the Author property. This property is defined with get and setters that simply return the value of the instance variable and set the value of this variable that was passed to the property.

The Book class provides two constructors. The first is an empty constructor that lets you create a new Book object with default values. The second constructor lets you specify the code, description, author, and price for a new Book object. This constructor calls the base constructor to initialize the Code, Description, and Price. As a result, the body of this constructor is just a single line of code that initializes the Author property.

The overridden GetDisplayText method for the Book class calls the GetDisplayText method to get a string that includes the code, price, and description. Then, it adds the author's name in parentheses to the end of this string.

The Software class, shown in figure 14-11, is similar to the Book class, but it adds a property named Version. It also provides a constructor that calls the base constructor to initialize the Code, Description, and Price properties before it initializes the Version property. It also overrides the GetDisplayText method by calling the base GetDisplayText method and then adding the version information to the end of the string that's returned.