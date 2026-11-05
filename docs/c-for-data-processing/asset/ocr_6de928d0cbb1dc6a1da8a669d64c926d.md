# 4.5.4 Test Driven Development

I love test driven development. If I ever write anything new you can bet your boots that I will write it using a test driven approach. This solves three problems that I can see:

+   1. You don't do the testing at the end of the project. This is usually the worst time to test, since you might be using code that you wrote some time back. If the bugs are in an old piece of code you have to go through the effort of remembering how it works. Far better to test the code as you write it, when you have the best possible understanding of what it is supposed to do.
+   
+   2. You can write code early in the project which will probably be useful later on. Many projects are doomed because people start programming before they have a proper understanding of the problem. Writing the tests first is actually a really good way of refining your understanding. And there is a good chance that the tests that you write will be useful at some point too.
+   
+   3. When you fix bugs in your program you need to be able to convince yourself that the fixes have not broken some other part (about the most common way of introducing new faults into a program is to mend a bug). If you have a set of automatic tests that run after every bug fix you have a way of stopping this from happening.

So, please develop using tests. You will thank me later.

# Programmer's Point: Some things are hard to test

Test development is a good way to travel, but it does not solve all your problems. Some types of programs are really hard to test in this way. Anything with a front end where users type in commands and get responses is very hard to test like this, because although it is easy to send things into a program it is often much harder to see what the program does in response. My approach in these situations is to make the user interface part a very thin layer which sits on top of requests to objects to do the work. In the case of our bank account above, the code that provides the user interface where the customer enters how much they want to withdraw will be very simple and connect directly to the methods provided by my objects. As long as my object tests are passed, I can be fairly confident that the user interface will be OK too.

The other kind of program that is very hard to test in this way is any kind of game. This is mainly because the quality of gameplay is not something you can design tests for. Only when someone comes back and says "The game is too hard because you can't kill the end of level boss without dying" can you actually do something about it. The only solution in this situation is to set out very clearly what your tests are trying to prove (so that the human testers know what to look for) and make it very easy to change the values that will affect the gameplay. For example it should be easy to adjust how much damage a hit from an alien causes to your spacecraft, and the speed of all the game objects.

# 4.6 Static Items

At the moment all the members that we have created in our class have been part of an instance of the class. This means that whenever we create an instance of the Account class we get a balance member. However, we can also create members which are held as part of the class, i.e. they exist outside of any particular instance.

# 4.6.1 Static class members

The static keyword lets us create members which are not held in an instance, but in the class itself.

It is very important that you learn what static means in the context of C# programs. We have used it lots in just about every program that we have ever written: