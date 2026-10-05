Because the sprite's base color is white, the new brown color fills it perfectly.

![](bbox=[0.3125, 0.1235, 0.6875, 0.2435])

> Note: You can manipulate a sprite the same way you manipulate any other GameObject in Unity. For example, you can change its scale, position and rotation using the Transform component and other Unity transform tools in the editor.

Sprites have a few different modes that you can set. You'll focus on the Single and Multiple modes.

You saw how to use sprites when you created the single-block GameObject, but what about Multiple mode sprites? They are special sprites that use a spritesheet, otherwise known as a texture atlas.

+   - **Single**: A single-image sprite.

+   - **Multiple**: A sprite with multiple elements. For instance, it might have several versions that you use to create frames — like different pages of a flipbook. Multiples may also comprise different parts, such as arms, legs and a torso.

That brings us toheets. You use them because every image in your game takes up one draw call, which isn't a big deal if you're just working with a few sprites. However, as your game grows in complexity and size, singles can cause performance issues. With spritesheets, you may just do one draw call for multiple sprites, thus reducing the cost to performance.

Super Boy uses a Multiple mode sprite so that animation state frames — running, jumping and sliding — are stored in one spritesheet.

Select the SuperSoyBoySpriteSheet.png sprite in the Sprites sub-folder make sure Sprite Mode is set to Multiple. Click Apply if you change the setting.