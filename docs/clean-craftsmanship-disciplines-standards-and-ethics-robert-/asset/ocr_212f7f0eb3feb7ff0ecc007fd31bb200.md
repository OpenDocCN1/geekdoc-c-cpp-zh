```
```java
assertWrapped("x x x", 1, "x\nx\nx");
assertWrapped("x x x", 2, "x\nx\nx");
assertWrapped("x x x", 3, "x x\nx");
assertWrapped("x x x", 4, "x x\nx");
assertWrapped("x x x", 5, "x x x");

assertWrapped("xx xx", 1, "x\nx\nx\nx");

assertWrapped("xx xx", 2, "xx\nxx");

assertWrapped("xx xx", 3, "xx\nxx");

assertWrapped("xx xx", 4, "xx\nxx");

private String wrap(String s, int w) {
    if (w >= s.length())
        return s;
    else {
        int br = s.lastIndexOf(" ", w);
        if (br == -1)
            br = w;
        return s.substring(0, br).trim() + "\n" +
                   wrap(s.substring(br).trim(), w);
    }
}

assertWrapped("xx xx", 5, "xx xx");
assertWrapped("xx xx xx", 1, "x\nx\nx\nx\nx\nx");
assertWrapped("xx xx xx", 2, "xx\nxx\nxx");
assertWrapped("xx xx xx", 3, "xx\nxx\nxx");
assertWrapped("xx xx xx", 4, "xx\nxx\nxx");
assertWrapped("xx xx xx", 5, "xx xx\nxx");
assertWrapped("xx xx xx", 6, "xx xx\nxx");
assertWrapped("xx xx xx", 7, "xx xx\nxx");
assertWrapped("xx xx xx", 8, "xx xx xx");
```
```