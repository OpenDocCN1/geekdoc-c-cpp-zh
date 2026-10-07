
# ISO/IEC 14882:2011(E)

## 预处理标记 `preprocessing-token`
- `header-name`
- `identifier`
- `pp-number`
- `character-literal`
- `user-defined-character-literal`
- `string-literal`
- `user-defined-string-literal`
- `preprocessing-op-or-unc`

每个不属于以下之一的非空白字符：

## 标记元 `token`
- `identifier`
- `keyword`
- `literal`
- `operator`
- `punctuator`

## 头文件名称 `header-name`
- `< h-char-sequence>`
- `" q-char-sequence "`

### h-字符序列 `h-char-sequence`
- `h-char`
- `h-char-sequence h-char`

### h-字符 `h-char`
源字符集中除换行和 `>` 以外的任何成员

### q-字符序列 `q-char-sequence`
- `q-char`
- `q-char-sequence q-char`

### q-字符 `q-char`
源字符集中除换行和 `"` 以外的任何成员

## 预处理数字 `pp-number`
- `digit`
- `. digit`
- `pp-number digit`
- `p-number identifier-nondigit`
- `p-number e sign`
- `p-number E sign`
- `pp-number .`

## 标识符 `identifier`
- `identifier-nondigit`
- `identifier identifier-nondigit`
- `digit`
- `identifier-nondigit`

### 标识符-非数字标识符 `identifier-nondigit`
- 非数字字符 `nondigit`
- 统一字符名称 `uniform-character-name`
- 其他由实现定义的字符

### 非数字字符 `nondigit`
范围之一
`a b c d e f g h i j k l m`
`o p q r s t u v w x y z`
`A B C D E F G H I J K L M`
`O P Q R S T U V W X Y Z =`

### 数字 `digit`
范围之一
`0 1 2 3 4 5 6 7 8 9`

# A.2

## 预处理运算符或标点符号 `preprocessing-op-or-punc`

| `+` | `<` | `#` | `##` | `( )` | |
|---|---|---|---|---|---|
| `{ }` | `[ ]` | `%` | `%: ` | | |
| `<:` | `>` | `%<` | ` %>` | `%:::` | `...` |
| `new delete ?` | `::` | | | | |
| `*` | `/` | `*.*` | | | `-` |
| `!` | | `++` | `-=` | `|=` | `|=` | `*=` | `/=` | `|=` | |
| `=` | `&=` | `=` | `<<` | `>>` | `>=` | `<=` | `=` | `!=` | | |
| `=` | `>` | `&&` | `||` | `-` | `->*` | |
| `and and and_eq bitand bitor compl not not not_eq` | | | | | |

## 整数字面量 `integer-literal`
- `character-literal`
- `floating-literal`
- `string-literal`
- `boolean-literal`
- `pointer-literal`
- `user-defined-literal`

### 整数字面量 `integer-literal`
- `decimal-literal` `integer-suffix_opt`
- `octal-literal` `integer-suffix_opt`
- `hexadecimal-literal` `integer-suffix_opt`

### 十进制字面量 `decimal-literal`
- 非零数字 `nonzero-digit`
- 十进制数字 `decimal-digit`

### 八进制字面量 `octal-literal`
- `0`
- `octal-octal-digit`

### 十六进制字面量 `hexadecimal-literal`
- `0x hexadecimal-digit`
- `0X hexadecimal-digit`
- `hexadecimal-literal hexadecimal-digit`

### 非零数字 `nonzero-digit`
范围之一
`1 2 3 4 5 6 7 8 9`

### 八进制数字 `octal-digit`
范围之一
`0 1 2 3 4 5 6 7`

### 十进制数字 `decimal-digit`
范围之一
`0 1 2 3 4 5 6 7 8 9`
`a b c d e f`

### 整数字面量后缀
- 无符号后缀 `unsigned-suffix` `long-suffix_opt`
- 有符号后缀 `signed-suffix` `long-suffix_opt`
- 后缀-后缀 `suffix-suffix` `unsigned-suffix_opt`
- 长长后缀 `long-long-suffix` `unsigned-suffix_opt`

### 无符号后缀 `unsigned-suffix`
范围之一
`u`
`1 L`

### 长长后缀 `long-long-suffix`
范围之一
`11 LL`

§ A.2

# ISO/IEC 14882:2011(E)

## 字符字面量 `character-literal`

```
' c-char-sequence \
u' c-char-sequence \
U' c-char-sequence \
L' c-char-sequence \
```

### c-字符序列 `c-char-sequence`
- `c-char`
- `c-char-sequence c-char`

### c-字符 `c-char`
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行
转义序列 `escape-sequence`:
通用字符名称 `universal-character-name`

### 转义序列 `escape-sequence`
- 简单转义序列 `simple-escape-sequence`
- 八进制转义序列 `octal-escape-sequence`
- 十六进制转义序列 `hexadecimal-escape-sequence`

### 简单转义序列 `simple-escape-sequence`
范围之一
`'\'' '\b' '\f' '\r' '\t' '\v'`

