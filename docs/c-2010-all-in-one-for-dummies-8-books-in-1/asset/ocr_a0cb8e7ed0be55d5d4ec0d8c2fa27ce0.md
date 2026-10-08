# 710 Mastering Master Pages

![](bbox=[0.248, 0.125, 0.859, 0.435])

Figure 5-4:
Making a header.

# # Adding content

You won't believe how simple adding content is. You see, the master page is something that the content page adheres to, not something you have to inject content into it. You just have to make pages like usual, and they will drop them themselves in that content placeholder. Follow these steps to add content:

+   1. Right-click on the Web site, and select Add New Item.
2. Click on Web Form (the master page is probably still selected) and name it Home.aspx.
\   Wait! Don't click Add yet!
3. Check the Select Master Page check box in the lower right-hand corner.
4. Now you can click Add.
5. You can select which master page you want — as shown in Figure 5-4. We have only one, so click it under Contents of Folder.
6. Click OK.

Notice how different the template content of the page is now that you have a master page. Visual Studio krew how to handle this! There are no HTML headers or footers, because VS knows they are in the master page.