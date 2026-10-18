# Table 15 (continued)

# GROUP 12

| Operator | Description | Examples |
|---|---|---|
| `expr1 \| expr2` | Bitwise OR<br>`111 → 1`<br>`011 → 1`<br>`110 → 1`<br>`010 → 0` | `unsigned char _control_register = 0xAB; // '1' means '0' is 'OFF'`<br>`unsigned char _bull_index = 3;`<br>`// turn on bulb at bulb_index`<br>`bulb_control_register = bulb_control_register \| (1 << bulb_index); // can use !!` |

# GROUP 13

| Operator | Description | Examples |
|---|---|---|
| `expr_1 && expr_2` | Logical AND.<br>Operands are treated as Boolean values (`true` or `false` in C++: integers). In `x && y`, `expr_1` is always evaluated first; if it is false, then `expr_2` is not evaluated at all. However, this holds only for built-in types—the user-defined overloaded versions always evaluate both operands. | `double x { };`<br>`cin >> x;`<br>`const double kValMin = -1.0, kValMax = +2.0; // define the range`<br>`if ( x >= kValMin && x <= kValMax )`<br>`{ // when x >= kValMin is false, then the rest is not evaluated at all`<br>`// proceed ...`<br>`}` |