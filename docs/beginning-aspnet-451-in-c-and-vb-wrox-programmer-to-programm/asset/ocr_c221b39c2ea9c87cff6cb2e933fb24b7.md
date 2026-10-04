# CHAPTER 2 BUILDING AN ASP.NET WEBSITE

the page in the browser as often as possible so you can check if it's going to look the way you want it. It's also recommended to test your site in as many browsers as you can get your hands on, because there may be small differences between them in the way they render a web page. The Planet Wrox website has been developed and tested against recent versions of Microsoft Internet Explorer, Firefox, Google Chrome, Safari, and Opera. You'll see screenshots of these browsers at various places in the book. In Chapter 18 you will be introduced to Browser Link, which makes browser testing a lot easier.

The Split enables you to look at Design and Markup View at the same time, as you can see in Figure 2-10.

![](bbox=[0.105, 0.303, 0.715, 0.492])

FIGURE 2-10

Split View is great if you want to see the code that VS generates when you add controls to the Design View of your page. The other way around is very useful too: When you make changes to the markup of the page in Markup View, you can see how it ends up in Design View. Sometimes Design View becomes out of sync with Markup View. If that's the case, a message appears at the top of Design View. Simply clicking the message or saving the page is enough to update the Design View. You can cycle through the three different modes using Ctrl+Page Up and Ctrl+Page Down keys.

If you want pages to open in a different view than Markup View, choose Tools Options. Then expand HTML Designer, and in the General category, select your preferred view. Alternatively, enter HTML Designer General in the Quick launch box (which you can access by pressing Ctrl+Q) at the top-right of VS and click the item in that list that appears.

> NOTE Initially, Visual Studio has two editors for markup-based files. For Forms (and User Controls, which you'll meet later in the book) Visual Studio uses the older editor shipped with earlier versions of Visual Studio. This editor supports Design View. The new HTML editor has a strong focus on code-only editing and does not support Design View. This means that you can switch to Design View for Web Forms, but not for regular HTML files. If you want Design View for HTML files as well, you can associate the .htm extension with the HTML (Web Forms) editor under Tools Options Text Editor File Extension.