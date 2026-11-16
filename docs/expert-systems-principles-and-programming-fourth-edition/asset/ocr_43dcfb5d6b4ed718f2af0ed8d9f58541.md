```
(active-message-duplicate-instance
    <instance-expression>
    [to <instance-name-expression>]
    [<slot-overrides>*])
```

where <instance-expression> is the instance to be modified or duplicated, <slot-overrides> is the list of slot modifications, and for the duplicate command, <instance-name-expression> is the optional new name for the duplicated instance.

The most basic instance-modification command is the modify-instance command. The following is an example of its use:

```
CLIPS> (unwatch all.)
CLIPS> (clear.)
CLIPS>
(defclass PERSON
   (is-a USER)
   (slot first-name)
   (slot last-name))
CLIPS>
(make-instance [p1] of PERSON
   (first-name "Jeff")
   (last-name "Public").)
[p1]
CLIPS> (watch messages.)
CLIPS> (watch slots.)
CLIPS>
(modify-instance [p1] (first-name "Jack")
   (last-name "Private").)
MSG >> direct-modify ED:1 (<Instance>p1>
   <Pointer-0x06b2b200>)
:: = local slot first-name in instance p1 <- "Jack"
:: = local slot last-name in instance p1
<- "Private"
MSG << direct-modify ED:1 (<Instance>p1>
   <Pointer-0x0062b200>)
TRUE
CLIPS> (unwatch all.)
CLIPS> (send [p1] print.)
[p1] of PERSON
(first-name "Jack")
(last-name "Private")
CLIPS>
```

Notice that a direct-modify message is sent to the instance [p1], but put-first-name and put-last-name messages are not sent. The direct-modify message-