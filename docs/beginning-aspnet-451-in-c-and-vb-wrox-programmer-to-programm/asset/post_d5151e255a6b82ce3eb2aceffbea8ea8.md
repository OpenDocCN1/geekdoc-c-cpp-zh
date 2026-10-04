
Click OK to close the dialog box and apply the changes to the heading. You end up with the following <h1> element with an inline style in Markup View:

```
<h1 style="padding: 0; margin: 0 0 10px 0">
</h1>
```

Hi visitor and welcome to Flanet Wrox

+   5. Next, in Design View, select the first paragraph by clicking it. A small glyph appears to indicate you selected a <p> element. The Tag Selector at the bottom of the Document Window highlight the <p> element, as shown in Figure 3-18.

![](img/9e033e3b9560597824f8b22941d6d8bb_128_0.png)

+   6. With the paragraph selected, choose Format New Style from the main menu. This time, instead of creating an inline style, type the .Introduction in the Selector box. Don't forget the dot (.) from the selector's menu.

+   7. At the top of the screen, select the checkbox for Apply New Style to Document Selection. With this setting, the new class you're about to create is applied to the <p> element that you have selected.

+   8. From the style drop-down list, choose italic.

+   9. Click OK to close the dialog. Note that the entire paragraph is now displayed with an italic font.

+   10. With the <p> element selected, open the CSS Properties Grid (Figure 3-19) by choosing ▼ CSS Properties. This gives you an overview of the CSS properties and which ones are currently active for your page.

This grid shows a list of applied rules in the top part of the window in the order in which they appear. The bottom part of the window is used to show the CSS properties for those rules. In Figure 3-19 you see the rules that are applicable to the .Introduction selector.

+   11. Locate the color in the CSS Properties Grid and set it to a dark blue color, like #003399. To achieve this, open the drop-down list for the property value and choose a color from the color picker. The color you're looking for is not available, click the More Colors to bring up the extended color picker, shown in Figure 3-20.

![](img/9e033e3b9560597824f8b22941d6d8bb_128_1.png)

![](img/9e033e3b9560597824f8b22941d6d8bb_128_2.png)

*

Instead of using the color picker, you can also take a value in the Properties Grid directly. This is how many of the properties work in the CSS Properties Grid: They let you enter values directly or enable you to change the value by using a drop-list or a box with ellipses at the end of the property's value box. Figure 3-21 shows the different options you have for the font-style property in a convenient drop-list down.

![](img/9e033e3b9560597824f8b22941d6d8bb_129_0.png)

Take special note of the three buttons at the top of the window, because they use some functionalities. The first two buttons enable you to switch between categorized mode and alphabetical mode, making it easier to find the right property. The third button enables you to display the applied properties at the top of the list or at their default locations in the list.

