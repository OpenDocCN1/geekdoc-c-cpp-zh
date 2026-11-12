# # The Aggregate method

The Aggregate method uses @import to collect all the relevant CSS files from your library. The HTML document then has to link to only a single external file ⑤.

**Pros**—Similar to the Divide and Conquer method, but by using only a single link, it's easier to add or remove styles as needed because they are in a single CSS file rather than spread out across multiple HTML files.

**Cons**—Similar to the Divide and Conquer method, but worse. This used to be a very popular CSS strategy until someone discovered that using @import often prevents external style sheets from loading simultaneously. Instead, they must load one after another, which slows things down. Additionally, since the linked parent style sheet has to load before the imported style sheets are seen by the browser, this method can lead to the page re-rendering as new styles become available.

![](bbox=[0.1, 0.535, 0.94, 0.765])

⑤ The Aggregate method uses the @import rule to bundle the style sheets into a single file that is linked to the HTML document.