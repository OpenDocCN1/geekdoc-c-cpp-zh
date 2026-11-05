
| 格式说明符 | 描述 |
|---|---|
|  | 对于所有类型：<br>- 结果中出现的数字位数（不包括指数）不会超过精度说明符的值；必要时会对值进行舍入。<br>- 只要可能，就会删除小数点和小数点后的尾随零。<br>- 格式说明符的大小写（'G' 或 'g'）决定科学格式指数前使用 'E' 还是 'e'。 |
| N<br>n | **数字格式：** 用于以下形式的字符串：<br>`[-]d,ddd,ddd.dd...d`<br>负值的表示由 System.Globalization.NumberFormatInfo.NumberNegativePattern 属性决定。如果模式包含负数符号（'-'），则该符号由 System.Globalization.NumberFormatInfo.NegativeSign 属性提供。<br>至少有一个非零十进制数字（d）在小数分隔符（'.'）之前，该分隔符由 System.Globalization.NumberFormatInfo.NumberDecimalSeparator 属性提供。十进制点与值中最显著数字之间的数字使用 System.Globalization.NumberFormatInfo.NumberGroupSizes 属性指定的组大小进行分组。组分隔符（','）插入在每个数字组之间，并由 System.Globalization.NumberFormatInfo.NumberGroupSeparator 属性提供。<br>精度说明符决定小数位数（dd...d）。如果省略精度说明符，则 System.Globalization.NumberFormatInfo.NumberDecimalDigits 决定字符串中的小数位数。必要时，结果会舍入到最接近的可表示值。 |
| P<br>p | **百分比格式：** 用于包含百分比的字符串。System.Globalization.NumberFormatInfo 的 System.Globalization.NumberFormatInfo.PercentSymbol、System.Globalization.NumberFormatInfo.PercentGroupSizes、System.Globalization.NumberFormatInfo.PercentGroupSeparator 和 System.Globalization.NumberFormatInfo.PercentDecimalSeparator 成员分别提供百分号、数字分组的大小和分隔符以及小数分隔符。<br>System.Globalization.NumberFormatInfo.PercentNegativePattern 和 System.Globalization.NumberFormatInfo.PercentPositivePattern 决定用于表示负值和正值的符号。例如，负值可以加上减号前缀，或用括号括起来。<br>如果未指定精度，则结果中的小数位数由 System.Globalization.NumberFormatInfo.PercentDecimalDigits 决定。必要时，结果会舍入到最接近的可表示值。<br>结果乘以 100（.99 变为 99%）。 |
| R<br>r | **往返格式：**（此格式仅在与 System.Double 或 System.Single 指定时有效。）用于确保浮点值的字符串表示的精度足以使解析该字符串与原始值相比不会丢失精度。如果数据类型（System.Single 为 7，System.Double 为 15）的最大精度会导致精度丢失，则精度会增加两位小数。如果在此格式说明符中提供了精度说明符，则会被忽略。此格式在其他方面与定点格式相同。 |
| X<br>x | **十六进制格式：**（此格式仅在与整数数据类型指定时有效。）用于以 16 进制表示数字的字符串。精度决定字符串中的最小数字位数。如果精度指定的位数多于数字包含的位数，则数字会用零左填充。格式说明符的大小写（'X' 或 'x'）决定十六进制表示中使用大写还是小写字母。 |

如果数值是 `System.Single` 或 `System.Double` 且值为 `NaN`、`PositiveInfinity` 或 `NegativeInfinity`，则格式说明符将被忽略，并返回以下之一：<br>
`System.Globalization.NumberFormatInfo.NaNSymbol`,<br>
`System.Globalization.NumberFormatInfo.PositiveInfinitySymbol`, 或<br>
`System.Globalization.NumberFormatInfo.NegativeInfinitySymbol`

自定义格式是指定为格式且不采用上述描述的标准格式字符串（Axx）形式的任何字符串。以下表格描述了用于构建自定义格式的字符。

| 格式说明符 | 描述 |
|---|---|
| 0 (zero) | **零占位符：** 如果要格式化的值在自定义格式中出现 '0' 的位置有数字，则该数字会被复制到输出字符串；否则在输出字符串的该位置存储零。十进制分隔符之前最左边的 '0' 的位置和十进制分隔符之后最右边的 '0' 的位置决定输出字符串中始终存在的数字范围。<br><br>十进制分隔符之后 Zero 和/或 Digit 占位符的数量决定十进制分隔符后出现的数字位数。必要时会对值进行舍入。 |
| # | **数字占位符：** 如果要格式化的值在自定义格式中出现 '#' 的位置有数字，则该数字会被复制到输出字符串；否则，在该位置不存储任何内容。请注意，如果该数字不是有效数字，则此说明符永远不会存储 '0' 字符，即使 '0' 是字符串中唯一的数字也是如此。（如果它是有效数字，则会在输出字符串中显示 '0' 字符。）<br><br>十进制分隔符之后 Zero 和/或 Digit 占位符的数量决定十进制分隔符后出现的数字位数。必要时会对值进行舍入。 |
| . (period) | **小数分隔符：** 格式字符串中最左边的 '.' 字符决定格式化值中小数分隔符的位置；任何额外的 '.' 字符都会被忽略。System.Globalization.NumberFormatInfo.NumberDecimalSeparator 属性决定用作小数分隔符的符号。 |
| , (comma) | **分组分隔符和数字缩放：** ',' 字符有两个用途。首先，如果自定义格式在两个 Zero 或 Digit 占位符（0 或 #）之间并且在小数分隔符的左侧（如果存在）包含此字符，则输出将在小数分隔符左侧的数字组之间插入分组分隔符。System.Globalization.NumberFormatInfo.NumberGroupSeparator 和 System.Globalization.NumberFormatInfo.NumberGroupSizes 属性分别决定用作分组分隔符的符号和每组中的数字位数。<br><br>如果格式字符串在小数分隔符的左侧立即包含一个或多个 ',' 字符，则数字将被缩放。缩放因子由小数分隔符左侧立即出现的分组分隔符字符的数量决定。如果有 x 个字符，则在格式化之前将值除以 1000^x。例如，格式字符串 '0,,' 将值除以一百万。请注意，使用 ',' 字符表示缩放不会在输出字符串中插入分组分隔符。因此，要将数字按 1 百万缩放并插入分组分隔符，请使用类似 '#,#0,,' 的自定义格式。 |
| % (percent) | **百分比占位符：** 自定义格式中出现 '%' 字符会导致数字在格式化之前乘以 100。百分号会插入到输出字符串中格式字符串中出现 '%' 的位置。System.Globalization.NumberFormatInfo.PercentSymbol 属性决定百分号。 |
| E0<br>E+0<br>E-0<br>e0<br>e+0<br>e-0 | **工程格式：** 如果自定义格式中存在 'E'、'E+'、'E-'、'e'、'e+' 或 'e-' 中的任何字符串，并且紧跟至少一个 '0' 字符，则值将使用科学记数法格式化。指数前缀（E 或 e）后跟随的 '0' 字符的数量决定指数中的最小数字位数。'E+' 和 'e+' 格式表示正负号始终位于指数之前。'E'、'E-'、'e' 或 'e-' 格式表示负号位于负指数之前；正指数前没有符号。正号由 System.Globalization.NumberFormatInfo.PositiveSign 属性提供。负号由 System.Globalization.NumberFormatInfo.NegativeSign 属性提供。 |
| \\ (backslash) | **转义字符：** 在某些语言中，例如 C#，反斜杠字符会导致自定义格式中的下一个字符被解释为转义序列。它被使用 |
