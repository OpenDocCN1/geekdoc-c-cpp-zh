specified by the type parameter T. In this class, you will use the methodToExecute field to reference the code that the Command object will run when it is invoked by the view. The methodToDetectCanExecute field will be used to reference the method that detects whether the command can run (it may be disabled for some reason, depending on the state of the app or the data).

6. Add a constructor to the Command class. This constructor should take two parameters: an Action object and a Func<T> object. Assign these parameters to the methodToExecute and methodToDetectCanExecute fields, as shown here in bold:

Click here to view code image

```
public Command : ICommand
{
    ...
    public Command(Action methodToExecute, Func<bool> methodToDetectCanExecute)
    {
        this.methodToExecute = methodToExecute;
        this.methodToDetectCanExecute = methodToDetectCanExecute;
    }
}
```

The ViewModel will create an instance of this class for each command. The ViewModel will supply the method to run the command and the method to detect whether the command should be enabled when it calls the constructor.

7. Implement the Execute and CanExecute methods of the Command class by using the methods referenced by the methodToExecute and methodToDetectCanExecute fields, as follows:

Click here to view code image

```
public Command : ICommand
{
    ...
    public Command(Action methodToExecute,
        Func<bool> methodToDetectCanExecute)
    {
        ...
    }

    public void Execute(object parameter)
    {
        this.methodToExecute();
    }

    public bool CanExecute(object parameter)
    {
        if (this.methodToDetectCanExecute == null)
```