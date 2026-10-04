# 676 Developing with Style

Implementing n-tier is simple. Just make a class project for every logical division in your code. Something so simple can sometimes be demanding, however. Determining where to put what and how to hook everything together is nontrivial—but also beyond the scope of this book. I recommend getting some of the Wrox Professional ASP.NET titles to learn about web application architecture.

# Modeling the View Controller

ASP.NET MVC takes the idea of n-tier step further by formalizing it. The tough decisions related to deciding where everything goes are largely made for you in ASP.NET MVC.

MVC stands for Model View Controller. In a nutshell, the idea is that your markup goes in the View, your business logic goes in the Controller, and your database connection code goes in the Model. Sounds like n-tier to you, too, huh? I understand. The differences are mostly theoretical.

The big benefit to MVC over other kinds of web forms apps is that the user interface code is much more testable with automated tests. In fact, when you start an ASP.NET MVC project, it asks you to create a test project along with it.

Another difference from n-tier is some formalization to the implementation of MVC. It is a project type, and rather than having to figure out how things hook up, MVC does some of the work for you.

MVC is a big topic that I just can't cover here in detail. If you have a large project for which you need to divide up the work among developers with varying skill sets, it's cool. Read more in Professional ASP.NET by Wrox Press.