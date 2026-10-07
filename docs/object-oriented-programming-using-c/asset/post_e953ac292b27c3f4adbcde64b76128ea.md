
| Client |
| --- |
| Know name, address, phone |
| Know current credit |
| Decrease credit |
| ClientBook |
| Hold list of client IDs and associated clients |
| Add a client | Client |
| Look up a client | Client |

| Message |
| --- |
| Know message text |
| Know days remaining |
| Decrement days remaining |
| Know if expired |
| MessageSet |
| --- | --- |
| Hold list of messages | Message |
| Add a message | Message |
| Display messages | DisplayBoardCtrl |
| Purge messages | Message, ClientBook, Client |

Object Oriented Programming using C#

# Activity 1

To purge the messages, the MessageBook cycles through its list of messages reducing the credit for the client who ‘owns’ this message, decrementing the days remaining for that message and deleting messages when appropriate.

Looking at the CRC cards above work through the following steps and identify any potential problems with these classes :-

For each message

- tell the Message to decrement its days remaining and
- tell the relevant Client to decrease its credit
- ask the Message for its client ID
- ask the Message for its cost
- ask the ClientBook for the client with this ID
- tell the Client to decrease its credit by the cost of the message

- if either the Client’s credit is <=0 or the Message is now expired
delete the message from the list

# Feedback 1

A problem becomes evident when we try to find the client associated with a message as Message does not know the client ID.

We therefore need to add this responsibility to the Message class.

A revised design for the Message class is given below....

| Message |
| --- |
| Know message text |
| Know clientID |
| Know days remaining |
| Decrement days remaining |
| Know if expired |
| Know cost |

By drawing CRC cards for each class and interface and by role playing a range of scenarios we have checked and revised our plans for the system - we can now refine these and document these using UML diagrams.

Object Oriented Programming using C#

# Case Study

# 11.4 Documenting the design UML

- Determine in detail what attributes go in each class
- Determine how the classes are related and
- Put classes into appropriate packages.

# Elaborating the Classes

Having worked through CRC scenarios we can make an initial assignment of instance variables and methods among our classes, including some accessors and mutators whose necessity has become evident (see diagram below).

Of course as we are going to program this system in C# we will replace our accessor and mutator methods with properties but as this could be programmed in any OO language we will leave our design showing appropriate accessor and mutator methods.

![](img/e143b38d00f95425fa4f3efca0527189_215_0.png)

Object Oriented Programming using C#

# Case Study

| Client | ClientBook |
| --- | --- |
| name address phone credit | ? |
| DecreaseCredit() | AddClient() GetClient() |

| Message | MessageSet |
| --- | --- |
| clientID text daysRemaining cost | ? |
| DecrementDays() GetText() HasExpired() GetCost() | AddMessage() Display() DailyPurge() |

| <<interface>> |
| DisplayBoardControl |
| LoadMessages() Run() |

We don't know of any simple attributes which ClientBook and MessageSet will require, but they will need to be associated with other classes so we still have some work to do - hence the ?s (which are not an official part of UML).

# Relationships Between Classes

We can now start to work out how these classes are related.

Starting with ClientBook and Client - a : ClientBook will record details of zero or more clients.

The navigability will be from ClientBook to client because the book “knows about” its Clients (in implementation terms it will have references to them) but the individual clients will have references back to the book.

The one-to-many relationship suggests that ClientBook will have a Collection (of some kind) of Clients. The specification states that each Client will have a unique ID thus the collection in fact be a dictionary where each entry is made up of a pair of values – in case a clientID (int) and a Client object. As we are likely to be retrieving clients by their ID more often than we will be adding and deleting the system will be more efficient if we use this sorted dictionary, where clients will be stored in order of their ID. With a sorted dictionary adding and deleting elements will be slower as the process is more complex but retrieving elements will be quicker.

Object Oriented Programming using C#

# Case Study

![](img/e143b38d00f95425fa4f3efca0527189_217_0.png)

The relationship between MessageSet and Message is very similar to the relationship between ClientBook and Clients.

Although MessageSet appears to have no attributes, one-to-many association with Message again implies an attribute which is a Collection type. The specification states that messages must be unique but does not imply a key value is required thus a simple set will suffice.

![](img/e143b38d00f95425fa4f3efca0527189_217_1.png)

# Relating the Classes: MessageSet, ClientBook, and DisplayBoard

Because MessageSet is responsible for initiating the display of messages on the board it has a dependency on DisplayBoardControl. MessageSet also has a relationship with ClientBook because it needs to access and update information when the daily purge is carried out. This is shown below.

Object Oriented Programming using C#

# Case Study

![](img/e143b38d00f95425fa4f3efca0527189_218_0.png)

# Relating the Classes: MessageSet, ClientBook, and DisplayBoard

The diagram below shows how all of these classes are related. An additional class, DummyBoard, has been included which will implement the DisplayBoard interface for testing purposes.

![](img/e143b38d00f95425fa4f3efca0527189_218_1.png)

Object Oriented Programming using C#

# Case Study

Since DummyBoard will have a collection of messages it also has a one-to-many relationship with Message.

![](img/e143b38d00f95425fa4f3efca0527189_219_0.png)

The use of the concise "ball and socket" notation for the DisplayControl interface.

While the classes above will form the heart of the system an additional class will be required to drive and manage the system as a whole. A class 'ApplicationWindow' will be created. This will be the GUI that will run the system and this will allow the user interact with the system adding clients, messages etc.

Other additional functionality, not specified by the owner, is implicitly required. At the end of the day the details of ClientBook and MessageSet will need to be saved to file. This data will need to be restored next time the system is run. This again be driven from the interface but the body of the code will be devolved to the relevant classes.

# 11.5 Prototyping the Interface

While methods for gathering user requirements are beyond the scope of this text – it is always a good idea to prototype an interface and get feedback on this before proceeding with the development.

The figure below shows the proposed interface for this system:-

![](img/e143b38d00f95425fa4f3efca0527189_220_0.png)

This is made up of three areas. From left to right these are a) an area for adding new clients, b) and area for adding new messages and c) an area for buttons dedicated to other essential operations.

# 11.6 Revising the Design to Accommodate Changing Requirements

Changing software requirements are a fact of life and OO programming is intended to help software engineers make program adaptations easier, quicker, and with less risk of generating errors. The principles of inheritance, method overriding and polymorphism are essential OO features that help in this manner.

In this project when gaining feedback from the shop owner on the prototype interface they comment that they generally like the interface but that they have an additional system requirement :

> Some messages are 'urgent messages'. These should be highlighted on the display by placing three stars before and after the message and the cost of these messages will be twice the cost of ordinary messages. Other than that urgent messages are just like ordinary messages.
