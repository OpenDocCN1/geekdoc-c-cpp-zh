# Object Oriented Programming using C#

# Creating And Using Exceptions

# Activity 1

Imagine part of a banking program made up of three classes, and three methods as shown below....

The system shown above is driven by the BankManager class. The AwardLoan() method is invoked, either via the interface or from another method. This method is intended to accept or reject a loan application.

The BookOfClients class maintains a set of account holders...people are added to or they may be created. However the only method of interest to us is the GetClient() method. This method requires a string parameter (a client ID) and returns a client object (if the client has an account at bank) – returns NULL (if the client does not exist).

The Client class has one method of interest DetermineCreditRating(). This method is invoked to invoke a clients credit rating – this is used by the BankManager class to decide if a loan should be approved or not.

Considering the scenario above at the snippet of code below ...

```
Client c = listOfClients.GetClient(clientID) 
c.DetermineCreditRating();
```

This fragment of code would exist in the AwardLoan() method. Firstly it would invoke the GetClient() method, passing a client ID as a parameter. This method would return the appropriate client object (assuming of course that a client with this ID exists) which is stored in a local variable 'c'. Having obtained a client the DetermineCreditRating() method would be invoked on this client.

At these two lines of code. Can you identify any potential problems with them?

# Feedback 1

If a client with the specified ID exists this code above will work. However if a client does not exist with the specified ID GetClient() method would return NULL.

The second line of code would cause a run error (specifically a NullReferenceException) as it tries to invoke the DetermineCreditRating() method on a non existent client and the program would crash at this point.

# Activity 2

Consider the following amendment to this code and decide if would fix this problem.

```
Client c = listOfClients.GetClient(pClientID) 
If (c !=NULL) {
  c.DetermineCreditRating();
}
```