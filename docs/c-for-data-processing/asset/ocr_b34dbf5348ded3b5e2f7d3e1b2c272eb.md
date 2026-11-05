```
case "name":
    EditName(account);
    break;
case "pay":
    PayInFunds(account);
    break;
case "draw":
    WithDrawFunds(account);
    break;
}
} while ( command != "exit" );
```

# Programmer's Point: Every Message Counts

You should remember that every time your program sends text to the user you may have a problem with language. The menu for my bank account edit method sample code prints out text which is hard wired to English. In a properly written program this would be managed in terms of message numbers to make it easier to change the text which is output.

As a general rule in a production system you should never write out straight text to your user (this includes the names of commands that the user might type in). Everything should be managed in terms of message numbers. The only exception to this is the situation where the customer has assured you that the program will only ever be written for use in a particular language. The C# libraries contain a set of resources which help you manage the internationalization of your programs.

# BANK NOTES: MORE THAN ONE USER INTERFACE

The bank may have a whole range of requirements for editing account details. These will range from an operator in a call centre, an operator on a dial up terminal, a customer on a mobile phone and a customer at a cash machine. I hope that you can see that the only way we can manage all these different ways of interacting with the bank account is to separate the business object (the account itself) from the input/output behaviour.

Note that we never do things like allow the user interface code to decide what constitutes a valid name. This question is not the responsibility of the front end. The only thing that can decide on the validity of a name is the account object itself. The user interface must always work on the basis that it will use the business object to perform this kind of validation.

# 5.4 A Graphical User Interface

It should come as no surprise that a graphical user interface on the screen is represented by objects. When we are dealing with windows on the screen our program is actually calling methods in the objects to make them do things like change size and colour.

# 5.4.1 Creating a Form

If I want a form on the screen for the user to interact with, I need to create an instance of an object to do this for me. The object that I create is a Form. This class can be found in the System.Windows.Forms namespace. I can create an instance of this class and ask it to do things for me.