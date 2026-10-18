![](bbox=[0.14, 0.12, 0.87, 0.66])

# FIGURE 12.6

Scalar volume data generated from RF simulation results. By capturing detailed information about the full path generated for each transmitter sample, StingRay enables computation and visualization of signal characteristics that are extremely costly, or even impossible, with other RF simulation methods. Here, RF energy characteristics are visualized using traditional volume rendering (top) and as a participating medium (bottom).

# OPTIMIZATION EXAMPLES

Ray tracing applications are often parallelized by exploiting task-level parallelism among rays. For example, in ray-based rendering, pixel color calculations are embarrassingly parallel: the computations along each ray are independent of those required by every other ray. In the same way, each path traced from a transmitter in RFRT is independent of every other path.