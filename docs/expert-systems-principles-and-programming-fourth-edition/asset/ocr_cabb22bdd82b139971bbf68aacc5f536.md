compute-total-price message, which invokes the MY-ORDER compute-total-price around handler. Within the around handler, the ORDER get-order-price primary handler is called to determine if order-price is numeric (which is it since it was just set to 10.0). Next the ORDER get-sales-tax primary handler is called to determine if sales-tax is numeric. It isn't, since the slot hasn't been set to the value supplied by make-instance, so the around handler calls the ORDER get-order-price primary handler again and returns this value. In this case, the computer-order-price around handler terminates without calling the primary handler. Finally the MY-ORDER put-order-price after handler exists:

```
HND >> put-sales-tax primary in class ORDER
ED:1 (<Instance-order5> 0.05)
HND << put-sales-tax primary in class ORDER
ED:1 (<Instance-order5> 0.05)
HND >> put-sales-tax after in class MY-ORDER
ED:1 (<Instance-order5> 0.05)
HND >> compute-total-price around in class MY-ORDER
ED:2 (<Instance-order5>)
HND >> get-order-price primary in class ORDER
ED:3 (<Instance-order5>)
HND << get-order-price primary in class ORDER
ED:3 (<Instance-order5>)
HND >> get-sales-tax primary in class ORDER
ED:3 (<Instance-order5>)
HND << get-sales-tax primary in class ORDER
ED:3 (<Instance-order5>)
HND >> compute-total-price primary in class ORDER
ED:2 (<Instance-order5>)
HND << compute-total-price primary in class ORDER
ED:2 (<Instance-order5>)
HND << compute-total-price around in class MY-ORDER
ED:2 (<Instance-order5>)
HND << put-sales-tax after in class MY-ORDER
ED:1 (<Instance-order5> 0.05)
```

Next the ORDER put-sales-tax primary message-handler is called to store the value 0.05 in the sales-tax slot. Once this handler finishes, the MY-ORDER put-sales-tax after handler is called. This handler sends the compute-total-price message, which invokes the MY-ORDER compute-total-price around handler. Within the around handler, the ORDER get-order-price primary handler is called to determine if order-price is numeric. It is, so next the ORDER get-sales-tax primary handler is called to determine if sales-tax is numeric (which it is because it was just set to 0.05). The around handler now calls the call-next/ handler function, which invokes the ORDER compute-total-price primary handler, which computes the updated value of the total-price slot. Finally the ORDER compute-total-price primary handler terminates, followed by the MY-