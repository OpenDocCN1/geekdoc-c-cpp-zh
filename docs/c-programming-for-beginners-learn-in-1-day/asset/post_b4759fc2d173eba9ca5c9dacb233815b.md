
2. In the Tutorial constructor, we are setting the value of TutorialID to 0 and TutorialName to “Default”. So whenever an object is created, these fields will always have these default values.

Now let’s switch over to our Program.cs file and just remove the line, which calls the SetTutorial method. This is because we want to just see how the constructor works.

```csharp
static void Main(string[] args)
{
    Tutorial pTutor = new Tutorial();
    Console.WriteLine(pTutor.GetTutorial());
    Console.ReadKey();
}
```

### Code Explanation:-

- 1. The first step is to create an object for the Tutorial class. This is done via the ‘new’ keyword.
- 2. We use the GetTutorial method of the Tutorial class to get the TutorialName. This is then displayed to the console via the Console.WriteLine method.

If the above code is entered properly and the program is executed, the following output will be displayed.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_52_0.png)

From the output, we can see that the constructor was indeed called, and that the value of the TutorialName was set to “Default”.

**Note:** Here the value “default” is fetched from the constructor.

## C# Inheritance

Inheritance is an important concept in C#. Inheritance is a concept in which you define parent classes and child classes.

The child classes inherits methods and properties of the parent class, but at the same time, they can also modify the behavior of the methods if required. The child class can also define methods of its own if required.

You will get a better understanding if we see this action.

Let’s now see how we can incorporate the concept of inheritance in our code.

Step 1) The first step is to change the code for our Tutorial class. In this step, we add the below code to the Tutorial.cs file.

```csharp
namespace DemoApplication
{
    public class Tutorial
    {
        protected int TutorialID;
        protected string TutorialName;

        public void SetTutorial(int pID , String pName) {
            TutorialID=pID;
            TutorialName=pName;
        }
    }
}
```

Mark the fields as protected.

Note that we need to now add the access modifier of ‘protected’ to both the TutorialID and TutorialName field.

Remember we had mentioned this access modifier in the Access Modifier chapter. Well here you can see the purpose of having this. Only when you have this access modifier (protected), the child class is able to use the fields of the parent class.

Step 2) The second step is to add our new child class. The name of this class will be “Guru99Tutorial”. In this step, we add the below code to the Tutorial.cs file. The code should be placed after the Tutorial class definition.

```csharp
public class Guru99Tutorial : Tutorial
{
    public void RenameTutorial(String pNewName)
    {
        TutorialName = pNewName;
    }
}
```

Defining the child class

Child class method

Setting the field TutorialName to a new name

### Code Explanation:-

- 1. The first step is to create the Guru99Tutorial child class. We also need to mention that this class is going to be a child class of the Tutorial class. This is done by the ':' keyword.
- 2. Next, we are defining a method called RenameTutorial. It will be used to rename the TutorialName field. This method accepts a string variable which contains the new name of the Tutorial.
- 3. We then assigned the parameter pNewName to the TutorialName field.

Note: - Even though we have not defined the TutorialName field in the “Guru99Tutorial” class, we are still able to access this field. This is because of the fact that “Guru99Tutorial” is a child class of Tutorial class. And because we made the fields of the Tutorial class as protected, they can be accessed by this class.

Step 3) The last step is to modify our main Program.cs file. In our console application, we are going to make an object of the Guru99Tutorial class. With this object, we are going to call the RenameTutorial method. We are then going to display the TutorialName field with the help of the GetTutorial method.

```csharp
class Program
{
    static void Main(string[] args)
    {
        Guru99Tutorial pTutor = new Guru99Tutorial();
        pTutor.RenameTutorial(".Net by Guru99");
        Console.WriteLine(pTutor.GetTutorial());
        Console.ReadKey();
    }
}
```

### Code Explanation:-

- 1. The first step is to create an object for the Guru99Tutorial class. This is done via the 'new' keyword. Note that this time we are not creating an object of the Tutorial class.
- 2. We use the RenameTutorial method of the Guru99Tutorial class to change the TutorialName field. We pass the string “.Net by Guru99” to the RenameTutorial method.
- 3. We then call the GetTutorial method. Note that even though this method is not defined in the Guru99Tutorial class, we are still able to access this method. The output of the GetTutorial method is then displayed to the console via the Console.WriteLine method.

If the above code is entered properly and the program is executed successfully, the following output will be displayed.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_56_0.png)

From the output, we can clearly see that the TutorialName field was renamed to “.Net by Guru99”. This was made possible by the RenameTutorial method called by the child class.

## C# Polymorphism

Polymorphism is a concept wherein a method can be defined more than one time. But each time, the function would have a different set of parameters passed on to it.

You will get a better understanding if we see this action.

Let’s now see, how we can incorporate the concept of Polymorphism in our code.

**Step 1)** The first step is to change the code for our Tutorial class. In this step, we add the below code to the Tutorial.cs file.

```csharp
public void SetTutorial(int pID, String pName)
{
    TutorialID = pID;
    TutorialName = pName;
}

public void SetTutorial(String pName)
{
    TutorialName = pName;
}
```

### Code Explanation:-

1 & 2) The first step is the same as in our earlier examples. We are keeping the definition of the SetTutorial method as it is.

3) This method sets the TutorialID and the TutorialName based on the parameters pID and pName.

4) This is where we make a change to our class wherein we add a new method with the same name of SetTutorial. Only this time we are only passing one parameter which is the pName. In this method, we are just setting the field of TutorialName to pName.

**Step 2)** The last step is to modify our main Program.cs file. In our console application, we are going to make an object of the Guru99Tutorial class.

```csharp
static void Main(string[] args)
{
    Tutorial pTutor = new Tutorial();

    pTutor.SetTutorial(1, "First Tutorial");
    Console.WriteLine(pTutor.GetTutorial());

    pTutor.SetTutorial("Second Tutorial");
    Console.WriteLine(pTutor.GetTutorial());

    Console.ReadKey();
}
```

![](img/8115a2172ef67838d7fe1933fc517c4d_58_0.png)

### Code Explanation:-

- 1. In the first step, we are using the SetTutorial method with 2 parameters. Where we are passing both the TutorialID and TutorialName to this method.
- 2. In the second step, we are now calling the SetTutorial method with just one parameter. We are just passing the TutorialName to this method.

If the above code is entered properly and the program is run the following output will be displayed. If in case you wanted to also fetch the Tutorial ID along with the Tutorial Name, you should follow the below step

- 1. Create a separate method called public int GetTutorialID
- 2. In that method write the code line “return TutorialID.” This can be used to return the TutorialID to the calling program.

### Output:

![](img/8115a2172ef67838d7fe1933fc517c4d_58_1.png)

From the output, we can clearly see that both methods were called successfully. Because of this, the strings “First Tutorial” and “Second Tutorial” were sent to the console.
