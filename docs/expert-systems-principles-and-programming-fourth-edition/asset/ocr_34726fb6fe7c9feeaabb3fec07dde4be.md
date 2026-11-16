```
ERROR:
(defmessage-handler MAIN::B bmh1
()
(* 2 ?self:x)
)
CLIPS>
(defmessage-handler B bmh2 ()
(* 2 ?self:y))
CLIPS>
```

The bmh1 message-handler makes a reference to ?self:x, which is not allowed since the x slot is inherited from class A. The bmh2 message-handler is allowed to make a reference to ?self since the y slot is defined by class B. COOL supports object encapsulation, which means that the implementation details of a class are hidden and that access to a class is limited to a well-defined interface: the message-handlers defined for the class. Since the get-x message-handler is the interface for retrieving the value of the x slot from instances of class A, this interface must be used by the bmh1 message-handler. With this change, the bmh1 message-handler can be defined without error:

```
CLIPS>
(defmessage-handler B bmh1 ()
(* 2 (send ?self get-x)))
CLIPS>
```

It's possible to disable the encapsulation behavior of a slot using the visibility slot attribute. If this attribute is set to private, which is the default, then the slot can be directly accessed only in message-handlers of a class defining it. If this attribute is set to public, then the slot can be directly accessed by subclasses and superclasses of any class defining it. In the prior example, defining class A as follows:

```
(defclass A
(is-a USER)
(slot x (visibility public)))
```

would allow you to define the message-handler bmh1 as follows:

```
(defmessage-handler B bmh1 ()
(* 2 ?self:x))
```

# Watching Messages and Message-Handlers

If messages or message-handlers are watched using the watch command, an informational message is printed whenever a message-handler begins or ends execution. For example:

```
CLIPS> (watch messages)
CLIPS> (watch message-handlers)
CLIPS> (send [circle-1] compute-area)
```