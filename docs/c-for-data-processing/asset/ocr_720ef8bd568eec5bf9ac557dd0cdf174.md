# 3 Creating Programs

In this chapter we will build on our programming abilities to make programs that are broken down into manageable chunks and find out how a program can store and manipulate large amounts of data using arrays.

# 3.1 Methods

We have already come across the methods Main, WriteLine and ReadLine. Main is the method we write which is where our program starts. WriteLine and ReadLine were provided by the creators of C# to give us a way of displaying text and reading information from the user.

This is what methods are all about. Your programs will contain methods that you create to solve parts of the problem and they will also use methods that have been provided by other people. In this section we are going to consider why methods are useful and how you can create your own.

# 3.1.1 The Need for Methods

In the glazing program above we spend a lot of time checking the values of inputs and making sure that they are in certain ranges. We have exactly the same piece of code to check widths and heights. If we added a third thing to read, for example frame thickness, we would have to copy the code a third time. This is not very efficient; it makes the program bigger and harder to write. What we would like to do is write the checking code once and then use it at each point in the program. To do this you need to define a method to do the work for you.

# Method and Laziness

We have already established that a good programmer is creatively lazy. One of the tenets of this is that a programmer will try to do a given job once and once only.

Up until now all our programs have been in a single method. The method is the block of code which follows the main part of our program. However, C# lets us create other methods which are used when our program runs. Methods give us two new weapons:

+   - We can use methods to let us re-use a piece of code which we have written.
+   - We can also use methods to break down a large task into a number of smaller ones.

We will need both of these when we start to write larger programs. Again, as with lots of features of the C# language, methods don't actually make things possible, but they do help with the organisation of our programs.

Essentially you take a block of code and give it a name. Then you can refer to this block of code to do something for you. As a silly example: