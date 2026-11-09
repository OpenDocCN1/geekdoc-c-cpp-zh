N13 M30
%

Assume tolerance on the 75 mm width to be tight, zero to 30 microns plus. Even with a brand new cutter, the width will be right on or slightly under. The width may be larger, too. Rather than taking a chance, use the following procedure:

+   1. Identify the normal offset value for D51.
+   2. Estimate the amount of possible error.
+   3. Temporarily increase the offset.
+   4. Cut, then measure and adjust offset.

Here are the details. For *Item 1*, the answer is 5.000 mm for a 10 mm end mill. *Item 2* needs special attention so the estimate is good. Tool quality is important — a new cutter should be within 10–15 microns. Consider this for *Item 3*: changing the offset, so the part will be wider than 15 microns. If stock size allows, you may go with 200 microns on the width. What will the temporary offset setting be?

From the original evaluation, a larger external width can be re-cut to final size. It means adding stock to the tool path by increasing offset from 5.000, but to what? Achieving the goal of width that is 200 microns larger means only 100 microns per side! The offset has to be set to 5.100, not 5.200! Upon completion of *Item 3*, D51 setting will contain a temporary 5.100 mm offset.

Next is *Item 4*. When the cutting is completed, measure the 75 mm width. It can be exactly 75.2 mm, or it can be larger or smaller. Even if the width is undersize, it still should be greater than the 75.03 maximum. If it is not, you made a mistake in *Item 2* — estimating the error amount. Let’s look at the outcomes and offset adjustments, but first you have to decide what the final width should be, for example, the middle 75.015 width. Measured sizes are only examples found on the next page: