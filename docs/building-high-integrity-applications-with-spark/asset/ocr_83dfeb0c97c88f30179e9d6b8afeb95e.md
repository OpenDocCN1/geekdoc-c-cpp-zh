tools did. However, the architecture of SPARK 2014 is much more flexible and extensible. It can also capitalize better on advances in proof technology. For example, to support a new theorem prover one only needs to create a suitable Why3 driver for it. This could even be done by a third party; no changes to GNATprove are required. The SPARK tools ship with Why3 drivers for several popular theorem provers, and this is the basis of how the tools support multiple provers.

Also, it is possible to directly interact with the underlying tools at the Why3 level. Consider, for example, asking the SPARK tools to prove a mathematical property about trigonometry functions such as the Pythagorean identity

Sin(X)*Sin(X) + Cos(X)*Cos(X) = 1.0

Even if we set aside the difficulties associated with floating point arithmetic, it is not a simple matter to write suitable (provable) postconditions for Sin and Cos that would allow the above to be proved. The Pythagorean identity is a consequence of an underlying mathematical theory relating the two functions. To illustrate, suppose Cos was declared as follows:

```
function Cos(X : Float) return Float
  with Post => Sin(X)*Sin(X) + Cos'Result*Cos'Result = 1.0;
```

The body of Cos might be something like⁷

```
function Cos(X : Float) return Float is
begin
  return Sqrt(1.0 − Sin(X)*Sin(X));
end Cos;
```

It might be possible to prove the given postcondition of such an implementation, provided a suitable postcondition for Sqrt was available, but clearly Sin cannot be written in a similar way or else the two functions would be infinitely mutually recursive. Instead, some other implementation of Sin would be necessary, say based on the Taylor series expansion of sin(x). The relationship between such an implementation and the Pythagorean identity is not obvious; the connection requires an appeal to broader mathematical concepts.

Yet the Pythagorean identity is an example of a basic relationship that might be quite useful in proving other properties of your program. How can you tell the SPARK tools about such relationships? One way it can be done is to provide an external axiomatization. This is, in effect, a handwritten Why3 theory that describes the desired properties. The Why3 tools will use this theory like any other, allowing proofs to succeed that otherwise might not. However, care is needed when using this technique