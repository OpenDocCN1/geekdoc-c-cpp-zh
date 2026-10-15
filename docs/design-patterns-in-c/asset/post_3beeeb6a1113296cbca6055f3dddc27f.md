
Following is the class diagram:

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_87_0.png)

This concludes our application using the Interpreter Pattern. Now the actions could be converted to a language for interpreting later.

## Comparison of Command Pattern and Interpreter Pattern

You can find some similarities between the Command and Interpreter patterns. The command pattern says about converting the actions into commands for logging or undo purposes. Here the commands are objects but for the Interpreter pattern the commands are sentences.

The Command pattern can be used for persisting objects by serializing the command list and results in large sized files compared with Interpreter pattern. The Interpreter pattern provides an easier approach at runtime but comes at the cost of developing an interpreter.

### Applications of Interpreter Pattern

You are creating your own Photoshop application. The objects drawn on the layer can be converted to a series of commands. Later the entire drawing could be represented using the command file which will be small in size compared to the entire canvas serialized. You will get the advantage of sending the file to another person where he/she can:

- Regenerate the Drawing
- View all the Draw Actions
- Modify the Draw Action Items
- Undo the last draw actions

### References

http://www.dofactory.com/Patterns/PatternInterpreter.aspx#_self1

### Summary

In this chapter we have seen about the Interpreter pattern with a small application using it. The above application shows only a simple usage for learning purpose but in the real world scenarios the language may include loops, conditions etc. The attachment contains the source code of application we have discussed.

## 23. Composite Pattern

In this chapter we can explore the Composite Design Pattern. It provides a better approach in addressing communication with individual and group of objects. As usual we can start with the Challenge – Solution approach.

### Challenge

You are working on a distributed application containing Head Office and Branch Offices. Each office will be having 2 Clock Controls which needed to be updated globally during Daylight Saving times.

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_89_0.png)

The above diagram shows the current structure. There will be only 1 Head Office and multiple branches under it. The head office and each branch will be having 2 clock controls. The time changing process starts from the head office and in the current approach, the head office has to remember all branches and all clocks inside each branch. This is very tedious and will break when there is consolidation of branches under one branch group.

How to provide a better solution?

### Definition

GoF Definition: "Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly"

### Implementation

We can use the Composite Design Pattern in the above scenario. Once our solution is implemented the Head Office needs to think about only the Branches. The Branches will think about their respective Clocks.

There are 2 classes in our solution: Office and Clock. The Office class can represent Head Office and Branches. The Clock class manages the clock control for changing time.

We need to introduce one interface which will be implemented by the Office and Clock classes.

```csharp
interface IComponent
{
    void Add (IComponent notifier);
    void SetTime(DateTime time);
}
```

The Add() method ensures adding a component of type IComponent. It can be used to add an Office or Clock instance.

The SetTime() method can be used to change the current time.

### Class Implementations

Following are the implementations of the Office and Clock classes:

```csharp
class Office : IComponent
{
    private IList<IComponent> _list = new List<IComponent>();

    public void Add(IComponent notifier)
    {
        _list.Add(notifier);
    }

    public void SetTime(DateTime time)
    {
        foreach (IComponent n in _list)
            n.SetTime(time);
    }
}

class Clock : IComponent
{
    public ClockControl ClockControl;

    public void Add(IComponent notifier)
    {
        throw new ApplicationException("You cannot add IClock!");
    }

    public void SetTime(DateTime time)
    {
        ClockControl.CurrentTime = time;
    }
}
```

Please note that the SetTime() implementation of Office class takes care of informing all the added IComponent instances. Thus the Head Office can notify all the branches. The branches will notify all the clock instances.

### Creating Instances

Following is the code of instance creation for Head Office and Branches.

```csharp
_headOffice = new Office();
_headOffice.Add(new Clock() { ClockControl = hForm.clock1 });
_headOffice.Add(new Clock() { ClockControl = hForm.clock2 });

Office branch1 = new Office();
branch1.Add(new Clock() { ClockControl = b1Form.clock1 });
branch1.Add(new Clock() { ClockControl = b1Form.clock2 });
_headOffice.Add(branch1);

Office branch2 = new Office();
branch2.Add(new Clock() { ClockControl = b2Form.clock1 });
branch2.Add(new Clock() { ClockControl = b2Form.clock2 });
_headOffice.Add(branch2);
```

Please note that the branch instances are added to the head office.

### Running the Application

On clicking the Set Time button you can see all the clocks are reset to 10:00 AM.

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_91_0.png)

Here the Head Office does not need to think about all the clock instances of branches. Here the individual objects (clocks) and composite objects (branches) are treated uniformly satisfying the pattern definition.

### Summary

In this chapter we have explored the Composite Pattern. It provides a centralized approach in talking with individual and combined objects. The attachment contains the example application including the clock control we have discussed.

### References

The ebook is compiled on information collected from Books, MSDN and other Online Resources. It took almost 1 year to cover all the chapters and so some of the reference links will be obsolete.

You can find more information on Design Patterns using the following links:

http://www.dofactory.com

http://www.oodesign.com

### Source Code

The source code for the ebook can be found over http://jeanpaulva.com.

