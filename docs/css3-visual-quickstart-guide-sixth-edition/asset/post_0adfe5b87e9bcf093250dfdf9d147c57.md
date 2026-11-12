
## CSS Level 1 (CSS1)

The W3C released the first official version of CSS in 1996. This early version included the core capabilities associated with CSS, such as the ability to format text, set fonts, and set margins. Netscape 4 and Internet Explorer 3 and 4 supported Level 1.

Web designers needed a way to position elements on the screen precisely. CSS1 was already released, and CSS Level 2 was still in the future, so the W3C released a stopgap solution: CSS-Positioning. This standard proposed that the parties concerned could debate the details for awhile before the CSS-P standard became official. Netscape and Microsoft jumped on these proposals, however, and included the preliminary ideas in version 4 of their browsers.

## CSS Level 2 (CSS2)

The CSS2 spec came out in 1998 and is the most widely adopted by browser makers. Level 2 includes all the attributes of the previous two versions, plus an increased emphasis on international accessibility and the capability to specify media-specific CSS.

In 2006, the W3C published an updated version: CSS Level 2.1, that corrected some errors, clarified a few issues, and included specifications for features that were already implemented in some browsers. CSS2.1 effectively replaced CSS2.

## CSS Level 3 (CSS3)

Unlike CSS1 and 2, a single, comprehensive CSS3 does not exist. Instead, rather than trying to release the entire specification at once, the CSS Working Group split the spec into a series of modules, each with its own developmental timeline. To read more about the ongoing work, check out www.w3.org/Style/CSS/current-work.

> TIP While knowing the differences among the CSS versions may be interesting, it isn't necessary for using styles on the Web. However, you do need to know which styles are supported by the browsers you're designing for. Although all modern browsers support most of the CSS Level 2 specification, older browsers support combinations of older versions of CSS. See Appendix A for details on which CSS properties each browser supports.

## CSS and HTML

When HTML was created, style properties were defined directly in the code. However, rather than just adding more and more tags and properties to HTML, the W3C introduced Cascading Style Sheets to fill the design void in straight HTML, allowing the Web to become semantic in structure. (See the sidebar “What Is the World Wide Web Consortium?”)

Take the `<strong>` tag, for example. In HTML, this common tag does one thing and one thing only: It makes text “stronger,” usually by displaying it in bolder font. However, using CSS, you can “redefine” the `<strong>` tag so that it not only makes text bolder, but also adds more emphasis by displaying text in all caps and in a specific font. You could even set the `<strong>` tag to not make text bold A.

Although both HTML and CSS have evolved over the years, they have rarely evolved in tandem. Instead, each standard has pretty much followed its own path. It’s a happy accident that both CSS3 and HTML5 have hit prime time at the same time, creating the new foundation and framework for modern Web sites.

The power of CSS comes from its ability to mix-and-match rules from multiple sources to tailor your Web pages’ layouts to your exact needs. In some ways, it resembles computer programming—which is not too surprising, because a lot of this stuff was created by programmers, rather than Web designers. But once you get the hang of it, “speaking” CSS becomes as natural as putting together a sentence B.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_29_0.png)

A The HTML `<strong>` tag is used to make text stand out; but using CSS, you can style that text any way you see fit.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_29_1.png)

B The three core Web technologies—HTML, CSS, and JavaScript—work similarly to parts of speech. HTML provides the nouns, CSS the adjectives and adverbs, and JavaScript adds the verbs.

## Types of CSS Rules

The best thing about Cascading Style Sheets is that they are amazingly simple to set up. They don’t require plug-ins or fancy software—just text files with rules in them. A CSS rule defines what the HTML should look like and how it should behave in the browser window.

CSS rules come in four types, each with specific uses:

- HTML selector: The text portion of an HTML tag is called the selector. For example, h1 is the selector for the <h1> tag. The HTML selector is used in a CSS rule to redefine how the tag displays. (See “(Re)Defining HTML Tags” in Chapter 3.) For example:

    h1 { color: red; }

  will style:

    <h1>...</h1>

- Class selector: A class is a “free agent” rule that can be applied to any HTML tag at your discretion. You can name the class almost anything you want. Because a class can be applied to multiple HTML tags, it is the most versatile type of selector. (See “Defining Reusable Classes” in Chapter 3.) For example, the class:

    .myClass { font: bold 1.25em .times; }

  will style the tag:

    <h1 class="myClass">...</h1>

- ID selector: Much like class selectors, ID rules can be applied to any HTML tag. ID selectors, however, should be applied only once to a particular HTML tag on a given page to create an object for use with a JavaScript function. For example, the ID:

    #myObject1 { position: absolute; top: 10px; }

  will style the tag:

    <h1 id="myObject1">...</h1>

- Universal selector: The universal selector is a stand-in selector represented by an asterisk (*) that is used when you want to apply a style regardless of the exact selector in use. This is especially helpful when you are using contextual styles and don't know the exact context. For example, the universal selector:

    article * strong { position: absolute; top: 10px; }

  will style the strong tag in:

    <article><p><strong>...</strong></p></article>

  as well as in:

    <article><blockquote><strong>...</strong></blockquote></article>

## What Is the World Wide Web Consortium?

The World Wide Web Consortium (www.w3.org) is an organization that sets many of the standards that browser developers will use to create their products, including HTML and CSS (with the notable exception of JavaScript).
Created in 1994, the W3C's mission is “to lead the World Wide Web to its full potential by developing protocols and guidelines that ensure the long-term growth of the Web.”
The W3C comprises more than 350 member organizations around the world. These organizations include vendors of technology products and services, content providers, corporate users, research laboratories, standards bodies, and governments.
According to its Web site, the W3C has four goals:

- Web for Everyone—To make the Web accessible to all people by promoting technologies that take into account the vast differences in culture, education, ability, material resources, and physical limitations of users on all continents.
- Web on Everything—To allow all devices easy access to the Web. Although most access is still through desktop or laptop computers, an increasing array of devices can access the Web.
- Knowledge Base—To develop an environment that permits each user to make the best use of the resources available on the Web.
- Trust and Confidence—To guide the Web’s development with careful consideration for the novel legal, commercial, and social issues raised by this technology.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_32_0.png)

(A) The basic syntax of a CSS rule. You start with a selector (HTML, Class, or ID). Then add a property, a value for that property, and a semicolon, which together are called a declaration. You can add as many definitions as you need as long as they are separated by a semicolon.

## The Parts of a CSS Rule

A CSS rule consists of properties and their values, which together are referred to as a declaration. A single CSS rule can have multiple declarations, each separated by a semicolon (;). All rules, regardless of their locations or types, have the following structural elements:

- Selectors are the alphanumeric characters that identify a rule. A selector can be an HTML tag selector, a class selector, an ID selector, a universal selector (discussed in Chapter 3), or a combination of those basic selectors to create context-based styles (discussed in Chapter 4).

- Properties identify what is being defined. Several dozen properties are available. Each is responsible for an aspect of the page content’s behavior and appearance.

- Values are assigned to a property to define its nature. A value can be a keyword such as “red,” a number, or a percentage. The type of value used depends solely on the property to which it is assigned.

> TIP Don’t confuse the selector of an HTML tag with its attributes. In the following tag, for example:
> <img src="picture.gif">
> img is the selector, and src is a property.

> TIP Although you don’t have to include a semicolon with the last definition in a list, experience shows that adding this semicolon can prevent future headaches. For example, if you forgot to put in the required semicolon before the addition and you later decide to add a new definition to the rule, you may cause the rule to fail completely. What’s worse, not only will that one definition fail, but all the definitions in the rule won’t be applied.
