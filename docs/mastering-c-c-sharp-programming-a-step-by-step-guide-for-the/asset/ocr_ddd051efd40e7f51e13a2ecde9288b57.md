that all the methods here are public. What that means is that the methods can be called from outside the class, by anyone who has created instances of the class. If we wanted, these could have been made private and, if we had done that, the method would only have been callable from within another method that is within the class. In our case, we want anyone to have the ability to call the methods, which is why we made them public.

Second, there are a number of methods that begin with ‘Get’. One of the most common things in programming is to have some methods that will just return whatever the instance variable value is and to have another that sets the variable value and checking that the value to be assigned is a valid one. Here we have a lot of these GetSomething methods and some SetSomething methods. For the time being, that is what we will go with. However, as this is common, there is a feature in C# that makes all of this so much easier to read and that feature is called Properties, which is what we will be discussing in the next section.

For now, let’s go back to our static keyword.

# Static Methods, Variables, and Classes

Up to now, we’ve been doing a lot of work with variables, specifically instance variables, and with methods belonging to class instances. What this means is that several instances of a class can be created and each will have its own set of data. When you call one of them, it will do the work it needs to by using a set of variables specific to it.

However, previously, all of our methods were static. What does that mean? Any class-level method or variable that has the static keyword belongs to the entire class, not just one instance of it.

As far as variables go, any instance that uses the variable will have the exact same values. For example, if an instance changes the value of a static class value to, let’s say 4, another instance will be able to see the new value and this is because the variables are shared with every class instance.