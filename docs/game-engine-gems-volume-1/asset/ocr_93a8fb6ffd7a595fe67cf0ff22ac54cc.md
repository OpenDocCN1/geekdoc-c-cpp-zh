being quick and flexible well, meaning that it abstracts much of the rendering code away while still allowing us to have an entry point for patching any rendering information, such as state or material changes, where necessary, for those last-minute fixes. For medium-sized or larger systems, the coupling between the model and view side of the object would need to be looser. The Render() function can simply make the following call:

```
renderer->Render(m_Visual);
```

This can be overridden via virtual function in derived classes where required.

This GuiComponent class allows us to extend trivially to create a basic GuiSprite class, as shown in Listing 6.2. This simplest of examples just adds an instance of a VisualSprite class and calls the renderer to draw it. Here, the VisualSprite itself contains most of the information required to render the sprite, which is set up inside the GuiSprite::SetupGuiSprite() function. Calling the GuiComponent::SetVisual(&m_Sprite) function inside the SetupGuiSprite() function ensures that the base class render function performs all of the rendering required for objects of this type.

# Listing 6.2: A sprite class.

```
class GuiSprite : public GuiComponent
{
public:

    void SetupGuiSprite(const Vec3& pos, Texture
    Color& sprite, float width = 0.0F, float h

    virtual void Update(Time& delta);

private:
```