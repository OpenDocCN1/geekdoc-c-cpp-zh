# How to code and call methods

In chapter 3, you learned how to code methods that are executed automatically when a Click event occurs. Now, you’ll learn how to code methods that you call explicitly from other methods in the application. That can lead to code that’s easier to read and maintain.

# How to code methods

Figure 6-1 shows how to code a method. To start, you code an access modifier that indicates whether the method can be called from other classes. In most cases, you’ll use the private access modifier so the method can only be called from within the class where it’s coded. If you need to call the method from another class, however, you can use the public access modifier.

After the access modifier, you code the return type for the method, which identifies the type of data that the method returns. To specify a return type, you can use the keyword for any of the built-in data types, or you can specify the name of any class, structure, or enumeration. Then, within the method, you must code a return statement that identifies the value to be returned. This value must correspond to the data type that’s specified as the return type.

If the method doesn’t return any data, you code the void keyword as the return type. Then, you don’t code a return statement.

After the return type, you code the name of the method. In most cases, you’ll give the method a name that indicates the action it performs. A common coding convention is to start each method name with a verb. This convention is used in the names for the methods in this figure: DisableButtons(), GetDiscountPercent(), and CalculateFutureValue().

After the method name, you code a set of parentheses. Within the parentheses, you declare the parameters that are required by the method. This is known as the parameter list. Later, when you call the method, you pass arguments that correspond to these parameters. You’ll learn more about that in the next figure.

If a method doesn’t require any parameters, you code an empty set of parentheses as shown in the first example in this figure. Here, a method named DisableButtons() simply assigns a false value to the Enabled properties of two buttons. However, if a method does require parameters, you code them within the parentheses as shown in the second and third examples. Here, the second method calculates and returns a decimal discount percent based on a subtotal, and the third method calculates and returns a decimal future value based on a monthly investment, a monthly interest rate, and a number of months.

When you code the name and parameter list of a method, you form the signature of the method. Later in this book, you’ll learn how to code two or more methods with the same name but with different parameters. This is known as overloading a method.

Incidentally, Visual Studio doesn’t provide an easy way to start the code for a new method. So you just start the method by typing the code into the class and using the IntelliSense feature whenever it’s available.