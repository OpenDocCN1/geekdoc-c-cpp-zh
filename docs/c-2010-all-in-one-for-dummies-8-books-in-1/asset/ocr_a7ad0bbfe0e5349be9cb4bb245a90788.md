To show what I mean in pictures, Figure 2-8 shows a normal code-behind style ASP.NET application. Now, say you put all the data access code — code that talks to the database — in one class project. Then you put all the business-logic — math and validation stuff — in another class project.

```
HTML/APS.NET Markup
```

```
C# view-specific code
```

```
C# business-specific code
```

Figure 2-8:
Structure of n-tier code.

```
C# data-specific code
```

All the code in the code-behind layer, then, would be stuff that makes the markup work, right? Yup. Layering your application like this makes debugging easier, separates concerns even more, and provides for code reuse. If you have a cellphone application that uses the same data model, then you can use the same database code if you break it out.

Implementing n-tier is simple. Just make a class project for every logical division in your code. Something so simple can sometimes be demanding, however. Determining where to put and how to hook everything together is non-trivial — but also beyond the scope of this book. recommend some of the W Professional ASP.NET titles to learn more about Web architecture.

# Modeling the View Controller

ASP.NET MVC takes the idea of n-tier a step further by formalizing it. The tough decisions I mentioned relate to deciding where everything goes are largely made for you in ASP.NET MVC.

MVC stands for Model View Controller. In a nutshell, the idea is that your markup goes in the View, your business logic goes in the Controller, and your database connection code goes in the Model. Sounds like n-tier to you, too, huh? I understand. The differences are mostly theoretical.