```
```python
print("number is ", n) outputs "number is 7"
print(f"number is {n}") outputs "number is 7"
```
```

`str.capitalize()` - Capitalize first letter of string, if its already capitalized it returns the original string.

```
```python
sent = "message was sent"
sent.capitalize() returns "Message was sent"
```
```

`str.count(substring)` - returns how many times substring occurs in str.

```
```python
mess = "Life is beautiful"
mess.count('is'), returns 1.
```
```

`str.isalnum()` - returns true if a string is alphanumeric meaning it’s a combination of alphabet or/and numbers.

```
```python
a = 'door2'
b = 'door'
c = 'door#$'

a.isalnum() return True.
b.isalnum() return True.
c.isalnum() return False.
```
```