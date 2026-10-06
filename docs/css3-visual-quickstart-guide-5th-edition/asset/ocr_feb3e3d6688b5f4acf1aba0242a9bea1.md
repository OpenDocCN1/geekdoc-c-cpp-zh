# Teaching the Browser to Count

Browsers can automatically create sequentially listed lists, starting at 1 and counting by ones. You will explore this later in the chapter. However, if you need to start numbering from 6 instead of 1! Or, if you need to create two sequential lists that are nested inside each other? CSS allows you to set up multiple counter lists using the content property (previous section). The counter-reset property (Table 9.4) is used to set the initial value for the count, and the counter-increment property (Table 9.5) is used to increase the counter by a specific value.

TABLE 9.4 Counter-Reset Values
| Value | Compatibility |
| --- | --- |
| <counterName> | IE8, FF1, S1, CSS2 |
| <num> | IE8, FF1, S1, CSS2 |
| none | IE8, FF1, S1, CSS2 |
| inherit | IE8, FF1, S1, CSS2 |

TABLE 9.5 Counter-Increment Values
| Value | Compatibility |
| --- | --- |
| <counterName> | IE8, FF1, S1, CSS2 |
| <num> | IE8, FF1, S1, CSS2 |
| none | IE8, FF1, S1, CSS2 |
| inherit | IE8, FF1, S1, CSS2 |

To use a counter:

+   1. Set up the parent element. Set up a CSS rule for the selector that will be the parent element for your numbered list (Code 9.4). This can be the o1 (ordered list) tag.
.top {...}
2. Add the counter-reset property to your declaration block.
counter-reset: counterName 0;
Type counter-reset: a, colon (:), and then the name of the counter you are defining (which can be any name you want). Then insert a space and the number you want to start the list.

```
Code 9.4 ui-generatedcontent-properties
css—The table of contents shows chapters before and after counter 4 A, so the continued list needs to skip 0.
*** CSS V05
* ui-generatedcontent-properties.css ***
.toc { margin: 0 auto; width: 90%;
text-align: center; font-size: 5em; }
a
  cursor: help;
h1
cursor: url(../images/cursor-02.png);
20 20, crosshair;
top
counter-reset: counterName 0;
toc h2:before
content: url(../images/bullet-01.png');
' ' counter(counterName) '. ';
counter-increment: counterName 1; }
toc h2:after
content: url(../images/bullet-02.png'); }

#chapter4 .continued {
counter-reset: counterName 4; }
```