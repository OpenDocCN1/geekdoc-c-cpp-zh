
(log <numeric-expression>)
返回其参数的以 e 为底的对数。

(log10 <numeric-expression>)
返回其参数的以 10 为底的对数。

(mod <numeric-expression> <numeric-expression>)
返回将第一个参数除以第二个参数的结果的余数。

(pi)
返回 π 的值。

(rad-deg <numeric-expression>)
返回将其参数从弧度单位转换为角度单位后的值。

(round <numeric-expression>)
返回其参数四舍五入到最接近的整数后的值。

(sqrt <numeric-expression>)
返回其参数的平方根。

(** <numeric-expression> <numeric-expression>)
返回其第一个参数的第二个参数次幂后的值。

## 调试

(dribble-off)
停止将输出发送到由 dribble-on 函数打开的跟踪文件。如果跟踪文件成功关闭，则返回 TRUE，否则返回 FALSE。

(dribble-on <file-name>)
将通常发送到屏幕的所有输出发送到跟踪文件 <file-name>。如果跟踪文件成功打开，则返回 TRUE，否则返回 FALSE。

(list-watch-items)
显示监视项的当前状态。

(unwatch <watch-item>)
禁用在发生某些 CLIPS 操作时显示信息性消息。

(watch <watch-item>)
<watch-item> ::= activations | all | compilations | deffunctions | facts | focus | generic-functions | globals | instances | message | message-handlers | methods | rules | slots | statistics
启用在发生某些 CLIPS 操作时显示信息性消息。

## Defclass

(browse-classes [<class-name>])
显示指定类及其子类之间的继承关系。如果未指定类，<class-name> 默认为 OBJECT。

(class-abstractp <class-name>)
如果指定的类是抽象类，则返回 TRUE，否则返回 FALSE。

(class-existp <class-name>)
如果指定的类已定义，则返回 TRUE，否则返回 FALSE。

(class-reactivep <class-name>)
如果指定的类是响应式的，则返回 TRUE，否则返回 FALSE。

(class-slots <class-name> [inherit])
在多字段值中返回类的显式定义的槽名称。如果使用可选的 inherit 关键字，还包括继承的槽。

(class-subclasses <class-name> [inherit])
在多字段值中返回类的直接子类名称。如果使用可选的 inherit 关键字，还包括间接超类。

(class-superclasses <class-name> [inherit])
在多字段值中返回类的直接超类名称。如果使用可选的 inherit 关键字，还包括间接超类。

(defclass-module <class-name>)
返回指定的 defclass 定义所在的模块。

(describe-classes [<class-name>])
提供类的详细描述。

(get-class-defaults-mode)
返回定义类时使用的当前默认模式。

(get-defclass-list [<module-name>])
返回一个多字段值，包含指定模块中的类列表（如果未指定 <module-name>，则为当前模块）。

(list-defclasses [<module-name>])
列出指定模块中的类（如果未指定 <module-name>，则为当前模块）。

(ppdefclass <class-name>)
显示指定的 definstances 的文本。

(set-class-defaults-mode convenience | conservation)
设置定义类时使用的默认模式。

(slot-allowed-values <class-name> <slot-name>)
在多字段值中返回槽的允许值。

(slot-cardinality <class-name> <slot-name>)
在多字段值中返回多槽允许的最小和最大字段数。

(slot-default-value <class-name> <slot-name>)
返回与槽关联的默认值。

(slot-direct-accessp <class-name> <slot-name>)
如果指定的槽可以直接访问，则返回 TRUE，否则返回 FALSE。

(slot-existp <class-name> <slot-name> [inherit])
如果指定的槽存在于类中，则返回 TRUE，否则返回 FALSE。如果指定了 inherit 关键字，则该槽可能是继承的。

(slot-facets <class-name> <slot-name>)
在多字段值中返回类指定槽的方面值。

(slot-initablep <class-name> <slot-name>)
如果指定的槽可初始化，则返回 TRUE，否则返回 FALSE。

(slot-publicp <class-name> <slot-name>)
如果指定的槽是公共的，则返回 TRUE，否则返回 FALSE。

(slot-range <class-name> <slot-name>)
在多字段值中返回槽允许的最小和最大数值。

(slot-sources <class-name> <slot-name>)
在多字段值中返回为指定类的指定槽提供方面的类名称。

(slot-types <class-name> <slot-name>)
在多字段值中返回指定类的指定槽允许的原始类型名称。

(slot-writablep <class-name> <slot-name>)
如果指定的槽可写，则返回 TRUE，否则返回 FALSE。

(subclassp <class1-name> <class2-name>)
如果第一个类是第二个类的子类，则返回 TRUE。

(superclassp <class1-name> <class2-name>)
如果第一个类是第二个类的超类，则返回 TRUE。

(undefclass <class-name>)
删除指定的类。

## Defacts

(defacts-module <defacts-name>)
返回指定的 defacts 定义所在的模块。

(get-defacts-list [<module-name>])
返回指定模块中所有 defacts 的列表（如果未指定 <module-name>，则为当前模块）。

(list-defacts [<module-name>])
列出指定模块中的 defacts（如果未指定 <module-name>，则为当前模块）。

(ppdefacts <defacts-name>)
显示指定的 defacts 的文本。

(undefacts <defacts-name>)
删除指定的 defacts。

## Defgeneric

(defgeneric-module <defgeneric-name>)
返回指定的 defgeneric 定义所在的模块。

(get-defgeneric-list [<module-name>])
返回一个多字段值，包含指定模块中的 defgenerics 列表（如果未指定 <module-name>，则为当前模块）。

(list-defgenerics [<module-name>])
列出指定模块中的 defgenerics（如果未指定 <module-name>，则为当前模块）。

(ppdefgeneric <defgeneric-name>)
显示指定的 defgeneric 的文本。

(preview-generic <generic-function-name> <expression>*)
按降序优先级列出特定泛型函数调用的所有适用方法，但不执行它们。

(type <expression>)
返回一个符号，即其参数的类型（或类）的名称。

(undefgeneric <defgeneric-name>)
删除指定的 defgeneric 及其所有方法。

## Defglobal

(defglobal-module <defglobal-name>)
返回指定的 defglobal 定义所在的模块。

(get-defglobal-list [<module-name>])
返回一个多字段值，包含指定模块中的 defglobals 列表（如果未指定 <module-name>，则为当前模块）。

(get-reset-globals)
返回重置全局变量行为的当前值（TRUE 或 FALSE）。

(list-defglobals [<module-name>])
列出指定模块中的 defglobals（如果未指定 <module-name>，则为当前模块）。

(ppdefglobal <defglobal-name>)
显示指定的 defglobal 的文本。

(set-reset-globals <boolean-expression>)
设置重置全局变量行为。启用此行为后（默认为 TRUE），执行 reset 命令时全局变量将重置为其原始值。

(show-defglobals [<module-name>])
列出指定模块中的 defglobals 及其当前值（如果未指定 <module-name>，则为当前模块）。

(undefglobal <defglobal-name>)
删除指定的 defglobal。

## Definstances

(definstances-module <definstances-name>)
返回指定的 definstances 定义所在的模块。
