component that generates an event must produce a type that is compatible with the expectations of the receiver. Violations of this implicit agreement will cause an error.

A more insidious problem with exchanging pointers is that the output object is shared by its producer and all of its recipients. If any of these modify the object while calculating their state transition, that modification will be visible to all the models that share the object and appear later in the *Simulator*’s iteration through imminent and active objects. In effect, the shared object becomes a hidden channel for communication, and its effects can be unpredictable, are generally undesirable, and the root cause can be difficult to pin down. This problem is avoided by treating input objects as read-only, and permitting modification of the object only in the scope of the *output_func* of the model that created it.

# A.2.4  Mixing Strategies with Model Wrappers

It is sometimes desirable to connect two models that, although otherwise compatible, differ in the type of object that they use for input and output. The problem is illustrated in Figure A.2, where model $M_A$ that operates on events of type A is connected to $M_B$ that operates on events of type B. The *Simulator*, which is designed for use as a component within a larger model, offers a simple solution. It is illustrated in Figure A.3.

One of the models, $M_B$ in this instance, and its simulator are contained in a *ModelWrapper*, which is derived from the Atomic class and implements the *EventListener* interface. The input and output types of the *ModelWrapper* are compatible with $M_A$, and the class has a virtual method *translateInput* for converting a *Bag* of events of type A into a *Bag* of events of type B. This method is called by the external and confluent transition functions, which subsequently inject the converted inputs into $M_B$ by using the *computeNextState* method of the encapsulated *Simulator*. The *gc_input* method disposes of the input events in a way that is compatible with the memory management strategy used by model $M_A$.

The conversion of outputs from $M_B$ to a type acceptable by $M_A$ is more complicated; the essential steps are illustrated in Figure A.4. Output from $M_B$ is calculated with the *Simulator*’s *computeNextOutput*, which is called by the *output_func* of the *ModelWrapper*. The output events are intercepted by the *ModelWrapper*’s

![](bbox=[0.224, 0.728, 0.775, 0.866])

**FIGURE A.2** Using a model wrapper to couple two models with different types for input and output.