
# declaration-declaration-list member-declaration

### (6.7.3.2) 成员声明:
`attribute-specifier-sequence_opt` `specifier-qualifier-list` `member-declarator-list_opt` ;

`static_assert-declaration`

### (6.7.3.2) 说明符限定符列表:
`type-specifier-qualifier` `attribute-specifier-sequence_opt`

`type-specifier-qualifier` `specifier-qualifier-list`

### (6.7.3.2) 类型说明符限定符:
`type-specifier`

`type-qualifier`

`alignment-specifier`

### (6.7.3.2) 成员声明符列表:
`member-declarator`

`member-declarator-list` , `member-declarator`

### (6.7.3.2) 成员说明符:
`declarator`

`declarator_opt` : `constant-expression`

### (6.7.3.3) 枚举说明符:
```
enum attribute-specifier-sequence_opt identifier_opt enum-type-specifier_opt
  { enumerator-list }
  enum attribute-specifier-sequence_opt identifier_opt enum-type-specifier_opt
  { enumerator-list , }
  enum enumerator list enum-type-specifier_opt
```

### (6.7.3.3) 枚举成员列表:
`enumerator`

`enumerator-list` , `enumerator`

### (6.7.3.3) 枚举成员:
`enumeration-constant` `attribute-specifier-sequence_opt`

`enumeration-constant` `attribute-specifier-sequence_opt` = `constant-expression`

  : `specifier-qualifier-list`

### (6.7.3.5) 原子类型说明符:
`_Atomic` ( `type-name` )

### (6.7.3.6) 类型说明符:
`type` (`type-specifier-argument`)

`type_unqual` (`type-specifier-argument`)

`type-specifier-argument`:
`expression`

`type-name`

### (6.7.4.1) 类型限定符:
`const`

`restrict`

`volatile`

`_Atomic`

### (6.7.5) 函数说明符:
`inline`

`return`

### (6.7.6) 对齐说明符:
`alignas` ( `type-name` )

`alignas` ( `constant-expression` )

### (6.7.7.1) 声明符:
`pointer_opt` `direct-declarator`

### (6.7.7.1) 直接声明符:
`identifier` `attribute-specifier-sequence_opt`

  { `declarator` }

`array-declarator` `attribute-specifier-sequence_opt`

`function-declarator` `attribute-specifier-sequence_opt`

```
(6.7.7.1) 数组声明符:
direct-declarator [ type-qualifier-list_opt assignment-expression_opt ]
direct-declarator [ static type-qualifier-list_opt assignment-expression ]
direct-declarator [ type-qualifier-list static assignment-expression ]
direct-declarator [ type-qualifier-list_opt * ]
```

### (6.7.7.1) 函数声明符:
`direct-declarator_opt` ( `parameter-type-list_opt` )

### (6.7.7.1) 指针:
* `attribute-specifier-sequence_opt` `type-qualifier-list_opt`

* `attribute-specifier-sequence_opt` `type-qualifier-list`

### (6.7.7.1) 类型限定符列表:
`type-qualifier`

`type-qualifier-list` `type-qualifier`

### (6.7.7.1) 参数类型:
`parameter-list`

`parameter-list` , ...

### (6.7.7.1) 参数列表:
`parameter-declaration`

`parameter-list` , `parameter-declaration`

### (6.7.7.1) 参数声明:
`attribute-specifier-sequence_opt` `declarator`

`attribute-specifier-sequence_opt` `abstract-declarator_opt`

### (6.7.8) 类型-name:
`specifier-qualifier-list` `abstract-declarator_opt`

### (6.7.8) 抽象声明符:
`pointer`

`pointer_opt` `direct-declarator`

### (6.7.8) 直接声明符:
{ `abstract-declarator` }

`array-abstract-declarator` `attribute-specifier-sequence_opt`

`function-declarator` `attribute-specifier-sequence_opt`

### (6.7.8) 数组声明符:
`direct-declarator_opt` [ `type-qualifier-list_opt` `assignment-expression_opt` ]

`direct-declarator_opt` [ `static` `type-qualifier-list_opt` `assignment-expression` ]

`direct-declarator_opt` [ `type-qualifier-list` `static` `assignment-expression` ]

`direct-declarator_opt` [ * ]

### (6.7.8) 函数声明符:
`direct-declarator_opt` ( `parameter-type-list_opt` )

### (6.7.9) typedef-name:
`identifier`

### (6.7.11) 括号初始化:
{
{ `initializer-list` }
{ `initializer-list` , }
}

### (6.7.11) 初始化:
`assignment-expression`

`braced-initializer`

### (6.7.11) 初始化列表:
`designation_opt` `initializer`

`initializer-list` , `designation_opt` `initializer`

### (6.7.11) 标记:
`designator-list` =

### (6.7.11) 声明符列表:
`designator`

`designator` `designator`

### (6.7.11) 声明符:
+   [ `constant-expression` ]

- `identifier`

### (6.7.12) 静态断言声明:
`static_assert` ( `constant-expression` , `string-literal` ) ;

`static_assert` ( `constant-expression` );

### (6.7.13.2) 属性说明符序列:
`attribute-specifier-sequence_opt` `attribute-specifier`

### (6.7.13.2) 属性说明符:
[ `attribute-list` ]

### (6.7.13.2) 属性列表:
`attribute_opt`

`attribute-list` , `attribute_opt`

### (6.7.13.2) 属性:
`attribute-token` `attribute-argument-clause_opt`

### (6.7.13.2) 标记:
`standard-attribute`

`attribute-prefixed-token`

### (6.7.13.2) 标准属性:
`identifier`

### (6.7.13.2) 属性前缀标记:
`attribute-prefixed-prefix` :: `identifier`

