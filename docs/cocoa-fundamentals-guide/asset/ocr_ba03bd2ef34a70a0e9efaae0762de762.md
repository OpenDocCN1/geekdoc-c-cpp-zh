# CHAPTER 2

# Cocoa Objects

Table 2-3 Class clusters and their public superclasses

| Class cluster | Public superclasses |
| --- | --- |
| NSData | NSData, NSMutableData |
| NSArray | NSArray, NSMutableArray |
| NSDictionary | NSDictionary, NSMutableDictionary |
| NSString | NSString, NSMutableString |

Other clusters of this type also exist, but these clearly illustrate how two abstract nodes cooperate in declaring the programmatic interface to a class cluster. In each of these clusters, one public node declares methods that all clusters can respond to, and the other node declares methods that are only appropriate for cluster objects that allow their contents to be modified.

This factoring of the cluster's interface makes an object-oriented framework's programmatic interface more expressive. For example, imagine an object representing a book that declares this method:

+   - (NSString *)title:

The book object could return its own instance variable or create a new string object and return that—it doesn't matter. It's clear from this declaration that the returned string can't be modified. Any attempt to modify the returned object will elicit a compiler warning.

# Creating Subclasses Within a Class Cluster

The class cluster architecture involves a trade-off between simplicity and extensibility. Having a few public clusters stand for a multitude of ones makes it easier to learn and use the classes in a framework subclass, but however it's rarely necessary to create a subclass within any of the clusters. However, the cluster architecture is clearly beneficial. Clusters are used in the Foundation framework in just these situations.

If you find a cluster doesn't provide the functionality you need, then a subclass may be in order. For example, imagine you want to create an array object whose storage is file-based rather than memory-based, as in the `NSArray` class cluster. Because you are using the underlying storage mechanism of the class, you'd have to create a subclass.

On the other hand, in some cases it might be better (and easier) to define a class that embeds within an object from the cluster. In this case, let's say that your program needs to be alerted whenever some data is modified. Creating a simple class that wraps a data object that the Foundation framework defines may be the best approach. An object of this class could intervene in methods that modify the data, intercepting the messages, acting on them, and then forwarding them to the embedded data object.