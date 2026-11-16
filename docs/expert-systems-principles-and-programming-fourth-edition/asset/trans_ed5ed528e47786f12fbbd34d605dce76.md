

现在我们将观察消息处理器，并向实例 a1 发送 msg1 消息：

```
CLIPS> (watch message-handlers)
CLIPS> (send [a1] msg1)
HND => msg1 around in class A
ED:1 <Instance-a1>
HND => msg1 before in class A
ED:1 <Instance-a1>
HND << msg1 before in class A
ED:1 <Instance-a1>
HND => msg1 primary in class A
ED:1 <Instance-a1>
HND << msg1 primary in class A
ED:1 <Instance-a1>
HND => msg1 after in class A
ED:1 <Instance-a1>
HND << msg1 after in class A
ED:1 <Instance-a1>
HND << msg1 around in class A
ED:1 <Instance-a1>
msg1-A
CLIPS>
```

对于此消息，有四个适用的消息处理器：类 A 的 msg1 主处理器、前置处理器、后置处理器和环绕处理器。从步骤 1 开始，执行类 A 的 msg1 环绕处理器。该处理器调用 call-next-handler 函数，因此我们重复步骤 1。由于没有剩余未调用的环绕处理器，我们继续执行步骤 2。允许类 A 的 msg1 前置处理器执行并返回。由于没有其他未调用的前置处理器，我们继续执行步骤 3。执行类 A 的 msg1 主消息处理器。它不调用 call-next-handler，因此我们继续执行步骤 4。允许类 A 的 msg1 主消息处理器完成，并返回符号 msg1-A。所有主处理器均已执行完毕，因此我们继续执行步骤 5。允许类 A 的 msg1 后置处理器执行并返回。由于没有其他未调用的后置处理器，我们继续执行步骤 6。允许类 A 的 msg1 环绕处理器完成。该处理器执行的最后一个操作是 call-next-handler 函数，因此返回值将是被调用的下一个环绕或主处理器的返回值。在此例中，返回值为 msg1-A 的是类 A 的 msg1 主处理器，因此环绕处理器的返回值相同。由于所有环绕处理器均已完成，我们继续执行步骤 7。send 命令的最终返回值是类 A 的 msg1 环绕处理器返回的值 msg1-A。

现在让我们向实例 b1 发送 msg1 消息：

```
CLIPS> (send [b1] msg1)
HND => msg1 around in class B
ED:1 <Instance-b1>
HND => msg1 around in class A
ED:1 <Instance-b1>
HND => msg1 before in class B
ED:1 <Instance-b1>
HND << msg1 before in class B
ED:1 <Instance-b1>
HND => msg1 before in class A
ED:1 <Instance-b1>
HND << msg1 before in class A
ED:1 <Instance-b1>
HND => msg1 primary in class B
ED:1 <Instance-b1>
HND << msg1 primary in class B
ED:1 <Instance-b1>
HND => msg1 after in class A
ED:1 <Instance-b1>
HND << msg1 after in class A
ED:1 <Instance-b1>
HND => msg1 after in class B
ED:1 <Instance-b1>
HND << msg1 after in class B
ED:1 <Instance-b1>
HND << msg1 around in class A
ED:1 <Instance-b1>
HND << msg1 around in class B
ED:1 <Instance-b1>
msg1-B
CLIPS>
```

对于此消息，有八个适用的消息处理器：类 A 的 msg1 主处理器、前置处理器、后置处理器和环绕处理器，以及类 B 的 msg1 主处理器、前置处理器、后置处理器和环绕处理器。从步骤 1 开始，执行类 B 的 msg1 环绕处理器，因为这是最具体的环绕处理器。该处理器调用 call-next-handler 函数，因此我们重复步骤 1。下一个最具体的环绕处理器是类 A 的 msg1 环绕处理器。该处理器也调用 call-next-handler 函数，因此我们再次重复步骤 1。由于没有剩余未调用的环绕处理器，我们继续执行步骤 2。类 B 的 msg1 前置处理器是最具体的前置处理器，因为它首先执行并允许完成。类 A 的 msg1 前置处理器是下一个最具体的处理器，因此允许其执行并返回。由于没有其他未调用的前置处理器，我们继续执行步骤 3。执行类 B 的 msg1 主消息处理器，因为这是最具体的主处理器。它不调用 call-next-handler，因此不执行类 A 的 msg1 主处理器，我们继续执行步骤 4。允许类 B 的 msg1 主消息处理器完成，并返回符号 msg1-B。所有主处理器均已执行完毕，因此我们继续执行步骤 5。与前置处理器的顺序相反，由于类 A 的 msg1 后置处理器是最不具体的后置处理器，因此允许其首先执行并返回。接下来，允许类 B 的 msg1 后置处理器执行并返回。由于没有其他未调用的后置处理器，我们继续执行步骤 6。允许类 A 的 msg1 环绕处理器完成。该处理器执行的最后一个操作是 call-next-handler 函数，因此返回值将是被调用的下一个环绕或主处理器的返回值。在此例中，返回值为 msg1-B 的是类 B 的 msg1 主处理器，因此环绕处理器的返回值相同。现在，允许类 B 的 msg1 环绕处理器完成。其最后一个操作也是调用 call-next-handler，因此其返回值是类 A 的 msg1 环绕处理器的返回值，该值为 msg1-B。由于所有环绕处理器均已完成，我们继续执行步骤 7。send 命令的最终返回值是类 B 的 msg1 环绕处理器返回的值 msg1-B。

preview-send 命令可用于显示发送到指定类实例的消息的适用处理器列表。该命令的语法是：

```
[preview-send <defclass-name> <message-name>]
```

例如，与其观察消息处理器并向实例 b1 发送 msg1 消息，不如执行以下命令：

```
CLIPS> (preview-send B msg1)
>> msg1 around in class B
| >> msg1 around in class A
| | >> msg1 before in class B
| | << msg1 before in class B
| | >> msg1 before in class A
| | << msg1 before in class A
| | >> msg1 primary in class B
| | << msg1 primary in class B
| | >> msg1 primary in class A
| | << msg1 primary in class A
| << msg1 primary in class A
<< msg1 primary in class B
| >> msg1 after in class A
| << msg1 after in class A
| >> msg1 after in class B
| << msg1 after in class B
<< msg1 around in class A
<< msg1 around in class B
CLIPS>
```

所有适用的处理器都按如果每个环绕和主处理器都调用 call-next-handler 时会被调用的顺序列出。缩进级别表示处理器调用的嵌套情况。与观察消息处理器类似，>> 和 << 符号表示处理器执行的开始和结束。垂直的 | 字符系列链接必须调用 call-next-handler 以允许超类处理器执行的处理器的执行开始和结束部分。如果你想查看给定消息和实例类的适用处理器列表，通常调用 preview-send 比观察消息处理器并实际向实例发送消息更方便。第一种方法显示可能被调用的内容，而第二种方法显示实际被调用的内容。

## 11.11 实例创建、初始化和删除消息处理器

如前所述，有几个预定义的消息处理器是从 USER 类继承的，包括 create、init 和 delete 消息处理器。create 消息处理器在创建实例时调用，但在应用任何默认值或槽覆盖之前。init 消息处理器在处理槽覆盖后调用，以将未被覆盖的任何剩余槽值设置为其默认值。delete 消息处理器要么被显式调用以删除实例，要么在你调用 make-instance 并指定已存在实例的实例名称时自动调用。通常，在定义自己的类时，不应覆盖 USER 类中定义的这些消息处理器的主处理器，但定义自己的前置和后置处理器来响应这些消息可能非常有用。

首先，让我们看看定义 init 后置处理器有用的情况。考虑以下 defclass：

```
(defclass PERSON
  (is-a USER)
  (slot first-name (type STRING)
    (access initialize-only))
  (slot middle-name (type STRING)
    (access initialize-only))
  (slot last-name (type STRING)
    (access initialize-only))
  (slot full-name (type STRING)
    (access initialize-only))))
```

在定义 PERSON defclass 时，我们设定了这样一个限制：人的姓名在创建 PERSON 实例时指定，之后不再更改。full-name 槽旨在将 first-name、middle-name 和 last-name 槽用空格连接起来。由于 full-name 槽只能在初始化时指定，我们必须在提供其他姓名的同时为其提供一个值，以使其成为适当的值：

```
CLIPS>
(make-instance [p1] of PERSON
  (first-name "John")
  (middle-name "Quincy")
  (last-name "Public")
  (full-name "John Quincy Public"))
```

