Of all these warnings, the most important is undoubtedly Treat Warnings as Errors. This forces you to clean up your code and get rid of all your warnings. This is a very good habit to get into. As frustrating as it may be, you really want to clear out all warnings. Otherwise, you may overlook something truly important one day.

Trust me, nothing’s worse than compiling someone else’s code and watching a steady stream of warnings scroll by. You get that sinking feeling in the pit of your stomach. Are these serious issues that need to be resolved, or are they trivial matters that you can simply ignore? Do everyone a favor and fix your warnings.

This brings up another point. Not all developers will follow this advice. You will find that some third-party libraries may trigger hundreds of warnings. As always, it’s better to be pragmatic and finish a project than to be dogmatic and proud of yourself. If you have to turn off one of the warnings to move forward, then turn off the warning.

# ## ADDING IMAGES

We will need icons for our tab buttons. These are a little odd. They need to be 30 by 30 PNG files (60 by 60 @2x.png files for phones with the Retina display). The actual color of the image does not matter; the tab-bar icons just use their alpha level. For this reason, I find it easiest to draw the icons in black on a transparent background. If I want shading, I change the opacity of the black ink. That way, the image I see in my graphics application will at least be close to what I get when I load the icon.

Feel free to create your own icons. Alternatively, you can just download the source code from www.freelancemadscience.com/source and copy over the artwork. Right-click the Images group, and select Add Files to “Health Beat.” Make sure the “Copy items into destination group’s folder (if necessary)” checkbox is selected. Then select graph.png, graph@2x.png, plus.png, and plus@2x.png from the downloaded code. Click Add.

The plus icon will be used on our tab for entering new weights. The graph tab will be used for our graph view (surprise, surprise). We will use a built-in icon for the history view, so it doesn’t need any additional artwork.