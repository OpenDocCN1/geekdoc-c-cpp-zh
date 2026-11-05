
## 12.8.8 空条件成员访问

null_conditional_member_access 是一个条件版本的 member_access (§12.8.7)，如果结果类型为 void，则为绑定时错误。对于结果类型可能为 void 的空条件表达式，请参见 (§12.8.10)。

null_conditional_member_access 由 primary_expression 组成，后跟两个标记 “?” 和 “.”，后跟一个带有可选 type_argument_list 的标识符，后跟零个或多个 dependent_accesses。

```
null_conditional_member_access
  : primary_expression '?' '.' identifier type_argument_list?
    dependent_access*
  ;

dependent_access
  : '.' identifier type_argument_list?   // member access
  | '[' argument_list ']'                // element access
  | '(' argument_list? ')'               // invocation
  ;

null_conditional_projection_initializer
  : primary_expression '?' '.' identifier type_argument_list?
  ;
```

null_conditional_member_access 表达式 E 的形式为 P?.A。其含义确定如下：

- 如果 P 的类型为可空值类型：
  - 设 T 为 P.Value.A 的类型。
  - 如果 T 是类型参数且无法确定为引用类型或非可空值类型，则发生编译时错误。
  - 如果 T 是非可空值类型，则 E 的类型为 T?，且 E 的含义与以下含义相同：
    ((object)P == null) ? (T?)null : P.Value.A
    除非 P 仅被求值一次。
  - 否则 E 的类型为 T，且 E 的含义与以下含义相同：
    ((object)P == null) ? (T)null : P.Value.A
    除非 P 仅被求值一次。
- 否则：
  - 设 T 为表达式 P.A 的类型。
  - 如果 T 是类型参数且无法确定为引用类型或非可空值类型，则发生编译时错误。
  - 如果 T 是非可空值类型，则 E 的类型为 T?，且 E 的含义与以下含义相同：
    ((object)P == null) ? (T?)null : P.A
    除非 P 仅被求值一次。

否则 E 的类型为 T，且 E 的含义与以下含义相同：

```
((object)P == null) ? (T)null : P.A
```

除非 P 仅被求值一次。

注意：在形式为：

```
P?.A₀?.A₁
```

则如果 P 求值为 null，则 A₀ 和 A₁ 都不会被求值。如果表达式是 null_conditional_member_access 或 null_conditional_element_access §12.8.12 操作的序列，则同样适用。

结束注意

null_conditional_projection_initializer 是 null_conditional_member_access 的限制，具有相同的语义。它仅作为匿名对象创建表达式 (§12.8.16.7) 中的投影初始化器出现。

## 12.8.9 调用表达式

### 12.8.9.1 通用

invocation_expression 用于调用方法。

```
invocation_expression
: primary_expression '(' argument_list? ')'
;
```

invocation_expression 在以下任一条件成立时为动态绑定 (§12.3.3)：

- primary_expression 的编译时类型为 dynamic。
- 可选 argument_list 的至少一个参数的编译时类型为 dynamic。

在这种情况下，编译器将 invocation_expression 分类为类型为 dynamic 的值。随后用于确定 invocation_expression 含义的规则将在运行时应用，使用运行时类型代替具有编译时类型 dynamic 的 primary_expression 和参数的编译时类型。如果 primary_expression 没有编译时类型 dynamic，则方法调用将进行如 §12.6.5 中所述的有限编译时检查。

invocation_expression 的 primary_expression 必须是一个方法组或 delegate_type 的值。如果 primary_expression 是方法组，则 invocation_expression 为方法调用 (§12.8.9.2)。如果 primary_expression 是 delegate_type 的值，则 invocation_expression 为委托调用 (§12.8.9.4)。如果 primary_expression 既不是方法组也不是 delegate_type 的值，则发生绑定时错误。

可选的 argument_list (§12.6.2) 为方法参数提供值或变量引用。

求值 invocation_expression 的结果分类如下：

- 如果 invocation_expression 调用 returns-no-value 方法 (§15.6.1) 或 returns-no-value 委托，则结果为 nothing。被分类为 nothing 的表达式仅允许在 statement_expression (§13.7) 的上下文中或作为 lambda_expression (§12.19) 的主体出现。否则，发生绑定时错误。
- 否则，如果 invocation_expression 调用 returns-by-ref 方法 (§15.6.1) 或 returns-by-ref 委托，则结果是一个变量，其关联类型为方法或委托的返回类型。如果调用的是实例方法，且接收者为类类型 T，则关联类型取自从 T 开始并搜索其基类时找到的方法的第一个声明或重写。
- 否则，invocation_expression 调用 returns-by-value 方法 (§15.6.1) 或 returns-by-value 委托，结果为一个值，其关联类型为方法或委托的返回类型。如果调用的是实例方法，且接收者为类类型 T，则关联类型取自从 T 开始并搜索其基类时找到的方法的第一个声明或重写。

### 12.8.9.2 方法调用

对于方法调用，invocation_expression 的 primary_expression 必须是一个方法组。方法组标识要调用的单个方法，或从中选择特定方法调用的重载方法集合。在后一种情况下，要调用的具体方法的确定基于 argument_list 中参数类型提供的上下文。

形式为 M(A) 的方法调用的绑定时处理，其中 M 是方法组（可能包括 type_argument_list），A 是可选 argument_list，由以下步骤组成：

- 构造方法调用的候选方法集合。对于与方法组 M 关联的每个方法 F：
  - 如果 F 是非泛型的，则当满足以下条件时 F 为候选：
    - M 没有类型参数列表，且
    - F 相对于 A 是适用的 (§12.6.4.2)。
  - 如果 F 是泛型的且 M 没有类型参数列表，则当满足以下条件时 F 为候选：
    - 类型推断 (§12.6.3) 成功，推断出调用的类型参数列表，且
    - 一旦将推断出的类型参数替换为相应的方法类型参数，F 的参数列表中的所有构造类型均满足其约束 (§8.4.5)，且 F 的参数列表相对于 A 是适用的 (§12.6.4.2)
  - 如果 F 是泛型的且 M 包含类型参数列表，则当满足以下条件时 F 为候选：
    - F 的方法类型参数数量与类型参数列表中提供的数量相同，且
    - 一旦将类型参数替换为相应的方法类型参数，F 的参数列表中的所有构造类型均满足其约束 (§8.4.5)，且 F 的参数列表相对于 A 是适用的 (§12.6.4.2)。
- 候选方法集合被缩减为仅包含来自最派生类型的 方法：对于集合中的每个方法 C.F，其中 C 是声明方法 F 的类型，所有在 C 的基类型中声明的方法都从集合中移除。此外，如果 C 是 object 以外的类类型，则所有在接口类型中声明的方法都从集合中移除。注意：此后一条规则仅在方法组是针对具有除 object 以外的有效基类且非空有效接口集合的类型参数进行的成员查找结果时才有效。结束注意
- 如果得到的候选方法集合为空，则放弃后续步骤的处理，而是尝试将调用作为扩展方法调用 (§12.8.9.3) 处理。如果失败，则不存在适用的方法，并发生绑定时错误。
