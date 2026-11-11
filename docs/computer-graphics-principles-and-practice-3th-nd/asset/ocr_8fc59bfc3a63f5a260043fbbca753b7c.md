![](bbox=[0.105, 0.108, 0.637, 0.528])

*Figure 21.5: A photo-manipulation interface. (Top) A touch (shown by the pink dot in the shark photo) and drag (the large orange-brown arrow) moves a photo to a new location. (Bottom) Two contacts are spread apart to move and enlarge the photo. (©Thomas W. Deppner, 2010.)*

+   3. We’ve chosen to scale uniformly, even though nonuniform scaling of photos makes sense. That’s because nonuniform scaling is so much less common, and it’s so difficult to move your fingers in exactly proportional amounts, that it makes more sense to restrict to uniform scaling for convenience.

# 21.3.1 Defining the Problem

There are many possible ambiguous situations that still remain. What happens when the user starts by grabbing the upper-right and lower-left corners, and rotates these contacts to the upper left and lower right, respectively? According to rule 1 above, the picture should flip about its vertical axis to maintain contact-point correlation, but that’s a nonuniform scale, which contradicts rule 2. We in fact choose rule 3 as the dominant one, since opening and closing the fingers is much easier than rotating the hand, and so the inconsistency of contact points isn’t likely to be a problem in general.

By how much should we translate the photo during a two-finger interaction? We could translate the photo so that the first contact point remained underneath its finger, but the other perhaps did not. We could translate by the average of the