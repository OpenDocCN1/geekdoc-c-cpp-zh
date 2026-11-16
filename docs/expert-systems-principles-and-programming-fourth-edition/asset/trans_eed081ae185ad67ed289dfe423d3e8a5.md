

```
(make-instance order5 of MY-ORDER
  (ID #005)
  (order-price 10.00)
  (sales-tax 0.05))
```
HND >> create primary in class USER
  ED:1 (<Instance-order5>)
HND << create primary in class USER
  ED:1 (<Instance-order5>)
HND >> put-ID primary in class ORDER
  ED:1 (<Instance-order5> #005)
HND << put-ID primary in class ORDER
  ED:1 (<Instance-order5> #005)

order5 实例是使用 make-instance 调用创建的。create 消息处理程序（另一个系统定义的消息处理程序）在实例创建后立即被调用。一旦原始实例被创建，make-instance 调用中指定的值就会被放入实例的槽中。首先调用 put-ID 消息处理程序，将 #005 存储在 ID 槽中：

```
HND >> put-order-price primary in class ORDER
  ED:1 (<Instance-order5> 10.0)
HND << put-order-price primary in class ORDER
  ED:1 (<Instance-order5> 10.0)
HND >> put-order-price after in class MY-ORDER
  ED:1 (<Instance-order5> 10.0)
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
HND >> get-order-price primary in class ORDER
  ED:3 (<Instance-order5>)
HND << get-order-price primary in class ORDER
  ED:3 (<Instance-order5>)
HND << compute-total-price around in class MY-ORDER
  ED:2 (<Instance-order5>)
HND << put-order-price after in class MY-ORDER
  ED:1 (<Instance-order5> 10.0)
```

接下来，ORDER put-order-price primary 消息处理程序被调用，以将值 10.0 存储在 order-price 槽中。该处理程序结束后，会调用 MY-ORDER put-order-price after 处理程序。该处理程序发送 compute-total-price 消息，从而调用 MY-ORDER compute-total-price around 处理程序。在 around 处理程序中，会调用 ORDER get-order-price primary 处理程序来判断 order-price 是否为数值（确实是，因为它刚刚被设置为 10.0）。接下来，会调用 ORDER get-sales-tax primary 处理程序来判断 sales-tax 是否为数值。它不是，因为该槽尚未设置为 make-instance 提供的值，因此 around 处理程序会再次调用 ORDER get-order-price primary 处理程序并返回该值。在这种情况下，compute-total-price around 处理程序在不调用 primary 处理程序的情况下终止。最后，MY-ORDER put-order-price after 处理程序退出：

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

接下来，ORDER put-sales-tax primary 消息处理程序被调用，以将值 0.05 存储在 sales-tax 槽中。该处理程序结束后，会调用 MY-ORDER put-sales-tax after 处理程序。该处理程序发送 compute-total-price 消息，从而调用 MY-ORDER compute-total-price around 处理程序。在 around 处理程序中，会调用 ORDER get-order-price primary 处理程序来判断 order-price 是否为数值。它是，因此接下来会调用 ORDER get-sales-tax primary 处理程序来判断 sales-tax 是否为数值（它是，因为它刚刚被设置为 0.05）。around 处理程序现在会调用 call-next-handler 函数，该函数会调用 ORDER compute-total-price primary 处理程序，从而计算 total-price 槽的更新值。最后，ORDER compute-total-price primary 处理程序终止，随后是 MY-ORDER compute-total-price around 处理程序，随后是 MY-ORDER put-sales-tax after 处理程序：

```
HND >> init primary in class USER
ED:1 (<Instance-order5>)
HND << init primary in class USER
ED:1 (<Instance-order5>)
[order5]
CLIPS>
```

最后，init 消息被发送到新创建的实例，然后返回实例名称。init 消息处理程序是另一个系统定义的消息处理程序。它在实例创建结束时、槽值初始化后被调用。

## 重写消息处理程序参数

可以通过使用 override-next-handler 命令来重写传递给消息处理程序的参数。该命令的语法如下：

```
(override-next-handler <expression>*)
```

其中每个 <expression> 都是要发送给下一个消息处理程序的替换参数。为了举例说明此命令的用法，让我们考虑如何处理外币订单。同样，假设出于各种原因我们不想直接修改 ORDER 类。如果 ORDER 实例的 order-price 值为美元，则可能会基于价格为美元而存在特殊逻辑。例如，超过 100 美元的订单可能会免除运费。

处理不同货币的一种方法是定义一个继承自 ORDER 类的类，但会自动在外币和美元之间进行转换。以下 FOREIGN-ORDER defclass 及其关联处理程序实现了这种方法：

```
(defclass FOREIGN-ORDER
(is-a ORDER)
(slot exchange-rate (default 1.0)))

(defmessage-handler FOREIGN-ORDER get-order-price
around ()
(* ?self:exchange-rate (call-next-handler)))

(defmessage-handler FOREIGN-ORDER put-order-price
around (?value)

(override-next-handler
(/ ?value ?self:exchange-rate)))
```

FOREIGN-ORDER 类具有一个 exchange-rate 槽，用于表示外币与美元之间的汇率。例如，如果汇率为 2，则 10 美元相当于 20 单位的外币。在实际使用中，我们可能还会提供一个槽来指示外币的单位（例如欧元），但对于本示例来说，这不是必需的。

FOREIGN-ORDER get-order-price around 处理程序通过使用 call-next-handler 命令调用 ORDER get-order-price primary 处理程序。然后将返回值乘以 exchange-rate 槽的值并返回该值。FOREIGN-ORDER put-order-price around 处理程序使用 override-next-handler 调用 ORDER put-order-price primary 处理程序，但它不是传入外币中的值，而是将该值除以汇率并传递该值，即美元中的值。

通过监视消息处理程序，我们可以观察 FOREIGN-ORDER 类的行为。首先，我们创建该类的一个实例：

```
CLIPS> (unwatch all)
CLIPS>
(make-instance order6 of FOREIGN-ORDER
    (ID #006)
    (exchange-rate 2)
    (sales-tax .10))
[order6]
CLIPS>
```

接下来，我们将 order-price 槽更改为外币中的 20.00 值：

```
CLIPS> (watch message-handlers)
CLIPS> (send [order6] put-order-price 20.00)
HND >> put-order-price around in class FOREIGN-ORDER   ED:1 (<Instance-order6 20.0)
HND >> put-order-price primary in class ORDER
ED:1 (<Instance-order6 10.0)
HND << put-order-price primary in class ORDER
ED:1 (<Instance-order6 10.0)
HND << put-order-price around in class FOREIGN-ORDER   ED:1 (<Instance-order6 20.0)
10.0
CLIPS>
```

首先，FOREIGN-ORDER put-order-price around 处理程序以值 20 被调用。然后，作为 override-next-handler 调用的结果，ORDER put-order-price primary 处理程序以值 10 被调用。这个美元值随后作为 send 命令的返回值被传回。

