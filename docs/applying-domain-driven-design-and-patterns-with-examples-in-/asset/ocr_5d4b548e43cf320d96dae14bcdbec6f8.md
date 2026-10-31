# Object-Oriented Data Model, Smart Service Layer, and Documents

By Mats Helander

Sometimes, during dark winter nights, I recall faintly what life was like in the days before the Domain Model. It is at times like those that I pour a little cognac into my hot chocolate and throw an extra log on the fire.

The evolution of the architecture in my applications, finally leading up to the use of the Domain Model, followed a pattern some readers may feel familiar with. I'm going to outline this evolution quickly, as it helps put my current approach for using the Domain Model into context.

# In the Beginning

I started out writing client-server applications where all the application code was stuffed into the client, which would talk directly to the database. When I started writing Web applications, they consisted of ASP pages with all the application code in them including the code for calling the database.

Because the result of this type of application architecture is, without exception, a horrific mess whenever the application grows beyond the complexity of a "Hello World" example, I soon learned to factor out most of the code from the presentation layer and to put it in a Business Logic Layer (BLL) instead.

Immediately, the applications became easier to develop, more maintainable, and as a bonus the BLL could be made reusable between different presentation layers. It should also be noted that in those days, it could make a big difference to the performance and scalability of a Web application to have the bulk of its code compiled in a component.

The next step was to lift out all the code responsible for communicating with the database from the BLL and put it in a layer of its own, the Data Access Layer (DAL). I recall that I was slightly surprised to see that the DAL was often substantially larger than the BLL meaning more of my application logic dealt with database communication than with actual business logic.

At this time, I was almost at the point where the Domain Model would enter into the equation. The PL would talk to the BLL that would talk to the DAL that would talk to the database. However, all data from the database was passed around the application in the form of Recordsets, the in-memory representation of rows in the database (see Figure A-1).

Figure A-1. Classic, pre-Domain Model layered application architecture