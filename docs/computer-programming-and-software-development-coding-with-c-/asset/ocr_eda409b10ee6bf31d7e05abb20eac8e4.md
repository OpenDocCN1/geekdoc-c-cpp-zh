instantiated either. That is, by the way, a common thing to have. In other words, it's possible to have several levels of abstract classes. Only when all abstract members have an implementation can the class be again a regular, class. We can actually, in Visual Studio, click on the lightbulb here and say implement the abstract class. It will then generate a bit of code that implements the ReceiveWage method.

```
public class Manager : Employee
{
    public Manager(string first, string last, string em, DateTime bd, double? rate) : base(first, last, em, bd, rate)
    { }

    public void AttendManagementMeeting()
    {
        NumberOfHoursWorked += 10;
        Console.WriteLine($"Manager {FirstName} {LastName} is now attending a long meeting that could have been an email!");
    }

    public override void GiveBonus()
    {
        if (NumberOfHoursWorked > 5)
            Console.WriteLine($"Manager {FirstName} {LastName} received a management bonus of 500!");
        else
            Console.WriteLine($"Manager {FirstName} {LastName} received a management bonus of 250!");
    }
}
```

Notice it does this by also using the override keyword, saying that from now on, when a manager is being used, this ReceiveWage method is going to be used, which is kind of logical. We don't even have a default anymore. I can now implement this method here, and this is the specific implementation for ReceiveWage for the Manager type. Or other types such as developer will also now start complaining because they also are missing this implementation for ReceiveWage. Let me add that quickly here.