![](bbox=[0.136, 0.121, 0.882, 0.462])

# FIGURE 11.3

3x GTX290 (5 GPUs) liquid-cooled machine built at CudaDeveloper.

grow significantly from where they currently are. A typical 480/580 series card can draw up to 250 W per card. Thus, a four-card system is easily exceeding 1 kW per node. The Kepler GTX680 comes in at just under 200 W per card with the dual GTX690 managing to come in at under 300 W.

However, the GPU is not the only component in a typical high-speed workstation or server. We'll look at each one of these in turn and see how they impact the system design. The key aspect to remember in designing any system is the slowest component will limit the overall throughput no matter what speed GPUs you have.

# CPU PROCESSOR

The choice of processor is primarily one between Intel and AMD. Ignoring obsolete processors, you have a choice today of the Intel I7 series or the AMD Phenom series. Note, the Sandybridge socket 1156/1155 designs are not considered here due to the limited PCI-E lanes provided. Looking at these options, we have:

+   - Intel I7 Nehalem (Socket 1366; Figure 11.4):
+     - 4 to 6 Cores
+     - QPI-based DDR-3 triple-bank memory interface
+     - 125 W thermal design
+     - 36 PCI-E 2.0 Lanes