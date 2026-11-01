This works very well for types that are primarily used for data representation, and as such, collection initializers are a great accompaniment to the LINQ technology described later in the book.

The following Try It Out illustrates how you can use object and collection initializers.

# TRY IT OUT Using Initializers: Ch13Ex04

+   1. Create a new console application called Ch13Ex04 and save it in the directory C:\BegVCSharp\Chapter13.
+   2. Right-click on the project name in the Solution Explorer window and select the Add Existing Item option.
+   3. Select the Animal.cs, Cow.cs, Chicken.cs, SuperCow.cs, and Farm.cs files from the C:\BegVCSharp\Chapter12\Ch12Ex04\Ch12Ex04 directory, and click Add.
+   4. Modify the namespace declaration in the file you have added as follows:
+      namespace Ch13Ex04
+   5. Remove the constructors from the Cow, Chicken, and SuperCow classes.

6. Modify the code in Program.cs as follows:

```
static void Main(string[] args)
{
    Farm<Animal> farm = new Farm<Animal>
    {
        new Cow { Name="Lea" },
        new Chicken { Name="Noa" },
        new Chicken(),
        new SuperCow { Name="Andrea" }
    };
    farm.MakeNoises();
    ReadKey();
}
```

7. Build the application. You should receive the build errors shown in Figure 13-10 because there is no Add(T animal) method definition in the Farm class. It is added in the next step.

![](bbox=[0.16, 0.78, 0.82, 0.94])

# FIGURE 13-10