# Chapter 12: Forms and Validation 345

# How It Works

This plug-in starts by calling itself recursively if id is an array, passing each element to be processed individually, like this:

```
if (id instanceof Array)
{
    for (var j = 0 ; j < id.length ; ++j)
    ResizeTextarea(id[j], min, max)
    return
}
```

Next, if min or max have not been passed values, they are assigned defaults of 0 and 100 lines, respectively:

Finally, in the setup section, the onmouseup and onerror events of id are assigned to the DoResizearea () function:

```
O(id).onmouseup = DoResizearea
O(id).onkeyup = DoResizearea
```

# TheDoResizearea() Function Subsection

This function contains just two while() loops. The first continuously increases the number of rows that id until either the text in the textarea is fully visible, or the maximum number of rows in the argument max is reached:

```
while (O(id).scrollHeight > O(id).clientHeight && O(id).rows < max
++O(id).rows
```

The second while() loop performs the inverse, reducing the height of the textarea so that it is only as large as the text contains or until it reaches the minimum height specified in the argument min:

```
while (O(id).scrollHeight < O(id).clientHeight && O(id).rows > min
--O(id).rows
```

> Note While expanding and reducing the textarea seems to work fine on most browsers, once the clientHeight property in Firefox has been increased it does not seem to reduce it back down again if text is deleted, so the textarea will shrink. If you can think of a way to get Firefox to reduce as well as increase a textarea according to the text within it, please let me know the website.