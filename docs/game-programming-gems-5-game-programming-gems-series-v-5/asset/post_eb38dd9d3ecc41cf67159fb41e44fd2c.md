
## Expanding Smoke

The expanding smoke is another secondary effect that occurs after the flash, flares, and core. It happens at about the same time as the fireball and generally overlays on top of all the previous effects. Starting at 0.1 seconds, about 30 to 50 smoke particles shoot from the center of the explosion (as seen in the fifth column of Color Plate 8A). The particle's texture should be a light gray smoke cloud with lots of billowing detail. The alpha channel should have a cloudlike density and amorphous shape.

The smoke effect is fairly important to the explosion since it will expand the farthest and linger the longest. There is no cheap way to create the smoke effect, especially since it provides the cover for the cheap core and fireball effects, masking their simplicity. Even with the expensive core and fireball, the smoke needs to be rather detailed to sell the effect. Many game explosions ignore smoke, but it is a rather convincing detail.

As the smoke shoots out of the center, it will use the same basic technique as the fireball. Each particle will shoot in a random direction with a very high velocity and exponential decay. Each particle should start out stretched in the direction of its velocity and then relax into the shape of a square over time as shown in Figure 5.6.4. After about 0.3 seconds, the smoke should begin to fade out very slowly (slower than the fireball step).

During the course of each smoke particle's lifetime, it should be carried by the wind and thermal buoyancy just like the core and fireball. However, there is one more effect that can add a nice touch. Normally, smoke has lots of billowing and interesting turbulence. This can be caricatured by rotating the smoke particles. The trick is to determine the wind direction as projected by screen space and rotate the particles to simulate subtle vorticity. All smoke particles on the left side of the wind direction should rotate counterclockwise, and all smoke particles on the right side of the wind direction should rotate clockwise, as shown in Figure 5.6.5. The rotations should be very slow, and each particle should have a different randomly determined angular velocity.

![](img/672fe9a2d008ba627b1991e15d70f43e_605_0.png)

FIGURE 5.6.5 Faked rotational turbulence based on the wind and thermal buoyancy direction.

## Debris

No explosion would be complete without debris flying from it. The debris can be embers, small dark chunks of dirt/metal, pieces on fire leaving smoke trails, or whole pieces of whatever just blew up. The debris should be given a high initial velocity and should not decay like the other gaseous effects. Instead, the initial velocity coupled with gravity should drive its motion.

Dark debris is quite effective, since it has a high contrast with the explosion itself. A cartoonish look can be achieved by having chunks of debris give off smoke trails as they sail away from the explosion. Usually these smoke trails give off smoke particles that start off hot white and change over time to yellow, orange, light gray, then finally dark gray. Of course, these smoke trails require rendering of even more particles, so the effect has to be used judiciously to maintain acceptable performance.

## Effects Table

The previous effects involved many precise timings, velocities, and forces. Table 5.6.1 lists each effect with all the relevant data so that you can easily compare and recreate the explosion effect. Referring to Color Plate 8A will also help you understand the precise timing of each effect.

Table 5.6.1 Comparison of the Timings, Velocities, and Forces Involved for Each Effect

| Effect | Particles | Start Time (sec) | Fade Up | Fade Down | Scale Up | Outward Velocity | Other Forces |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Initial Flash | 1 | 0.0 | quickly | very quickly | very quickly | none | none |
| Radial Flares | 10 to 30 | 0.0 to 0.2 | instantly | quickly after 0.1 seconds | none | none | none |
| White Hot Inner Core (cheap) | 1 | 0.0 | instantly | very slowly after one second | quickly with exponential decay | none | wind and thermal buoyancy |
| White Hot Inner Core (expensive) | 100 | 0.0 | instantly | very slowly after one second | none | very fast with exponential decay | wind and thermal buoyancy |
| Intense Fireball (cheap) | 1 | 0.1 | instantly | slowly after 0.3 seconds | quickly with exponential decay | none | wind and thermal buoyancy |
| Intense Fireball (expensive) | 50 | 0.1 | instantly | slowly after 0.3 seconds | slowly until square | very fast with exponential decay | wind and thermal buoyancy |
| Smoke | 30 to 50 | 0.1 | instantly | very slowly after 0.3 seconds | slowly until square | very fast with exponential decay | wind and thermal buoyancy |
| Debris | 10 to 100 | 0.0 to 0.2 | instantly | depends | none | fast with exponential decay | gravity |

