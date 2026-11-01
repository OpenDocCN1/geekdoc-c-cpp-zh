Note that combining is very different from grouping. Grouping is just a shortcut to avoid typing the same declarations over and over again, whereas combining enables you to target specific elements in your document.

With combining, you're not limited to ID and Type selectors; you can also use it with the other selectors, as is demonstrated with the following example:

```
```css
section#MainContent p.Attention
{
    font-weight: bold;
}
```
```

This rule changes all paragraphs with the class Attention within the <section> element with its id set to MainContent and leaves all others untouched. The following HTML snippet uses this rule to show the effect:

```
```html
<section id="MainContent">
<p class="Attention">My class is Attention, so my text is bold.</p>
<p>My text is not bold, as it lacks the Attention class.</p>
</section>
<p class="Attention">I am NOT bold because I don't fall within MainContent.</p>
```
```

The second question that needs to be answered to apply a certain style in your page is about what part of the element must be styled. You do this with properties.

# Properties

Properties are the part of the element that you want to change with your style sheet. The CSS specification defines a long list of properties (VS's IntelliSense list shows more than 100 items), although you won't use all of them in most websites. The following table lists some of the most common CSS properties and describes where they are used.

| PROPERTY | DESCRIPTION | EXAMPLE |
|---|---|---|
| background-color
background-image | Specifies the background color or image of an element. | background-color: White;
background-image: url(image.jpg); |
| border | Specifies the border of an element. | border: 3px solid Black; |
| color | Changes the font color. | color: Green; |
| display | Changes the way elements are displayed, enabling you to hide or show them. | display: none;
This causes the element to be hidden, and not take up any screen space. |
| float | Enables you to "float" an element in the page using a left or right float. Other content is then placed on the opposite side. | float: left;
This setting causes other content following a float to be placed at the top-right corner of the element. You see how this works later in the chapter. |