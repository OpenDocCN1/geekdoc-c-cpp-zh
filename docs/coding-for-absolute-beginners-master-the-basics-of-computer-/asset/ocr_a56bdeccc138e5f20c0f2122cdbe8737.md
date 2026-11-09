```
~~~html
</body>
</html>
~~~
```

Output:

# ### Separate Border Table with border-spacing

<table>
  <tr><td>Cell A</td></tr>
  <tr><td>Cell B</td></tr>
</table>

# ### Separate Border Table with border-spacing

<table>
  <tr><td>Cell A</td></tr>
  <tr><td>Cell B</td></tr>
</table>

Syntax for caption side property:

```
~~~html
<head>
  <style type = "text/css">
    caption.top {caption-side:top }
    caption.bottom {caption-side:bottom}
    caption.left {caption-side:left}
    caption.right {caption-side:right}
  </style>
</head>
~~~
```

Syntax for Empty Sides Property

```
~~~html
<head>
  <style type = "text/css">
    table.empty {
      width:350px;
      border-collapse:separate;
      empty-cells:hide;
~~~
```