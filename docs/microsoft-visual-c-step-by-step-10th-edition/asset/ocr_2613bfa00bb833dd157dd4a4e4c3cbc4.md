```
class MyEventHandlingClass
{
    private MyClass myClass = new MyClass();
    ....
    public void Stop()
    {
        myClass.MyEvent -
        new myClass.MyDelegate (this.eventHandlingMethod);
    }
    ....
}
```