+   12. Save all changes and open Default.aspx in your browser (You'll see that the first paragraph is displayed with a blue and italic font for the link in the text, which is red or green depending on whether you visited that before. Additionally, if you followed all the instructions from the previous chapter, the text “paying a visit” is red, set by the embedded CSS class.

![](img/9e033e3b9560597824f8b22941d6d8bb_129_1.png)

FIGURE 3-22

+   13. Switch back to VS and look at your page in Markup View. In the <head> section of the page, you should see the following embedded style sheet:

## How It Works

The numerous tools that VS make it easy to write CSS for your website. You don't need to hand code anything, or remember all the different properties that the CSS standard supports. Instead, you

## Working with CSS in Visual Studio

can simply choose them from different lists on the CSS Properties Grid. This grid enables you to enter values manually but offers handy tools to select colors, items from drop-down lists, and more.

All changes you make in the Properties Grid are applied to the relevant style sheet, whether you're working with an inline, embedded, or external style sheet. At the same time, the Design View is updated to reflect the new CSS options you have set.

When you look at the <h1> element, you can see that VS created an inline style with padding to 0 to affect all four sides at once, and margin to 0 0 10px to control all four sides individually.

Once you have created a bunch of useful and reusable styles, you need a way to apply your existing styles to other pages or HTML elements. You see how this works next.

## Applying Styles

If you have experience with Microsoft Word, you may be familiar with the Styles dialog box, which lists all available styles and enables you to select them for portions of text. You can quickly apply identical formatting to blocks of text. This works similarly in VS. With the Apply Styles window — accessible by choosing Apply Styles from the main menu — you can easily apply style rules to elements in the page.

> TRY IT OUT Using the Apply Styles

In this exercise, you will use the .Introduction class and apply it to the second paragraph of the page as well. That, both paragraphs end up looking the same.

+   1. In Default.aspx, make sure you're in Design View and select the second paragraph of the page by clicking it. Ensure that the Tag Selector at the bottom of the Document Window shows that <p> element is selected, and not another one like <strong> which is part of <p>. If you have only one paragraph of text, create a new one (by pressing Enter after the first paragraph in Design View), enter some text, and then select that paragraph.

+   Open Apply Styles by choosing Apply Styles. Make sure the window is not docked in the Document Window, either floats or is placed at the side of the Document Window. This window shows all the selectors in the current page and any attached style sheet. If you don't see all the styles shown in Figure 3-23, click the Options button and Choose All Styles.

+   3. Click the Introduction class in the CSS Styles list. VS adds a class attribute to the <p> tag:

```
<p class="Introduction">
Feel free to add a <a href="Default.aspx">around</a>; there are lots of interesting <strong>reviews and concert pictures</strong> to be found here.
</p>
```

![](img/9e033e3b9560597824f8b22941d6d8bb_130_0.png)

FIGURE 3-23

## CHAPTER 3 DESIGNING YOUR WEB PAGES

If you want to apply multiple classes, hold down the Ctrl key while clicking one of the other classes in the list. This applies a list of classes separated by a space to the element's class attribute. You can follow the same steps to apply the selected style in Markup View as well.

4. Using the Clear button, you can quickly remove existing classes and inline styles from a tag. Consider the HTML fragment you saw in the previous chapter when you used the Foreground Color button, you ended up with the toolbar to format text in the page.

```
We&#39;re glad you&#39;re <span class="auto-style*">paying a visit;</span>
```

To remove the class attribute, select the <span> tag in the Tag Selector, or simply click the <span> tag in Markup View and then click Clear in the Apply Styles window, which you can see below the toolbar in Figure 3-23. You'll end up with this:

```
We&#39;re glad you&#39;re <span>-around paying a visit
```

Because an empty tag has no use, VS removes it for you as well. In addition, VS also removes the auto-style rule because it's no longer used by any code on the page. If the Apply Styles window is empty when you click the <span> in Markup View, you may need to switch to Design View first to populate the dialog.

Removing styles from HTML elements works the same way.

## How It Works

Once again, VS is able to keep all relevant windows in sync: the Design View, Markup View, and your CSS design tools. When you apply a class from the Apply Styles window, VS adds the requested class to the selected HTML element in Markup View. It also updates the Design View. Similarly, when you remove a selector or a declaration from an embedded style in Design View, both the Design View and the CSS tools are updated.

The final CSS functionality you need to look at in this chapter is located on the Manage Styles and Apply Styles windows. Besides helping you attach CSS files to your documents, these windows enable you to manage your styles easily.

## Managing Styles

Because it's to add new inline and embedded styles, your pages may quickly become a mess with styles all over the place. To achieve reusability, you should move as much of your inline and embedded styles as an external stylesheet. This is exactly what the Apply Styles and Manage Styles windows enable you to do.

> TRY OUT Managing the Manage Styles and Apply Styles Windows

Earlier in this chapter, you modified the <h1> element and applied padding and margin to the heading. However, default.aspx is not the only page that could benefit from this style for a heading, so it makes sense to move it to the Styles.css file. The Introduction class seems reusable enough to include it in the Styles.css file so other pages can access it. This Try It shows you how to move styles around your site.
