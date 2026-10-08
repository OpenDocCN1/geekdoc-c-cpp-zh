# 6.3.4 Using tokens

So, maybe now we can complete our calculator! However, maybe a small amount of planning ahead would be worthwhile. How would we use **Tokens** in the calculator? We can read input into a **vector of Tokens**:

```
```
Token get_token();    // function to read a token from cin

vector<Token> tok;    // we'll put the tokens here
int main()
{
    while (cin) {
        Token t = get_token();
        tok.push_back(t);
    } // . . . 
}
```
```

Now we can read an expression first and evaluate later. For example, for **11*12**, we get

|   |   |   |
|---|---|---|
| '8' | 1*1 | '8' |
| 11  |   | 12  |

We can look at that to find the multiplication and its operands. Having done that, we can easily perform the multiplication because the numbers 11 and 12 are stored as numeric values and not as strings.
Now let’s look at more complex expressions. Given **1+2\*3**, **tok** will contain five **Tokens**:

|   |   |   |   |   |
|---|---|---|---|---|
| '8' | '+' | '8' | 1*1 | '8' |
| 1   |   | 2   |   | 3   |

Now we could find the multiply operation by a simple loop:

```
```
for (int i = 0; i<tok.size(); ++i) {
    if (tok[i].kind=='*') {            // we found a multiply!
        double d = tok[i-1].value*tok[i+1].value;
        // now what?
    }
}
```
```