### (6.7.13.2) 属性前缀:
`identifier`

### (6.7.13.2) 属性参数子:
{ `balanced-token-sequence_opt` }

### (6.7.13.2) 平衡标记序列:
`balanced-token`

`balanced-token-sequence` `balanced-token`

### (6.7.13.2) 平衡标记:
{ `balanced-token-sequence_opt` }

{ `balanced-token-sequence_opt` }

除圆括号、中括号或大括号外的任何标记

## A.3.3 语句

### (6.8.1) 语句:
`labeled-statement`

`unlabeled-statement`

### (6.8.1) 未标记语句:
`expression-statement`

`attribute-specifier-sequence_opt` `primary-block`

`attribute-specifier-sequence_opt` `jump-statement`

### (6.8.1) 主块:
`compound-statement`

`selection-statement`

`iteration-statement`

### (6.8.1) 次级块:
`statement`

### (6.8.2) 标记:
`attribute-specifier-sequence_opt` `identifier` :

`attribute-specifier-sequence_opt` `case` `constant-expression` :

`attribute-specifier-sequence_opt` `default` :

### (6.8.2) 标记语句:
`label` `statement`:

### (6.8.3) 复合语句:
{ `block-item-list` }

### (6.8.3) 块项列表:
`block-item`

`block-item-list` `block-item`

### (6.8.4) 表达式语句:
`expression_opt` ;

`attribute-specifier-sequence_opt` ;

### (6.8.5.1) 选择语句:
`if` ( `expression` ) `secondary-block`

`if` ( `expression` ) `secondary-block` `else` `secondary-block`

`switch` ( `expression` ) `secondary-block`

### (6.8.6.1) 迭代语句:
`while` ( `expression` ) `secondary-block`

`do` `secondary-block` `while` ( `expression` )

`for` ( `expression_opt` ; `expression_opt` ; `expression_opt` ) `secondary-block`

`for` ( `declaration` `expression_opt` ; `expression_opt` ) `secondary-block`

### (6.8.7.1) 跳转语句:
`goto` `identifier`;

`continue` ;

`break`;

`return` `expression_opt` ;

## A.3.4 外部定义

### (6.9.1) 翻译单元:
`external-declaration`

`translation-unit` `external-declaration`

### (6.9.1) 外部声明:
`function-definition`

`declaration`

### (6.9.2) 函数定义:
`attribute-specifier-sequence_opt` `declaration-specifiers` `declarator` `function-body`

### (6.9.2) 函数体:
`compound-statement`

## A. 预处理指令

### (6.10.1) 预处理文件:
`group_opt`

### (6.10.1) 组:
`group-part`

`group-part`

# ISO/IEC 9899:2024(en)

### (6.10.1) 组-part:
`if-section`

`control-line`

`text-line`

# 非指令性

### (6.10.1) if-section:
`if-group` `elif-groups_opt` `new-line` `else-group_opt` `endif-line`

### (6.10.1) if-group:
```
# if constant-expression new-line group_opt
# ifdef identifier new-line group_opt
# endif identifier new-line group_opt
```

### (6.10.1) elif-groups:
`elif-group`

`elif-groups` `elif-group`

### (6.10.1) elif-group:
```
# elif constant-expression new-line group_opt
# elif identifier new-line group_opt
# endif identifier new-line group_opt
```

### (6.10.1) else-group:
# else new-line group_opt

### (6.10.1) endif-group:
```
# endif new-line
```

### (6.10.1) control-line:
```
# include pp-tokens new-line
# embed pp-tokens new-line
# define identifier replacement-list new-line
# define identifier paren identifier-list_opt ... replacement-list new-line
# define identifier paren replacement-list new-line
# define identifier paren identifier-list_opt , ... ) replacement-list new-line
# undef identifier new-line
# line pp-tokens new-line
# error pp-tokens_opt new-line
# warning pp-tokens_opt new-line
# pragma pp-tokens_opt new-line
# new-line
```

### (6.10.1) text-line:
`pp-tokens_opt` `new-line`

### (6.10.1) 非指令性:
`pp-tokens` `new-line`

### (6.10.1) 左括号:
a ( 且前面没有紧跟空白字符

### (6.10.1) replacement-list:
`pp-tokens_opt`

### (6.10.1) pp-tokens:
`preprocessing-token`

`pp-tokens` `preprocessing-token`

### (6.10.1) new-line:
换行字符

### (6.10.1) identifier-list:
`identifier`

`identifier-list` , `identifier`

© ISO/IEC 2024 — 版权所有

### (6.10.1) pp-parameter:
`pp-parameter-name` `pp-parameter-clause_opt`

### (6.10.1) pp-parameter-name:
`pp-standard-parameter`

`pp-prefixed-parameter`

### (6.10.1) pp-prefixed-parameter:
`identifier`

### (6.10.1) pp-prefixed-parameter:
`identifier` :: `identifier`

### (6.10.1) pp-parameter-clause:
( `pp-balanced-token-sequence_opt`

### (6.10.1) pp-balanced-token-sequence:
`pp-balanced-token`

`pp-balanced-token-sequence` `pp-balanced-token`

### (6.10.1) pp-balanced-token:
( `pp-balanced-token-sequence_opt`

{ `pp-balanced-token-sequence_opt` }

{ `pp-balanced-token-sequence_opt` }

除括号、中括号或大括号以外的任何 pp-token

### (6.10.1) embed-parameter-sequence:
`pp-parameter`

`embed-parameter-sequence` `pp-parameter`

`defined-macro-expression`:
`defined` `identifier`

`defined` ( `identifier` )

`h-preprocessing-tokens`:
除 > 以外的任何 preprocessing-token

`h-pp-tokens`:
