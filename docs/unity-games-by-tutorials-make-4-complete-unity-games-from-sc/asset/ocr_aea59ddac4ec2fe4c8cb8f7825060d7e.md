# Sprite Renderer

| | | |
|---|---||
| Sprite | buzzsaw |
| Color | |
| Flip | | |
| Material | Sprites-Default |
| Draw Mode | Simple |
| Sorting Layer | Hazards |
| Order in Layer | 1 |
| Mask Interaction | None |
| Sprite Sort Point | Center |

Lastly, select the **single-block** and **top-left-small** GameObjects and change **Sorting Layer** to Foreground and **Order in Layer** to 0.

Use the **move** tool to arrange the sprites in the Scene view so they overlap slightly, like below, to check your ordering.

![](bbox=[0.293, 0.376, 0.706, 0.533])

All the sprites appear to be in the correct order. **Foreground** sprites are on top, and the **Hazard** layer is below. The **Order in Layer** setting for Soy Boy renders him in front of the blocks in spike of the fact that they share the **Foreground** layer.

The background layer is not yet there, but you can use it to add some ornamental scenery to the level. It will sit behind everything else when rendered.

# # Prefabs and Resources

Prefabs are essential to fluid gameplay. Rather than creating hundreds (thousands?) of sprites during the game, which nibbles away at processing power, Unity can use prefabs as templates to create various GameObjects on demand.

In the case of Soy Boy, you'll use prefabs to create levels. They consist of multiple copies of a base set of level blocks and shapes. Then you'll just clone these prefabs to make new levels.