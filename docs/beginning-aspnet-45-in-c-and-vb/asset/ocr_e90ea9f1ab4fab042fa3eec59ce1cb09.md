![](bbox=[0.14, 0.13, 0.68, 0.52])

FIGURE 3-27

+   7. From the main menu, choose View ▸ Manage Styles. Again, make sure the window is placed beside the Document Window and not docked in the Document Window. Under the Current Page item, locate the `.Introduction` selector.
+   
+   8. Click the `.Introduction` selector once, and then drag it into the area for `Styles.css`, for example dropping it after the `h1` selector. Note that VS draws lines between the selectors as you hover over them to indicate the point where the selector will end up. Figure 3-28 shows how the `.Introduction` selector is dragged from the current page into `Styles.css`, between the `h1` and `#PageWrapper` selectors.
+   
+   9. Once you drop the selector in the `Styles.css` section of the Manage Styles window, the associated style is removed from your current page, and then inserted in `Styles.css`. Because that CSS file is included in your current page using the `<link />` element, you won’t see a difference in Design View. You can now remove the empty `<style>` element from `Default.aspx`, because it’s not needed anymore.

![](bbox=[0.67, 0.53, 0.92, 0.86])

FIGURE 3-28