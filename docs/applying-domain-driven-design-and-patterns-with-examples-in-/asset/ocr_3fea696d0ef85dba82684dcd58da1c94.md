# Object Database

Historically, there have been many different styles of object databases, but the common denominator was that they tried to avoid the transformation between objects and some other storage format. This was done for more or less the same reasons as I have been talking about when wanting to delay adding infrastructure to the Domain Model, as well as for performance reasons.

# Note

The number of styles increases even more if we also consider the hybrids, such as object-relational databases, but I think those hybrids have most often come from a relational background and style rather than from the object-oriented side.

As it turned out, the number of distractions was not zero. In fact, you could say that the impedance mismatch was still there, but compared to bridging the gap between objects and a relational database, using object databases was pretty clean.

So far, the problems with object databases have been as follows:

+   - Lack of standards
+   - No critical mass
+   - Maturity
+   - More of a niche product
+   - Integration with other systems
+   - Reporting

# Note

My evil friend Martin Rosén-Lidholm pointed out that many of the same arguments actually could be used against DDD and O/R Mapping compared to data-oriented solutions in a .NET-world, considering Microsoft's application blocks, papers, guidelines, and so on.

I'll pretend I didn't hear that. And a focus on the domain will probably become more and more popular for Microsoft's guidance as well, which Martin totally agrees with.