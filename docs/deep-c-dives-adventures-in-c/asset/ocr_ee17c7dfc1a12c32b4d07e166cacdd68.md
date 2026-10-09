# # These aren’t the types you’re looking for

> > “These aren't the droids you're looking for.”
> Ben Obi-Wan Kenobi

Types, love them or hate them you cannot ignore them. Strongly typed languages currently rule the earth and anyone who suggests that strong static typing isn't a good idea is swiftly stamped on. C is a strongly typed static language, but this does not necessarily mean what you think it does. C types aren't the types you might want or expect. This said, the concept of type in C fits in perfectly with its low level intent.

# ## The Origin of Type

The concept of types in programming is both deep and shallow.

It is shallow when you first meet it and gets increasingly elaborate as one abstraction is added on top of another. At its most advanced, types provide a theory of programming in the form of the Curry Howard correspondence which views programs and mathematical proofs as being one and the same. This leads us into areas of pure mathematics that are generally labeled as category theory and logic.

The good news is that type in C is much more at the shallow end of the range but over time there have been efforts to make it deeper and hence more respectable and more like every other programming language. There is an argument that C needs a simple interpretation of type to be effective as a language that works at a lower level than most. Rather than abstracting type away from the way that the machine represents data, it is better to keep the association between data type and representation.

The fundamental, but not the only, idea of type in C is simply how many bits are in use and how those bits are to be interpreted.

This is a fairly rare interpretation of type these days and is another thing that makes C different.