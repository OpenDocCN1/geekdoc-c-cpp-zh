This example partial function would operate on an Int, but would only be defined if the argument was 1 or 2.

This is more useful when we use more of the options for cases and the pattern matching they do. For GUIs in particular, it is most important to be able to match on different types. If the case includes a name that begins with a lowercase letter, it will use that as a variable name to store the value of the match in.

```
{
  case v => println(v) // this will happen for everything
}
```

Using the colon syntax that you have been using all along to specify the types of arguments to functions and the fields in case classes, you can also specify that a named value in a case has to have a specific type.

```
{
  case i:Int => println("Partial functions called on an Int "+i)
  case d:Double => println("Partial functions called on a Double "+d)
  case s:String => println("String = "+s)
}
```

This example partial function is only defined for Int, Double, and String. If you pass in any other type, it will fail. If you call it with one of those types, it will give that value to the name i, d, or s, then print the appropriate output.

# 11.3.2 Publishers and Reactors

The model for having users interact with GUIs in the scala.swing library is based on types called Publisher and Reactor. The idea is that the components in a GUI are Publishers. When something happens to them, let us call it an EVENT. The Publisher will publish that event. Code can be set up in a Reactor to pay attention to a particular Publisher and then it can react to these events in the proper way. There is a type called Event that represents something that can happen in the GUI. There are lots of different subtypes of Event that are part of the scala.swing.event package.

As we saw above, you do not have to do this for Buttons because when you create a Button, there is a simple syntax for providing the code that will be executed. Not everything is so simple though. For many components there are several different possible events that you might react to or there is other information that you need to know when the interaction occurs.

To see this, consider the example of a ListView. Two of these were placed in the GUI for the recipe book. When the user clicks on something in the ListView, the program needs to be able to display the appropriate information in other fields. To illustrate how this works, we will start with a simpler example that contains only a ListView and a TextField. When the user selects an item from the ListView, the text field should be set to the value of what was clicked. This example can be set up with the following code.

```
import scala.swing._
import scala.swing.event._

val options = "A list of words".split(" ")
val list = new ListView(options)
val field = new TextField
```