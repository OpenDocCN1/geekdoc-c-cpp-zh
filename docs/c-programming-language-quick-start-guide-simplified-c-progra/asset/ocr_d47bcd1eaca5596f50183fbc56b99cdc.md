retain their state when blocks are entered and exited frequently. Remember, normal

variables are de-allocated as soon as the block is closed. The second use is its use with

external class declarations.

Here is an example:

![](bbox=[0.14, 0.47, 0.44, 0.6])

```
void demo()
{
int normalVariable = 5;
static int staticVariable = 5;
normalVariable += 10;
staticVariable += 10;
printf("Normal: %d\n", normalVariable);
printf("Static: %d\n", staticVariable);
}
void main(void)
{
demo();
}
```