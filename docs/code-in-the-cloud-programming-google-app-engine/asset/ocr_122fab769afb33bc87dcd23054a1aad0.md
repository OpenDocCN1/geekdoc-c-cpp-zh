+   1. The float property can be set to either left, right, or none. left, as in our example, means that the element should be floated to the left; right means that the element should float over to the right; none allows you to “unfloat” something that inherited a float property from its class.
+   
+   2. The border property lets you draw a border around the edges of that `<div>`. It’s got the format `width style color.` style describes what the border outline should look like: it can be solid, dotted, dashed, double, grooved, ridge, inset, or outset. For this, we’ll use a simple solid outline.
+   
+   3. Small amounts of can make things look better. CSS allows you to use two kinds of space around things: margins and padding. Margins are space added outside of a `<div>` box; padding is space added inside the box.

The result of using this style is:

![](bbox=[0.118, 0.426, 0.499, 0.621])

![](bbox=[0.118, 0.774, 0.499, 0.789])

# Clears

As you can see in the screenshot, the text of the body block flows around the sidebar. It appears next to the sidebar, up to the point where the sidebar ends, and then it flows to the left margin.

We could prevent the transcript text from flowing around the sidebar by making it into a float as well. If we did that naively—just setting float: right;—what we’d get would look like this: