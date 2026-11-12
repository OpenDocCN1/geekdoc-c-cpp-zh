![](bbox=[0.331, 0.103, 0.949, 0.526])

*FIG. 8.7 Generate Lightmap UVs Will Autounwrap Your Mesh and Create a Second Set of UVs for Lightmapping*

# ## Autogenerate UVs

We've discussed the importance of creating appropriate UVs for lightmapped objects; however, you can choose to autogenerate UVs upon import in the FBX Importer Settings as shown in Fig. 8.7. This is a great time-saver, as you no longer have to worry about creating a second set of UVs for lightmapping in your 3D program. If you already have a second UV set, then Beast will use it in lightmapping process.

The Advanced Settings, as can be seen in Fig. 8.7, are for controlling the unwrap process in order to minimize the distortions that we discussed earlier in the section, "Correct Lightmap UVs," of this chapter. For example, Area Error will help to ensure that the scale between the UVs and the actual mesh geometry remains proportional to each other as shown in Fig. 8.5.

# ## The Process

The process of lightmapping is very straightforward in Unity iOS. To begin, the objects that are to be lightmapped must be marked as Static, which also make them available for Static Batching as shown in Fig. 8.8.