

请注意，`GuiTextItem` 类仅接受宽字符字符串来显示文本。这些多字节字符使我们能够显示多种语言的字符，尽管各种平台可能会进行字节序交换。两个函数根据文本和字体获取文本的计算宽度和高度。当我们想要允许使用指针设备选择一段文本时，这将很有用。

## 扩展我们的系统

不幸的是，GUI 系统需要执行的操作不仅仅是显示精灵和文本，因此让我们来看看添加另一个重要类 `GuiSelectable`。如清单 6.4 所示，`GuiSelectable` 类是菜单项、可点击图标、可选择文本以及任何可能被高亮和/或选择的内容的父类。此类的目的是提供一个响应两项主要活动的界面——被高亮（例如，当用户将鼠标、触控笔或其他指针设备指向组件上方时）和被选择（例如，当指针设备在此项上单击或按下“选择”按钮时）。所使用的设备类型无关紧要，因为高亮和选择是屏幕导航中常见的操作，无论是通过键盘、手柄、触控笔/触摸屏控制器、远程指针设备等进行的。

### 清单 6.4：可选择组件的基类。

```
class GuiSelectable : public GuiComponent
{
    public:
        bool IsSelectable() const;
        virtual void SetSelectable(bool selectable);
        bool IsHighlightable() const;
        virtual void SetHighlightable(bool highlightable);
        GuiHotSpot *GetHotSpot();
        void SetHotSpot(GuiHotSpot *hotSpot);

        // Process what to do when the user's focus is
        // in the specified position.
        virtual bool SetFocus(float x, float y);

        // Test to see if the specified position is within
        virtual bool IsInHotSpot(float x, float y);

        // Virtual function called when the item is selected
        // whether it is possible to select this item
        virtual bool OnSelect();

        // The GuiSelectable is highlighted
        // (mouseover, menu item selected).
        virtual bool OnHighlight(bool highlighted);

        virtual void Update(Time& delta);
    private:

        GuiHotSpot     *m_HotSpot;

        bool           m_Highlightable;
        bool           m_Selectable;
};
```

`GuiSelectable` 对象包含对 `GuiHotSpot` 项的引用，该项保存了屏幕区域的信息，单击该区域会使 `GuiSelectable` 对象变为活动状态。通常，这是一个与项本身的图标或文本大致相同大小的矩形区域。派生类可以描述自己的圆形或多边形区域，只要重写 `IsInside()` 虚函数即可。`GuiHotSpot` 对象保留对 `Frame` 对象的指针，以便该对象随 `GuiComponent` 对象本身一起跟踪。

对于基于指针的设备，确定 `GuiSelectable` 对象的高亮状态是通过将当前屏幕光标坐标传递给 `SetFocus()` 函数来实现的。如果在查询 `m_HotSpot` 变量后，确定应更改高亮状态，则会使用新的所需值调用虚函数 `OnHighlighted()`。同样，我们可以在派生类中重写此虚函数以更新其自身状态，因此也更新其视觉表示。

对于基于按钮的控制器（主要是键盘和手柄/摇杆），焦点可能更具定制性，也许是通过按 Tab 键在各种可高亮组件之间转移焦点，或者在菜单的情况下，使用输入设备上的方向键。我们稍后将再次讨论此话题。

可以告知 `GuiSelectable` 对象它们不可高亮。在此状态下，除非再次明确设置为可高亮，否则它们无法像其他 `GuiComponent` 对象一样变为活动状态。这最可能用于那些当前不可用或尚未可用的组件。例如，可能有一个当前隐藏的游戏模式选项。

同样，即使某些项可高亮，也可能无法实际选择它们。例如，也许在关卡选择屏幕上将光标移动到当前不可用的最后一关会高亮或动画化该组件，但用户仍然无法选择它。被选中的对象会调用 `OnSelect()` 虚函数，该函数返回选择是否成功。随后由当前状态进行处理。

## 那菜单呢？

