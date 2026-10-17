
# ISO/IEC 14882:2011(E)

## 预处理标记元 (preprocessing-token)
- `header-name`
- `identifier`
- `pp-number`
- `character-literal`
- `user-defined-character-literal`
- `string-literal`
- `user-defined-string-literal`
- `preprocessing-op-or-unc`

每个不属于以下之一的非空白字符：

## 标记元 (token)
- `identifier`
- `keyword`
- `literal`
- `operator`
- `punctuator`

## 头文件名称 (header-name)
- `< h-char-sequence>`
- `" q-char-sequence "`

### h-字符序列 (h-char-sequence)
- `h-char`
- `h-char-sequence h-char`

### h-字符 (h-char)
源字符集中除换行和 `>` 以外的任何成员

### q-字符序列 (q-char-sequence)
- `q-char`
- `q-char-sequence q-char`

### q-字符 (q-char)
源字符集中除换行和 `"` 以外的任何成员

## 预处理数字 (pp-number)
- `digit (digit)`
- `. digit`
- `pp-number digit`
- `p-number identifier-nondigit`
- `p-number e sign`
- `p-number E sign`
- `p-number .`

## 标识符 (identifier)
- `identifier-nondigit`
- `identifier identifier-nondigit`
- `digit`
- `identifier-nondigit`

### 标识符-非数字标识符 (identifier-nondigit)
- 非数字字符 (`nondigit`)
- 统一字符名称 (`uniform-character-name`)
- 其他由实现定义的字符 (`other implementation-defined characters`)

### 非数字字符 (nondigit)
范围之一
- `a b c d e f g h i j k l m`
- `o p q r s t u v w x y z`
- `A B C D E F G H I J K L M`
- `O P Q R S T U V W X Y Z =`

### 数字 (digit)
范围之一
- `0 1 2 3 4 5 6 7 8 9`

# A.2

## 预处理运算符或标点符号 (preprocessing-op-or-punc)

| `+` | `<` | `#` | `##` | `( )` | |
|---|---|---|---|---|---|
| `{ }` | `[ ]` | `%` | `%: ` | | |
| ` <: ` | `>` | `%<` | ` %>` | `%:::` | `...` |
| `new delete ?` | `::` | | | | |
| `*` | `/` | `*.*` | | | `-` |
| `!` | | `++` | `-=` | `|=` | `|=` | `*=` | `/=` | `|=` | |
| `=` | `&= =` | `<<` | `>>` | `>=` | `<= =` | `!=` | | |
| `=` | `>` | `&&` | `||` | `-` | `->*` |
| `and and and_eq bitand bitor compl not not not_eq` | |

## 整数字面量 (integer-literal)
- 字符字面量 (`character-literal`)
- 浮点字面量 (`floating-literal`)
- 字符串字面量 (`string-literal`)
- 布尔字面量 (`boolean-literal`)
- 指针字面量 (`pointer-literal`)
- 用户定义字面量 (`user-defined-literal`)

## 整数字面量 (integer-literal)
- 十进制字面量 (`decimal-literal`) `integer-suffix_opt`
- 八进制字面量 (`octal-literal`) `integer-suffix_opt`
- 十六进制字面量 (`hexadecimal-literal`) `integer-suffix_opt`

## 进制字面量 (decimal-literal)
- 非零数字 (`nonzero-digit`)
- 十进制数字 (`decimal-digit`)

## 八进制字面量 (octal-literal)
- `0`
- `octal-octal-digit`

## 十六进制字面量 (hexadecimal-literal)
- `0x hexadecimal-digit`
- `0X hexadecimal-digit`
- `hexadecimal-literal hexadecimal-digit` 注：此处原文可能存在重复错误，按原文翻译为 `hexadecimal-literal hexadecimal-digit`

### 非零数字 (nonzero-digit)
范围之一
- `1 2 3 4 5 6 7 8 9`

### 八进制数字 (octal-digit)
范围之一
- `0 1 2 3 4 5 6 7`

### 十进制数字 (decimal-digit)
范围之一
- `0 1 2 3 4 5 6 7 8 9`
- `a b c d e f`

## 整数字面量 (integer-literal)
- 无符号后缀 (`unsigned-suffix`) `long-suffix_opt`
- 有符号后缀 (`signed-suffix`) `long-suffix_opt`
- 后缀-后缀 (`suffix-suffix`) `unsigned-suffix_opt`
- 长长后缀 (`long-long-suffix`) `unsigned-suffix_opt`

### 无符号后缀 (unsigned-suffix)
范围之一
- `u`
- `1 L`

### 长长后缀 (long-long-suffix)
范围之一
- `11 LL`

§ A.2

# ISO/IEC 14882:2011(E)

## 字符字面量 (character-literal)
```
' c-char-sequence \
u' c-char-sequence \
U' c-char-sequence \
L' c-char-sequence \
```

### c-字符序列 (c-char-sequence)
- `c-char`
- `c-char-sequence c-char`

### c-字符 (c-char)
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行
转义序列 (`escape-sequence`):
通用字符名称 (`universal-character-name`)

## 转义序列 (escape-sequence)
- 简单转义序列 (`simple-escape-sequence`)
- 八进制转义序列 (`octal-escape-sequence`)
- 十六进制转义序列 (`hexadecimal-escape-sequence`)

### 简单转义序列 (simple-escape-sequence)
范围之一
`'\'' '\b' '\f' '\r' '\t' '\v'`

### 八进制转义序列 (octal-escape-sequence)
- `octal-digit`
- `octal-digit octal-digit`
- `octal-digit octal-digit`

### 十六进制转义序列 (hexadecimal-escape-sequence)
- `\ hexadecimal-digit`
- `hexadecimal-escape-sequence hexadecimal-digit`

## 浮点字面量 (floating-literal)
- `fractional-constant exponent-part floating-suffix_opt`
- `digit-sequence exponent-part floating-suffix_opt`

### 分数常数 (fractional-constant)
- `digit-sequence_opt, digit-sequence`
- `digit-sequence ,\exponent-part:`
- `e suffix_opt digit-sequence`
- `E suffix_opt digit-sequence`

### 符号 (sign)
范围之一
`+`

### 数字序列 (digit-sequence)
- `digit`
- `digit-sequence digit`

### 浮点后缀 (floating-suffix)
范围之一
`f F L`

## 字符串字面量 (string-literal)
- `encoding-prefix_opt " s-char-sequence_opt"`
- `encoding-prefix_opt R raw-string`

### 编码前缀 (encoding-prefix)
- `uS`
- `U`
- `L`

§ A.2

# ISO/IEC 14882:2011(E)

## s-字符序列 (s-char-sequence)
- `s-char`
- `s-char-sequence s-char`

## s-字符 (s-char)
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

## s-序列 (s-char-sequence)
- `s-char`
- `s-char-sequence s-char`

## s-字符 (s-char)
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

```
(注：此处根据原文逻辑翻译，原文-char---定义)
```

# ISO/IEC 14882:2011(E)

## s-字符序列 (s-char-sequence)
- `s-char`
- `s-char-sequence s-char`

## s-字符 (s-char)
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

## s-字符序列 (s-char-sequence)
- `s-char`
- `s-char-sequence s-char`

## s-字符 (s-char)
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

`s-char-sequence:`

## s-字符序列 (s-char-sequence)
- `s-char`
- `s-char-sequence s-char`

## s-字符 (s-char)
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

```
(注：由于原文文本中存在大量重复和截断，已严格遵循原文结构进行翻译)
```

# ISO/IEC 14882:2011(E)

## s-字符序列 (s-char-sequence)
- `s-char`
- `s-char-sequence s-char`

## s-字符 (s-char)
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

## s-char-sequence (s-char-sequence)
- `s-char`
- `s-char-sequence s-char`
- `s-字符 (s-char):`
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行

## s-char-sequence (s-char-sequence)

## s-字符序列 (s-char-sequence)
- `s-char`
- `s-char-sequence s-char`

## s-字符 (s-char)
源字符集中除以下以外的成员
单引号 `'`, 反斜杠 `\` 或换行
