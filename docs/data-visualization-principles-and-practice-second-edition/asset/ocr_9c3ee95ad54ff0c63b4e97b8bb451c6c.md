graph nodes or edges (for streaming graphs) or keyframes (for sequence graphs) are provided to the visualization "on the fly," and have to be accommodated in the image drawn. This scenario is important when not all data are available at a given moment. This class of techniques is also known as online techniques. Online techniques are in general considerably more complicated, as they cannot make provisions for what next will change in the graph dataset.

Several methods exist for the visualization of both streaming and sequence graphs, as follows.

*Visualizing small numbers of keyframes:* Arguably the easiest task is to show changes between just two keyframes in a sequence graph. Given two such keyframes G' and G'', let us first assume that G is a tree rather than a general graph. In this case, we can start by showing the node correspondence relation c_node(u \in V', v \in V''), as follows (Figure 11.24(a)). First, we draw both hierarchies of the graphs G' and G'' using two horizontal icicle plots. These plots are identical to the ones used for the hierarchically bundled edges presented earlier in this section, with the difference that the plots are now linear rather than circular. Next, we connect nodes u \in V' and v = c_node(u) \in V'' which are linked by correspondence relations. Next, we bundle the correspondence edges using the hierarchical edge bundle (HEB) technique. Compared to the application of

![](bbox=[0.23, 0.6, 0.92, 0.83])

Figure 11.24. Visualizing two keyframes (a), respectively six keyframes (b) in sequence hierarchies.