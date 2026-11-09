The COM+ Event Service brings into play the COM+ catalog that you've seen used in several different contexts throughout this book. In this context, the COM+ catalog is being used to provide the database seam expounded upon in the previous section.

# **FIGURE 26.4**  
*The COM+ catalog acts as a kind of “middle man” in connecting publishers with subscribers.*

![](bbox=[0.332, 0.188, 0.778, 0.557])

Up until now, I’ve used the term event to signify a particular happening in a system such as parts being received into inventory or a stock price change. However, COM+ has a slightly different usage of the term. With regards to the COM+ Event Service, the term event represents the actual call (using a COM interface) from the publisher to the subscriber in notification of a data change. This requires that the subscriber implement a predefined COM interface (more on this shortly) and, as such, acts as a COM server to the publisher, which acts as a COM client. If you’re at all familiar with COM, you’ll recognize this as being a standard and straightforward means of having the publisher and subscriber communicate with each other. The only new entity added to the mix is the Event Service itself that acts as a layer of abstraction. This layer of abstraction is exactly what makes this whole mechanism the kind of loosely coupled system that is desirable in a distributed application.

Now that you know an event is the call itself, it’s important to understand that the act of calling this event is known as firing an event. In this case, this term is being used exactly as before in the tightly coupled event example in which I discussed the pros and cons of using the ActiveX mechanism for asynchronous notification.