
Look at all possible (if seemingly unrelated) factors in the manifestation of the bug. This is particularly important if the bug is intermittent. If the bug appears on Friday afternoons on your UNIX system, find out if another department uses the machine to do a payroll run at that time and fills up all the scratch space, or the loading department turns on the big hoist and injects loads of noise into the mains.

Leave the problem alone for a while. Go off and do something different and you may find that the answer will just appear. Alternatively, you may find the answer as soon as you come back to the problem.

Remember that although the bug is of course impossible, it is happening. This means that either the impossible is happening, or one of your assumptions that it is impossible is wrong!

Can you get back to a state where the bug was not present, and then look at the changes made since? If the system is failing as a result of a change or, heaven forbid, a bug fix, try to move back to a point where the bug is not there, and then introduce the changes until the bug appears. Alternatively, look carefully at how the introduction of the feature affects other modules in the system. A good Source Code Control System is very valuable here, in that it can tell you exactly what changes have been made from one version to the next.

One thing that I should make clear at this point is that the process of debugging is that of fixing faults in a solution which should work. In other words, you must know how the program is supposed to work before you try and fix problems with what it actually does. I have been nearly moved to tears by the sight of people putting in another loop or changing the way their conditions operate to 'see if this will make the program work'. Such efforts are always doomed, just like throwing a bunch of electrical components at the wall and expecting a DVD player to land on the floor is also not going to work.

### Rip it up and start again

In some projects it is possible that the effort involved in starting again is less than trying to find out what is wrong with a broken solution that you have created. If you have taken some time off from debugging, explained the code to a friend and checked all your assumptions, then maybe, just maybe, this might be the best way forward.

### Programmer's Point: Bug Fixes Cause Bugs

The primary cause of bugs is probably the bug fixing process. This is because when people change the program to make one bit of it work, the change that they make often breaks other features of the system. I have found statistics which indicate that 'two for one' is frequently to be expected, that is, every bug fix will introduce two brand new bugs. The only way round this is to make sure that your test process (which you created as a series of lots of unit tests) can be run automatically after you've applied the fix. This at least makes sure that the fix has not broken anything important.

## 5.9.3 Making Perfect Software

There is no such thing as perfect software. One of the rules by which I work is that 'any useful program will have bugs in it'. In other words I can write programs that I can guarantee will contain no bugs. However, such programs will be very small and therefore not be good for much. As soon as I create a useful program, with inputs, outputs and some behaviours, I start introducing bugs.

This does not mean that every program that I write is useless, just that it will not be perfect. When considering faults you must also consider their impact. Part of the job of a project manager in a development is deciding when a product is good enough to sell, and whether or not a fault in the code is a 'stopper' or not.

A stopper is a fault which makes the program un-saleable. If the program crashes every third time you run it, or sometimes destroys the filestore of the host computer, this is probably the behaviour of a stopper bug. But if it does something like always output the first page twice if you do a print using the Chinese font and a certain kind of laser printer, this might be regarded as a problem most users could live with.

This means that you need to evaluate the impact of the faults that get reported to you, prioritise them and manage how they are dealt with. You also need to be aware of the context of the development. For example, a fault in a video game is much less of a problem than one in an air traffic control system.

The key to making software that is as perfect as possible is to make sure that you have a good understanding of the problem that you are solving, that you know how to solve it before you start writing code and that you manage your code production process carefully. Read some of the recommended texts at the end of this document for more on this aspect of programming.

## 5.10 The End?

This is not all you need to know to be a programmer. It is not even all you need to know to be a C# programmer. However, it is quite a good start, but there are quite a few things missing from this text, because we don't have time to teach them all. You should take a look at the following things if you want to become a great C# programmer:

- serialisation
- attributes
- reflection
- networking

### 5.10.1 Continuous Development

A good programmer has a deliberate policy of constantly reviewing their expertise and looking at new things. If you are serious about this business you should be reading at least one book about the subject at any one time. I have been programming for as long as I can remember but I have never stopped learning about the subject. And I've never stopped programming, reading books about programming and looking at other people's code:

### 5.10.2 Further Reading

**Code Complete Second Edition:**  
Steve McConnell  
Published by Microsoft: ISBN 0-7356-1967-0

Not actually a book about C#. More a book about everything else. It covers a range of software engineering and programming techniques from the perspective of "software construction". If you have any serious intention to be a proper programmer you should/must read/own this book.

**How to be a programmer**

This web site is also worth a read, as it covers the behaviours of a programmer very well indeed.

http://samizdat.mines.edu/howto/HowToBeAProgrammer.html

## 6 Glossary of Terms

### Abstract

Something which is abstract does not have a "proper" existence as such. When writing programs we use the word to mean "an idealised description of something". In the case of component design an abstract class contains descriptions of things which need to be present, but it does not say how they are to be realised. In C# terms a class is abstract if it is marked as such, or if it contains one or more methods which are marked as abstract.

You can't make an instance of an abstract class, but you can use it as the basis of, or template for, a concrete one. For example, we may decide that we need many different kinds of receipt in our transaction processing system: cash receipt, cheque receipt, wholesaler receipt etc. We don't know how each particular receipt will work inside, but we do know those behaviours which it must have to make it into a receipt.

We can therefore create an abstract Receipt class which serves as the basis of all the concrete ones. Each "real" receipt class is created by extending the parent, abstract one. This means that it is a member of the receipt family (i.e. it can be treated as a Receipt) but it works in its own way.

### Accessor

An accessor is a method which provides access to the value managed within a class. Effectively the access is read only, in that the data is held securely in the class but code in other classes may need to have access to the value itself. An accessor is implemented as a public method which will return a value to the caller. Note that if the thing being given access to is managed by reference, the programmer must make sure that it is OK for a reference to the object to be passed out. If the object is not to be changed it may be necessary to make a copy of the object to return to the caller.

### Base

base is a C# keyword which has different meanings depending on the context in which it is given. It is used in a constructor of a child class to call the constructor in the parent. It is also used in overriding methods to call the method which they have overridden.

### Call

When you want to use a method, you call it. When a method is called, the sequence of execution switches to that method, starting at the first statement in its body. When the end of the method, or the return statement, is reached, the sequence of execution returns to the statement immediately following the method call.

### Class

A class is a collection of behaviours (methods) and data (properties). It can be used to represent a real world item in your program (for example a bank account). Whenever you need to collect a number of things into a single unit you should think in terms of creating a class.
