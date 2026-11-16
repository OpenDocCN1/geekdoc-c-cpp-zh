
## THE BUSINESS LAYER

The Business layer represents the smarts of your application. Oh, there may be some tricky stuff in the DAL (and there's almost always tricky stuff in the Presentation layer), but applications hardly ever just retrieve data from the DAL and show it to the user, and all the logic that processes the data and makes sure that business rules are enforced lives here.

Most of the functionality of the Business layer lives in the Business components that implement the logic of the applications.

These are collectively known as BUSINESS RULES, and the business layer is where they're enforced.

- The Business layer is responsible for:
  - Handling communication between the DAL and the Presentation and Service layers
  - Enforcing data integrity and consistency
  - Making sure things happen in the right order

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_495_0.png)

BUSINESS ENTITIES are the objects you write to represent the objects that your application models.

BUSINESS WORKFLOWS are processes that need to be performed in a specific order. Workflows can get pretty complicated. If you're writing them, you'll want to check out the Windows Workflow technology.

An APPLICATION FACADE makes the components defined in the Business layer simpler for the Presentation layer to handle. For example, the application facade might combine several distinct operations into a single AddRecipe() method. Not all applications (in fact, not many applications) need an application facade.

## THE SERVICE LAYER

You can think of the Service layer as the user interface for users who aren't people. It exposes the functionality of your application as a service, which means that it has a standards-based interface. That interface is defined in this layer.

Some methods in the Service layer are used to translate between the way data is represented in the Business layer and the way it needs to be exposed. Like the utilities in the DAL, the functions in the Service layer are usually private.

SERVICE INTERFACES define the operations the service exposes.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_496_0.png)

DATA CONTRACTS define the data objects the service exchange with its clients.

When you're working in .NET, the Service layer is almost always implemented using Windows Communication Foundation (WCF).

## WORDS FOR THE WISE

Internet services are a HUGE topic, and unfortunately we don't have room to explore them here. But to get you started, here are some basic terms you can check out in MSDN or your favorite search engine:

- RESTful - REST stands for REpresentational State Transfer, and a RESTful service is one that conforms to the REST constraints. In essence, REST translates the basic Client/Server two-tiered architecture to the Web.
- SOAP - SOAP stands for "Simple Object Access Protocol". It's a protocol for exchanging structured data over the Web.
- SOA - SOA stands for "Service-Oriented Architecture". It refers to structuring applications as a set of interacting services.

And, of course, don't forget to check out WCF, which makes exposing your application as a service (almost) trivial.

## PUT ON YOUR THINKING HAT

Here's a description of some functions that your application might implement. Can you assign them to the correct architectural layer?

The IsValid() method ensures all the data is valid before calling SaveChanges().

The GetRecipe() method combines two different ADO.NET DataTable objects into a single .NET object.

The FormatForWeb() method translates a .NET object into XML.

The LoadData() method populates an ADO.NET DataSet from an XML file.

The CheckCredit() method verifies that a customer is in good standing before allowing an order to be placed.

## HOW'D YOU DO?

The IsValid() method ensures all the data is valid before calling SaveChanges().

> Validity is determined by business rules, so this one belongs in the Business layer.

The GetRecipe() method combines two different ADO.NET DataTable objects into a single .NET object.

> Did you get this one in the DAL? Many people would, but data manipulation is done in the Business layer. The DAL only saves and retrieves it. Remember that the whole point of separating the DAL from the business logic is so that you can swap any one data store and replace it with another. You don't want to have to duplicate that manipulation code, right?

The FormatForWeb() method translates a .NET object into XML.

> The name of this was previously a give-away. Anything that talks to other software, and particularly anything that talks across HTTP, lives in the Service layer.

The LoadData() method populates an ADO.NET DataSet from an XML file.

> Loading data is exactly what the DAL is intended to do, so that's where this function should live.

The CheckCredit() method verifies that a customer is in good standing before allowing an order to be placed.

> This involves both a business rule (“customer must be in good standing”) and the enforcement of a process (“credit check before order placement”), so it belongs in the Business layer.

## THE PRESENTATION LAYER

The Presentation layer is responsible for the way your application interacts with real people. It includes the actual interface (the widgets that the user see) and what's called the presentation logic, which is just geek-speak for “what happens when the user clicks this button.”

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_499_0.png)

.NET gives you a lot of options for building a user interface. We’ll be examining Windows Presentation Foundation (WPF) in this book, but you might also want to explore some of these others.

### WINDOWS FORMS (WINFORMS)

This is an older technology for writing desktop applications. If you’re working on an existing application, this is probably what you'll use.

### ASP.NET WEB FORMS

This is (more or less) the Web-based version of the WinForms toolkit. Again, you’ll probably use it if you’re working on existing applications.

### SILVERLIGHT

Silverlight is closely related to WPF. It runs over the Web (as a replacement for Web Forms), on the desktop (with some limitations), and on mobile devices like Windows Phone. If you need to deploy your application on multiple platforms, Silverlight is probably your best option.

### MAKE A NOTE

The design of interfaces that don’t make people crazy is a non-trivial task. You don’t need me to tell you that, right? You struggle with them every day. And the interface is important, because to your users, the interface IS the application. To improve your interface design skills, you couldn’t do better than to read the books of Donald Norman and Alan Cooper. I think they should be on every programmer’s shelf.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_499_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_499_2.png)

## PRESENTATION PATTERNS

There are several common patterns for the Presentation layer, and each one has a number of variations, but they all have the same basic goal: to separate the widgets the user sees from the logic that maintains the data those widgets displays or responds to interactions the user has with the widgets. This is often described as separating state and behavior from presentation.

The presentation logic is called different things in different patterns. It represents the state and behavior of the interface.

The presentation logic provides data to the presentation widgets, and receives notification of anything the user does like change some data or click a button.

The presentation logic interacts with the model to retrieve information and issue commands.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_500_0.png)

The view is the actual interface with which the user interacts.

Some patterns allow the View to know about the Model; some don't.

The model is responsible for actually processing the data.

The user don't care about any of this. They just have a job to do.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_500_1.png)

### ON YOUR OWN

When you separate the logic behind an interface from the interface itself, it becomes much easier to do a couple of things. Do you know what they are? (Hint: both words begin with “re”.)
