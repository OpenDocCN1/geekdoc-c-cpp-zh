First, focus on the six configuration commands noted with white highlight boxes in Figure 13-21 as pointed to with arrows. The **interface multilink 1** command on each router creates the multilink interface on that router. The network engineer chooses the interface number, but the number must be the same on both routers, or the link will not work. Additionally, the multilink interfaces and the physical serial interfaces must all have both a **ppp multilink group 1** command, and they must all again refer to that same number (1 in this example). Any number in range could be used, but the number must match with the commands highlighted in the figure.

![](bbox=[0.16, 0.256, 0.835, 0.555])

# **Figure 13-21**  *MLPPP Configuration*