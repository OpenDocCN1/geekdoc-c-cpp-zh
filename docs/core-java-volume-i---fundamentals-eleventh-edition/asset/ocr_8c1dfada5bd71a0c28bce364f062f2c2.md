```
```java
class TimePrinter implements ActionListener
{
   private TalkingClock outer;
   . . .
   public TimePrinter(TalkingClock clock)
   {
      outer = clock;
   }
}
```
```

Now let us look at the actionPerformed method. It needs to access outer.beep.

```
```java
if (outer.beep) . . . // ERROR
```
```

Here we run into a problem. The inner class can access the private data of the outer class, but our external TimePrinter class cannot.

Thus, inner classes are genuinely more powerful than regular classes because they have more access privileges.

You may well wonder how inner classes manage to acquire those added access privileges, if they are translated to regular classes with funny names—the virtual machine knows nothing at all about them. To solve this mystery, let’s again use the ReflectionTest program to spy on the TalkingClock class:

```
```java
class TalkingClock
{
   private int interval;
   private boolean beep;

   public TalkingClock(int, boolean);

   static boolean access$0(TalkingClock);
   public void start();
}
```
```

Notice the static access$0 method that the compiler added to the outer class. It returns the beep field of the object that is passed as a parameter. (The method name might be slightly different, such as access$000, depending on your compiler.)

The inner class methods call that method. The statement

```
```java
if (beep)
```
```

in the actionPerformed method of the TimePrinter class effectively makes the following call:

```
```java
if (TalkingClock.access$0(outer))
```
```