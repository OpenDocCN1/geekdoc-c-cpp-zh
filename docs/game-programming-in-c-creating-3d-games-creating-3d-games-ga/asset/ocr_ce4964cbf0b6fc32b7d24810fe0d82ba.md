```
{
    mCurrFrame -= mAnimTextures.size();
}

// Set the current texture
SetTexture(mAnimTextures[static_cast<int>(mCur
}
}
```

One feature missing from AnimSpriteComponent is better support for switching between animations. Currently, the only way to switch an animation is to call SetAnimTextures repeatedly. It makes more sense to have a vector of all the different textures for all of a sprite’s animations and then specify which images correspond to which animation. You’ll explore this idea further in Exercise 2.2.

# SCROLLING BACKGROUNDS

A trick often used in 2D games is having a background that scrolls by. This creates an impression of a larger world, and infinite scrolling games often use this technique. For now, we are focusing on scrolling backgrounds, as opposed to