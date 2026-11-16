# Uses of Defglobals

Defglobals are most appropriately used in rules as either constants or to pass in information that is used only on the RHS of the rule and should not trigger pattern matching. Used as constants, defglobals can make your program easier to understand. Consider the following rule:

```
(defrule plant-advisory
   (temperature ?value Fahrenheit)
   (test (<= ?value 32))
   =>
   (printout t "It's freezing." crlf)
   (printout t "Bring your plants inside." crlf))
```

Certainly most people are that aware that the freezing point of water is 32° Fahrenheit (or 0° Celsius), so the significance of the constant 32 in the plant-advisory rule should be easily deduced. But not all constants are common knowledge. By assigning the value of 32 to a global variable, we can use a meaningful symbolic name in the plant-advisory rule making it easier to understand:

```
(defglobal ?*water-freezing-point-Fahrenheit* = 32)

(defrule plant-advisory
   (temperature ?value Fahrenheit)
   (test (<= ?value ?*water-freezing-point-Fahrenheit*))
   =>
   (printout t "It's freezing." crlf)
   (printout t "Bring your plants inside." crlf))
```

One use of defglobals to avoid triggering pattern matching is for debugging. Suppose you want to print some additional information beyond what's provided by the watch command. One way to do that would be by adding printout or format commands to your rules like the following:

```
(defrule debug-example
   (data ?x)
   =>
   (printout t "Debug-example ?x = " ?x crlf))
```

The problem arises, however, that you may not want to see these debugging messages all the time so you would either have to delete them or convert them into comments when you don't want them active. One way to conveniently get around this problem is to store the logical name to which the debugging output is sent in a defglobal. If nil is used as the logical name argument to either the printout or the format command, then no output is produced (although the format command still returns the formatted string as its return value). You can take