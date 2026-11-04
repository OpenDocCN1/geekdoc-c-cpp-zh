![](bbox=[0.115, 0.105, 0.215, 0.18])

Enter the protected keyword: If the _balance instance variable in the base class is declared protected rather than private, outsiders can't see it — it's effectively private to them. But subclasses can see it just fine.

An even better solution is to mark _balance private in BankAccount as before and then provide a Balance property marked protected. Subclasses such as SavingsAccount can access _balance by using the Balance property. But the balance is invisible to outsiders, which protects the BankAccount implementation even from its subclasses.

If the balance does indeed need to be accessible (read-only) to outsiders, you should, of course, provide the public Balance property to get the balance (read-only). However, you may still need to set the balance from inside SavingsAccount itself. To do that, you can give the set accessor of Balance protected access — accessible from SavingsAccount and other subclasses but inaccessible to outsiders. The discussion of properties in Chapter 5 of this minibook shows how to do it, and here's what the code looks like:

```
~~~csharp
// In BankAccount:
public decimal Balance
{
    get { return _balance; }    // Public
    protected set { _balance = value; }  // Not public
}
~~~
```

![](bbox=[0.115, 0.363, 0.22, 0.438])

The ProtectedLimitsAccess example on the web illustrates using the protected keyword as just described.

You can even subclass BankAccount in a different assembly, and the subclass has access to anything declared protected in BankAccount. The ProtectedLimitsAccess example also illustrates this process.

The example has two subclasses of BankAccount: one in the same assembly as BankAccount and one in a different assembly. What's interesting with respect to protected is that either BankAccount subclass can access any item in BankAccount marked protected. The subclass doesn't have to be in the same assembly as its base class.

![](bbox=[0.115, 0.63, 0.22, 0.71])

The ability to extend (subclass) a class from outside the base class's assembly has implications for security, which is why many classes should be marked sealed. Sealing a class prevents outsiders from gaining access by subclassing it. That's why you're advised to make classes extendable (nonsealed) only if they need to be subclassable. One way to give other code in the same assembly access to a base class's members — including a subclass in the same assembly — is to mark those members internal rather than protected. That way, you gain the desired level of access from a local subclass while preventing access from an external subclass. Of course, access is then

Book II
Chapter 10
Can I Use Your Namespace in the Future?