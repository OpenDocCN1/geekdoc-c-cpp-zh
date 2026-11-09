attribute in every paragraph (`<p>`) tag. Styling a single paragraph this way is easy, but applying the `<p>` tag to a series of paragraphs (or an entire page or website) quickly becomes tedious. By contrast, CSS requires the typeface to be specified only once, and it automatically applies to all paragraphs. This feature makes it easier for developers to write and maintain code. In addition, separating the styling of the content from the actual content itself has allowed search engines and other automated website agents to more easily process the content on web pages.

+   - **Inertia:** Currently millions of web pages use HTML and CSS separately, and every day that number grows. CSS started as a separate language for reasons stated above, and it remains a separate language because its popularity continues to grow.

# CSS Structure

CSS follows a set of rules to ensure that websites will be displayed in the same way no matter the browser or computer used. Sometimes, because of varying support of the CSS standard, browsers can and do display web pages differently. Nevertheless, generally speaking, CSS ensures that users have a consistent experience across all browsers.

You can use any browser to see CSS you write style your HTML files, though I strongly recommend you download, install, and use Chrome or Firefox.

![](bbox=[0.133, 0.494, 0.209, 0.567])

# Choosing the element to style

CSS continues to evolve and support increased functionality, but the basic syntax for defining CSS rules remains the same. CSS modifies HTML elements with rules that apply to each element. These rules are written as follows:

```
selector {
  property: value;
}
```

A CSS rule is comprised of three parts:

+   - **Selector:** The HTML element you want to style.
+   - **Property:** The feature of the HTML element you want to style, such as, for example, font typeface, image height, or color.
+   - **Value:** The options for the property that the CSS rule sets. For example, if color was the property, the value could be red.