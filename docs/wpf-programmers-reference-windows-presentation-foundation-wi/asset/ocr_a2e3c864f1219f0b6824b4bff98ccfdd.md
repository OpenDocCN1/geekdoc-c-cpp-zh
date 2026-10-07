# CHAPTER 16 THEMES AND SKINS

![](bbox=[0.093, 0.098, 0.573, 0.258])

FIGURE 16-6

The following sections describe skins and explain several ways you can implement them in WPF.

> HARD WORK WARNING
Be warned that skinning takes a lot of work! Depending on the technique you use, it may not be very complicated, but it can be very time-consuming.
WPF provides many tools for creating attractive user interfaces, it's easy to spend hours fiddling with control properties and arrangements, trying to build the world's most beautiful interface. Now multiply that to provide multiple skins, and you could end spending days on a window instead of “only” hours.

# Skin Purposes

Usually skins are mostly decorative, changing the application colors, button shapes, form designs, background images, and forth. The skins shown in Figures 16-5 and 16-6 look very different but only superficially. They still use the same controls in the same positions.

Others are often decorative and used to increase a program’s “coolness factor,” multiple skins can have legitimate business purposes.

In example, in the United States, 8 percent of men and 0.4 percent of women have form of color vision deficiency and thus trouble distinguishing among certain colors. If your application provides multiple skins, users can change the colors or shapes used by the program if they have less trouble identifying the information.

In addition, as the general user population ages, applications must be made to help older users. Larger fonts, menus, buttons, and other components can make understanding and using an application easier for users. Providing multiple skins with different element sizes also allows users with larger screens to take advantage of the space they have available.

One for skins that is usually overlooked to make different interfaces use the same application for different purposes. For example, suppose you’re writing an order entry system. Different kinds of users would need to see different pieces of an order at different times.