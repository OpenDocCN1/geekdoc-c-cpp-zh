
other. Suppose that GroupA is the holder of Secret X, so the group marked it private. The code looks something like this:

```assembly
// In assembly InternalLimitsAccess:
class Congress
{
    static void Main(...)
    {
        // Code to oversee CIA
    }
}

// In assembly CIAAssembly:
public class GroupA
{
    private string _secretFormulaForCocaCola; // Secret X
    internal GroupA() { _secretFormulaForCocaCola = "lots of sugar";
}
public class GroupB
{
    public void DoSomethingWithSecretX()
    {
        // Do something with Secret X, if only you could access it.
    }
}
```

Now GroupB can’t see Secret X, but suppose that it has a legitimate need to know it. GroupA can, of course, bump Secret X to public status, but if it does, the secret isn’t much of a secret any more. If GroupB can see the secret, so can those snoops over in Congress. Even worse, CNN knows it too, not to mention Fox, ABC, and other networks. And you know how well those folks keep secrets. Oh, right — Russia can see Secret X, too.

![](img/6df7bb88e9302e98442acc219cfbd7fc_409_0.png)

Luckily, C# also has the internal keyword. Using internal is just one step down from public and well above private. If you mark the GroupA class and its “public” methods — the ones that are visible outside the class — with the internal keyword instead, everybody at the CIA can see and access Secret X — as long as you either mark the secret itself (a data member) as internal or provide an internal property to get it with, as shown in this version:

```assembly
// In assembly CIAAssembly:
internal class GroupA
{
    private string _secretFormulaForCocaCola; // Secret X
    internal string SecretX { get { return _secretFormulaForCocaCola; } }
    internal GroupA() { _secretFormulaForCocaCola = "lots of sugar";
}
public class GroupB
{
    public void DoSomethingWithSecretX()
    {
        // Do something with Secret X, now that we can see it:
        Console.WriteLine("I know Secret X, which is {0} characters long, but " + "I'm not telling.", GroupA.SecretX.Length);
    }
}
```

## Going Beyond Public and Private: More Access Keywords 385

Now class GroupB has the access it needs — and it's not giving up the secret (even under threat of waterboarding). All it tells Congress, over in Main(), is that it knows Secret X, and Secret X has 11 characters. Here's that chunk of code:

```csharp
class Congress
{
    static void Main(string[] args)
    {
        // Code to oversee CIA
        // The following line doesn't compile because GroupA isn't accessible
        // outside CIAAssembly. Congress can't get over CIA.

        // CIAAssembly.GroupA = new CIAAssembly.GroupA();
        // Class cannot access GroupB because it's declared public.
        // GroupB is willing to know the secret, but it's
        // not telling — except for a small hint.
        GroupB groupB = new GroupB();
        groupB.SomethingWithSecretX();
    }
    Console.WriteLine("Press Enter to terminate...");
    Console.Read();
}
```

From Main(), GroupA is invisible, so an attempt to construct an instance of it isn't possible. But because GroupB is public, Main() can access and call its public method DoSomethingWithSecretX().

Wait! CIA has to talk to Congress about certain topics, I'm happy to report — but on a need-to-know basis, limited to selected members of Congress and senators, you can do so, via GroupB, as long as they present the proper credentials, although you need to add them to the code:

```csharp
public string SomethingWithSecretXUsingCredentials(string credentials)
{
    if (credentials == "congressman with approved access")
    {
        return GroupA.SecretX;
    }
    return String.Empty;
}
```

The internal keyword makes classes and members accessible only inside their own assembly. But within the assembly, the internal items are effectively "public" to all local classes.

You can mark a method inside an internal class as public, though it isn't truly public. A class member can't be more accessible than its class, so the so-called "public" member is just internal.

![](img/6df7bb88e9302e98442acc219cfbd7fc_410_0.png)

CIA can still keep its deepest, darkest secrets ultra-hush-hush by declaring them private inside their owning class. That strategy makes them accessible only in that class.

