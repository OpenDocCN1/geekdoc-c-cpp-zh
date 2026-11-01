# TRY IT OUT Creating a User Control

In this exercise, you create a basic user control that displays a single vertical banner using an Image control. In later exercises, you see how to use this control in your pages and how to add another (horizontal) image.

For this exercise, you need two images that represent banners—one in portrait mode with dimensions of roughly 120 x 240 pixels, and one in landscape mode with a size of around 486 x 60 pixels. The Resources folder for this chapter's code download that comes with this book has these two images, but you could also create your own. Don't worry about the exact size of the images; as long as they are close to these dimensions, you should be fine.

+   1. Open the Planet Wrox site in VS.
+   2. If you haven't done so already, create a new folder called Controls in the root of the site. Although user controls can be placed anywhere in the site hierarchy, placing them in a separate folder makes them easier to find and manage.
+   3. Create another folder called Images at the root of the site.
+   4. Using File Explorer (Windows Explorer on Windows 7), open up the Resources folder for this chapter (at C:\BegASPNET\Resources\Chapter 08 if you followed the instructions in the introduction of this book). If you haven't done so already, you can download the necessary resources from www.wrox.com. Drag (or copy and paste) the files Banner120x240.gif and Banner486x60.gif from File Explorer into the Images folder you created in step 3. If you're using your own images, drag them into the Images folder as well and give them the same names.
+   5. Right-click the Controls folder and choose Add ▸ Add New Item. In the dialog box that follows, choose your programming language, click Web User Control, and make sure that Place Code in Separate File is checked, as shown in Figure 8-1. Name the file Banner and then click Add to add the control to the site. Notice how VS adds the extension .ascx for you automatically if you don't type it in. VS does this for all file types you add through the Add New Item dialog box so you don't need to type the extension yourself. Your Solution Explorer should now look like Figure 8-2.
+   6. Switch the user control to Design View and drag a Panel from the Standard category of the Toolbox onto the design surface. Using the Properties Grid, change the ID of the Panel to VerticalPanel.
+   7. From the Toolbox, drag an Image control into the Panel. Select the Image and then open the Properties Grid. Locate the ImageUrl property and click its ellipsis button, shown in Figure 8-3. Browse to the Images folder, select the Banner120x240.gif image, and click OK to add it to the user control. Your Design View now looks like Figure 8-4.
+   8. Using the same Properties Grid, locate the AlternateText property and type This is a sample banner. Most browsers display the alternate text (rendered as a client-side alt attribute) only

![](bbox=[0.68, 0.6, 0.9, 0.92])