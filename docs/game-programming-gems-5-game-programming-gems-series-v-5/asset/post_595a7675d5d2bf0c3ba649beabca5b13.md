
A fully heads-up aware and capable editor is a step forward for users for the following reasons:

- Automation. Eliminates the need for manually changing tools all the time (the cursor changes automatically according to context, simultaneously switching tools as appropriate).
- User-interface simplification. Most of the little icons on toolbars can be removed, since the user no longer needs to select them manually.
- Learning curve reduction and productivity increase. Learning how to use the editor takes much less time because it automatically presents the user with the correct tool, saving the user from having to hunt for it in a menu, toolbar, or elsewhere.

But it gets better: heads-up editing can be implemented with a very simple architecture that makes maintenance and extendibility much easier for the developers, staving off bit rot almost indefinitely. The proposed architecture forces all new features to be added as fully encapsulated modules, preserving existing code and making components easy to replace in the future.

## Implementation

The implementation of the solutions covered thus far is broken down in a number of areas: acetates, renderers, and tools. We'll also discuss details in sharing code between components.

## Acetates

To the user, we present a conceptual model of acetates on an overhead projector (OHP) as seen in most conference and lecture rooms. Each acetate is merely a transparent sheet of plastic, which the lecturer can insert, remove, or edit independently of the others. Each acetate contains one or more diagrams or text, and the grouping is arranged to keep the number of acetates as small as possible (easier to manage) while allowing however fine a granularity the lecturer needs to rapidly change diagrams. Often the contents of a particular acetate make no sense on their own (for instance a set of disembodied arrows), but when placed in the context of the other acetates, they suddenly become meaningful.

With real acetates, it is easy to reorder them, to twist or translate individual layers, to hide and reveal sections, etc. This particular approach has proven very powerful, because it gives the user (the lecturer) the ability to instantly change the information being displayed in many ways: the user can very rapidly add or remove content and easily simplify or add more detail.

Our software approach is to build a system of layers, where each layer is akin to an acetate. Like acetates, each layer is transparent and overlays the main data (viewport); i.e., each layer is a HUD. However, unlike acetates, our layered HUDs have much richer control options, mainly because we have much more power with a computer GUI. Furthermore, each layer has one or more control modes (a.k.a. tools) associated with it; for instance, “translate selection” and “rotate selection.” This turns each layer into an encapsulated context-sensitive HUD with associated editing modes.

## Renderers

The main editor viewport is just like a traditional editor. It shows the current document being edited, where the document may be a textual document, a 3D model, or any arbitrary rendered data. The document is the set of data on the screen that is saved or loaded as opposed to being part of the GUI/editor. The main viewport displays nothing else; everything else will be handled by HUDs (and this can provide a convenient means for the user to see exactly what will be saved, without mistaking a HUD-applied tint on a texture as part of the model plus texture that will be saved. All they need to do is turn off all HUDs and they will then have a “What You See Is What You Save.”

Where the document itself is particularly complicated, you may even render only part of the document in the core renderer and do the rest in HUDs. For instance, some 3D model formats save the vertex data, the texture data, the bones, and the animation all in one file. You can get an editor up and running quickly by implementing only the vertex reading and rendering in the core renderer, and later adding a separate HUD/layer for each more advanced element, without needing to alter your existing code. If there are any bugs in the texture renderer, for example, the user can always simply disable that layer and carry on viewing the vertex renderer as if they were using an early version of the editor.

Each HUDs renders itself transparently on top of the editor viewport. As with acetates, some careful planning is required to divide up the desired visual features (selection highlighting, etc.) into HUDs, although generally it is better to have more HUDs rather than fewer.

The user has a simple tool for choosing which layer they are editing in, and wizard actions may programmatically select a queue of layers, transferring the user automatically from one to the next in order to complete the editing task.

This may sound familiar to the layers of modern paint programs: individual independent layers, with user actions constrained to only those they explicitly choose at any given moment. This interface should be immediately familiar to most artists. The main difference is that we are using acetates for the actual GUI, whereas paint programs typically use layers for isolation of content (make changes only in one layer) and for composition of content (e.g., blending to a background is very hard to undo once done, so compositing temporarily via layers makes things much easier; it acts like an instant preview without permanently committing the author to the current composition).

## Tools

Each tool is either allotted a unique acetate of its own or shares one belonging to a display element (and zero or more other tools). If you are unsure, it is safest just to have one tool per acetate.

## Shared Code and Extending the Context

Dividing the code up into one or more classes per HUD presents some problems with duplication of code. This is a natural side effect of attempting to make the HUDs as independent of each other as possible. However, code duplication could easily undermine the ease of maintenance, and so we definitely want to avoid it if possible.

Most of the code that typically gets duplicated is common display code, not tool code, such as x, y, and z coordinates of a point. It is duplicated because in any particular editor, the different tools tend to display or affect exactly the same information, although in different ways. This is fortunate, because it means we can safely encapsulate that code in a single HUD renderer, introducing only a very narrow dependency of each tool on that one single renderer (i.e., they are not dependent upon each other in any way).

A better long-term solution is to completely avoid the dependency by making rendering X a fundamental feature of the renderer (where X is some information that will be set at different times in different ways by different tools). We do this by supplementing our definition of context, which was originally just cursor position, to also include the current value of X. We also need to supply at least one HUD that queries that aspect of the context and renders it. One of the advantages of doing it this way is that you can have multiple different HUDs rendering that context at once in different ways (different formatting, different details, etc.) and leave it to the user to decide which they want to see (using the show/hide HUDs controls).

For example, if you have multiple tools that need to pop up the (x, y, z) coordinates of a point or for a vector, the context can be supplemented with a field current point, which the tools will fill whenever appropriate, and then assume that one of the HUDs will render it for them.

## Source Code

There are two main elements to the source implementation, regardless of the windowing system you are using: a HUD manager and the individual HUDs themselves (all of which are of the same type).

The HUD manager is a Model in MVC (Model, View, Controller) terminology: it has data-structures containing references to all the current HUDs and has methods for adding or removing HUDs programmatically. It also keeps track of the state of the GUI (e.g., managing the HUD stack, described in the “User Controls” section).

All HUDs are implementations of a template/interface that provides callbacks for things like triggering rendering to a suitable surface (i.e., painting the HUD to a back buffer) and for feeding in GUI events (e.g., mouseclicks).
