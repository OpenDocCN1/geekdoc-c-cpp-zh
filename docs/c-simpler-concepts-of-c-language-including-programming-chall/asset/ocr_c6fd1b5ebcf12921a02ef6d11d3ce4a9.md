[ Statement n ]

end;

Others feel it should look like this:

```
if (expression) then
begin
[ Statement 1 ]
[ Statement 2 ]
.
.
[ Statement n ]
end;
```

C/++ programmers are even worse, there are no less than four common ways of putting the opening and closing braces around a compound statement after an "if". The second problem with C/C++s and Pascal's "if" statements is the ambiguity involved. Consider the following Pascal code:

```
if (expression) then
if (expression) then
(* Statement *)
else (* Statement *);
```

The nested code should be clearly intended. For example, in the below code it is difficult to say which 'if' does the 'else' belongs to.

# Incorrect

```
if (expression) then
If (expression) then
...
def;
else
...
def;
```

# Correct

```
if (expression) then
If (expression) then
...
```