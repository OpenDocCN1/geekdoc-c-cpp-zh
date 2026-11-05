A big part of learning to program is learning how to use all the additional features of the system which support your programs.

# using System;

This is an instruction to the C# compiler to tell it that we want to use things from the System namespace. A namespace is a place where particular names have meaning. We have namespaces in our conversations too, if I am using the “Football” namespace and I say “That team is really on fire” I’m saying something good. If I am using the “Firefighter” namespace I’m saying something less good.

In the case of C# the System namespace is where lots of useful things are described. One of these useful things provided with C# is the Console object which will let me write things which will appear on the screen in front of the user. If I want to just refer to this as Console I have to tell the compiler I’m using the System namespace. This means that if I refer to something by a particular name the compiler will look in System to see if there is anything matching that name. We will use other namespaces later on.

Classes are the basis of object oriented programming, as we shall see later.

# class GlazerCalc

A C# program is made up of one or more classes. A class is a container which holds data and program code to do a particular job. In the case of our double glazing calculator the class just contains a single method which will work out our wood lengths and glass area, but a class can contain much more than that if it needs to.

You need to invent an identifier for every class that you create. I’ve called ours GlazerCalc since this reflects what it does. For now, don’t worry too much about classes, just make sure that you pick sensible names for the classes that you create.

Oh, and one other thing: There is a convention that the name of the file which contains a particular class should match the class itself, in other words the program above should be held in a file called GlazerCalc.cs

# static

This keyword makes sure that the method which follows is always present, i.e. the word static in this context means “is part of the enclosing class and is always here”. When we get to consider objects we will find that this little keyword has all kinds of interesting ramifications. But for now I’d be grateful if you’d just make sure that you put it here in order to make your programs work properly.

# void

A void is nothing. In programming terms the void keyword means that the method we are about to describe does not return any item of interest to us. The method will just do a job and then finish. In some cases we write methods which return a result (in fact we will use such a method later in the program).

However, in order to stop someone else accidentally making use of the value returned by our Main method, we are explicitly stating that it returns nothing. This makes our programs safer, in that the compiler now knows that if someone tries to use the value returned by this method, this must be a mistake.

# Main

You choose the names of your methods to reflect what they are going to do for you. Except for Main. This method (and there must be one, and only one such method) is where your program starts running. When your program is loaded and run the first method given control is the one called Main. If you miss out the Main method the system quite literally does not know where to start.