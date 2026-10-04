![](bbox=[0.268, 0.063, 0.703, 0.396])

**Figure 25-8:** A 3D scatterplot of the famous iris1 data, displaying all five present variables with the additional use of color (for sepal length) and point character (for species).

With the creative use of color and point type, you've now been able to display the five-dimensional data in a single 3D scatterplot. This reveals important information about the data. For instance, you can identify Iris setosa as the clearly separate group of points in the foreground and that while Iris setosa tends to have smaller petal widths and lengths and larger sepal widths than the other two species (especially Iris versicolor), the purple coloring at the lower end of the scale suggests they tend to have smaller sepal lengths.

# ## Exercise 25.2

Ensure the scatterplotd library has been loaded in your current session.

a. Turn your attention back to the diabetes data frame found in the faraway package (you first looked at these data in Section 21.5.2). Your goal is to produce a scatterplotd plot of weight, hip, and waist measurements as per the following guidelines:

+   - Hip, waist, and weight variables should correspond to the x-axis, y-axis, and z-axis, respectively; provide neat axis titles.
- Use built-in functionality to ensure the 3D depth is highlighted by color.