# 4.4 Preprocess Phase

The preprocessing phase has two main parts—design and terrain analysis. In the design portion of this phase, we focus on identifying unique path tile types. This step is done without any coding, and it relies on full knowledge of actors and their movement rules. Designers should be prepared to define every actor rule such as prohibiting submarines from approaching shore lines, or declaring that only ninjas can climb walls. A rule only needs to be added only if it has a significant affect on an actor. For example, if movement on grass and movement on sand are the same for all actors in terms of pathfinding, then there is no need to define them as different region types. If, however, sand is illegal for a unicycle, then it needs to be its own path type.

The last part of this phase is terrain analysis, and this is where the creation of path regions occur. For an in-depth explanation of terrain analysis and it's many uses, it's strongly recommended that "Terrain Analysis in an RTS—The Hidden Giant" [3] is read before beginning any actual coding.

# Design Time

Prior to coding, it's crucial to categorize each tile into a unique pathfinding type. For example, a water tile is rarely just a water tile. A given water tile may be best classified as being part of a river, bay, deep ocean, or coral reef. To identify these regions, we determine if all actors have the same restriction for traversing or avoiding the tile. If any actor is designed with a constraint that modifies their passage across the tile, we make a new path type. Perhaps it's a difference in terrain type, or maybe there's a special rule for large actors. When this occurs, we may turn the special case rule into a unique type.

Let's see a few examples. In our effort to reinforce the army to the North, each of our soldiers has very different pathfinding