## Extra Touches

The billboard effects presented so far will create a nice explosion, but the following extra touches can help make the explosion really come alive.

### Randomness

While this article presented a great deal of timing information for start times, fading rates, and velocities, the entire effect is much more effective if each particle is unique and isn’t in lockstep with the others. Randomness should be used to tweak all these times, rates, and velocities, but it helps to keep the randomness within narrow ranges. Most of the particles need to behave similarly, so the randomness shouldn’t introduce any large variations.

### Screen Shake

When a powerful explosion takes place, the perceived intensity can be amplified by briefly shaking the camera up and down (not left and right). Not every explosion might warrant this effect, but close or powerful explosions will certainly be enhanced by the brief shaking.

### Efficiency Concerns

There are several efficiency concerns that are raised when many explosion effects occur at the same time. The following explains how to deal with three such concerns.

### Controlling the Number of Particles

In a game, it is typically difficult to control how many near-simultaneous explosions occur at a time, due to the unpredictability of the players or AI. Therefore, the cost of each explosion effect should be relatively small since the cumulative cost can skyrocket quickly. Not only must each particle be updated every frame, but all particles from all explosions must be sorted on the CPU in order to blend correctly with the frame buffer. As more particles are drawn, the sorting cost will rise exponentially.

The explosion effect described in this article showed how to make a cheap white hot inner core and a cheap fireball in order to limit the number of particles. The cheaper explosion effect uses about 43 particles (not including debris). The more expensive explosion effect uses about 230 particles (not including optional debris) and has considerable overhead, which can be expensive for the GPU.

Choosing whether to use cheap or expensive explosions is one way to limit particles, but an equally important technique is to put a hard limit on the number of drawn particles and recycle the oldest ones when the limit is about to be hit. For example, a limit of 1,000 particles may be imposed so that the fifth overlapping explosion will start to recycle particles from the first explosion. Since the first explosion is probably far into its lifetime and already fading out, the removal of these older particles is generally not noticeable, especially since new explosions are very distracting to the eye.

### Optimizing Billboard Orientation

During gameplay, it might be common to see half a dozen simultaneous explosions represented by thousands of particles. Each particle must recalculate its orientation in order to face the camera each frame. This represents some serious computation, but it isn't necessary or even desirable.

Within a single explosion, if each particle faced the camera based on its center point, the particles would intersect with each other and cause ugly artifacts. Therefore, the particles within an explosion must all be oriented in the same direction. The solution is for each spawned explosion to have a single center point that travels with the explosion during its lifetime (affected by wind and thermal buoyancy). This orientation can be calculated once per frame for each explosion. All particles belonging to a given explosion then use this same orientation, reducing the number of orientation calculations from over a thousand to less than a dozen.

### Sorting Particles within Framerate Constraints

With thousands of potential semitransparent particles, all must be sorted with respect to the camera so that they can be rendered properly. Unfortunately, this task falls on the CPU, so efficiency is a major concern.

It is well known that the quicksort algorithm is ideal for this type of sorting, taking on average O(n log n). However, the time that quicksort takes can fluctuate wildly each frame, even up to O(n^2) in the worst case. This can be a big problem for games that are trying to maintain a fixed or respectable framerate.

One solution is to use a sorting algorithm that can be stopped after taking a specified amount of time, thus ensuring that it will never take too long. Obviously, this will cause some artifacts, as not all particles are properly sorted on every rendered frame, but this is a concession that may be acceptable in practice. The chosen algorithm must be incremental in that whenever the sorting is interrupted, the list is more sorted than when it started. Since explosions stay confined to small areas and don't move quickly, the sorted list of particles will be relatively unchanged from frame to frame.

One sorting algorithm that can solve the problem is the infamous bubblesort. This very simple sorting algorithm is well known to perform poorly, but it has two nice properties. First, it can steadily sort a list and be interrupted at any time while leaving the list intact and partially sorted. Second, if the list is sorted, it can escape early with as little work as O(n). Therefore, the bubblesort algorithm can be capped, for example, to never take more than 3% of the frame time.
