![](bbox=[0.085, 0.055, 0.215, 0.165])

# # ARCHITECTURES

Application architectures aren't technically design patterns, but they serve the same purpose: They are accepted ways of organizing your application that address particular situations. The difference is that while design patterns typically address the interaction of objects within an application, application architectures address larger components, the various executables, libraries and services that interact to provide your application's functionality.

# ## MONOLITHIC APPLICATIONS

By now you've probably gotten the idea that the .NET Framework provides a lot of functionality. You're right; it does—enough that a lot of applications don't need anything else. There's absolutely nothing wrong with this design, but even when everything's going to be compiled into a single executable, it's useful to think about your application as a series of roles (displaying things to the user, manipulating data, and so forth) and organize the code accordingly. We'll look at one way to do this in the next section.

# ## CLIENT/SERVER APPLICATIONS

N-tiered applications that talk to some kind of back-end service like a database engine or a Web service are a special category. That back end isn't part of your application, and may not be (in fact, usually isn't) part of the development project.

The framework servers like SQL Server and SharePoint Server are often used in this situation, and the client application (the bit you're writing) often provides an interface to whatever the server provides in a form that's more comfortable to your users.

# ## N-TIERED APPLICATIONS

When an application is divided into different executable components, like the client and server in a Client/Server application, each component is called a tier. So, technically, the Client/Server architecture is two-tiered.

As applications grow in size and complexity, the number of tiers often increases. "N-Tiered application" is used to refer to any application that has more than one tier, but is generally reserved for those that have more than two.