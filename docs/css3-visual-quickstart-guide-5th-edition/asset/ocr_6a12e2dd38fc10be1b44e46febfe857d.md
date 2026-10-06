4. Add the class attribute to the HTML tag to which you want to apply it.

```
<p class="byline"><span>span class="author">...</span></p>
```

You can apply multiple classes to a single HTML tag by adding additional class names in a space separated list: class="name1 name2 name3"

Notice that when you defined the class in the CSS, it began with a period (.). However, you do not use the period when referencing the class name in an HTML tag. Using a period here will cause the class to fail.

TIP You can mix a class with ID and/or inline rules within an HTML tag (See "Inline: Adding Styles to an HTML Tag" and "Defining Unique IDs" in this chapter).

TIP Because the <div> and <span> tags have no preexisting properties, you can use them to effectively create your own HTML tags by adding classes. However, use these sparingly because once they are associated, you are locked into using those specific classes with those specific locations.