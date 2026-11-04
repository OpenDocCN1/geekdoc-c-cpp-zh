# Chapter 19: Developing Silverlight Applications

Figure 19-59 shows the organization and hierarchy of the various controls. Those controls correspond to the controls listed in Figure 19-58.

![](bbox=[0.38, 0.2, 0.7, 0.55])

Figure 19-59

The most delicate part of the media player is the slider used to indicate the progress of the media playback. As shown in Figure 19-60, the slider (canvasProgress) consists of two Rectangle elements and an Ellipse element. The first Rectangle element (rectProgressWell) represents the entire duration of the movie. This control also forms the path that the marker (ellMarker, an Ellipse element) slides on. The second Rectangle control (rectDownloadProgress) is used to indicate the percentage of the media downloaded from the remote server. The lower part of Figure 19-60 shows this control in action (partially filled).

![](bbox=[0.28, 0.85, 0.75, 0.98])

The progress bar in action:

Figure 19-60