![](bbox=[0.12, 0.08, 0.92, 0.27])

We'll define event binding by specifying the event within parentheses. We bind it to a method in the component that we'll call onClick. Next, we write the onClick method in the component. The method has no return type, so we specify void. For now, let's log a message to the console every time the user clicks on the stars. Here, I'm using ES2015 backticks to specify a JavaScript template literal. A template literal allows us to use a placeholder to insert an expression within a string. In this expression, we display the product rating.

![](bbox=[0.12, 0.58, 0.92, 0.8])

Bring up the browser and open the developer tools. Then let's clear the default Filter by so we have more products. Click on a product, and we see the star rating logged to the console. Click another product, and we see its star rating.