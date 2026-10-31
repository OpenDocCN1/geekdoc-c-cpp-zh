# Domain Patterns

Domain Patterns have a very different focus from the Design Patterns and the Architectural Patterns. The focus is totally on how to structure the Domain Model itself, how to encapsulate the domain knowledge in the model, and how to apply the ubiquitous language and not let the infrastructure distract away from the important parts.

There is some overlap with Design Patterns, such as the Design Pattern called Strategy, [GoF Design Patterns] which is considered to be a Domain Pattern as well. The reason for the overlap is that patterns such as Strategy are very good tools for structuring the Domain Model.

As Design Patterns, they are technical and general. As Domain Patterns, they focus on the very core of the Domain Model. They are about making the Domain Model clearer, more expressive, and purposeful, as well as letting the knowledge gained of the domain be apparent in the Domain Model.

When I ended the previous section, I mentioned that the Specification pattern as a Domain Pattern is an alternative to Query Objects pattern. I think that's a good way of explaining how I see what Domain Patterns are. Query Objects is a technical pattern where the consumer can define a query with a syntax based on objects, for finding more or less any of the objects in the Domain Model. The Specification pattern can be used for querying as well, but instead of using a generic query object and setting criteria, one by one, a specification is used as a concept that itself encapsulates domain knowledge and communicates the purpose.

For example, for finding the gold customers, you can use both query objects and specifications, but the solutions will differ. With Query Objects, you will express criteria about how you define gold customers. With a Specification, you will have a class that is perhaps called `GoldCustomerSpecification`. The criteria itself isn't revealed or duplicated in that case, but encapsulated in that class with a well-describing name.

One source of Domain Patterns is [Arlow/Neustadt Archetype Patterns], but I have chosen a Domain Pattern-example from another good source, Eric Evans' book Domain Driven Design [Evans DDD]. The chosen example pattern is called Factory.

# Note

Pattern-aware readers might get confused because I talk about the Domain Pattern Factory here and the Design Patterns book [GoF Design Patterns] also has some Factory patterns. Again, the focus of Design Patterns is more on a technical level and the focus of Domain Patterns is on a semantic Domain Model level.

They are also different regarding the detailed intents and typical implementations. The Factory patterns of GoF are called Factory Method and Abstract Factory. Factory Method is about deferring instantiation of the "right" class to subclasses. Abstract Factory is about creating families of dependent objects.