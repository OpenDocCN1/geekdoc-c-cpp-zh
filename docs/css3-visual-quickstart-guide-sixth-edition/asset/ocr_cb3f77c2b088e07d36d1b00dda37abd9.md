# Embedded: Adding Styles to a Web Page

To add styles that apply to a single Web page—rather than just a single element (inline) or an entire Web site (external)—you embed the style rules in the Web page using the `<style>` tag, which in turn will hold all your style rules.

Adding styles in this manner can look identical to adding styles directly to an HTML tag (as seen in the previous section). However, when you place styles in a common location—preferably in the `<head>`.

![](bbox=[0.54, 0.07, 0.95, 0.25])

Code 3.2 Style rules are added within the `<style>` tag. A rule is added for the level 1 header to set its color, but it has no effect because the `inline` style overrides it. That's why you should never use inline styles in your final code.

```
<!- - HTML 5 -- >
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Alice#8217;s Adventures in Wonderland</title>
<style type="text/css" media="all">
h1 {
color: orange;
font-size: 3em;
font-weight: normal; }
h1 .chaptertitle {
color: yellow;
font-size: .5em; }
</style>
</head>
<body>
<h1 style="color:red;">Alice&#8217;s Adventures In Wonderland</h1>
<h1 id="ch01">Chapter 1 <span class="chaptertitle">Down the Rabbit-Hole</span></h1>
<p>...strong>Alice was beginning to get very tired of sitting by her sister on the bank,...</p>
...
</body>
</html>
```