好吧，我们已经能够随意在屏幕上放置对象，但将这些项目放入菜单中不是更好吗？登场的是 `GuiSelectableGroup` 类，如清单 6.5 所示。可以将 GuiSelectableGroup 对象视为菜单，其中包含构成其菜单项的 GuiSelectable 对象指针集合。这使我们能够将高亮和选择对象组的通用代码移至单个界面。在最简单的情况下，GuiSelectableGroup 类允许我们按数组索引、按 GuiComponent 名称或按 ID 高亮对象。它还允许我们简单地高亮当前组中的下一项或上一项，如有需要，可跳过不可高亮项并循环遍历列表。

### 清单 6.5：GuiSelectableGroup 处理许多 GuiSelectable 对象的选择。

```
class GuiSelectableGroup : public GuiSelectable
{
    public:
    // Add item and set the attached item's m_Frame
    virtual void AddItem(GuiSelectable *item, bool);
    // Remove all items from list and detach any
    virtual void Clear();
    // Highlight the next/previous item skipping
    // items and wrapping where necessary.
    virtual bool HighlightNext();
    virtual bool HighlightPrevious();
    // Highlight an item in the list by index,
    // or Id (name CRC).
    virtual bool HighlightIndex(int index);
    virtual bool HighlightItem(const String& name);
    virtual bool HighlightItem(uint32_t id);
    // Find an item in the GuiSelectableGroup either
    // or Id (name CRC)
    virtual int FindItemIndex(uint32_t id);
    virtual int FindItemIndex(const String& name);
    virtual GuiSelectable *FindItem(uint32_t id);
    virtual GuiSelectable *FindItem(const String& name);

    // Get the currently highlighted object (if there is one)
    GuiSelectable *GetHighlighted();

    virtual bool SetFocus(float x, float y);

    // Test to see if the specified position is within
    // the GuiComponent's HotSpot.
    virtual bool IsInHotSpot(float x, float y);

    // Virtual function called when item is selected
    virtual bool OnSelect();

    // Virtual function called when the GuiSelectable
    // (mouseover, menu item selected).
    virtual bool OnHighlight(bool highlighted);

    // Update all the items in this GuiSelectableGroup
    virtual void Update(Time& delta);

    private:
    // A static-sized array of pointers to GuiSelectable
    GuiSelectable *m_Selectables[GUI_SELECTABLE_MAX];
    int m_NumSelectables;
    int m_Highlighted;
    bool m_Wrapped;
};
```

通过 `AddItem()` 函数将项添加到 `GuiSelectableGroup` 对象，该函数提供自动将新项的 `Frame` 附加到此对象的选项。如果用作菜单，这种附加意味着菜单中的所有项可以一起移动，也许只需动画化根节点矩阵的 x 分量，即可将项动画显示到屏幕上或从屏幕上移除。还要注意，在向空列表添加项后，如果我们想要高亮某一项，仍然希望手动执行此操作，或调用 `HighlightNext()` 来高亮第一个可用项。这对于基于控制台或键盘的控制系统很典型。

该类符合 *组合* 设计模式，因为 `GuiSelectableGroup` 类本身派生自 `GuiSelectable` 类。这种简单但强大的区别意味着它继承了可被选择、可被高亮的能力，并且重要的是，可以作为列表包含在另一个 `GuiSelectableGroup` 对象中。这在许多情况下很有用——例如，在选项屏幕中，主项垂直排列，通过手柄的上/下键选择，但某些项提供多个选项供选择，例如为图形细节选择低、中或高，为声音选择立体声或单声道等，这些选项水平排列。

在符合组合设计模式时，`GuiSelectableGroup` 类还负责管理通过 `GuiSelectable` 虚函数的调用。`Update()` 和 `Render()` 调用会传递给所有包含的 `GuiSelectable` 对象，`OnSelect()` 函数确定当前高亮的项，并且（如果存在且活动）仅对该项调用相关的 `OnSelect()` 函数。`OnHighlighted()` 和 `SetActive()` 等函数遵循类似模式，尽管值得浏览代码以了解对象何时变为活动或非活动的详细信息。

## 使用示例

