# An Introduction to ASP.NET 4.5.1 | 15

Both options work, as long as you use the same type of quote on both ends of the value. For values that don't contain a space, you can also leave out quotes:

```
<input value=yes>
```

It's sometimes necessary to nest single and double quotes. For example, when some special .NET syntax requires the use of double quotes, you should use single quotes to wrap the attribute's value:

```
<asp:Label ID="TitleLabel" runat="server" Text='&#x; Eval("Title")' />
```

You will see this a lot in later chapters in this book.

For consistency, this book uses double quotes where possible in all HTML that ends up in the client, as this is generally the accepted standard.

# Nest Your Elements Correctly

When you nest elements, make sure that you first close the inner element you opened last, and then close the outer element. Consider this correct example formats a piece of text with both bold and italic:

```
<strong><em>This is some formatted text</em></strong>
```

Notice how the <em>tag is closed before the <strong> tag. Swapping the order of the closing tags leads to invalid HTML:

```
<strong><em>This is some formatted text</</strong></em>
```

# Add a DOCTYPE to Your Page

A DOCTYPE gives the browser information about the kind of HTML it can expect. By default, VS adds a DOCTYPE for HTML5 to your page:

```
<!DOCTYPE html>
```

The DOCTYPE greatly influences how browsers like Internet Explorer render the page, if you're seeing odd behavior on your page, check that your page has the DOCTYPE.

You can view the complete HTML5 syntax rules at the W3C at www.w3.org/TR/html-markup/syntax.html.

Besides HTML, an ASP.NET web page can contain other markup as well. Posts may have one or more ASP.NET Controls to give them some additional functionality. The next section briefly touches on these ASP.NET Controls work, but you get an in-depth look at them in Chapter 4.

# A First Look at ASP.NET Markup

To extent, the markup for ASP.NET Server Controls is similar to that of HTML. It also has the notion of tags, elements, and attributes, using the same angle brackets and closing tags as HTML does. One big difference is that the ASP.NET tags start with an asp: prefix. For example, a bton in ASP.NET looks like this:

```
<asp:Button ID="Button1" runat="server" Text="Click Me" />
```

Note how the tag is self-closing with the trailing slash (/) character, eliminating the need to type a separate closing tag. If you wanted to, you could use a separate closing tag, though.