

## 算术表达式求值

表达式被定义为若干操作数或数据项与多个运算符组合。算术表达式由算术运算符和操作数组成。

算术表达式中有三种记号法。

- i) 中缀记法
- ii) 前缀记法
- iii) 后缀记法

### 中缀记法

通常，在算术表达式中，二元运算符出现在其两个操作数之间。这称为中缀记法。中缀记法的一般形式是：

```
Op1 operator Op2   where Op1 and Op2 are two operands
```

### 示例：

```
a + b
```

### 前缀记法

在前缀记法中，二元运算符出现在其两个操作数之前。这种记号法也称为波兰记法。在前缀记法中，要执行的操作完全由表达式中运算符和操作数的位置确定。因此，在使用前缀记法编写表达式时，永远不使用括号。前缀记法的一般形式是：

```
operator Op1 Op2   where Op1 and Op2 are two operands
```

### 示例：

```
+ a b
```

### 后缀记法

在后缀记法中，二元运算符出现在其两个操作数之后。这种记号法也称为逆波兰记法。在后缀记法中，要执行的操作完全由表达式中运算符和操作数的位置确定。因此，在使用后缀记法编写表达式时，永远不使用括号。后缀记法的一般形式是：

```
Op1 Op2 operator   where Op1 and Op2 are two operands
```

### 示例：

```
a b +
```

我们熟悉常规的中缀记法。然而，后缀记法最适合计算机计算任何表达式，并且是设计CPU算术逻辑单元（ALU）时普遍接受的记号法。因此，我们有必要学习后缀记法。后缀表达式是计算机看待任何算术表达式的方式。

### 中缀表达式的缺点

- 中缀表达式需要遍历多次才能求值。
- 中缀表达式不唯一确定运算符求值的顺序。在中缀表达式中，运算符基于运算符优先级约定进行求值。
- 在中缀记法中，可以通过使用括号来提高运算符优先级。因此，括号可以改变中缀表达式中的求值顺序。
- 存储完全带括号的表达式是浪费的，因为为了正确求值表达式，需要存储表达式中的括号。

### 后缀表达式的优点

- 后缀表达式只需遍历一次即可求值。因此，后缀表达式的求值速度快于中缀表达式。
- 后缀表达式已经根据运算符优先级排列。因此，在求值过程中永远不需要查看运算符的优先级
- 在后缀表达式中，永远不使用括号。

计算机通常分两步求值用中缀记法编写的表达式：

- i) 将中缀表达式转换为等价的后缀表达式
- ii) 一次遍历求值后缀表达式

### 将中缀表达式转换为后缀形式

求值顺序可以通过为每个运算符分配优先级来确定。括号内的运算符具有最高优先级，将首先被求值。当表达式中有两个优先级相同的运算符时，表达式根据其结合性（从左到右或从右到左）顺序求值。在表6.2中，指定了不同运算符的优先级。

表6.2：求值顺序中运算符的优先级

| 运算符 | 描述 | 优先级 |
| :--- | :--- | :--- |
| + - | 一元运算符 | 5 |
| ^ | 幂运算符 | 4 |
| * / % | 乘法、除法、取余 | 3 |
| + - | 加法、减法 | 2 |
| <= >= == != | 关系运算符 | 1 |

有一种算法可以将中缀表达式转换为等价的后缀表达式。这里使用栈来存储运算符而不是操作数。栈的目的是反转表达式中运算符的顺序。

### 将中缀表达式转换为等价后缀表达式的算法

```
Algorithm: POSTFIX (Q, P)
[Q is a given infix expression and P is a postfix expression]
1. Push "(" onto stack & add ")" to the end of Q.
2. Scan Q from left to right and repeat step 3 to 6
for each element (symbol) of Q while the stack is not empty
3. If the element is an operand then add it to P.
4. If the element is left parenthesis "(" then push it onto the stack.
5. If the element is an operator then:
   a) Repeatedly pop from stack (until the element on top of the stack has higher or same precedence than the operator currently scanned) and add it to P.
   b) Add the operator to stack.
6. If the element is a right parenthesis ")" then:
   a) Repeatedly pop from stack and add to P each operator until a left parenthesis "(" is found
   b) Pop the left parenthesis from the stack.
[End of Loop]
7. Return
```

### 示例：

求以下中缀表达式的后缀表达式：

Q = A + (B * C - (D / E ↑ F) * G) * H

