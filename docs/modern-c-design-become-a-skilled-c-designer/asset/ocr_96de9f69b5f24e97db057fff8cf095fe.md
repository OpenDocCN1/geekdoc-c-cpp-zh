perfectly valid; each is illustrated in Figure 6-3.

(a) Separate input/output (b) Merged input/output

6: 5:5: 4:4: 3:3: 2: 0.037₂ 0.037 1: 101: 10

1.23e−7 1.23e−7

# Figure 6-3. Input and output display options

Choosing one style of I/O versus the other ultimately reduces to the customer’s preference. Having no particular affinity for either style, I chose a merged display because it looks more like the display of my HP48S calculator. With a display style chosen, let’s now focus on the design implications this choice implies.

With a separate on-screen widget for input and output, as seen in Figure 6-3a, the choice to have separate input and output display classes would be obvious. The input display would have slots to receive theInputWidget’s signals, and the output display would have slots to receive completed numbers (from the input display) and stack updates. The