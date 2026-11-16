

```
(get-definstances-list [<module-name>])
```

返回一个包含指定模块中definstances列表的多字段值（如果未指定<module-name>，则为当前模块）。

```
(list-definstances [<module-name>])
```

列出指定模块中的definstances（如果未指定<module-name>，则为当前模块）。

```
(ppdefinstances <definstances-name>)
```

显示指定definstances的文本。

```
(undefinstances <definstances-name>)
```

删除指定的definstances。

## Defmessage-handler

```
(call-next-handler)
```

当从消息处理器内部调用时，调用被执行的消息处理器所覆盖或遮蔽的下一个消息处理器。

```
(get-defmessage-handler-class <class-name> [inherit])
```

返回一个多字段值，包含指定类的类名、处理器名称和处理器类型的三元组。如果指定了inherit，则继承的消息处理器也将包含在多字段值中。

```
(list-defmessage-handlers [<class-name> [inherit]])
```

列出当前模块中指定类的defmessage-handlers。如果未指定类，将列出当前模块中所有类的消息处理器。如果指定了inherit，也将显示继承的消息处理器。

```
(message-handler-existp <class-name> <handler-name> [<handler-type>])
```

```
<handler-type> ::= around | before | primary | after
```

如果指定的消息处理器直接为指定类定义（而非通过继承），则返回TRUE，否则返回FALSE。

```
(next-handlerp)
```

如果有另一个可执行的消息处理器，则返回TRUE，否则返回FALSE。

```
(override-next-handler <expression>*)
```

调用下一个被遮蔽的处理器，并允许更改参数。

```
(ppdefmessage-handler <class-name> <handler-name> [<handler-type>])
```

```
<handler-type> ::= around | before | primary | after
```

显示指定defmessage-handler的文本。如果未指定<handler-type>，则假定为primary。

```
(preview-send <class-name> <message-name>)
```

显示发送到指定类实例的消息的适用处理器列表。

```
(undefmessage-handler <class-name> <handler-name>
      [<handler-type>])
<handler-type> ::= around | before |
            primary | after
```

删除指定的defmessage-handler。如果未指定<handler-type>，则假定为primary。

## Defmethod

```
(call-next-method)
```

调用下一个被遮蔽的方法。

```
(call-specific-method <defgeneric-name> <method-index>
<expression>*)
```

不考虑方法优先级，调用通用函数的特定方法。

```
(get-defmethod-list {<defgeneric-name>})
```

返回一个多字段值，包含当前模块中所有方法的defgeneric名称和方法索引对。如果指定了defgeneric名称，则返回值中将仅包含属于该defgeneric的方法。

```
(get-method-restrictions <defgeneric-name>)
<method-index>
```

返回一个多字段值，包含有关指定方法的限制的信息。

```
(list-all-defmethods [<defgeneric-name>])
```

按优先级顺序列出当前模块中的所有defmethods。如果指定了defgeneric名称，则仅列出属于该defgeneric的方法。

```
(next-methodp)
```

如果从通用函数的方法中调用，当有另一个方法被当前方法遮蔽时，函数next-methodp将返回符号TRUE。否则，该函数将返回符号FALSE。

```
(override-next-method <expression>*)
```

调用下一个被遮蔽的方法，并允许提供新参数。

```
(ppdefmethod <defgeneric-name> <index>)
```

显示与指定通用函数和方法索引关联的defmethod的文本。

```
(preview-generic <generic-function-name>
<expression>*)
```

按递减优先级顺序列出特定通用函数调用的所有适用方法，但不执行它们。

```
(undefmethod <defgeneric-name> <index>)
```

删除与指定通用函数和方法索引关联的defmethod。

## Defmodule

```
(list-defmodules)
```

列出CLIPS环境中的所有defmodules。

```
(ppdefmodule <defmodule-name>)
```

显示指定defmodule的文本。

```
(set-current-module <defmodule-name>)
```

将当前模块设置为指定模块，并返回之前的当前模块。

## Defrule

```
(defrule-module <defrule-name>)
```

返回定义指定defrule的模块。

```
(get-defrule-list [<module-name>])
```

返回指定模块中所有defrules的列表（如果未指定<module-name>，则为当前模块）。

```
(get-incremental-reset)
```

返回增量重置行为的当前值。

```
(list-defrules [<module-name>])
```

列出指定模块中的defrules（如果未指定<module-name>，则为当前模块）。

```
(matches <defrule-name>)
```

显示与指定规则模式匹配的事实和部分匹配列表。

```
(ppdefrule <defrule-name>)
```

显示指定defrule的文本。

```
(refresh <defrule-name>)
```

刷新指定的defrule。对于规则的已触发但仍然有效的激活，将其放置在议程上。

```
(remove-break [<defrule-name>])
```

删除指定规则的断点。如果未指定规则，则删除所有断点。

```
(set-break <defrule-name>)
```

为指定规则设置断点。这将导致规则在触发前停止执行。

```
(set-incremental-reset <boolean-expression>)
```

设置增量重置行为。

```
(show-breaks [<module-name>])
```

列出指定模块中设置了断点的规则（如果未指定<module-name>，则为当前模块）。

```
(undefrule <defrule-name>)
```

删除指定的defrule。

## Deftemplate

```
(deftemplate-module <deftemplate-name>)
```

返回定义指定deftemplate的模块。

```
(get-deftemplate-list [<module-name>])
```

返回指定模块中所有deftemplates的列表（如果未指定<module-name>，则为当前模块）。

```
(list-deftemplates [<module-name>])
```

列出指定模块中的deftemplates（如果`<module-name>`未指定，则为当前模块）。

```
(ppdeftemplate <deftemplate-name>)
```

显示指定deftemplate的文本。

```
(undeftemplate <deftemplate-name>)
```

删除指定的deftemplate。

## Environment

```
(apropos <lexeme>)
```

显示CLIPS环境中当前定义的所有包含指定子字符串`<lexeme>`的符号。

```
(batch <file-name>)
```

通过用文件`<file-name>`的内容替换标准输入，允许对CLIPS交互命令进行“批处理”。如果文件成功执行，则返回TRUE，否则返回FALSE。

```
(batch* <file-name>)
```

从文件执行命令。与`batch`命令不同，它在返回前评估指定文件中的所有命令，而不是替换标准输入。

```
(bload <file-name>)
```

从文件加载二进制映像。如果文件成功加载，则返回TRUE，否则返回FALSE。

```
(bsave <file-name>)
```

将二进制映像保存到文件。

```
(clear)
```

从CLIPS环境中删除所有构造。

```
(exit)
```

退出CLIPS环境。

```
(get-auto-float-dividend)
```

返回自动浮点数股息行为的当前值。

```
(get-dynamic-constraint-checking)
```

返回动态约束检查行为的当前值。

```
(get-static-constraint-checking)
```

返回静态约束检查行为的当前值。

```
(load <file-name>)
```

将由`<file-name>`指定的文件中存储的构造加载到CLIPS环境中。如果文件成功加载，则返回TRUE，否则返回FALSE。

```
(load* <file-name>)
```

将由`<file-name>`指定的文件中存储的构造连同信息性消息一起加载到CLIPS环境中。如果文件成功加载，则返回TRUE，否则返回FALSE。

```
(options)
```

列出CLIPS编译器标志的设置。

```
(reset)
```

重置CLIPS环境。

