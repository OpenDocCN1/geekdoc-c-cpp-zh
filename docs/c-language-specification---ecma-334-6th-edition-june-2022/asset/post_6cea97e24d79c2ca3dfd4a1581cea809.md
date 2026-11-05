
- 10.3.9 User-defined explicit conversions................................................121
### 10.4 Standard conversions.......................................................121
- 10.4.1 General.......................................................121
- 10.4.2 Standard implicit conversions................................................121
- 10.4.3 Standard explicit conversions................................................121
### 10.5 User-defined conversions................................................122
- 10.5.1 General.......................................................122
- 10.5.2 Permitted user-defined conversions................................................122
- 10.5.3 Evaluation of user-defined conversions................................................122
- 10.5.4 User-defined implicit conversions................................................123
- 10.5.5 User-defined explicit conversions................................................124
### 10.6 Conversions involving nullable types................................................125
- 10.6.1 Nullable Conversions................................................125
- 10.6.2 Lifted conversions................................................126
### 10.7 Anonymous function conversions................................................126
- 10.7.1 General................................................126
- 10.7.2 Evaluation of anonymous function conversions to delegate types................................................128
- 10.7.3 Evaluation of lambda expression conversions to expression tree types................................................129
### 10.8 Method group conversions................................................129
## 11. Expressions................................................133
### 11.1 General................................................133
### 11.2 Expression classifications................................................133
- 11.2.1 General................................................133
- 11.2.2 Values of expressions................................................134
### 11.3 Static and Dynamic Binding................................................134
- 11.3.1 General................................................134
- 11.3.2 Binding-time................................................135
- 11.3.3 Dynamic binding................................................135
- 11.3.4 Types of subexpressions................................................136
### 11.4 Operators................................................136
- 11.4.1 General................................................136
- 11.4.2 Operator precedence and associativity................................................137
- 11.4.3 Operator overloading................................................138
- 11.4.4 Unary operator overload resolution................................................139
- 11.4.5 Binary operator overload resolution................................................139
- 11.4.6 Candidate user-defined operators................................................140
- 11.4.7 Numeric promotions................................................140
- 11.4.7.1 General................................................140
- 11.4.7.2 Unary numeric promotions................................................141
- 11.4.7.3 Binary numeric promotions................................................141
- 11.4.8 Lifted operators................................................142
### 11.5 Member lookup................................................143
- 11.5.1 General................................................143
- 11.5.2 Base types................................................144
### 11.6 Function members................................................144
- 11.6.1 General................................................144
- 11.6.2 Argument lists................................................147
- 11.6.2.1 General................................................147
- 11.6.2.2 Corresponding parameters................................................148
- 11.6.2.3 Run-time evaluation of argument lists 149
### 11.6.3 Type inference 151
- 11.6.3.1 General 151
- 11.6.3.2 The first phase 152
- 11.6.3.3 The second phase 152
- 11.6.3.4 Input types 152
- 11.6.3.5 Output types 152
- 11.6.3.6 Dependence 153
- 11.6.3.7 Output type inferences 153
- 11.6.3.8 Explicit parameter type inferences 153
- 11.6.3.9 Exact inferences 153
- 11.6.3.10 Lower-bound inferences 153
- 11.6.3.11 Upper-bound inferences 154
- 11.6.3.12 Fixing 155
- 11.6.3.13 Inferred return type 155
- 11.6.3.14 Type inference for conversion of method groups 156
- 11.6.3.15 Finding the best common type of a set of expressions 157
### 11.6.4 Overload resolution 157
- 11.6.4.1 General 157
- 11.6.4.2 Applicable function member 158
- 11.6.4.3 Better function member 158
- 11.6.4.4 Better conversion from expression 159
- 11.6.4.5 Exactly matching expression 160
- 11.6.4.6 Better conversion target 160
- 11.6.4.7 Overloading in generic classes 160
### 11.6.5 Compile-time checking of dynamic member invocation 161
### 11.6.6 Function member invocation 162
- 11.6.6.1 General 162
- 11.6.6.2 Invocations on boxed instances 163
### 11.7 Primary expressions 163
- 11.7.1 General 163
- 11.7.2 Literals 164
- 11.7.3 Interpolated string expressions 164
- 11.7.4 Simple names 169
- 11.7.5 Parenthesized expressions 171
### 11.7.6 Member access 171
- 11.7.6.1 General 171
- 11.7.6.2 Identical simple names and type names 173
- 11.7.7 Null Conditional Member Access 174
### 11.7.8 Invocation expressions 174
- 11.7.8.1 General 174
- 11.7.8.2 Method invocations 175
- 11.7.8.3 Extension method invocations 177
- 11.7.8.4 Delegate invocations 179
- 11.7.9 Null Conditional Invocation Expression 180
### 11.7.10 Element access 180
- 11.7.10.1 General 180
- 11.7.10.2 Array access 181
- 11.7.10.3 Indexer access 181
- 11.7.11 Null Conditional Element Access 182
## Table of Contents
- 11.7.12 This access — 183
- 11.7.13 Base access — 184
- 11.7.14 Postfix increment and decrement operators — 184
- 11.7.15 The new operator — 186
  - 11.7.15.1 General — 186
  - 11.7.15.2 Object creation expressions — 186
  - 11.7.15.3 Object initializers — 187
  - 11.7.15.4 Collection initializers — 190
  - 11.7.15.5 Array creation expressions — 191
  - 11.7.15.6 Delegate creation expressions — 194
  - 11.7.15.7 Anonymous object creation expressions — 195
- 11.7.16 The typeof operator — 197
- 11.7.17 The sizeof operator — 199
- 11.7.18 The checked and unchecked operators — 200
- 11.7.19 Default value expressions — 202
- 11.7.20 Nameof expressions — 202
- 11.7.21 Anonymous method expressions — 204
### 11.8 Unary operators — 204
  - 11.8.1 General — 204
  - 11.8.2 Unary plus operator — 205
  - 11.8.3 Unary minus operator — 205
  - 11.8.4 Logical negation operator — 206
  - 11.8.5 Bitwise complement operator — 206
  - 11.8.6 Prefix increment and decrement operators — 206
  - 11.8.7 Cast expressions — 208
  - 11.8.8 Await expressions — 208
    - 11.8.8.1 General — 208
    - 11.8.8.2 Available expressions — 209
    - 11.8.8.3 Classification of await expressions — 209
    - 11.8.8.4 Run-time evaluation of await expressions — 209
### 11.9 Arithmetic operators — 210
  - 11.9.1 General — 210
  - 11.9.2 Multiplication operator — 210
  - 11.9.3 Division operator — 211
  - 11.9.4 Remainder operator — 213
  - 11.9.5 Addition operator — 214
  - 11.9.6 Subtraction operator — 216
### 11.10 Shift operators — 218
### 11.11 Relational and type-testing operators — 219
  - 11.11.1 General — 219
  - 11.11.2 Integer comparison operators — 220
  - 11.11.3 Floating-point comparison operators — 221
  - 11.11.4 Decimal comparison operators — 222
  - 11.11.5 Boolean equality operators — 222
  - 11.11.6 Enumeration comparison operators — 222
  - 11.11.7 Reference type equality operators — 223
  - 11.11.8 String equality operators — 225
  - 11.11.9 Delegate equality operators — 225
  - 11.11.10 Equality operators between nullable value types and the null literal — 226
  - 11.11.11 The is operator — 226
