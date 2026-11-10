![](bbox=[0.235, 0.078, 0.736, 0.419])

FIGURE 9.3  (*See color insert.*) Phasor clustering example.

Figure 9.3 gives the results of the clustering algorithm for a set of mode phasors drawn from the example data. Here, each measurement device yields one phasor. The clustering algorithm proceeds to identify those forming coherent groups by classifying them according to the direction in which they point. In Figure 9.3, each group is identified by a separate color, with the group centroid given by the dashed line of the same color.

# 9.3.4 Visualization of Modal Extraction Results

A visualization package was developed to display the results from the preceding modal identification procedure. This visualization is based on a geographic display that gives the mode amplitude and phase at each measurement point. These phasors are placed on the map so that the coherent groups can be observed spatially. This visualization architecture was used to generate movies that run across a given oscillation to present the graphics over time such that the temporal evolution can be observed in real time. One such movie is represented in Figure 9.4 by a series of frame captures. This movie was constructed from a dataset centered on the example case used throughout this section.

Figure 9.4(a) gives a movie frame from before the event and demonstrates a region with very little oscillatory content. The plot at the top of