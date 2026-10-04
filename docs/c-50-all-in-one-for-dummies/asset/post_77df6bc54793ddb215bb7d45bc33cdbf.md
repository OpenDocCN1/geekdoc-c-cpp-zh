
# 406 Designing Secure Software

# Designing Secure Software

Security takes a fair amount of work to accurately design. If you break the process into pieces, you find that it's a lot easier to accomplish. The Patterns and Practices team (a group of software architects at Microsoft whose devising program (best practices) have created a systematic approach to designing secure programs that I think you will find straightforward, so I describe it in the following sections.)

## Determining what to protect

Different applications have different artifacts that need protection, but if you have a database in your application, that is something that needs protection. If your database is the most important item to protect. If your application is a server-based application, the server should rate fairly high when you are determining what to protect.

Even if your program is just a little single-user application, the software should do no wrong — an outsider shouldn't be able to use the application to break into the user's computer.

## Documenting the components of the program

If you think this section's title sounds like part of the design process, you're right. A lot of threat modeling is just understanding how the application works and describing it well.

First, describe what the application does. This description becomes a functional overview. If you follow the commonly accepted Software Development Life Cycle (SDLC), then the use cases, requirements, or user stories document (depending on your personal methodology) should give you a good starting point.

Next, describe how the application accomplishes all those tasks at the highest level. A Software Architecture Overview (SAO) diagram is a useful way to do it. This diagram shows which machines and services do what in your software.

![](img/6df7bb88e9302e98442acc219cfbd7fc_431_0.png)

If you are to be using Visual Studio Team System, building a diagram in the Enterprise Architect version is the ultimate SAO diagram and is a good

Sometimes the SAO is a simple diagram — if you have a stand-alone Windows Forms program like a game, that's all there! A stand-alone program has no network connection, and no communication between software parts. Therefore, the software architecture diagram contains only one instance.

# Designing Secure Software 407

### Decomposing components into functions
After you create a document that describes what the software is doing and how, you need to break out the individual functional pieces of the software. If you've set up your software in a component fashion, the classes and methods show the functional decomposition. It's simpler than it sounds.

The end result of breaking the software into individual pieces is having a decent merit of which components need to be protected, which parts of the software interact with each component, which parts of the network and hardware system interact with each component, and which functions of the software do with each component.

## Identifying potential threats in functions
After you create the list of components that you need to protect, you tackle identifying threats. Identifying threats process gets the security consultants the big bucks, and it's almost entirely a factor of experience.

For instance, if your application connects to a database, you have to imagine how the connection could be intercepted by a third party. If you use a file to store sensitive information, the file could, theoretically, be compromised.

To create a threat model, you need to categorize the potential threats to your software. An easy way to remember the different categories of threats is as the acronym STRIDE:

- **Spoofing identity**: Users pretend that they are someone they are not.
- **Tampering with data or files**: Users edit something that shouldn't be edited.
- **Reputation of action**: Users have the opportunity to say they didn’t do something that they actually did.
- **Information disclosure**: Users see something that shouldn't be seen.
- **Denial of service**: Users prevent legitimate users from accessing the system.
- **Elevation of privilege**: Users get access to something that they haven't have access to.

All these threats must be documented in an outline under the functions that expose the threat. This strategy not only gives you a good, discrete list of threats but also focuses your security hardening on those parts of the application that pose the greatest security risk.

| Book III Chapter 1 |
| :--- |
| Writing Secure Code |

# 408 Building Secure Windows Applications

## Rating the risk

The final step in the process is to rate the risks. Microsoft uses the DREAD model to assess risk to its applications. The acronym DREAD represents five key attributes used to measure risk:

- **Damage potential**: The cost to the company for a breach
- **Reproducibility**: Special conditions that might make it harder or easier to find
- **Exploitability**: How far a hacker can get into the system
- **Affected users**: The number of users who are affected
- **Discoverability**: The ease with which you can find the potential vulnerability

You can research the DREAD model at http://msdn.microsoft.com/security or position your threat model to consider those attributes. The key is to determine which threats are most likely to cause problems and how to mitigate them.

## Building Secure Windows Applications

The .NET framework lives in a tightly controlled sandbox. Because of the realities of this sandbox, the configuration of security policy for your application becomes important. The first place you need to look for security in writing Windows applications is in the world of authentication and authorization. Authentication confirms the identity of a user, and authorization determines what they and can do within an application.

When you’re threat modeling, you can easily consider all possible authentication and authorization threats using STRIDE. (See the earlier section “Identifying potential threats in functions,” for more about STRIDE.)

## Authentication using Windows login

To be straightforward, the best way for an application to authorize a user is to make use of the Windows login. A host of arguments take place about this strategy and others, but the key is simplicity: Simple things are more secure.

For much of the software developed with Visual Studio, the application will be used in an office by users who have different roles in the company; for example, some users might be in Sales or Accounting department.

# Building Secure Windows Applications 409

environments, the most privileged users are managers or administrators another set of roles. In most offices, each employee has her own user account, and each user is assigned to the Windows groups that are appropriate for the roles she plays in the company.

Using Windows security works only if the Windows environment is set up correctly. You can't effectively build a secure application in a workspace with a bunch of Windows machines everyone logs on as the administrator, you can't tell who is in what role.

Building a Windows application to take advantage of Windows security is straightforward. The goal is to check who is logged on (authentication) and then check that user's role (authorization).

The following steps show you how to create an application that protects the menu system for each user by showing and hiding buttons:

- 1. Start a new Windows Forms Application project by creating File:New Project and giving your project a descriptive name. This would work for Windows Presentation Foundation (WPF), too, but it's easier to show in Windows Forms. (Book V is all about WPF.) I named my project Windows Security.
- 2. Add two buttons to your form — one for Sales Menu, one for Accounting Menu, and one for your Manager's Menu. My example is shown in L-1.
