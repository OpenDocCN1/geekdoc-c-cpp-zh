And here is a child package specification with a new operation for our stack type:

```
```ada
package Stacks.More is
    function Peek (Stack : in Stack.Type) return Integer ;
    -- Returns a copy of the top element on the Stack
end Stacks.More;
```
```

We certainly could have added function Peek to our original stack package. However, that change to the original package would require us to recompile all clients that used it. And, of course, we wanted to illustrate a use of child packages. To that end, here is the body of our child package:

```
```ada
package body Stacks.More is
    function Peek (Stack : in Stack.Type) return Integer is
    begin
        return Stack.Items (Stack.Top);
    end Peek;
end Stacks.More;
```
```

You can see that this body makes use of the details of the stack type given in the private part of the stack package specification.

# ### 3.5.1 *Private Children*

Package Stacks.More is an example of a *public child package*. Public child packages allow extension and continued privacy of their private types to provide additional resources for clients.

When developing a subsystem, there are times that we would like to decom-pose it into pieces without giving clients of that subsystem direct access to those pieces. Ada's private child package provides the mechanism for hiding these pieces. The use of resources from a private child package is restricted to the hierarchy of packages rooted at its parent.

To illustrate this role of private child packages, consider a flight management system (FMS). An FMS is a component of the cockpit software that automates a wide variety of in-flight tasks. A primary function of an FMS is in-flight management of the flight plan. Here is an outline of a package that supplies clients with operations on flight plans:

```
```ada
package FMS is
    type Flight_Plan is private;
    . . .
    -- Many operations on flight plans
    . . .
```
```