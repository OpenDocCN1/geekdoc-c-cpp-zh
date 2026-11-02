drag and drop, and layouts. Optimizing item rendering then follows in the last section of this chapter (and applies to FlipView and ListView). First, however, let me answer a very important question.

# # When Is ListView the Right Choice?

ListView is the hands-down richest control in all of Windows. It's very powerful, very flexible, and, as we're already learning, very deep and intricate. But for all that, sometimes it's also just the wrong choice! Depending on the design, it might be easier to just use basic HTML/CSS layout or the WinJS.UI.Hub control, as we'll see in Chapter 8.

Conceptually, a ListView is defined by the relationship between three parts: a data source, templates, and layout. That is, items in a data source, which can be grouped, sorted, and filtered, are rendered using templates and organized with a layout (typically with groups and group headers). In such a definition, the ListView is intended to help visualize a collection of similar and/or related items, where their groupings also have a relationship of some kind.

With this in mind, the following factors strongly suggest that a ListView is a *good* choice to display a particular collection:

+   - The collection can contain a variable number of items to display, possibly a very large number, showing more when the app runs on a larger display.
+   
+   - It makes sense to organize and reorganize the items in various groups.
+   
+   - Group headers help to clarify the common properties of the items in those groups, and they can be used to navigate to a group-specific page.
+   
+   - It makes sense to sort and/or filter the items according to different criteria.
+   
+   - Different groupings of items and information about those groups suggest ways in which semantic zoom would be a valuable user experience.
+   
+   - The groups themselves are all similar in some way, meaning that they each refer to a similar kind of thing. Different place names, for example, are similar; a news feed, a list of friends, and a calendar of holidays are not similar.
+   
+   - Items might be selectable individually or in groups, such that app bar commands could act on them.

On the flip side, opposite factors suggest that a ListView is *not* the right choice:

+   - The collection contains a limited or fixed number of items, or it isn't really a collection of related items at all.
+   
+   - It doesn't make sense to reorganize the groupings or to filter or sort the items.
+   
+   - You don't want group headers at all.
+   
+   - You don't see how semantic zoom would apply.