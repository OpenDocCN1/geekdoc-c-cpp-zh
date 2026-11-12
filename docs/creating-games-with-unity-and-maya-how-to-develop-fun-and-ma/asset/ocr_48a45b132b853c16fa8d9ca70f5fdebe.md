**Step 14:** Take a break. Baking this AO pass with high-quality render settings and our high number of Occlusion rays will take a while. When the process is done, the view panel will look something like Figure 9.48.

![](bbox=[0.16, 0.19, 0.88, 0.45])

**Step 15:** Close Maya—DO NOT SAVE.
**Step 16:** Open Maya and open AegisChung.mb. He should look like he did before baking.
**Step 17:** Open the baked AO texture in Photoshop (Figure 9.49). The results of the baking process in Maya will also yield an image. This image can be found in your project file (IncurSION-Maya\VenderData\mentallay\lightmap). It will have some crazy name like bakedAO-surfaceShader1SG_AC_AegisChung. Open this image in Photoshop.
**Step 18:** Copy and paste this image into the AegisChung raw version of the texture. You can do this quickly by selecting all, Edit>Copy, then in the AegisChung raw texture Edit>Paste (it will automatically create a new layer).
**Step 19:** Make sure this layer is the topmost layer (except for the UV Guide layer).
**Step 20:** Change the Blend Mode to Multiply for this AO layer. Do this either in the Layers palette, or double-click the image and change the Blend Mode in the Layer Style window. The results can be seen in Figure 9.50.

# Tips and Tricks

Note that a blend mode of Overlay will reveal a similar result but be a bit lighter. This is largely a matter of taste and can change based upon the project. Give both a look to decide which you like better.

**Step 21:** Save a new version of AC_AegisChung_Color.psd. Be sure the UV Guide layer is shut off. Remember to not save it with Layers and remember to save it in the sourceimages folder. Back in Maya, select AC_AegisChung.