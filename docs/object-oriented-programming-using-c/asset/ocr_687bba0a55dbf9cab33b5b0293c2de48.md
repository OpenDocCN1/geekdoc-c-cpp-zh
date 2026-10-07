# Object Oriented Programming using C#

And the methods include :-

+   - display
- add (client to book)
- add (message to set)
- lookUp (client in book)
- purge
- decrement
- expire
- delete

# 11.3 Further Analysis

We could now document this proposed design using UML diagrams and program a system accordingly. However before doing so it would be better to find any potential faults in our designs as fixing these faults now would be quicker than fixing the faults after time has been spent programming the system. We should now refine our design using CRC cards and elaborate our classes.

CRC cards (see Chapter 6 section 6.10 and 6.11) allow us to play various scenarios to see if our designs feasible before refining these designs and documenting them using UML class diagrams.

The two CRC cards below have been developed to describe the Client and ClientBook classes. The panel on the left shows the class responsibilities and the panel on the right shows the classes they are expected to collaborate with.

| Client |
|---||
| Know name, address, phone |
| Know current credit |
| Decrease credit |

| ClientBook | |
|---||
| Hold list of client IDs and associated clients | Client |
| Add a client | Client |
| Look up a client | Client |

We can use these to roleplay, or test out, a scenario. In this case what happens when we get a new client in the shop? Can this client be created and added to the client book?