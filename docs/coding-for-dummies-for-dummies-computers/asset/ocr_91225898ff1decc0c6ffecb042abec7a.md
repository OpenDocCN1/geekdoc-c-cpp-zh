+   - Styling specific HTML elements based on position to other elements.
+   - Naming HTML elements, and only styling elements by name.

# ### Styling specific elements

When styling specific elements, it is helpful to visualize the HTML code as a family tree with parents, children, and siblings. In the following code example (also shown in Figure 7-4), the tree starts with the html element, which has two children head and body. The head has a child element called title. The body has h1, ul, and p elements as children. Finally, the ul element has li elements as children, and the p element has a elements as children. Figure 7-5 shows how the following code appears in the browser, and Figure 7-6 shows a depiction of the following code using the tree metaphor. Note that Figure 7-6 shows each relationship once. For example, in the code below there is an a element inside each of three li elements, and Figure 7-6 shows this ul li a relationship once.

```
```html
<html>
  <head>
    <title>Figure 7-3: DOM</title>
  </head>
  <body>

  <h1>Parody Tech Twitter Accounts</h1>
  <ul>
    <li>
      <a href="http://twitter.com/BoredElonMusk">Bored Elon Musk</a>
    </li>
    <li>
      <a href="http://twitter.com/VinodColeslaw">Vinod Coleslaw</a>
    </li>
    <li>
      <a href="http://twitter.com/Horse_ebooks">Horse ebooks</a>
    </li>
  </ul>

  <h1>Parody Non-Tech Twitter Accounts</h1>
  <p><a href="http://twitter.com/SeinfeldToday">Modern Seinfeld</a></p>
  <p><a href="http://twitter.com/Lord_Voldemort">Lord Voldemort</a></p>

  </body>
</html>
```
```

![](bbox=[0.13, 0.82, 0.19, 0.89])

Bored Elon Musk is a parody of Elon Musk, the founder of PayPal, Tesla, and SpaceX. Vinod Coleslaw is a parody of Vinod Khosla, the Sun Microsystems co-founder and venture capitalist. Horse ebooks is a spambot that became an Internet phenomenon.