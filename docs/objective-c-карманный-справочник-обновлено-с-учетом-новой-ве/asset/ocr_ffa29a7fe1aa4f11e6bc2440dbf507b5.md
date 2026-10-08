```
int semicolons = 0;
NSUInteger length = [str length];\NSRange range = { 0, 10 };
while (range.location < length) {
    uchar buffer[10];
    if (range.location + range.length > length) {
        range.length = length - range.location;
    }
    [str getCharacters: buffer range: range];
    range.location += 10;
    for (unsigned i=0; i<range.length ; i++) {
        uchar c = buffer[i];
        if (c == ';') {
            semicolons++;
        }
    }
}
printf("Source file contained %d semicolons\n", semicolons);
```

From: StringIterate.m

careful to make sure you set the range.
Otherwise, you might potentially introduce some security holes into your application.
Remember that string objects hide their encoding. This code will work irrespective of how the string is stored internally. If it is 7-bit ASCII or UTF-8, converting most characters to UTF-16 is very fast. If it’s something like Mac Roman, it may take slightly longer, but it’s still