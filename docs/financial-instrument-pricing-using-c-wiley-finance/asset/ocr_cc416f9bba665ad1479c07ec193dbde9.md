We can view the call option price C as a function because it maps a vector of parameters into a real value. The well-known exact formula for C is given by:

```
C = S e^{(b - r)T} N(d1) - K e^{-rT} N(d2)  (15.9)
```

where N(x) is the standard cumulative normal (Gaussian) distribution function defined by:

```
N(x) = 1/√(2π) ∫_{-∞}^{x} e^{-y²/2} dy  (15.10)
```

and where:

```
d1 = [log(S/K) + (b + σ²/2)T] / (σ√T)
d2 = [log(S/K) + (b - σ²/2)T] / (σ√T) = d1 - σ√T.  (15.11)
```

The cost-of-carry parameter b has specific values depending on the kind of security (Haug, 2007):

+   - b = r is the Black–Scholes stock option model
+   - b = r − q is the Merton model with continuous dividend yield q
+   - b = 0 is the Black–Scholes futures option model
+   - b = r − R is the Garman and Kohlhagen currency option model, where R is the foreign risk-free interest rate.

Since we are mainly interested in computing option prices and their sensitivities, we have decided to design the software here using the Command design pattern based on subtype polymorphism in combination with a class hierarchy (GOF, 1995). The definition is:

> Command is a behavioural design pattern in which an object is used to encapsulate all information needed to perform an action or trigger an event at a later time. This information includes the method name, the object that owns the method and values for the method parameters.

In the current case each dedicated object computes either an option price or one of its greeks. The corresponding UML diagram is shown in Figure 15.2 for the case of call options, for convenience (the case of put options as well as option vega, rho and theta have been left out). We note the presence of a composite command class that can contain other commands. In this way we can create trees and recursive aggregates of commands. Finally, each command (when executed) sends its result to a Receiver object which in the current case is the console but it could be adapted to other receivers such as another algorithm, Excel or a remote API. Composite receivers are also possible. In this case the event is multicasted to several receivers.