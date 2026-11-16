```
(defmessage-handler CIRCLE compute-area
()
(* (pi)
(send ?self get-radius)
(send ?self get-radius)))
(definstances figures
(rectangle-1 of RECTANGLE (height 2) (width 4))
(circle-1 of CIRCLE (radius 3)))
```

This example defines two classes, RECTANGLE and CIRCLE, with the appropriate slots for each. A message-handler, compute-area, is attached to each class. The purpose of this message-handler is to compute the area for each object. For the RECTANGLE class, the area of the RECTANGLE instance is the height of the instance multiplied by the width. For the CIRCLE class, the area of the RECTANGLE instance is the value of π returned by the pi function multiplied by the radius of the instance squared. Notice the variable ?self is used in both message-handlers. This is a special variable automatically defined for each message-handler. When the message-handler is called, the value of the ?self variable is assigned the instance-address of the instance to which the message has been sent. You can use this variable to send messages to the instance as we do in this example to retrieve the values of the height, width, and radius slots.

Once the message-handlers are defined, we can send a compute-area message to instances of the RECTANGLE and CIRCLE classes to determine the area of the instance:

```
CLIPS> (reset).]
CLIPS> [send [circle-1 compute-area].]
28.2743338823081
CLIPS> (send [rectangle-1 compute-area].]
8
CLIPS>
```

Notice that we send each instance the same message, but each responds differently in computing their area. This ability for different instances to respond to the same message in a manner specific to itself is known as polymorphism.

# Slot Shorthand References

It's often inconvenient to always have to send a message to an instance in order to retrieve or set a slot value, so a shorthand mechanism is available that allows you to access the slots of the instance bound to the ?self variable. Instead of using the expression:

```
(send ?self get-<slot-name>)
```

the expression:

```
?self:<slot-name>
```