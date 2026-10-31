# Another Classification: Infrastructure Patterns

In this second part of the classification, I will use some of the PoEAA patterns [Fowler PoEAA], some of which are focused on infrastructure.

Again, this description can be used even if you decide to go the custom route. Who knows, perhaps this description will help one or two readers avoid creating their own custom solutions and instead choose one of the existing solutions. I think this is usually a good idea because it's so much work building your own full-fledged solution. Been there, tried that.

# Metadata Mapping: Type of Metadata

We need to describe the relationship between the Domain Model and the database schema in metadata; that's what Metadata Mapping [Fowler PoEAA] is all about. O/R Mappers are implementations of the Metadata Mapping pattern, but different mappers use different types of metadata. Typical examples are

+   - XML document(s) or other document formats
+   - Attributes (annotations might be a clearer term; for example, `[MyAttribute]` in C#)
+   - Source code

As usual, each one comes with its own catch. For instance, XML documents suffer from XML hell. For most developers, XML isn't a very productive format to work with. It's often said that XML isn't for people but for parsers, but it's still the case that tools aren't up to par here, so we often find ourselves sitting there editing huge XML documents.

Another problem with the XML documents is that they are external to the Domain Model source code, so it's easy for them to get out of synch with each other. And many IDEs lack an understanding of the semantics of the XML documents, and therefore refactoring won't work seamlessly.

Attributes are used for decorating the Domain Model, so the risk of getting out of synch with the Domain Model is somewhat smaller. A bigger problem in this case is that the Domain Model is slightly more coupled to the database. If you want to use your Domain Model with two different databases, there is a greater risk that you'll have to have two different versions of the source code for the Domain Model if you use attributes than if you use some external type of metadata. This might not be a huge problem, but it can be. It's also harder to get an overview of the mapping in this case, but tooling can help.

It is debatable whether providing the mapping information in source code is a category of its own. It's actually just another document format. Anyway, I thought having just two categories was a bit cheap. The distinction I'm after here is that the source code describes the mapping information in a procedural way rather than a declarative way. I also see this option as something coming between