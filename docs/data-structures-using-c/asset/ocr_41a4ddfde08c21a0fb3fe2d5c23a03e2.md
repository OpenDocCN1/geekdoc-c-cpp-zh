# Table 3.13 Reversal of a string using a stack

| Input | Action | Stack | Display |
| :--- | :--- | :--- | :--- |
| ABCDEF | Push A | A <- top of stack | - |
| BCDEF | Push B | AB <- top of stack | - |
| CDEF | Push C | ABC <- top of stack | - |
| DEF | Push D | ABCD <- top of stack | - |
| EF | Push E | ABCDE <- top of stack | - |
| F | Push F | ABCDEF <- top of stack | - |
| End | Pop and display | ABCDE <- top of stack | F |
| | Pop and display | ABCD <- top of stack | FE |
| | Pop and display | ABC <- top of stack | FED |
| | Pop and display | AB <- top of stack | FEDC |
| | Pop and display | A <- top of stack | FEDCB |
| | Pop and display | Stack empty | FEDCBA |
| | Stop | | |

Reading a string character and writing it backward can be accomplished by pushing each character on to a stack as it is read. When the string is finished, pop the characters off the stack, and they will come out in the reverse order. This process is illustrated in Program Code 3.7.

```
PROGRAM CODE 3.7

main()
{
   Stack S;   // here Stack is the character stack
   char str[], ch;
   int i;
   ch = str[0];
   i = 1;
   while(ch != '\0')
   {
      S.push(ch);
      Ch = str[i++];
   }
   while(!S.Isempty())
   {
      cout << S.pop();
   }
}
```