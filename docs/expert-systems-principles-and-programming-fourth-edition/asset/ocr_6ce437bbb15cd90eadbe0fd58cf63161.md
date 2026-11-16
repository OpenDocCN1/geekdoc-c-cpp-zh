```
(ID #001)
(order-price 10.00)
(sales-tax 0.05)).]
[order1>
CLIPS> (send [order1] put-ID #002).]
[MSGFUN3] ID slot in [order1] of ORDER: write
access denied.
[PRCCODE4] Execution halted during the actions of
message-handler put-ID primary in class ORDER
FALSE
CLIPS>
```

Note that the ID slot can be set when the order1 instance is created, but not later using the put-ID handler. Similarly, the total-price can be retrieved using the get-total-price handler but not set using put-total-price handler:

```
CLIPS> (send [order1] get-total-price).]
0.0
CLIPS> (send [order1] put-total-price 10.50).]
[MSGFUN1] No applicable primary message-handlers
found for put-total-price..
FALSE
CLIPS>
```

The compute-total-price handler has to be called in order to set the correct price:

```
CLIPS> (send [order1] compute-total-price).]
10.5
CLIPS> (send [order1] get-total-price).]
10.5
CLIPS>
```

It's possible to manually define the get-total-price handler so that the compute-total-price handler doesn't have to be explicitly called in order to compute the correct value for the total price. When you use the create-accessor attribute to define a get-handler for a class it creates a message-handler of the following form:

```
(defmessage-handler <class> get-<slot-name>
primary ()
?self:<slot-name>)
```

Similarly for put- handlers the following form is used:

```
(defmessage-handler <class> put-<slot-name>
primary (?value)
(bind ?self:<slot-name> ?value))
```