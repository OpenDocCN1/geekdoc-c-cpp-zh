
**FIGURE 2.14:** Handoff management process

When performing an intracell handoff, it is quite possible that an MT is simultaneously receiving strong signals from multiple new base stations because of physical proximity from all of them. In such a case, some kind of signaling diversity may be used by the MT to combine the multiple signals received from those base stations, to stay connected to all new base stations. This transient situation is termed *soft hand-off*. Eventually, the MT will be handed over to only one of these new base stations as may be decided from the direction of movement of the MT and the received signal strengths. The connection with the former base station will be cleared under this situation after transferring the data packets of any ongoing call to the MT that might be buffered during the establishment of this handoff process. Also, the MT’s required resources will be allocated from the new base station and the routing path for receiving the packets of the ongoing calls will be determined. At this point, a *hard handoff* of the MT from the old base station to the new one occurs. All these steps involved in handoff management are represented in Figure 2.14 [1].

For a smooth handoff process, it is essential that when a mobile user is changing its point of attachment (base station in a PLMN or an Internet access point (AP) in a MANET or a wireless sensor network (WSN)).

# 2.4.1 Random Walk Mobility Model

According to the model proposed by Royer et al. [22], a mobile user chooses a random direction in the interval [0, 2π] and a random velocity within some range, say [vₘᵢₙ, vₘₐₓ], to make a movement from a certain point in a closed region R. When the mobile user reaches the boundary of R, it again chooses some other random direction and velocity to move from that point, and so on. Thus, this model effectively assumes obstacle-free random movement for every individual MT (or MN) leading to a uniform spatial distribution of mobile nodes within region R during any simulation run.

There are some variants of this model proposed in the literature. The first proposes that a mobile node is bounced back from the boundary when it reaches a boundary point of the region R [23, 24]. A second variant allows a mobile node to move in a randomly chosen direction at a randomly chosen velocity for a time duration which is exponentially distributed and then the mobile node will again change its direction, velocity, and duration of movement with these chosen direction and velocity.

A third variant, known as the *Gauss-Markov mobility model* [25] involves the assignment of an initial speed and a direction of movement to each mobile node. After a fixed time interval, the speed and direction of each mobile node for the next interval, say nᵗʰ time interval, are determined from the speed and direction at the previous time interval (i.e., (n−1)ᵗʰ interval) using two statistically random variables Sₓ and Dₓ (for speed and direction, respectively) that follow Gaussian (normal) distribution and some tuning parameter α, 0 ≤ α ≤ 1 that determines the relative contribution by the current status and the variability in node movement. Specifically,

the values of speed $S_n$ and direction $D_n$ at the $n^{th}$ time interval are calculated based on the values of speed $S_{n-1}$ and $D_{n-1}$ at the $(n-1)^{th}$ time interval with incremental random changes from the following equations:

$$S_n = \alpha * S_{n-1} + (1 + \alpha) * \bar{S} + \sqrt{(1 - \alpha^2)} * S_{x_{n-1}}$$  (2.1)

$$D_n = \alpha * D_{n-1} + (1 + \alpha) * \bar{D} + \sqrt{(1 - \alpha^2)} * D_{x_{n-1}},$$  (2.2)

where $\bar{S}$ and $\bar{D}$ are the mean values of speed and direction, respectively, and $S_{x_{n-1}}$ and $D_{x_{n-1}}$ are values of two random variables $S_x$ and $D_x$ at the $(n - 1)^{th}$ time interval.

# 2.4.2 Random Way Point Mobility Model

This is one of the most popular mobility models and is implemented in the $ns2$ simulator [18]. This model (also referred to as the *RWP model* in the literature) was proposed by Johnson and Maltz [23] to study the performance of the DSR protocol used for routing in ad hoc networks. Its main difference from the random walk model is that instead of choosing a random direction for movement, the mobile node chooses a destination point at random in a given region $R$. Then, with a randomly chosen velocity from a given interval, say $[v_{min}, v_{max}]$, the mobile node starts moving toward this randomly chosen destination point or *way point*. After reaching this way point, it remains stationary (pause time) for a predefined period (this is another point of difference from the random walk model), and then repeats the above steps to make another movement from that point. This RWP model also allows obstacle-free movements of individual mobile nodes in a given region $R$ which may represent the movement pattern of a person moving in a shopping complex, market place, or convention site.

Figure 2.15 is a representative diagram showing the mobility pattern according to this RWp model where \( A, B, C, D, E \) and \( F \) are different mobile terminals. The figure shows that the mobile nodes have a tendency to move across the central part of the deployment region. Several researchers [28, 29, 30] noted that the mobile nodes following the RWp model concentrate near the center of the deployment region in the long run. This is known as the _border effect_ of the RWp model. The border effect is, however, not exhibited in the random walk model.

One small variation of the RWp model has been proposed by Bettsletter et al. [29] who suggests that the pause time between the time instants of reaching the destination point and starting the next move from there can also be randomly chosen following an arbitrary probability distribution. Also, some random fraction of the nodes in the network may be allowed to remain stationary for the entire duration of interest to reflect a more practical scenario.

The above two models reflect the mobility pattern in a network where the nodes make intentional movements, with randomized direction and velocity of each move-

# 2.4.4 Map-based Mobility Model

In the above three models, nodes are assumed to be free to move around within the deployment region $R$. In this model, we assume that the nodes move only along specified paths within the region $R$. Examples of such constrained movements include driving along roads or highways and people moving along sidewalks on the streets. Thus, a road map of the region $R$ is needed in this model. The nodes will be randomly deployed on these roads and the movements of the nodes will be confined to these defined paths only. An example of a map-based model is the *freeway mobility model* proposed by Bai et al. [32] that assumes several freeways with varying numbers of lanes in both directions. Nodes will be deployed on the freeway in a random manner and they can move along these lanes in specified directions only, with randomly chosen velocities which are temporally dependent on their immediate
