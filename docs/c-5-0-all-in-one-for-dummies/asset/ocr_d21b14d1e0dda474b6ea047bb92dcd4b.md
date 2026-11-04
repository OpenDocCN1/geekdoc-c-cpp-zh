# Decomposing components into functions

After you create a document that describes what the software is doing and how, you need to break out the individual functional pieces of the software. If you've set up your software in a component fashion, the classes and methods show the functional decomposition. It's simpler than it sounds.

The end result of breaking the software into individual pieces is having a decent matrix of which components need to be protected, which parts of the software interact with each component, which parts of the network and hardware system interact with each component, and which functions of the software do what with each component.

# Identifying potential threats in functions

After you create the list of components that you need to protect, you tackle the tough part: Put two and two together. Identifying threats is the process that gets the security consultants the big bucks, and it's almost entirely a factor of experience.

For instance, if your application connects to a database, you have to imagine that the connection could be intercepted by a third party. If you use a file to store sensitive information, the file could, theoretically, be compromised.

To create a threat model, you need to categorize the potential threats to your software. An easy way to remember the different categories of threats is as the acronym STRIDE:

+   - **Spoofing identity:** Users pretend that they are someone who they are not.
+   - **Tampering with data or files:** Users edit something that shouldn't be edited.
+   - **Repudiation of action:** Users have the opportunity to say they didn't do something that they actually did do.
+   - **Information disclosure:** Users see something that shouldn't be seen.
+   - **Denial of service:** Users prevent legitimate users from accessing the system.
+   - **Elevation of privilege:** Users get access to something that they shouldn't have access to.

All these threats must be documented in an outline under the functions that expose the threat. This strategy not only gives you a good, discrete list of threats but also focuses your security hardening on those parts of the application that pose the greatest security risk.