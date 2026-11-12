# # Tile Map Renderer

A tile-based video game is a type of game or video game where the playing area consists of small square (or, much less often, rectangular, parallelogram, or hexagonal) graphic images referred to as tiles laid out in a grid. That the screen is made of such tiles is a technical distinction and may not be obvious to people playing the game. The complete set of tiles available for use in a playing area is called a tile set. Tile-based games usually simulate a top-down, side view, or 2.5D view of the playing area, and are almost always two-dimensional.

Much video game hardware from the late 1970s through the mid-1990s had native support for displaying tiled screens with little interaction from the CPU. [24]

You can already have an idea of how we are going to implement this feature in our engine. If you remember in section (0), we spoke about the fact that each tile would be an entity with a tile component. The tile map itself is also going to be an entity with a tile map component. So, let’s create both components.