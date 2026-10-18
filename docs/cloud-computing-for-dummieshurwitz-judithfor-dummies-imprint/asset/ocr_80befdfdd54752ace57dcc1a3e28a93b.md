The ESB is a collection of software components that manage messaging from one software component to another. A software component connects to the ESB and passes it a message by using a specified format along with the address of the software component that needs to receive the message. The ESB completes the job, getting the message from the sending component to the receiving component.

# Telling your registry from your repository

The self-contained and reusable software components that you create to carry out your important business processes are called business services. Business services are often made up of a group of component services, some of which may also have additional component services. Each service provides a function.

Simply, here’s the difference between the repository and the registry:

+   Repository: Central reference point for all the components within the software development environment from which services are built

+   Registry: Central reference point for definitions, rules, and descriptions associated with every service within an SOA environment

# Registry

Information describing the function of each reusable component is recorded in the SOA registry — a type of electronic catalog. The SOA registry has two roles:

+   One rooted in the operational environment: In the day-to-day working business computing environment, the SOA registry provides reference information about software components that are running or available for use. This information is of particular importance to the service broker — the software in a SOA framework that brings components together by using the rules associated with each component.

+   One rooted in the world of programmers and business analysts: For programmers and business analysts, on the other hand, the SOA registry acts as a reference that helps them select components and then connect them to create composite applications that represent business processes. It also stores information about how each component connects to other components. In other words, the SOA registry documents the rules and descriptions associated with every given component.

The SOA registry is extremely important because it acts as the central reference point within a service oriented architecture. The SOA registry contains information (metadata) about all the components that the SOA supports. For that reason, it defines the domain of the architecture.