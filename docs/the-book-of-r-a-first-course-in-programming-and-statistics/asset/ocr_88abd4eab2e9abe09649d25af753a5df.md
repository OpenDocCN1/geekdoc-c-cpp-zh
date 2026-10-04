# 24

# GOING FURTHER WITH THE
GRAMMAR OF GRAPHICS

![](bbox=[0.166, 0.463, 0.355, 0.599])

You covered the basics of the ggplot2 package—which offers an alternative to traditional R graphics—in Section 7.4 and throughout Chapter 14. In this chapter, you'll look at a couple of this package's more popular and useful features, as well as its relatively young cousin, ggvis, which provides an interactive, browser-based experience.

# 24.1 ggplot or qplot?

So far when creating the relatively simple ggplot graphics, you've used the qplot function to initialize the visual object. In fact, the more general ggplot command is the core function of ggplot2. There are several key differences between these two initialization functions:

+   - qplot is a shortcut version of ggplot; it's used if you just want a quick look at your data or if you're working directly in the R console.