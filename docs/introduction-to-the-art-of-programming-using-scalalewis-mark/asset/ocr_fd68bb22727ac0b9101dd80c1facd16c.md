![](bbox=[0.135, 0.06, 0.825, 0.38])

# FIGURE 34.2: This is a screen shot of the drawing program with a DrawCircuit added

and two different circuits. Each circuit has two switches on the left side represented by squares. Clicking a square can toggle them on or off. You can think of them as being inputs A and B. The bottom circuit is an “exclusive or”. It implements the logic A xor B = (A or B) and not (A and B). The top circuit does not have an output. However, when both switches are turned on, a signal propagates around the loop.

```
case class WireData(index:Int, x:Double, y:Double, state:Boolean)
class CompData
case class GateData(gType:String, x:Double, y:Double, ins:Seq[Int]) extends CompData
case class SwitchData(x:Double, y:Double, state:Boolean) extends CompData
}
```

If you run this you can make some simple circuits like the ones shown in figure 34.2 then flip the switches and watch signals propagate through.

The elements of this code that are new center on the use of actors. Instead of calling methods on any element of comps, messages are passed. When values are needed immediately for things like drawing, the message is sent with !?.²

In addition to the Wire type there is a Gate with several subtypes and a Switch that are also subtypes of CircuitComponent. Each of the Gate subtypes has to define a delay value. This is proportional to how long it will take between the time an input wire changes and when the output wire changes. Note that the WireChange message handling in the Gate class includes a call to Thread.sleep to affect the delay. Because of this delay, and the desire to not block the actor thread, this was put in a call to Actor.actor so that it would occur in a separate thread and allow the actor to handle other messages during that time.

The way the actor message handling is written here should almost make it look like

> ²It should be noted that during the development of this code, that lead to the application hanging more than once when the !? operator was used with an actor that had not been started or did not respond to that message.