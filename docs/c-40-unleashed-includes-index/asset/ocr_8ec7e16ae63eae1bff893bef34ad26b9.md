# The BCL: What, Where, and How?

Our main goal in this chapter is to introduce you to the essential libraries that come with the .NET Framework and tend to be used in a wide variety of scenarios. No matter whether you’re writing a UI application, a web application, services, or even some kind of cloud-based application, having a clue about libraries turns out to be very beneficial. Although the term Base Class Library (BCL) has become harder to define over the years, I’ll piggyback on this widely used acronym to introduce what I believe to be essential.

# What Is Covered?

A significant number of namespaces that are part of the BCL are not covered here because they’ve gotten attention already in the context of language feature discussion. For example, while talking about generics, we covered the main uses of the feature, namely collections. Similarly, the discussion about LINQ put us in a great spot to discuss essential interfaces such as IEnumerable<T> and some APIs that are used to deal with specific data models. During our dynamic programming exploration, things such as System.Reflection and the DLR were covered in quite some detail as well.

Highlights of this chapter include coverage of namespaces (for example, the root System namespace) and various children (for example, Diagnostics, IO, Text, and Threading). So that you get a feel for the components and their installation, we’ll work through a simple Windows Service example, covering System.ServiceProcess and System.Configuration. From a scenario point of view, our emphasis is on themes, such as working with text, doing I/O, and so on, instead of tackling specific domains like UI programming. To set realistic expectations, don’t expect to master the covered namespaces in an end-to-end manner: Lots of those APIs have different levels of complexity, ranging from the very simple to the more involved scenarios that require tight control. Most of the time, we focus on the basics and call out areas that may require deeper exploration if you’re interested.

Things I consider too specialized for meaningful coverage in the limited number of pages available include APIs like DirectoryServices (to interact with Active Directory and LDAP-based directory services), Messaging (exposing MSMQ message queuing to managed code), Transactions (to deal with things such as distributed transactions), COM+ support in ComponentServices, and many more hidden gems throughout the rich .NET Framework set of APIs.

# Default Project References

The assemblies that get referenced upon creation of a new project serve as a good starting point for exploration of the BCL and commonly used APIs. Depending on the project type, a different set of references is present. It should be obvious that building a Windows Presentation Foundation (WPF) application requires different dependencies than the creation of a WCF service library.

The most primitive set of references is likely to be found in our much beloved Console Application template, so let’s take a look at it. Figure 26.2 shows the default set of references displayed for such a project, targeting .NET Framework 4.