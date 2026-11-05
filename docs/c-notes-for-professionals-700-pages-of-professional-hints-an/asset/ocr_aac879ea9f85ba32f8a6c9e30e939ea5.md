```
///
class Programs
{
    static void Main(string[] args)
    {
        ITarget Itarget = new EmployeeAdapter();
        ThirdPartyBillingSystem client = new ThirdPartyBillingSystem(Itarget);
        client.ShowEmployeeList();
        Console.ReadKey();
    }
}
```

# When to use

+   - Allow a system to use classes of another system that is incompatible with it.
+   - Allow communication between new and already existing system which are independent to each other
+   - Ado.Net SqlAdapter, OracleAdapter, MySqlAdapter are best example of Adapter Pattern.