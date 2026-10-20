# 16 Implementing an “Infinite Scroll”

Gmail introduced us to infinite scroll, spelling doom for pagination in a number of scenarios. Many people (certainly not all, though) find it more efficient to scroll through a boatload of items and use visual pattern matching rather than pointing to and clicking pagination link after pagination link.

Pagination mostly arose for technical reasons alone:

+   - Older browsers render slowly, forcing us to keep our pages “light enough.”
+   - Bandwidth may be limited anywhere between client and server, encouraging us to stay lean.
+   - Server-side processing time grows as the data grows. Rendering the entire dataset all at once is not only unnecessary from a consumption standpoint but is infeasible for our servers (or at the very least impractical and unwieldy), especially if they want to keep handling enough concurrent requests.

Still, pagination was just one way—the non-JavaScript way. But as soon as JavaScript is enabled, you can hide any pagination links and replace them with infinite scroll when that makes sense. I leave that decision to your usability experts—and to your good sense.

As you can see on the facing code, infinite scroll is nothing too fancy. The only tricky part is jumping through a couple of hoops to get our metrics right, across browsers, as evidenced in the lowEnough() method code.

We check, essentially, that the bottom of the document is not too far below the bottom of our viewport. Then it’s just a matter of looking at the current state of vertical scrolling often enough—ten times per second is certainly snappy!—and loading more content through Ajax.

From an accessibility (and failover) perspective, you may want to also offer pagination and perhaps hide Next links at setup time and then restore these links if your Ajax fetching fails so users get an alternative.

A note for those of you without a working PHP setup handy: you’ll just end up loading more stuff instantaneously; the PHP code simulates load time by waiting half a second before returning static content.