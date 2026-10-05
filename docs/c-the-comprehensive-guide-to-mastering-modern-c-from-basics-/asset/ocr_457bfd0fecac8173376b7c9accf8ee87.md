example, returning not implemented in all unsupported methods.

```
<<interface>>
Vehicle
  * startEngine()
  * accelerate()
  * break()
  * lightsOn()
  * signal(Direction)
  * shift(Gear)
  * radioOff()
  * ejectCd()
```

**Figure 19.1** These could be the methods of a “Car” class.

It should be obvious that neither of these two options is acceptable for implementing the module.

Let's try it differently: I break the large interface into several smaller, specialized interfaces that, for example,