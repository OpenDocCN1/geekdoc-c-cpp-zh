Here’s a diagram that tries to capture the structure of our server:

![](bbox=[0.099, 0.094, 0.898, 0.545])

In this diagram, the difference between a Handler and a Manager is whether it interfaces to the outside world or not.

While the nomenclature is arbitrary, the distinction is helpful because it tells us that the Managers should only interface with internal parts of our server, whereas the Handlers will interface to both internal parts of our server and external elements outside of our server, e.g. the File System and the client.

The two-way arrows between the boxes and ellipses shows the flow of information. The one-way arrows with text gives us an idea of which API calls will be making calls to the receiving box, i.e. where the arrow points, e.g. during the Logon API call, information regarding the Accounts will be needed to verify that the Logon request was made by a user of the system.

There is another one-way arrow labeled Logon that goes from the API Handler to the Session Manager. This is to show that after the user has been authenticated, that a new session needs to be created.

This is not meant to capture every last detail, but it’s there to help us think and talk about our design, and subsequently our code. It’s very difficult to build such a diagram like this from just looking at code. And having this diagram before we code, will make the process so much easier.

We’ll modify this diagram if we discover some unforeseen issue that requires an architectural restructuring.