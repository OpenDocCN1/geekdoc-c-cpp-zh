
Retrieving the order-price-slot works similarly:

```
CLIPS> (send [order6] get-order-price.)
HND >> get-order-price around in class FOREIGN-ORDER
EV:1 (<Instance-order6>)
HND >> get-order-price primary in class ORDER
EV:1 (<Instance-order6>)
HND << get-order-price primary in class ORDER
EV:1 (<Instance-order6>)
HND << get-order-price around in class FOREIGN-ORDER
EV:1 (<Instance-order6>)
20.0
CLIPS>
```

The FOREIGN-ORDER get-order-price around handler is invoked first and calls the ORDER get-order-price primary handler using call-next-handler. The U.S. dollar value of 10 is returned by the primary handler which is then multiplied by the exchange rate in the around handler to return a final value of 20 in units of the foreign currency.

Sending a print message to the FOREIGN-ORDER instance shows that the currency value is actually stored in the U.S. dollar amount rather than the foreign currency amount:

```
CLIPS> (unwatch all.)
CLIPS> (send [order6] print.)
[order6] of FOREIGN-ORDER
(ID #006)
(total-price 0.0)
(order-price 10.0)
(sales-tax 0.1)
(exchange-rate 2)
CLIPS>
```

## Handler Execution Order

We've used four different techniques to modify the behavior of the ORDER class by attaching handlers to the MY-ORDER class: overriding the primary handler, defining a before handler, defining after handlers, and defining after and around handlers. The obvious question at this point is which approach is the best. In this case using the before handler is probably the best solution. It uses the least amount of code and it has a key advantage compared to overriding the primary handler (which uses the second least amount of code): All inherited before and after message-handlers belonging to a class or its superclass are called unless an error occurs or an around handler terminates the message. This means that a class can slightly modify the behavior of a superclass using before and after handlers without overriding the primary handler and subclasses can't prevent the execution of a before or after handler unless they terminate the message, thus preventing the execution of all before, after, and primary handlers. If you modify the behavior of an existing class by redefining a new class and then overriding the primary handler, your primary handler is also subject to being overridden by a subclass. Unless the overriding class calls the call-next-handler function, your primary handler won't get executed. This is not to say that you should never override the primary handler, but if you have some special behavior that you don't want inheriting classes to be able to override, you should definitely consider placing this behavior in a before or after handler.

Given that you may have specialized behavior in multiple before, after, and around handlers inherited by a class, it's important to know the order in which the various message-handlers are called. When a message is sent to an instance using the send command, all the applicable message-handlers are determined and the following steps are taken:

- 1. If there are any uncalled around handlers, then invoke the most specific one; otherwise proceed to step 2. If the invoked around handler calls call-next-handler or override-next-handler, then repeat this step; otherwise proceed to step 6.
- 2. If there are any uncalled before handlers, then invoke the most specific one, wait for it to finish, then repeat this step. Otherwise, proceed to step 3. The return values of the before handlers are ignored. There is no way to directly return these values to another handler.
- 3. If there are any uncalled primary handlers, then invoke the most specific one; otherwise proceed to step 4. If an invoked primary handler calls call-next-handler or override-next-handler, then repeat this step; otherwise proceed to step 4. You can't send a message to an instance unless there is at least one applicable primary handler.
- 4. Allow each primary handler to finish and return, then remove it from the list of called primary handlers. If a primary handler calls call-next-handler or override-next-handler again, go back to step 3. Once all primary handlers have finished, remember the return value of the last primary handler executed and proceed to step 5.
- 5. If there are any uncalled after handlers, then invoke the least specific one, wait for it to finish, then repeat this step. Otherwise proceed to step 6. The return values of the after handlers are ignored. There is no way to directly return these values to another handler.
- 6. If no around handlers were called, proceed to step 7. Otherwise, allow each around handler to finish and return, then remove it from the list of called around handlers. If an around handler calls call-next-handler or override-next-handler again, proceed back to step 1. Once all around handlers have finished, remember the value of the last around handler executed and proceed to step 7.
- 7. The final return value of the send command is the return value of the most specific around handler from step 6. If there are no around handlers, then the return value of the most specific primary handler from step 4 is used.

The return value of the call-next-handler or override-next-handler function is the last action executed in the next around or primary handler called. A handler can either ignore this value or use it as its return value.

Figure 11.2 shows a flowchart that yields equivalent results to steps 1 through 7. Step 1 begins in the box in the upper-left corner of the figure. Figure 11.3 shows a flowchart that yields the equivalent results to steps 3 and 4 in executing the applicable primary handlers associated with a message sent to an instance. In cases where there are no applicable around, before, or after handlers (i.e., only primary handlers), the Figure 11.2 flowchart reduces equivalently to the Figure 11.3 flowchart.

The following constructs will be used to demonstrate the order of handler execution:

```
(defclass A
  (is-a USER))
(defmessage-handler A msg1 primary ()
  (return msg1-A))
(defmessage-handler A msg1 before ())
(defmessage-handler A msg1 after ())
(defmessage-handler A msg1 around ()
  (call-next-handler))
(defclass B
  (is-a A))
(defmessage-handler B msg1 primary ()
  (return msg1-B))
(defmessage-handler B msg1 before ())
(defmessage-handler B msg1 after ())
(defmessage-handler B msg1 around ()
  (call-next-handler))
```

Class B is a subclass of class A. Each class has its own primary, before, after, and around handlers. First, we'll create instances of both classes:

```
CLIPS> (make-instance [a1] of A.)
[a1]
CLIPS> (make-instance [b1] of B.)
[b1]
CLIPS>
```

## Figure 11.2 Handler Execution Order Determination

Determine all applicable message-handlers for the message sent to the instance

Are there any uncalled around handlers?

Invoke the most specific uncalled around handler.

Does the executing handler call-next-handler?

Are there any uncalled around handlers?

Invoke the most specific uncalled before handler and wait for it to finish.

Allow the currently around handler to finish and return a value. Treat the handler as uncalled.

Execute the primary handlers and remember the return value. (See Figure 11.3)

The return value of the message is the return value of the last around handler executed.

Are there any around handlers still existing?

Are there any uncalled after handlers?

Invoke the least specific uncalled after handler and wait for it to finish.

Allow the currently around handler to finish and return a value. Treat the handler as uncalled.

Are there any uncalled around handlers?

Pass the primary handler return value back to the around handler via call-next-handler.

The return value of the message is the return value of the last primary handler executed.

## Figure 11.3 Primary Handler Execution Order Determination

Begin with all applicable primary handlers for the message sent to the instance.

Are there any uncalled around handlers?

Invoke the most specific uncalled around handler.

Does the executing handler call-next-handler?

Allow the currently executing primary to finish and return a value. Treat the handler as uncalled.

Are there primary handlers still executing?

Continue executing the most recent primary handler invoked.

The return value from the primary is the return value of the last primary handler executed.
