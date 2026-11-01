calculations, hiding or showing specific controls, and much more. You learn more about this Code Behind file in the next chapter, and programming your ASP.NET web pages is discussed in great detail in Chapter 5.

Once the page is done processing, and all the HTML for the page has been collected, the HTML is sent back to the browser. The browser then reads it, parses it, and, finally, displays the page for you to look at.

Because HTML is so critical for displaying web pages, the next section gives you an overview of HTML.

# Understanding HTML

HTML is the de facto language for creating web pages and is understood by every web browser that exists today. Since the beginning of the '90s it has been the driving force of the World Wide Web, the part of the Internet that deals with web pages. HTML documents are simple text files that contain markup, text, and additional data that influences that text. The most recent version of HTML is HTML5. Although the specification of HTML5 is still under development, a lot of modern browsers support important parts of this specification, and this support increases with each new release of those browsers. Despite the fact that not all browsers support HTML5 fully, it is really the future of HTML-based applications, and therefore I use it in this book and for the Planet Wrox demo website. Don't worry about the limited browser support too much. All major browsers support all of the HTML5 features you use in this book, or support can easily be simulated by a script library called Modernizr, which you see later in the book.

# HTML Elements and Tags

HTML uses text surrounded by angle brackets to indicate how your content should be rendered (or displayed) in the browser. The text with angle brackets is referred to as a tag; a pair of tags holding some text or other content is referred to as an element. Take another look at the HTML you saw in the previous Try It Out where you opened the source window for the page in the browser:

```
<h2>Hello World</h2>
<p>Welcome to Beginning ASP.NET 4.5 on 8/31/2012 2:13:15 AM</p>
```

The first line of this example contains an <h2> element with an opening tag (<h2>) and a closing tag (</h2>). This element is used to signify a heading at the second level (if you scroll up a bit in the final source in the browser, you also see an <h1> element). Notice how the element is closed with a similar tag, but with an additional forward slash (/) in it: </h2>. Any text between these opening and closing tags is considered part of the element, and is thus rendered as a heading. In most browsers, this means the text is rendered in a larger font. Similar to the <h2> tag are tags for creating headings up to level six, such as <h1>, <h3>, and so on.

Below the heading element, you see a <p> element, which is used to denote a paragraph. All text within the pair of <p> tags is considered part of the paragraph. By default, a browser renders a paragraph with some additional margin spacing at the bottom, although you can override that behavior.

Many tags are available in HTML, too many to cover them all here. The following table lists some of the most important tags and describes how they can be used. For a complete list of all HTML elements, take a look at the website of the organization that maintains the HTML standard: www.w3.org/TR/html5/index.html.