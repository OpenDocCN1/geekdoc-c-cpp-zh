```
$x = $x - $y;
 echo "Hello Olympians!";
 if ($x + $y == 24) {
   echo "The sum of x + y equals to 24";
 }
 else {
   echo "Nothing of the above";
 }
 }
 ?>
```

# Solution

This is the case in which you can’t proceed with the conversion because there are some statements (in bold) existing between the else and if keywords.

# 21.10 Converting a Case Decision Structure to Nested Decision Control Structures, and Vice Versa

Converting a case decision structure to nested decision control structures is quite easy. All you need to do is get the variable or the expression that the switch statement evaluates and use it in all nested decision control structures.

# Case Decision Structure

```
switch (var_expr) {
  case value-1:
    block of statements 1
    break;
  case value-2:
    block of statements 2
    break;
  case value-3:
    block of statements 3
    break;
  .
  .
  .
  case value-N:
    block of statements N
    break;
  default:
    block of statements N+1
}
```

# Nested Decision Control Structures

```
if (var_expr == value-1) {
  block of statements 1
}
else {
  if (var_expr == value-2) {
    block of statements 2
  }
  else {
    if (var_expr == value-3) {
      block of statements 3
    }
    .
    .
    .
    else {
      if (var_expr == value-N) {
        block of statements N
      }
      else {
```

![](bbox=[0.35, 0.78, 0.48, 0.95])