![](bbox=[0.06, 0.07, 0.46, 0.28])

Code 9.3 applied to Code 9.1: The previous and next chapters now have back and forth arrows.

TIP Because the content property was not supported until Internet Explorer 8, it is best not to rely on this property for critical information.

TIP Information rendered using the content property will not be searchable by search engine spiders, so never use it to insert information that defines your page.

TIP Content added this way is also invisible to screen readers, so don't include anything that they will miss.

TIP One idea is to use content to add figure captions pulled from the image's alt tag. Because this is visible to screen readers and search engines, it's a good way to cut down on repetitive content.

# 3. Specify the content to be added.

```
url('../images/chrome/
  bullet-01.png') 'Chapter '
  'counter(chapterNum) ':' ;
```

To define the content that is being added, type one or more of the following values, separating each value with a space:

+   Type a string value, such as Chapter, within single or double quotes. Anything within the quotes will be displayed just as you typed it, including HTML code, although spaces are collapsed (that is, more than two spaces are collapsed into a single space when displayed).

+   url(), with an absolute or relative URL within the parentheses pointing to an external file, such as an image or sound file. For example, url(bg_flourish.png) will load an image.

+   counter(), with a counter name in parentheses. For example, counter(chapterNum) adds the counter number for the chapterNum counter. (Counters are explained in the next section.)

+   open-quote or close-quote to add a quotation mark using the current quotation style. (See “Specifying the Quote Style” later in this chapter.)

+   no-open-quote or no-close-quote to increase the level of quoting by one level.

+   attr() to display the value of the indicated attribute. For example, attr(alt) will display the value for the alt attribute of the element being styled.

+   inherit, which will use the content defined for the parent element.

+   normal or none, which will not add any content or apply any other values.