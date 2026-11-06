And in such arguments (sorry — discussions), one of the words that usually pops up is encapsulation. People who defend C++ as being object-oriented point out that it supports encapsulation.

Instead of arguing, let's just all agree that yes, C++ lets you program objects and classes. Now that we've put that argument to rest and can all live peacefully, what exactly does encapsulation mean?

First, think about the word itself. A big part of it is capsule. A capsule is a small container. In the bigger picture, it's, well, a self-contained container that contains things. In the world of computer programming, encapsulation refers to the process of creating a stand-alone object that can take care of itself and do what it must do while holding on to information.

For example, to model a cash register, it would likely be a class. We'd encapsulate the cash register by putting everything about the register (its capabilities and characteristics) into a single class. In C++, the capabilities would be member functions and the characteristics would be member variables.

When we create the class, we would make some of the member variables and member functions public; we would make others private. (Some members can be protected, so derived classes could access them, but they still would not be public.) What exactly would private and protected member variables and member functions be? The parts that you don't want other functions modifying, that's what. For example, the cash register would probably have a value inside it representing the total dollar amount that the register contains. But the functions that use the class would not directly modify that value. Instead, they would call various member functions to perform transactions. One transaction might be Sale(). Another transaction might be Refund(); another might be Void(). These would be the capabilities of the register in the form of public methods, and they would modify the cash value inside the register, making sure that it balances with the sales and returns. If a function could just modify the cash value directly, the balance would get out of whack.

Book II Chapter 1 Planning and Building Objects

# # Accessing read-only member variables

Suppose that you have a class that contains a member variable, and you want to allow users to retrieve the value of the variable but not change it. For example, in the Dog class, you might set the weight in the constructor, and that's it — after that, users can get the weight but can't change it. The way to do that is to simply not have a method that sets the value. Instead, you have a method that only retrieves the value. Thus, the Dog class would have the GetWeight() method, but you would not have the SetWeight() method. Then users can only read the value, not set it.