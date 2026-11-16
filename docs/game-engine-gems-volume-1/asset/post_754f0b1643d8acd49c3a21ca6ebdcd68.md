
## 6.2 Design Patterns: Model View Controller (MVC)

A common problem, particularly evident with GUI systems, is that over time, last minute hacks and "temporary" bug fixes lead to strongly coupled code, leaving changes to one area of the system to cause unintended effects elsewhere and also making it difficult to refactor. The model-view-controller (MVC) design pattern aims to ensure only a loose coupling of elements by separating the framework into three distinct constituent parts to be maintained independently:

- The *model* refers to the actual data that we represent on the screen. For example, this could be the game time or the number of lives remaining.
- The *view* concerns itself only with the visual representation and rendering of that object. In our previous example, perhaps we might display an analogue clock to represent the time remaining or an icon for every life remaining.
- The *controller* refers to how the object interacts with the game, user input, and general state, system, or game logic.

MVC has gained popularity, now being a major contributing concept in many of the larger GUI and system frameworks, from Cocoa to Qt, MFC, and the current Windows Presentation Foundation.

Taking our previous timer example, the *controller* would refer to our game update loop; being responsible for determining the current time and passing a `TimerUpdate` message to the timer *model* object, which in turn updates its internal representation. The *view* will typically have its own internal description, but will update that based on information inside the *model* itself.

Implementing MVC does require a change in thinking, as the three constituent parts are unaware of the others' inner workings and unable to alter each other's data so communication relies on sending messages. This could just take the form of calling a function on another object. In larger systems, though, it is beneficial to ensure a greater distinction between components by using event queues and traditional message passing systems.

Depending on the technique used, this message passing can add a substantial amount of overhead to the system, reducing its flexibility. Choosing the correct method by which these messages are passed is crucial, and worthy of its own Gems topic.

## 6.3 A GUI Design

The goal of this gem is to present a simple and extensible drop-in GUI module whose target audience ranges from the student or smaller indie studio to the experienced professional wanting to quickly add some user interface interaction to their game without devoting too much of their time to reinventing the wheel. Therefore, the system must exhibit the following attributes:

- Modular. As a drop-in replacement, it must have the minimum possible number of external API dependencies.
- Lightweight and flexible. It should be adaptable to as many platforms as possible, have bindings to specific areas such as various input types, and rendering or audio code should be kept as minimal as possible. This guarantees the highest level of portability.
- Both programmer and artist-driven. For many smaller products, it is often feasible (if not fun) to hand-code our own front end design. While this exposes us to the dangers of localization, minor font changes, and rewordings, it can sometimes be the quickest way of creating a usable GUI. This system allows programmatically created GUI screens where necessary, and it leaves scope for data-driven designs from an external tool at a later date.
- Extensible. The code provided should give the user a solid base from which further, more advanced controls may be produced with the least amount of effort.
- Object oriented. Object-oriented programming tends to lend itself particularly well to GUI objects with inheritable behaviors and data sets.
- Localization-ready. All text rendering must be able to handle international character sets.
- "Boilerplate code"-minimizing. It should encapsulate common programming tasks so the user can concentrate on adding content rather than repetitive functionality.

### A Little Code [1]

First, let's look at the basic `GuiComponent` class shown in Listing 6.1. This is the base class from which all other GUI components are derived, and it contains very little specific information or functionality other than it is an object, it has a visual representation that exists somewhere in a hierarchy, and it has a little information about whether it is active and whether it is visible.

### Listing 6.1: Our `GuiComponent` base class.

```
class GuiComponent
{
    public:

        GuiComponent();
        virtual ~GuiComponent();

        virtual TypeId GetTypeId() const = 0;
        static TypeId GetStaticTypeId();

        uint32_t GetId() const;

        void SetupGuiComponent(const String& name, bo
        void SetVisual(Visual *visual, bool makeVisib
        void SetPosition(const Vec3& pos);

        virtual void Update(Time& timeDelta) = 0;
        virtual void Render(Renderer *renderer);

    private:

        static TypeId s_TypeId;

        String m_Name;
        uint32_t m_Id;
        Frame m_Frame;
        Visual *m_Visual;

        // Is the GuiComponent taking input and being
        bool m_Active;

        // Default to invisible false until we have a
        bool m_Visible;
};
```

The GuiComponent class contains two simple boolean variables that determine whether the object is considered active and whether it is visible. The distinction here is that an object could be visible on screen, but not active in that it does not respond to input or update itself. Likewise, an object could be actively being processed, but not visible on-screen.

A string is stored to keep a human-readable name for the object. This is largely used for debugging, but also used to generate the CRC of this name, which is stored in the m_Id variable for fast access and comparison/finding. This can also be used by tool editors and loaders for referencing objects.

The GuiComponent also contains a Frame node that specifies a local translation to apply to this object, as well as its position inside a hierarchy. This allows us to attach together GuiComponents into groups which can then be moved together as a whole.

The model contains a single pointer to a Visual object containing rendering information. I consider this to be a loose abstraction of the model and view of the object, but it serves our design goal of being quick and flexible well, meaning that it abstracts much of the rendering code away while still allowing us to have an entry point for patching any rendering information, such as state or material changes, where necessary, for those last-minute fixes. For medium-sized or larger systems, the coupling between the model and view side of the object would need to be looser. The Render() function can simply make the following call:

```
renderer->Render(m_Visual);
```

This can be overridden via virtual function in derived classes where required.

This GuiComponent class allows us to extend trivially to create a basic GuiSprite class, as shown in Listing 6.2. This simplest of examples just adds an instance of a VisualSprite class and calls the renderer to draw it. Here, the VisualSprite itself contains most of the information required to render the sprite, which is set up inside the GuiSprite::SetupGuiSprite() function. Calling the GuiComponent::SetVisual(&m_Sprite) function inside the SetupGuiSprite() function ensures that the base class render function performs all of the rendering required for objects of this type.

### Listing 6.2: A sprite class.

```
class GuiSprite : public GuiComponent
{
public:

    void SetupGuiSprite(const Vec3& pos, Texture
    Color& sprite, float width = 0.0F, float h

    virtual void Update(Time& delta);

private:

    VisualSprite   m_Sprite;
};
```

Likewise, a GuiTextItem class can be derived that stores a pointer to text and rendering parameters, as shown in Listing 6.3. In the full code sample on the accompanying CD, a BMFont class stores glyph-based information and texture data loaded from files exported from the AngelCode BMFont library [2].

### Listing 6.3: The GuiTextItem class.

```
class GuiTextItem : public GuiComponent
{
    public:

        void SetupGuiTextItem(wchar_t *text, FONT::BM
        float GetTextWidth() const;
        float GetTextHeight() const;

        void SetText(wchar_t *text);
        void SetAlignment(GuiTextHAlign hAlign, GuiTe

        void SetColor(const Color& color);
        virtual void Update(Time& delta);

    private:

        float        m_xScale;
        float        m_yScale;

        VisualText   m_VisualText;
};
```
