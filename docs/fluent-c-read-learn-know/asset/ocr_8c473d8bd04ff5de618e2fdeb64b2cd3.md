# # THE SERVICE LAYER

You can think of the Service layer as the user interface for users who aren't people. It exposes the functionality of your application as a service, which means that it has a standards-based interface. That interface is defined in this layer.

Some methods in the Service layer are used to translate between the way data is represented in the Business layer and the way it needs to be exposed. Like the utilities in the DAL, the functions in the Service layer are usually private.

SERVICE INTERFACES define the operations the service exposes.

![](bbox=[0.15, 0.32, 0.88, 0.4])

DATA CONTRACTS define the data objects the service exchange with its clients.

When you're working in .NET, the Service layer is almost always implemented using Windows Communication Foundation (WCF).

# ## WORDS FOR THE WISE

Internet services are a HUGE topic, and unfortunately we don't have room to explore them here. But to get you started, here are some basic terms you can check out in MSDN or your favorite search engine:

RESTful - REST stands for REpresentational State Transfer, and a RESTful service is one that conforms to the REST constraints. In essence, REST translates the basic Client/Server two-tiered architecture to the Web.

SOAP - SOAP stands for "Simple Object Access Protocol". It's a protocol for exchanging structured data over the Web.

SOA - SOA stands for "Service-Oriented Architecture". It refers to structuring applications as a set of interacting services.

And, of course, don't forget to check out WCF, which makes exposing your application as a service (almost) trivial.