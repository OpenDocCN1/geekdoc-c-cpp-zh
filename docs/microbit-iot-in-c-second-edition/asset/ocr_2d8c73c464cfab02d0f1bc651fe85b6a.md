All you have to do surround the bit reading loop with __disable_irq() and
__enable_irq();
int threshold=11;
//threshold=40// uncomment for V2
int buf[41];
int j;
disable_irq();nfor (j = 0; j < 41; j++) {
  for (i = 1; i < 200; i++) {
    if (P0.getDigitalValue() == 1)break;
  }
  for (i = 1; i < 200; i++) {
    if (P0.getDigitalValue() == 0) break;
  }
  buf[j] = 0;
  if (i > threshold)buf[j] = 1;
}
__enable_irq();

With this change it all works.

# Extracting the Data

Now we have the data in the buffer as zeros and ones. All that remains is
decode it into temperature and humidity readings. But first we will convert
bits into five bytes of data. The simplest way of doing this is to write a
function that will pack eight bits into an uint32_t:

```
uint32_t getByte(int b, int buf[])
{
  int i;
  uint32_t result = 0;
  b = (b - 1) * 8 + 1;
  for (i = b; i <= b + 7; i++) {
    result = result << 1;
    result = result | buf[i];
  }
  return result;
}
```

The b can be the byte that you want to extract from the array. For
example, if b = 2 then the loop runs from i = 9 to i = 16, i.e. the second
byte stored in the array. Notice that we skip the first bit because this just
ssignals the start of the data. The bit manipulation in the for loop is a fairly
standard shift left and OR the least significant bit into the result.