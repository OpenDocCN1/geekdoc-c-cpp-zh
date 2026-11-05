
You might think this is strange, in that normally the compiler loses no time in telling you off when you don't do something, but in this case it is simply solving the problem without telling you. There are two ways to look at this:

- nice compiler: the compiler is trying to make life easier for you
- evil compiler: the compiler knows that if it does this automatically now you will suffer more later when you try to understand why you don't need to add one

How you regard the action of the compiler is up to you.

## 4.7.1 The Default Constructor

A constructor method has the same name as the class, but it does not return anything. It is called when we perform new. If you don't supply a constructor (and we haven't so far) the compiler creates one for us.

```
public class Account
{
    public Account ()
    {
    }
}
```

This is what the default constructor looks like. It is public so that it can be accessed from external classes who might want to make instances of the class. It accepts no parameters. If I create my own constructor the compiler assumes that I know what I'm doing and stops providing the default one. This can cause problems, which we will discuss later.

## 4.7.2 Our Own Constructor

For fun, we could make a constructor which just prints out that it has been called:

```
public class Account
{
    public Account ()
    {
        Console.WriteLine ( "We just made an account" );
    }
}
```

This constructor is not very constructive (ho ho) but it does let us know when it has been called. This means that when my program executes the line:

```
robsAccount = new Account();
```

the program will print out the message:

We just made an account

Note that this is not very sensible, in that it will result in a lot of printing out which the user of the program might not appreciate, but it does show how the process works.

### Feeding the Constructor Information

It is useful to be able to get control when an Account is created, but it would be even nicer to be able to feed information into the Account when I create it. As an example, I might want to set the name, address, and initial balance of an account holder when the account is created. In other words I want to do:

```
robsAccount = new Account( "Rob Miles", "Hull", 0 );
```

This would create a new account and set the name property to Rob Miles, the address to Hull and the initial balance to zero. It turns out that I can do this very easily, all I have to do is make the constructor method to accept these parameters and use them to set up the members of the class:

```
class Account
{
    // private member data
    private string name;
    private string address;
    private decimal balance;

    // constructor
    public Account(string inName, string inAddress, decimal inBalance)
    {
        name = inName;
        address = inAddress;
        balance = inBalance;
    }
}
```

The constructor takes the values supplied in the parameters and uses them to set up the members of the Account instance that is being created. In this respect it behaves exactly as any other method call.

Note that adding a constructor like this has one very powerful ramification:

You must use the new constructor to make an instance of a class, i.e. the only way I can now make an Account object is by supplying a name, address and starting balance. If I try to do this:

```
robsAccount = new Account();
```

- the compiler will stop being nice to me and produce the error:

```
AccountTest.cs(9,27): error CS1501: No overload for method 'Account' takes 0 arguments
```

When the compiler is telling me that there is no constructor in the class which does not have any parameters, in other words, the compiler only provides a default constructor if the programmer doesn't provide a constructor.

This can cause confusion if we have made use of the default constructor in our program and we then add one of our own. The default constructor is no longer supplied by the compiler and our program now fails to compile correctly. In that situation you have to either find all the calls to the default one and update them, or create a default constructor of your own for these calls to use. Of course you don't have to do this because your design of the program was so good that you never have this problem. Just like me, hem hem.

## 4.7.3 Overloading Constructors

Overload is an interesting word. In the context of the "Star Trek" science fiction series it is what they did to the warp engines in every other episode. In the context of a C# program it means:

> "A method has the same name as another, but has a different set of parameters."

The compiler is quite happy for you to overload methods, because it can tell from the parameters given at the call of the method which one to use. In the context of the constructor of a class, what this means is that you can provide several different ways of constructing an instance of a class. For example, many (but not all) of your accounts will be created with a balance value of zero, i.e. nothing in the account. This means that we would like to be able to write

```
robsAccount = new Account("Rob Miles", "Null");
```

I've missed off the balance value, since I want to use the "default" one of zero. If your code does this the compiler simply looks for a constructor method which has two strings as parameters, and nothing else. Something a bit like this:

```
public Account (string inName, string inAddress)
{
    name = inName;
    address = inAddress;
    balance = 0;
}
```

### Overloading a method name

In fact, you can overload any method name in your classes. This can be useful if you have a particular action which can be driven by a number of different items of data, for example you could provide several ways of setting the date of a transaction:

```
SetDate ( int year, int month, int day )
SetDate ( int year, int julianDate )
SetDate ( string dateInMMDDYY )
```

A call of:

```
SetDate ( 23, 7, 2005 );
```

- would be matched up with the method which accepts three integer parameters and that code would be executed.

## 4.7.4 Constructor Management

If the ACCOUNT class is going to have lots of constructor methods this can get very confusing for the programmer:

```
public Account (string inName, string inAddress, decimal inBalance)
{
    name = inName;
    address = inAddress;
    balance = inBalance;
}
```

```
public Account (string inName, string inAddress)
{
    name = inName;
    address = inAddress;
    balance = 0;
}
```

```
public Account (string inName)
{
    name = inName;
    address = "Not Supplied";
    balance = 0;
}
```

I've made three constructors for an ACCOUNT instance. The first is supplied with all the information, the second is not given a balance and sets the value to 0. The third is not given the address either, and sets the address to "Not Supplied".

To do this I have had to duplicate code. Good programmers hate duplicating code. It is regarded as "dangerous extra work". The scary thing is that it is quite easy to do, just use the block copy command in the text editor and you can take the same piece of program and use it all over the place. But you should not do this. Because it is bad. If you need to change this piece of code you have to find every copy of the code and change it.

This happens more often than you'd think, even if you don't put a bug in your code, you still might find yourself having to change it because the specification changes. So, C# provides a way in which you can call one constructor from another. Consider:

```csharp
public Account (string inName, string inAddress,
                decimal inBalance)
{
    name = inName;
    address = inAddress;
    balance = inBalance;
}

public Account ( string inName, string inAddress ) :
    this (inName, inAddress, 0 )
{
}

public Account ( string inName ) :
    this (inName, "Not Supplied", 0 )
{
}
```

The keyword this means “another constructor in this class”. As you can see in the code sample above, the highlighted bits of the code are calls to the first constructor. They simply pass the parameters which are supplied, along with any default values that we have created, on to the “proper” constructor to deal with. This means that the actual transfer of the values from the constructor into the object itself only happens in one method, and the other constructor methods just make calls to it.

The syntax of these calls is rather interesting, in that the call to the constructor takes place before the body of the constructor method. In fact it is outside the block completely. This is sensible, because it reflects exactly what is happening. The “this” constructor runs before the body of the other constructor is entered. In fact, in the code above, since the call of this does all the work, the body of the constructor can be empty.

> > **Programmer's Point: Object Construction Should Be Planned**
> >
> > The way in which objects are constructed is something that you should plan carefully when you write your program. You should create one “master” constructor which handles the most comprehensive method of constructing the object. Then you should make all the other constructor methods use this to get hold of that method.

## 4.7.5 A constructor cannot fail

If you watch a James Bond movie there is usually a point at which agent 007 is told that the fate of the world is in his hands. Failure is not an option. Constructors are a bit like this. Constructors cannot fail. And this is a problem.

Whenever we have written methods in the past we have made sure that their behaviour is error checked to that the method cannot upset the state of our object. For example, attempts to withdraw negative amounts of money from a bank account should be rejected.

The whole basis of the way that we have allowed our objects to be manipulated is to make sure that they cannot be broken by the people using them. If you try to do something stupid with a method call it should refuse to perform the action and return something which indicates that it could not do the job.

So we know that when we create a method which changes the data in an object we have to make sure that the change is always valid. For example, we would not let the following call succeed:

```csharp
RobsAccount.PayInFunds (1234567890);
```

There will be an upper limit to the amount of cash you can pay in at once, so the PayInFunds method will refuse to pay the money in. But what is to stop the following:

```csharp
RobsAccount = new Account ("Rob", "Hull", 1234567890);
```
