# Defining Styles
Based on Context

Contextual styles allow you to specify how
a particular element should appear based
on its parents and siblings. For example,
you may want an emphasis tag to appear
one way when it’s in the main header of
the page and differently when it appears in
the sub-header. You may want still another
appearance in a paragraph of text. These
combinatory selectors (Table 4.1) are
among the most used and useful in CSS.

# Styling descendents

You can style individual descendent ele-
ments depending on their parent selector
or selectors in a space-separated list. The
last selector will receive the style if and
only if it is the descendent of the preceding
selectors 4.

When you want to indicate that the exact
selector does not matter at any given
level, you can use the universal selector (*)
described in Chapter 3 5.

```
Space-separated list of selectors
p strong em {
    color: red;
}
Declaration list
```

A The general syntax for the descendant selector.

```
Universal selector
p * em {
    color: red;
}
Space-separated
list of selectors
Declaration list
```

B The general syntax for the descendant selector
using the universal selector.

# TABLE 4.1 Combinatory Selectors

| Format | Selector Name | Elements Are Styled If... |
| :--- | :--- | :--- |
| a b c | Descendant | c descendant of b descendant of a |
| a * b | Universal | b within a regardless of b's parents |
| a > b | Direct child | b direct child of a |
| a + b | Adjacent sibling | sibling b immediately after a |
| a ~ b | General sibling | sibling b anywhere after a |