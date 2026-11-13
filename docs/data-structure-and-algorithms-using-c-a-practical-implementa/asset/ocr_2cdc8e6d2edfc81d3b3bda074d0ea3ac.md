```
```cpp
//if the scanned character is operator
else
{
//perform the operation if the operator in
oplist having equal or higher priority to the scanned
character, then perform the operation
while(!oplist.empty() && priority(oplist.top())
>= priority(expression[i]))
{
y = numArr.top(); //extract the top element
into y
numArr.pop(); //pop the stack
x = numArr.top(); //extract the top element
into x
numArr.pop(); //pop the stack
ch = oplist.top(); //extract the operator in
top o the stack
oplist.pop(); //pop the stack
res = operate(x,ch, y);//perform the
operation
numArr.push(res); //push the result into the
stack
}
oplist.push(expression[i]);
}
}
```
```

```
```cpp
while(!oplist.empty())
{
y = numArr.top(); //extract the top element into y
numArr.pop(); //pop the stack
x = numArr.top(); //extract the top element
into x
numArr.pop(); //pop the stack
ch = oplist.top(); //extract the operator in
top o the stack
oplist.pop(); //pop the stack
res = operate(x,ch, y);//perform the operation
numArr.push(res); //push the result into the
stack
}
```
```