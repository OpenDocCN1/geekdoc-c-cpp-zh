# 22.6 The Problem with GET Requests

Periodically, a debate reemerges about the way web applications use links to trigger actions.

Here's the issue. Almost since HTTP was invented, it has been recognized that there is a fundamental difference between HTTP GET and HTTP POST requests. Tim Berners-Lee wrote about it back in 1996.13 Use GET requests to retrieve information from the server, and use POST requests to request a change of state on the server.

The problem is that this rule has been widely ignored by web developers. Every time you see an application with an Add to Cart link, you're seeing a violation, because clicking that link generates a GET request that changes the state of the application (it adds something to the cart in this example). And mostly, we've gotten away with it.

This changed for the Rails community in the spring of 2005 when Google released its Google Web Accelerator (GWA).14 a piece of client-side code that sped up end users' browsing. It did this in part by precaching pages. While the user reads the current page, the accelerator software scans it for links and arranges for the corresponding pages to be read and cached in the background.

Now imagine that you're looking at an online store containing Add to Cart links. While you're deciding between the maroon hot pants and the purple tank top, the accelerator is busy following links. Each link followed adds a new item to your cart.

The problem has always been there. Search engines and other spiders constantly follow links on public web pages. Normally, though, these links that invoke state-changing actions in applications (such as our Add to Cart link) are not exposed until the user has started some kind of transaction, so the spider won't see or follow them. The fact that the GWA runs on the client side of the equation suddenly exposed all these links.

In an ideal world, every request that has a side effect would be a POST.15 not a GET. Rather than using links, web pages would use forms and buttons whenever they want the server to do something active. The world, though, isn't ideal, and thousands (millions?) of pages out there break the rules when it comes to GET requests.

13. http://www.w3.org/DesignIssues/Axioms
14. http://radar.oreilly.com/2005/05/google-web-accelerator-conside.html
15. Or a rarer PUT or DELETE request