# Chapter 7

# # Spotlight, Quick Look,
and Core Data

Developing for Mac OS X is about functionality meeting quality. When our applications have either without the other, we leave our users wanting more. They may not be able to define it, but “something” will be missing. Spotlight and Quick Look integration are two of those things that users don’t look for when trying a new application but are pleasantly surprised by them when they stumble upon them. Surprisingly, not a lot of developers handle this integration. Perhaps it is because Spotlight does not get along with Core Data very well. Perhaps the feature is too new. But one thing is for certain—integrating with Spotlight is the right move going forward. Spotlight is here to stay, and users will be using it more often and in more creative ways.

Unfortunately, for technical reasons, Spotlight and Core Data are at odds with each other. Spotlight works on the metadata of individual files, and Core Data stores everything in a single file. Because Spotlight is designed to work with the metadata of a file to discover things about the file, it will not work very well with a single file design such as Core Data. When Tiger was first released, there were a number of applications (such as Entourage) that, because of their single file design, did not play nicely with Spotlight. In fact, Apple rearchitected Mail for that reason.

The incompatibility between Spotlight and Core Data is corrected in Snow Leopard but unfortunately it’s Snow Leopard only and not backward compatible with plain old vanilla Leopard. How? It’s in a manner that is very similar to the solution described in this chapter.