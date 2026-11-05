```
static void handleCasement ()
{
    Console.WriteLine("Handle Casement");
}
static void handleStandard ()
{
    Console.WriteLine("Handle Standard");
}
static void handlePatio ()
{
    Console.WriteLine("Handle patio");
}
```

These methods are the ones which will eventually deal with each type of window. At the moment they just print out that they have been called. Later you will go on and fill the code in (this is actually quite a good way to construct your programs). Once you have the methods in place, the next thing you need to do is write the code that will call the one that the user has selected.

We already have a method that we can use to get a number from the user (it is called readInt and is given a prompt string and high and low limits). Our program can use this method to get the selection value and then pick the method that needs to be used.

# 3.5.2 Selecting using the if construction

When you come to perform the actual selection you end up with code which looks a bit like this:

```
int selection ;
selection = readInt ( "Window Type : ", 1, 3 ) ;

if ( selection == 1 )
{
    handleCasement();
}
else
{
    if ( selection == 2 )
    {
        handleStandard();
    }
    else
    {
        if ( selection == 3 )
        {
            handlePatio() ;
        }
        else
        {
            Console.WriteLine ( "Invalid number" );
        }
    }
}
```

This would work OK, but is rather clumsy. You have to write a large number of if constructions to activate each option.

# 3.5.3 The switch construction

Because you have to do this a lot C# contains a special construction to allow you to select one option from a number of them based on a particular value. This is called the switch construction. If you write the above using it your program would look like this.