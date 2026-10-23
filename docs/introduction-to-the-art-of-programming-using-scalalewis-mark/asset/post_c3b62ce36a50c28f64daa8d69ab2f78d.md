
## Advanced Visibility Options

Scala has more flexibility in visibility modifiers than what is described here. Either private or protected can be followed by square brackets and the name of an enclosing scope of a package, class, trait, or object type. (The object construct will be introduced later in this chapter. The trait construct will appear in a few chapters.) This will make that member publicly visible for everything at that scope and closer to the declaration. The primary benefit of this is that you can give special access to closely related bits of code without making a member public to the whole world.

The square brackets can also include the keyword this. Declaring a member to be private[this] means that it is private not only to other pieces of code, but also to any other instances of the enclosing class. Normally if a method gets hold of a reference to another object of the same type, they can access private members. This will not be the case if the member is private[this].

### 16.1.2 this Keyword

By default, when you write code in a class that calls a method or uses a member of that class, the call is made on the current object or the value from the current object is used. All calls are implicitly made on the current instance. That is exactly what you want most of the time and given the scoping of variables it feels very natural. This implicit specification of an object prevents you from having to specify one. That is fine in general, but occasionally you will have a need to be able to put a name to the current object. For example, you might need to call a function/method that needs an instance of the object as an argument and you want to use the one that the code is currently executing on. When that situation arises you will use the this keyword. this is a name that always refers to the current instance in a class.

Scala is implicitly adding this. in front of your calls to methods and when you access local members. For example, the line

```
bal += amount
```

is really short for

```
this.bal += amount
```

Scala simply added the this for you.

### 16.1.3 Encapsulation/Separating Interface from Implementation

The binding of data and functions together is called ENCAPSULATION. It might not seem like much, but it can have a profound impact on the way that software is developed. Having functionality bound into them makes objects far more self-sufficient. It can also free the programmer from having to think about many types of details.

One of the goals we would like to strive for in our object-oriented programs is to have SEPARATION OF INTERFACE AND IMPLEMENTATION. The interface of an object or some other module of code is the set of constructs that you can interact with directly. For objects that are instances of a class, that would be the public members and methods. The implementation of that interface is what goes on to make the interface do what it is supposed to do. You want these things separate for a few reasons.

One reason is so that modifications to the details of the implementation do not break other code. If the interface and implementation are truly separated, then the code that makes calls to the interface does not depend at all on the details of the implementation. All that it depends on is that the elements of the interface adhere to a particular CONTRACT. That contract tells you what information is needed, what information you will get back, and what side effects, if any, will happen in between. It should not tell you how things are done in between. It should be possible to completely redo the details of how things happen, as long as the new approach does not violate the contract, and still have any code using the implementation work just fine.

Another reason for trying to keep interface and implementation separated is that the interface is typically much simpler than the implementation and it benefits coders to not have to keep too many details in their heads at once. Software has the ability to be arbitrarily complex. This is both a blessing and a curse. The flexibility that this provides is part of why software can do so many different things. However, humans can only keep so many details straight in their head at any given time. When the complexity of the software goes beyond what the programmer can deal with, it is essential that some parts of the complexity can be safely ignored.

The reality is that you have been taking advantage of this separation in everything you have done in this book and will continue to do so as long as you program computers. When you call println, you do not really care about all the details that go on between your call and having characters appear on a display. Thankfully you do not have to think about them either. All those details could change and as long as println keeps its contract of sending your information to the standard output you will not care that it has been changed. This is not just true of println, but of most of the Scala library code that we have been using.

### 16.1.4 Special Methods

There are a few method names that are special when you put them into classes in Scala. In a way, these special methods are rules that you have to learn as special cases. Such things often weigh upon a language. In this case there are not many of them, and the power they provide is quite remarkable.

#### 16.1.4.1 Operator Methods

The first set of things that we might consider special are operator methods. It turns out that these are not really special in Scala. In reality they are just like any other methods in Scala. You can use any method call that takes a single argument using operator syntax as was discussed back in chapter 3. That means you can leave out the dot and the parentheses and just put the operator between the two operands. What makes this more interesting is that Scala accepts names that have symbols in them and most languages do not. This includes names for methods.

We have been using names that contain only letters and numbers and begin with a letter.¹ You can also include symbolic operator characters in certain ways. You can have names that include only operator characters, or you can have letters and numbers, beginning with a letter, followed by an underscore and operator characters. Note that once you get to operator characters in a name, all subsequent characters must be operator characters.

So while we have been using names like timesTwo or times2, the names *, **, ****, etc,

¹ Names can also start with and include underscores though that has also been avoided in this book.

are also completely valid. As with so many things in life, just because you can use symbolic operator names for methods does not mean that you should. They have their place, but if you abuse them it can lead to code that is very difficult to read. As a general rule, you should only use symbolic names when they make sense. Changing from text names that people can read to arbitrary symbol sequences will make it nearly impossible for you, or others, to understand what is going on.

When you call a method using the normal method notation, the order in which things happen is obvious. This is because the argument to the method is found inside of parentheses and the parentheses determine the order. When you use operator notation, there have to be PRECEDENCE rules. You already know that 2+3*4 is 14, not 20. That is because multiplication has higher precedence than addition. This is true in Scala as it is in math. However, the + and * are simply names for methods in Int in this expression. So how does Scala decide that the * should happen before, or have higher precedence than, the +? When methods are used in operator notation, Scala uses the first character in the name to determine precedence. Table 16.1 lists the different levels of precedence that are used.

| Precedence (highest at the top) |
|---|
| other special characters |
| * / % |
| + - |
| : |
| = ! |
| < > |
| & |
| ^ |
| | |
| all letters |
| assignment operators |

TABLE 16.1: This table shows the precedence rules for operators in Scala. The precedence is based on the first character in the operator.

In the case of + and *, the first character happens to be the only character. The table tells us that * has higher precedence than + so it is done first. If you put methods called *** and +++ in a class, the *** would have higher precedence by virtue of starting with *. If you also put a method named ^* it would have lower precedence than either of the other two because of the low precedence of ^. These types of precedence rules exist in most other programming languages as well. The only difference with Scala is that you have the capability of defining our own methods that can be used as operators and have the appropriate precedence.

What if two operators are at the same level of precedence? Which comes first? For example, is 5-3+2 equal to 4 or 0? If the - happens first you get 4. If the + happens first you get 0. The order in which operators of the same precedence occur depends on ASSOCIATIVITY. You are used to operators being LEFT-ASSOCIATIVE. This means that the furthest left operator of a given precedence is done first. Such is the case of + and - and hence the value of the expression 5-3+2 is 4. However, there are some operations that should be RIGHT-ASSOCIATIVE. An example of this from standard math is exponentiation. For example 3^3^3 = 3^(3^3) ≠ (3^3)^3. The numbers are grouped from right to left here, not the normal left to right of other operations.

An operator in Scala is right-associative if it ends with a :. In addition to being right-associative, it is called on the object to the right side of it and the value on the left side
