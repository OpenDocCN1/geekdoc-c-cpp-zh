# ## Chapter Overview

In this chapter we will be using the character style sheet of Aegis Chung as designed and created by Jake Green to model, UV map, and texture the game character. The image is downloadable on the accompanying website (http://www.Creating3DGames.com), although you might want to use your own design if you have one that is better. Note that the Photoshop work of ensuring that the front and side images are lined up has been done and these drawings are reasonably close. So, if you are going to use your own, make sure you do the appropriate prep work.

# ## Tutorial 8.1: Game Character Modeling: Aegis Chung

As is the case in most of 3D, there are many ways to skin this cat. There are almost as many methods of organic modeling as there are organic modelers. The method we are going to use here is based upon the idea that most muscles in our face tend to ring the orifice they manipulate. There are rings of muscles around the eye and mouth. By creating polygons in rings around these objects the forms are easier to find, and more importantly, the area can deform in a more lifelike manner.

This is largely an additive method then. The method will start with a single polygon, and the additional polygons will be extruded out from that.

As always, polycount will be important. Knowing how many extrusions to make and how close to make them can be a tricky thing and is largely informed by experience. It is not too hard to go back and eliminate unwanted rings. Similarly, it is fairly easy to go back and add rings if added detail is needed. So as the forms are built, use the screenshots as a rough guide to the density of polygons, but don't sweat it.

# ### Polycount

For this character we will be aiming at the 15,000 tri mark. If there were going to be 300 of this character on the screen at a time, this is likely too high. If this is the only character to ever be seen we could probably go higher. But 15,000 is a very reasonable count with most hardware today and will allow for a good balance of efficient modeling with engaging detail.

# ### Image Planes in Photoshop

**Step 1:** Prepare resource image in Photoshop. If you are using the preprepared images contained in the downloadable files on the resource web site (http://www.Creating3DGames.com), you're set. There are four images of note: AC_Front_Body, AC_Side_Body (both full body images), AC_Front_Head, and AC_Side_Head (just head shots). If you're using your own, be sure to review the steps in Appendix C, “Preparing Character Style Sheets.” At the end, be sure to have two separate files, a Front view of the character and a Side view. Save the files that will be used for reference in the sourceimages folder.