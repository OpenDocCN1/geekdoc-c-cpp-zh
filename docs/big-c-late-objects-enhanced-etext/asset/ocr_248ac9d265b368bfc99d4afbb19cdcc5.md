```
```cpp
int term_value()
{
   int result = factor_value();
   bool done = false;
   while (!done)
   {
      char op = cin.get();
      if (op == '*' || op == '/')
      {
         int value = factor_value();
         if (op == '*') { result *= value; }
         else { result /= value; }
      }
      else { cin.unget(); done = true; }
   }
   return result;
}
```
```

```
```cpp
/**
   Evaluates the next factor found in cin.
   @return the value of the factor
*/
int factor_value()
{
   int result = 0;
   char c = cin.get();
   if (c == '(')
   {
      result = expression_value();
      cin.get(); // Read ')'
   }
   else
   {
      cin.unget();
      cin >> result;
   }
   return result;
}
```
```

```
```cpp
int main()
{
   cout << "Enter an expression: ";
   cout << expression_value() << endl;
   return 0;
}
```
```

# Program Run

```
```text
Enter an expression: 1+2*12*12
1729
```
```

# 11.6 Backtracking

Backtracking is a problem solving technique that builds up partial solutions that get increasingly closer to the goal. If a partial solution cannot be completed, one abandons it and returns to examining the other candidates.