## Protected: Sharing with subclasses

The main purpose of private is to hide information. In particular, private hides a class’s internal implementation details. (Classes who know classes too intimately aren’t the luckiest classes in the world. In fact, they’re the unluckiest.) Classes with a lot of implementation details are said to be “too tightly coupled” with the classes they know too much about. If class A is aware of the internal workings of class B, A can come to rely too much on those details. If they ever change, you end up having to modify both classes.

The less the other classes — and assemblies — know about how class B performs its magic, the better. In Chapter 5 of this minibook, I use the example of a BankAccount class. The bank doesn’t want forgetful folks like me — or forgetful classes such as class A — to be able to change a balance directly. That balance is properly part of the BankAccount class’s implementation. It’s private. BankAccount provides access to the balance — but only through a carefully controlled public interface. In the BankAccount class, the public interface consists of three public methods:

- ♦ Balance: Provides a read-only way to find out the current balance. You can’t use Balance to modify the underlying balance.
- ♦ Deposit(): Lets someone outside the class add to the balance in a controlled way.
- ♦ Withdraw(): Lets someone (presumably the account owner) subtract from the balance, but within carefully controlled limits. Withdraw() enforces the business rule that you can’t withdraw more than you have.

Access control considerations other than private and public arise in programming. I explain the previous section how the internal keyword opens a class — but only to other classes in its own assembly.

However, suppose that the BankAccount class has a subclass, Savings Account. Methods in SavingsAccount need access to that balance defined in the base class, of course, although other classes, even in the same assembly, probably don’t. Luckily, SavingsAccount can use the same public interface, the same access, as outsiders: using Balance, Deposit(), and Withdraw().

Sometimes, though, the base class doesn’t supply such access methods for its subclasses (and others) to use. What if the _balance data member in BankAccount is private and the class doesn’t provide the Balance property?

![](img/6df7bb88e9302e98442acc219cfbd7fc_412_0.png)

Enter the protected keyword: If the _balance instance variable in the base class is declared protected rather than private, outsiders can’t see it — it’s effectively private to them. But subclasses can see it just fine.

An even better solution is to mark _balance private in BankAccount as before and then provide a Balance property marked protected. Subclasses such as SavingsAccount can access _balance by using the Balance property. But the balance is invisible to outsiders, which protects the BankAccount implementation.

If the balance does indeed need to be accessible (read-only) to outsiders, you should, of course, provide the public Balance property to get the balance. However, you may still need to set the balance from inside SavingsAccount. To do that, you can give the set accessor of Balance protected access — accessible from SavingsAccount but inaccessible to outsiders.

```csharp
// In BankAccount:
public decimal Balance
{
    get { return _balance; }      // Public
    protected set { _balance = value; }  // Not public
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_412_1.png)

The ProtectedLimitsAccess example on the web illustrates using the protected keyword as just described.

You can even subclass BankAccount in a different assembly, and the subclass has access to anything declared protected in BankAccount. The ProtectedLimitsAccess example also illustrates this process.

The example has two subclasses of BankAccount: one in the same assembly as BankAccount and one in a different assembly. What’s interesting with respect to protected is that either BankAccount subclass can access any item in BankAccount marked protected. The subclass doesn’t have to be in the same assembly as its base class.

![](img/6df7bb88e9302e98442acc219cfbd7fc_412_2.png)

The ability to extend (subclass) a class from outside the base class’s assembly has implications for security, which is why many classes should be sealed. Sealing a class prevents outsiders from gaining access by subclassing it. That’s why you’re advised to make classes extendable (nonsealed) only if they need to be subclassable. One way to give other code in the same assembly access to a base class’s members — including a subclass in the same assembly — is to mark those members internal rather than protected. That way, you gain the desired level of access from a local subclass while preventing access from an external subclass.

Book II
Chapter 10
Can I Use Your Namespace in the Library?
