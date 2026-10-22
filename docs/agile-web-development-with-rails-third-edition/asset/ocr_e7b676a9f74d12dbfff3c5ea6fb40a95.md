field to a cart item, does that change ripple through the code?) Can you find a way to further reduce coupling?

+   - What happens if you click the Checkout button in the sidebar while the checkout screen is already displayed? Can you find a way of disabling the button in this circumstance? (Hint: variables set in the controller are available in layouts and partials as well as in the directly rendered template.)
+   - The list of possible payment types is currently stored as a constant in the Order class. Can you move this list into a database table? Can you still make validation work for the field?

(You'll find hints at http://pragprog.wiki dot.com/rails-play-time.)