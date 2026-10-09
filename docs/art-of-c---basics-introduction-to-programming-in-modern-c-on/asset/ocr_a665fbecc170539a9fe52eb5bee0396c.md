# 22.2. Code Review - Total Salary Calculator

```
salary-calculation/Employees.cs (lines 3-17)
```

```
public abstract record Employee(string Name) {
    public abstract decimal Salary { get; }
}

public sealed record Manager(string Name) : Employee(Name) {
    public override decimal Salary => 1_000_000m;

    public string Manage() => $"I just manage and I get paid {Salary} dollars.";
}

public sealed record Worker(string Name) : Employee(Name) {
    public override decimal Salary => 100_000m;

    public string Work() => $"I work and I get paid {Salary} dollars for my hard work.";
}
```

Interestingly, all *Managers* in this Corporation make a million dollars annually, whereas all rank and file *Workers* have an annual salary of only 100,000 dollars. ☺

As we will discuss shortly, a *Worker* is an *Employee* in this example. Likewise, a *Manager* is an *Employee* as well.

There are also two kinds of *Organizations* in this Corporation, a *Management*, which includes only *Managers*, and a *RankAndFile*, which includes only *Workers*. (As stated, this is a somewhat contrived example for more than one reason. ☺)