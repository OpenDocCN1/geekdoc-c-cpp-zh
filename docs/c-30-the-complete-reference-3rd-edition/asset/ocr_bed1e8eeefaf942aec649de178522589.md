In Main(), four delegate instances are created. One, strOp, is null. The other three refer to specific string modification methods. Next, a multicast is created that calls RemoveSpaces() and Reverse(). This is accomplished via the following lines:

```
strOp = replaceSp;
strOp += reverseStr;
```

First, strOp is assigned replaceSp. Next, using +=, reverseStr is added. When strOp is invoked, both methods are invoked, replacing spaces with hyphens and reversing the string, as the output illustrates.

Next, replaceSp is removed from the chain, using this line:

```
strOp -= replaceSp;
```

and removeSP is added using this line:

```
strOp += removeSp;
```

Then, strOp is again invoked. This time, spaces are removed and the string is reversed. Delegate chains are a powerful mechanism because they allow you to define a set of methods that can be executed as a unit. This can increase the structure of some types of code. Also, as you will soon see, delegate chains have a special value to events.

# Covariance and Contravariance

There are two features that add flexibility to delegates: covariance and contravariance. Normally, the method that you pass to a delegate must have the same return type and signature as the delegate. However, covariance and contravariance relax this rule slightly, as it pertains to derived types. Covariance enables a method to be assigned to a delegate when the method's return type is a class derived from the class specified by the return type of the delegate. Contravariance enables a method to be assigned to a delegate when a method's parameter type is a base class of the class specified by the delegate's declaration.

Here is an example that illustrates both covariance and contravariance:

```
// Demonstrate covariance and contravariance.

using System;

class X {
    public int Val;
}

// Y is derived from X.
class Y : X { }

// This delegate returns X and takes a Y argument.
delegate X ChangeIt(Y obj);

class CoContraVariance {

    // This method returns X and has an X parameter.
```