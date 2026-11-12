![](bbox=[0.38, 0.12, 0.72, 0.31])

# ## Why?

We are cutting the heads off so we can sew up the side edges of the shaft. In the game, we will see much more of the shaft than the capital of the columns. So making sure there is only one seam on the shaft makes for a better experience for the game player.

Step 11: Move the head away via UVs. Right-click again and choose UV from the hotbox. Marquee select a few UVs (that are part of the column capital - maybe the top right corner of UVs) and then Ctrl-right-click-hold (I know it's a lot) and choose To Shell (Figure 3.7). This will select the shell of UVs that make up the top of the column. Move them aside. Moving a UV shell can be done with the regular Move tool (press W to activate it) or in the Editor window choose Tool>Move UV Shell Tool and then move them aside (anywhere really).

![](bbox=[0.36, 0.58, 0.76, 0.8])

# ## Why?

What is a shell? Shells of UVs are shared UVs that share UVs, or edges. Because we cut the edges at the bottom of the column capital, the edges there were no longer shared, so when we selected a shell, it stopped there.