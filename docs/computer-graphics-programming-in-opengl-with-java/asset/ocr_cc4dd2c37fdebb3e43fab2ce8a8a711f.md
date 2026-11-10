# ## Exercises

3.1 Modify Program 2.5 so that the vertex shader includes one of the buildRotate() functions from Program 3.1 and applies it to the points comprising the triangle. This should cause the triangle to be rotated from its original orientation. You don't need to animate the rotation.

3.2 *(RESEARCH)* At the end of Section 3.4 we indicated that Euler angles can in some cases lead to undesirable artifacts. The most common is called "gimbal lock." Describe gimbal lock, give an example, and explain why gimbal lock can cause problems.

3.3 *(RESEARCH)* One way of avoiding the artifacts that can manifest when using Euler angles is to use *quaternions*. We didn't study quaternions; however, JOML includes a Quaternionf class. Do some independent study on quaternions, and familiarize yourself with the related JOML Quaternionf class.

# ## References

+   - [CR86] C. Crivelli, *The Annunciation, with Saint Emidius* (1486), in the National Gallery, London, England, accessed July 2020, https://www.nationalgallery.org.uk/paintings/carlo-crivelli-the-annunciation-with-saint-emidius
+   - [EU76] L. Euler, *Formulae generals pro translatione quacunque corporum rigidorum* (General formulas for the translation of arbitrary rigid bodies), Novi Commentarii academiae scientiarum Petropolitanae 20, 1776.
+   - [FV95] J. Foley, A. van Dam, S. Feiner, and J. Hughes, *Computer Graphics—Principles and Practice*, 2nd ed. (Addison-Wesley, 1995).
+   - [KU98] J. B. Kuipers, *Quaternions and Rotation Sequences* (Princeton University Press, 1998).
+   - [TR15] T. Reed, OpenGL Part 3B: Camera Control (blog). Accessed March 2021, https://www.trentreed.net/blog/qt5-opengl-part-3b-camera-control
+   - [WB15] W. Brown, LearnWebGL (2015), chapter 8.2 (Orthographic Projections), Accessed March 2021, http://learnwebgl.brown37.net/08_projections/projections_ortho.html