| 序号 | 扫描符号 | 栈 | 后缀表达式 (P) |
| :--- | :--- | :--- | :--- |
| 初始 | | ( | |
| 1 | A | ( | A |
| 2 | + | (+ | A |
| 3 | ( | (+( | A |
| 4 | B | (+( | AB |
| 5 | * | (+(* | AB |
| 6 | C | (+(* | ABC |
| 7 | - | (+(- | ABC * |
| 8 | ( | (+(-( | ABC * |
| 9 | D | (+(-( | ABC *D |
| 10 | / | (+(-(/ | ABC *D |
| 11 | E | (+(-(/ | ABC *DE |
| 12 | ↑ | (+(-(/↑ | ABC *DE |
| 13 | F | (+(-(/↑ | ABC *DEF |
| 14 | ) | (+- | ABC *DEF↑/ |
| 15 | * | (+-* | ABC *DEF↑/ |
| 16 | G | (+-* | ABC *DEF↑/G |
| 17 | ) | (+ | ABC *DEF↑/G*- |
| 18 | * | (+* | ABC *DEF↑/G*-H |
| 19 | H | (+* | ABC *DEF↑/G*-H |
| 20 | ) | 栈为空 | ABC *DEF↑/G*-H*+ |

后缀表达式 A B C * D E F ↑ / G * - H * +

### 示例：

求以下中缀表达式的后缀表达式：
Q = (a + b * x) / (a - d). s - c ^ y

| 序号 | 扫描符号 | 栈 | 后缀表达式 |
| :--- | :--- | :--- | :--- |
| 初始 | | ( | |
| 1 | ( | (( | |
| 2 | a | ((( | a |
| 3 | + | (((+ | a |
| 4 | b | (((+ | a b |
| 5 | * | (((+* | a b |
| 6 | x | (((+* | a b x |
| 7 | ) | ((( | a b x * + |
| 8 | / | (/ | a b x * + |
| 9 | ( | (/(( | a b x * + |
| 10 | a | (/(( | a b x * + a |
| 11 | - | (/((- | a b x * + a |
| 12 | d | /((- | a b x * + a d |
| 13 | ) | (/ | a b x * + a d - |
| 14 | . | ( | a b x * + a d - / |
| 15 | s | (. | a b x * + a d - / s |
| 16 | - | (. - | a b x * + a d - / s . |
| 17 | c | (. - | a b x * + a d - / s . c |
| 18 | ^ | (. - ^ | a b x * + a d - / s . c |
| 19 | y | (. - ^ | a b x * + a d - / s . c y |
| 20 | ) | 栈为空 | a b x * + a d - / s . c y ^ - |

给定中缀表达式的等价后缀表达式是 a b x * + a d - / s c y ^ -.

求值算法的时间复杂度为 O(n)，其中 n 是输入表达式中的字符数。

### 后缀表达式求值

该算法求出用后缀记法编写的算术表达式 P 的值。

```
Algorithm: EVALUATION (P)
[P is a postfix expression]
1. Add a right parenthesis “)” at the end of P.
2. Read P from left to right and repeat step 3 and 4
for each element of P until the “)” is found.
3. If an operand is found, put it onto the stack.
4. If an operator # is found then
   a) Pop the two top elements of the stack,
   Where A is the top element and B is the next to top element
   b) Evaluate R = B # A
   c) Push R onto the stack
   [End of If]
   [End of Loop]
5. Set Result equals to the top element on stack
6. Return
```

### 示例：

求以下后缀表达式的值：

5 3 2 * 8 + * +

| 序号 | 扫描符号 | 栈 | 输出 |
|---|---|---|---|
| 1 | 5 | 5 | |
| 2 | 3 | 5 3 | |
| 3 | 2 | 5 3 2 | |
| 4 | * | 5 6 | |
| 5 | 8 | 5 6 8 | |
| 6 | + | 5 14 | |
| 7 | * | 70 | 70 |

求值算法的时间复杂度为 O(n)，其中 n 是输入表达式中的字符数。

### 将中缀表达式转换为前缀形式

有一种算法可以将中缀表达式转换为等价的前缀表达式。这里使用栈来存储运算符而不是操作数。

将中缀表达式转换为等价前缀表达式的算法。

```
Algorithm: PREFIX (A, B)
[A is a given infix expression and B is a prefix expression]
1. Push ")" onto STACK, and add "(" to end of the A
2. Scan A from right to left and repeat step 3 to 6
   for each element(symbol) of A while the STACK is not empty
3. If the element is an operand then add it to B
4. If the element is a right parenthesis then push it onto STACK
5. If the element is an operator then:
   a) Repeatedly pop from STACK and add to B, each operator (on the
   top of STACK) which has same or higher precedence than the operator.
   b) Add operator to STACK
6. If the element is a left parenthesis then
```

