A common approach is to apply a traditional AI path finding algorithm like A* to create a root motion spline, and then use another greedy algorithm to look ahead a small time interval and avoid small-scale collisions.

So far, we have considered only translational root motion for navigation. The problem of synthesizing dynamic character motion becomes even more challenging when we must solve for the motion of limbs, coordinate multiple characters, or handle deformation. This general problem is called **motion planning**, and it is an active area of research in not only computer graphics but also AI and robotics. Most solutions draw on the principles and algorithms described in this chapter. However, they also tend to leverage search and machine learning strategies that require more AI background to describe. Having motivated it, we now leave the motion planning aside. The remainder of this chapter overviews basic primitives up to motion in the *absence* of AI, with emphasis on the motion of rigid primitives.

# 35.2.4 Notation

Variables in animation algorithms are qualified in many ways. Reference frames have three translational dimensions and three rotational dimensions, all quantities are functions of time, and most quantities are actually arrays to accommodate multiple objects or vertices. The algorithms we use also typically involve first and second time derivatives, and often consider the instantaneous value before and after an event such as a collision.

Animation-specific notations address these qualifications, but they differ from the notations predominant in rendering that are used elsewhere in this book. The following notation, which is common in the animation literature, applies only within this chapter (see Table 35.1).

*Table 35.1: Formatting conventions for this chapter.*

| Symbol | Interpretation |
|---|---|
| *f(t)* | Value of a scalar function *f* of time at time *t* |
| **x**(*t*) | Vector value of a function **x** at time *t* |
| **ẋ**(*t*) | First derivative of **x**(*t*) with respect to time |
| **ẍ**(*t*) | Second derivative of **x**(*t*) with respect to time |
| *xᵢ* | Element *i* of an ordered set of homogeneous elements |
| **x**[1] | First element of a vector |
| *xᵢ* | Element *i* of an array of vectors |
| **ẋ**⁻ | Quantity immediately before an event (here, a single-sided derivative) |
| **ẋ**⁺ | Quantity immediately after an event |
| **X**(*t*) | Ideal state function for the entire system |
| **Yᵢ** ≈ **X**(*i*Δ*t* + *t₀*) | Actual state of the system at frame *i* resulting from a numerical integration scheme |

Vectors are in boldface (e.g., **x**), to leave space for other hat decorations. A dot over the **x** denotes that **ẋ** is the first derivative of **x** with respect to time. This is