### 八进制转义序列 `octal-escape-sequence`
- `octal-digit`
- `octal-digit octal-digit`
- `octal-digit octal-digit`

### 十六进制转义序列 `hexadecimal-escape-sequence`
- `\ hexadecimal-digit`
- `hexadecimal-escape-sequence hexadecimal-digit`

## 浮点字面量 `floating-literal`
- `fractional-constant exponent-part floating-suffix_opt`
- `digit-sequence exponent-part floating-suffix_opt`

### 分数常数 `fractional-constant`
- `digit-sequence_opt , digit-sequence`
- `digit-sequence , exponent-part :`
- `e suffix_opt digit-sequence`
- `E suffix_opt digit-sequence`

### 符号 `sign`
范围之一
`+`

### 数字序列 `digit-sequence`
- `digit`
- `digit-sequence digit`

### 浮点后缀 `floating-suffix`
范围之一
`f F L`

## 字符串字面量 `string-literal`
- `encoding-prefix_opt " s-char-sequence_opt"`
- `encoding-prefix_opt R raw-string`

### 编码前缀 `encoding-prefix`
- `uS`
- `U`
- `L`

§ A.2

# ISO/IEC 14882:2011(E)

## s-字符序列 `s-char-sequence`
- `s-char`
- `s-char-sequence s-char`

## s-字符 `s-char`
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

## s-字符 `s-char`
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行
序列:
通用字符名称 `universal-character-name`

## s-序列 `s-char-sequence`
- `s-char`
- `s-char-sequence s-char`

## s-字符 `s-char`
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

## 异或表达式
`and-expression =`
`exclusive-or-expression ^ and-expression`

## 包含或表达式
`exclusive-or-expression`
`inclusive-or-expression | exclusive-or-expression`

## 逻辑与表达式
`inclusive-or-expression`
`logical-and-expression && inclusive-or-expression`

## 逻辑或表达式
`logical-or-expression`
`logical-or-expression || logical-and-expression`

## 条件表达式
`logical-or-expression`
`logical-or-expression ? expression : assignment-statement`

## 赋值表达式
`conditional-expression`
`logical-or-expression assignment-operator-initializer-clause`

## 抛出表达式
`assignment-operator:` 选之一
`* = / % != = => => >> << &= = =`

## 表达式
`assignment-expression`
`expression , assignment-`

## 常量表达式
`conditional-expression`

## A.5 语句

`gram.stmt`

### 语句
- `labeled-statement`
- `attribute-specifier-seq_01 expression-statement`
- `attribute-specifier-seq_02 compound-statement`
- `attribute-specifier-seq_03 selection-statement`
- `attribute-specifier-seq_04 iteration-statement`
- `attribute-specifier-seq_05 jump-statement`
- `declaration-statement`
- `attribute-specifier-seq_06 try-block`

### 标记语句
- `attribute-specifier-seq_07 identifier : statement`
- `attribute-specifier-seq_08 case constant-expression : statement`
- `attribute-specifier-seq_09 default : statement`

### 表达式语句
`expression_opt;`

### 复合语句
`{ statement-seq_01 }`

### 语句序列
- `statement`
- `statement-seq statement`

## ISO/IEC 14882:2011(E)

```
selection-statement:
  if ( condition ) statement
  if ( condition ) statement else statement
  switch ( condition ) statement
```

```
condition:
  expression
  attribute-specifier-seq_opt decl-specifier-seq-declarator = initializer-clause
  attribute-specifier-seq_opt decl-specifier-seq-declarator braced-init-list
```

```
iteration-statement:
  while ( condition ) statement
  do while ( expression );
  for ( (for-init-statement condition_opt; expression_opt ) statement
  for ( (for-range-declaration : for-range-initializer ) statement
```

```
for-statement:
  expression
  simple-declaration
```

```
for-range-declaration:
  attribute-specifier-seq_opt decl-specifier-seq-declarator
```

```
for-range-initializer:
  expression
  braced-init-list
```

```
jump-statement:
  break;
  continue;
  return expression_opt;
  return braced-init-list;
  goto identifier;
```

```
declaration-statement:
  block-declaration
```

## A.6 声明

`gram.dcl`

```
declaration-seq:
  declaration
  declaration-seq declaration
```

```
declaration:
  block-declaration
  function-definition
  template-declaration
  explicit-instantiation
  explicit-specialization
  linkage-specification
  namespace-definition
  empty-declaration
  contribution-declaration
```

## ISO/IEC 14882:2011(E)

```
block-declaration:
  simple-declaration
  asm-definition
  namespace-alias-definition
  using-directive
  static_assert-declaration
  alias-declaration
  opaque-enum-declaration
```

```
alias-declaration:
  identifier attribute-specifier-seq_opt = type;
```

```
simple-declaration:
  decl-specifier-seq_opt init-declarator-list_opt
  attribute-specifier-seq decl-specifier-seq_opt init-declarator-list;
```

```
static_assert-declaration:
  static ( constant-expression, string-literal );
```

```
empty-declaration:
  ;
```

```
attribute-declaration:
  attribute-specifier-seq;
```

```
decl-specifier:
  storage-class-class-specifier
```
