
- 4. At the top of the CSS file, type the following code that uses an ID selector to select the header element:

```
header
{
}
```

- 5. Position your mouse between the curly braces, right-click, and choose Build Style from the context menu. The Modify Style dialog box shown in Figure 3-6 appears.

![](img/eadab2ccd79b253c01a3fdff2321202d_125_0.png)

FIGURE 3-6

- 6. In the Category list on the left, click Background and then open the drop-down list for the background color. From the color picker that appears, click the Silver color, as shown in Figure 3-7.

Alternatively, you can type the hexadecimal color code for Silver (#C0C0C0) in the background-color text box directly.

- 7. Switch to the Position category by clicking it in the list on the left. The panel that appears enables you to set position-related information, including the height and width. Under width, enter 844 and make sure that px is selected in the drop-down list at the right. For the height, enter 86. Click OK to dismiss the dialog box and to insert the declarations into your code, which now looks like this:

```
header
{
  background-color: #C0C0C0;
  width: 844px;
  height: 86px;
}
```

## Bibliography

本刊始终关注中国现代美术的演进历程，并在其中积极回应艺术实践与社会思潮之间的复杂互动。在既往的栏目中，我们曾围绕现实主义、形式探索、主体意识、图像叙事等议题展开多角度讨论，力图呈现历史现场中的思想张力与艺术家的个体抉择。

In previous issues, this journal has consistently focused on the evolution of modern Chinese art, actively responding to the intricate interactions between artistic practice and social thought. Around themes such as realism, formal exploration, subjectivity, and visual narrative, we have sought to reveal the intellectual tensions of the historical scene and the individual choices of artists.

需要强调的是，对于‘现代性’这一概念，我们并不将其视为某种单一、线性的发展逻辑，而是将其放置在跨文化传播、民族国家建构以及艺术本体自律等多重脉络之中加以审视。由此，在推进相关研究时，我们尤为重视文献的整理与辨伪，主张将图像、文本与实物证据相互参证。

It should be emphasized that “modernity” is not treated as a single, linear developmental logic, but rather is examined within multiple contexts, including cross-cultural dissemination, nation-state construction, and the autonomy of art. In advancing related research, we place particular emphasis on the sorting and authentication of archival documents, advocating a cross-referential approach that combines images, texts, and material evidence.

本卷所收录的论文与方法论札记，即为上述关怀的具体展开。各篇文章在议题与写法上不尽相同，但均力求在扎实的史料基础之上，形成有启发性的问题意识，进而为后续研究提供可资讨论的起点。

The essays and methodological notes collected in this volume represent a concrete elaboration of the above concerns. Though they differ in topic and approach, each contribution strives to develop a thought-provoking set of questions on the basis of solid historical evidence, thereby providing a point of departure for further scholarly discussion.

Adding Modernizr to your site is very easy using the Package Manager Console that ships with Visual Studio. To add the library, follow these steps:

- 1. Choose Tools ← Library Package Manager ← Package Manager Console.
- 2. Type the following command and press Enter:
  ```
  Install-Package Modernizr
  ```
- 3. After a short delay, your site is expanded with a file called packages.config that keeps track of the installed packages and a Scripts folder that now contains the file modernizr-2.6.2.js. Note: your version number could be different if a newer version of Modernizr has been released by the time you read this book. To add this library to your page, open Default.aspx in Markup View and drag the file from the Solution Explorer to the head section of the code, directly after the link to the style sheet. You should end up with this code:
  ```html
  <link href="Styles/Styles.css" rel="stylesheet" type="text/css" />
  <script type="text/javascript" src="Scripts/modernizr-2.6.2.js"></script>
  </head>
  ```

You should add the Modernizr library to your site even if you have a modern web browser. Since you can't control the browsers visiting your site, you want to make sure everybody sees your site as intended. Adding Modernizr fixes the HTML5 compatibility issues for older browsers while hardly causing any overhead. You can learn more about Modernizr on its website at http://modernizr.com/. You'll see a lot more about the Package Manager Console in Chapter 11.

- 12. Finally, save the changes to all open documents (press Ctrl+Shift+S) and then request Default.aspx in your browser. Your screen should look similar to Figure 3-8, which shows the page in Mozilla Firefox.

![](img/eadab2ccd79b253c01a3fdff2321202d_128_0.png)

FIGURE 3-8

## How It Works

The Style Builder makes it easy to select CSS properties and change their values. You don't need to memorize every little detail about CSS, but instead you can create your CSS code visually. Once you get a better understanding of CSS and its many properties and values, you may find yourself entering CSS in the CSS file directly, because that's often quicker to do.

Note that the header, PageWrapper, nav, and footer elements have an exact width of 844 pixels. This way, the site fits nicely on screens with a size of 1024 x 768 pixels, a common screen size for many of today's computers, without being squeezed between the Windows borders. Systems with bigger screens simply center the site in the available space. This centering is done by the PageWrapper element, which has its margin set to auto. This means that the available space on the left and right sides (but not at the top and bottom) is equally divided, effectively centering the PageWrapper element in the middle of the browser window.

Note also that the MainContent section and the aside are positioned next to each other. You do this with the CSS float property:

```
section#MainContent
{
    width: 664px;
    float: left;
}

aside
{
    background-color: Gray;
    width: 180px;
    float: left;
}
```

This tells the MainContent to "float" on the left side of content that follows it, effectively placing the aside to the right of it. You need to tell the aside to float as well; if you leave it out, it will be placed at the left of the page, right where it was before you applied the CSS. If you have multiple aside elements in your site (which is a common practice), you can target this aside that acts as a sidebar by adding an id attribute (such as Sidebar) just as I did with the MainContent section element and then update the CSS as follows:

```
aside#Sidebar
{
    ...
}
```

The combined width of the MainContent and aside elements adds up to 844 pixels, which is exactly the width of their parent element: the PageWrapper.

To end the float and tell the footer element to be placed directly under the MainContent and aside elements, the clear property is used to clear any float (left or right) that may be in effect:

```
footer
{
    background-color: #C0C0C0;
    width: 844px;
    clear: both;
}
```

The gray backgrounds are just temporarily added to the code, so it's easier to see what <div> ends up where. In future exercises, you modify the CSS file again to fit the scheme of the Planet Wrox website.

To tell the browser what styles to apply, you link the style sheet in the head of the page:

```
<link href="Styles/Styles.css" rel="stylesheet" type="text/css" />
```

This tells the browser to look in the Styles folder for a file called Styles.css and apply all rules in that file to the current document. Once the browser has downloaded the CSS file, it applies all the styles it finds in there to your HTML elements, resulting in the layout shown in Figure 3-8.

In this exercise, you saw how to link an external style sheet to a page using the <link> tag. However, you have more ways to include style sheets in your web pages.

## Adding CSS to Your Pages

The first way to add CSS style sheets to your web pages is through the <link> element that points to an external CSS file, as you saw in the previous exercise. Take a look at the following <link> to see what options you have when embedding a style sheet in your page:

```
<link href="StyleSheet.css" rel="Stylesheet" type="text/css" media="screen" />
```

The href property points to a file within your site, just as you saw in the previous chapter when you created links between two pages. The rel and type attributes tell the browser that the linked file is in fact a cascading style sheet. The media attribute is quite interesting: it enables you to target different devices, including the screen, printer, handheld devices, and even Braille and aural support tools for visually impaired visitors. The default for the media attribute is screen, so it's OK to omit the attribute if you're targeting standard desktop browsers.

You briefly saw the second way to include style sheets at the beginning of this chapter: using embedded <style> elements. The <style> element should be placed at the top of your ASPX or HTML page, between the <head> tags. Within the <style> tags, you can write the exact same CSS you saw earlier. For example, to change the appearance of an <h1> element in the current page only, you can add the following code to the <head> of your page:

```
<head runat="server">
<title></title>
<style type="text/css">
h1
{
    color: Blue;
}
</style>
</head>
```

The third way to apply CSS to your HTML elements is to use inline styles with the style attribute that you saw in the previous chapter. Because the style attribute is already applied to a specific HTML element, you don't need a selector and you can write the declaration in the attribute directly:

```
<span style="color: White; background-color: Black;">
    This is white text on a black background.
</span>
```
