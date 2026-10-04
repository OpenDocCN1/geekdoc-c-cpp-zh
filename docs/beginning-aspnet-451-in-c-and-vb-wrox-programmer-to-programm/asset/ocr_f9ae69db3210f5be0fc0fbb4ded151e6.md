# SUMMARY

User controls greatly improve the maintainability of your site. Instead of repeating the same markup and code on many pages in your site, you encapsulate the code in a single control, which you can use in different areas of your site.

To improve the usefulness of your controls, you can add behavior to them. It's common to create controls with properties you can set in consuming pages, enabling you to change the behavior of the control at run time. Although View State properties solve some of the state issues you come across, you should carefully consider whether you really need them. Because these properties add to the size of the page, they can have a negative impact on your site's performance.

You can further improve the Banner control by keeping track of the number of times each image has been clicked. The Planet Wrox site doesn't implement this, but with the knowledge you gain in the chapters about database interaction, this is easy to implement.

In the next chapter you create another user control that serves as a contact form. By building the form as a user control, it's easy to ask your users for feedback from different locations in the site.

# EXERCISES

+   1. In this chapter you saw how to create a standard property and a View State property. What is the main difference between the two? And what are the disadvantages of each of them?

+   2. Currently, the DisplayDirection property of the Banner control doesn't maintain its state across postbacks. Change the code for the property so it is able to maintain its state using the ViewState collection, similar to how NavigateUrl maintains its value.

+   3. What are the two main benefits of using a custom enumeration like Direction over built-in types like System.Byte or String?

You can find answers to these exercises in Appendix A.