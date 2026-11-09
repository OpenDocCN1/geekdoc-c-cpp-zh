# Customizing links

In general, browsers display links as blue underlined text. Originally, this default behavior minimized the confusion between content on the page and an interactive link. Today, almost every website styles links in its own way. Some websites don’t underline links; others retain the underlining but style links in colors other than blue, and so on.

![](bbox=[0.122, 0.249, 0.205, 0.32])

The HTML anchor element (a) is used to create links. The text between the opening and closing anchor tag is the link description, and the URL set in the `href` attribute is the address the browser visits when the link is clicked.

The anchor tag has evolved over time and today has four states:

+   - **link:** A link that a user has not clicked or visited.
+   - **visited:** A link that a user has clicked or visited.
+   - **hover:** A link that the user hovers the mouse cursor over without clicking.
+   - **active:** A link the user has begun to click but hasn’t yet released the mouse button.

CSS can style each of these four states, most often by using the properties and values shown in Table 6-2.

**Table 6-2. Common CSS Properties and Values for Styling Links**

| Property name | Possible values | Description |
|---|---|---|
| `color` | `name` | Link color specified using names (`color: blue;`), hexadecimal code (`color: #0000FF;`), or RGB value (`color: rgb(0,0,255);`). |
|  | `hex code` |  |
|  | `rgb value` |  |
| `text-decoration` | `none` | Sets link to have and underline (or not). |
|  | `underline` |  |

The following example styles links in a way that’s similar to the way they’re styled in articles at Wikipedia, where links appear blue by default, underlined on mouse hover, and orange when active. As shown in Figure 6-6, the first link to Chief Technology Officer of the United States appears underlined as it would if my mouse was hovering over it. Also, the link to Google appears orange as it would if active and my mouse was clicking it.