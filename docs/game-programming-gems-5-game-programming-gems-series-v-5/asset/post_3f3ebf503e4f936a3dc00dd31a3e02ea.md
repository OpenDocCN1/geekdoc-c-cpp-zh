
By encapsulating all the logic for a particular HUD into one class, we make it easy for the developer to add/remove HUDs from the editor and to alter existing ones without having to edit more than one source file at a time. Obviously, a particularly complex tool may itself consist of many classes, but the logic to activate that tool and render the interactive HUD parts is all in one place.

![](img/672fe9a2d008ba627b1991e15d70f43e_54_0.png)

The implementation given on the CD-ROM is simplistic, but should be easy to extend as you desire. The HUD manager is net.machine.ggp.hud.HUDManager. The interface/ADT for HUDs is net.machine.ggp.hud.HUD and the base abstract class (contains some common methods) is net.machine.ggp.hud.BaseHUD. A demo application is in net.machine.ggp.hud.HudDemo (which is run automatically if you try to run heads-up-editor.jar).

## User Controls

There are three aspects to the users' interaction with the heads-up editing system:

- Interactive, heads-up selection of which tool to use
- Activation and de-activation of individual HUDs (and their tools)
- Peeking at the internal state of the heads-up editing system

## Tool Selection

One HUD is a proxy for a set of other HUDs and tools. This HUD will have many context-sensitive rendering features, including an activation symbol for each and every HUD for which it is proxying. For instance, if it proxies for a translate object, a rotate object, and a stretch object, it will have icons that appear for each within suitable activation areas (e.g., the translate icon is activated while the cursor is inside the bounds of an object, rotate is activated when the outside object is within 10 pixels of a corner, and stretch is activated when the outside object is outside 10 pixels of a corner but inside 10 pixels of any edge).

LMB on an activation area delegates to the other HUD + tool mapped to that area, placing the current HUD + tool on a stack. When the delegated tool is finished, it automatically pop the activating HUD + tool. This allows arbitrary nesting of proxying HUDs, which is good for extremely complex editing situations but also allows one HUD/tool to be invoked from several different contexts, without needing to be context aware, or having to be re-implemented with almost identical code once for each different context.

## HUD Activation

To manage the different HUDs, we simply copy the standard layer palette from high-end paint programs. This is a well-established form of GUI—with which many users will already be familiar—that shows all the layers in order as a list, with controls to show/hide any particular layer and allow the layers to be dragged and dropped to reorder them in the list.

With our HUDs, reordering can be useful since it controls which HUDs are over-painting which other HUDs; with this feature, the user can usually resolve any paint conflicts on screen, keeping the underlying code simple. Otherwise, the individual HUDs would need to interact with each other so that they could avoid overlapping so as to negotiate use of screen space; e.g., to reserve particular screen regions for painting in.

The show/hide feature is used just as in a paint program: hiding a HUD simply turns off its painting code. This may be done to reduce clutter on the screen, to increase rendering performance, or simply because the user doesn't need a particular HUD during the current session. Since HUDs are persistent and identical across editing sessions (unlike layers in a paint program, which are ephemeral and tied only to the current document), a helpful feature in particularly complex heads-up editors is the ability for the user to quickly save and restore particular patterns of hidden HUDs. A particularly neat way of doing this is to create a tab along the top of the dialog for each saved preset of hidden HUDs, with the user providing a name for each preset when creating them. This allows extremely fast switching between different editing modes, in keeping with the aim of the user being able to do most of his work with minimal navigation of dialogs, menus, toolbars, etc.

## Internal State

This serves two nonobvious purposes. Since the internal state of the system can arbitrarily mask out tools that would otherwise be available, it's often important for users to understand what they've selected mid-selection (e.g., if they make a mistake and select the wrong element they typically won't know what they clicked on, only what they intended to click on), and this acts as a navigation map. Secondly, it makes debugging much easier, since users can easily quote the situation they got into, rather than the developer having to guess or examine log files. This is especially helpful in that it empowers users to avoid particular situations that are subject to outstanding bugs; if they know that a certain part of the "map" causes crashes, it's easier to avoid ending up there.

## Conclusion

This gem has shown how a simple editor design can give more power to the users and simultaneously make life easier for the developers. This is a virtuous circle that reduces stress all around: developers spend less time getting tangled up in unmaintainable code, and users spend less time waiting for seemingly simple (yet deceptively complex) features to be added.

Organizing your editor around HUDs keeps it very flexible in terms of features: adding a new feature is rarely difficult, thanks to the independence of individual HUDs. At the same time, the editor is effortlessly able to simultaneously run alternative implementations of the same control: both run at once, and the user runs them on/off in real time as desired. This allows you to experiment more easily with unusual features or new ideas for the editor, at a low development cost.

However, it doesn't go much beyond the basics of what can be achieved with heads-up editing (HUE). There are many ways this gem could be extended to provide far greater support for HUE, although most of these require considerable extra programming and are not to be attempted lightly. The core support presented in this gem is easy to develop and maintain, while providing most of the benefits.

![](img/672fe9a2d008ba627b1991e15d70f43e_56_0.png)

Errata and updates for the source on the CD-ROM will be available from [Martin04]. The supplied code is minimal, but a library free for both commercial and personal use is being built on top of it, and later versions and improvements will be available free on that site.

## References

- [Eclipse04] Eclipse. Available online at http://eclipse.org, 2004.
- [Martin04] Martin, Adam, et al. Java Games Factory, "Libraries and Code Snippets." http://grexengine.com/people/adam/gps5/ and http://grexengine.com/sections/externalgames/.
- [Popa99] Popa, Adrian. "Re: How Does a Heads-Up Display (HUD) Work on the Aircraft?" http://www.madscifi.org/posts/archives/jul99/931328936.Eg.r.html.

## 1.2

## Parsing Text Data in Games

### Aurelio Reis

AurelioReis@gmail.com

Most games require a vast amount of text data to be read and interpreted. From scripting languages to shaders, the text must most often be taken from a standardized format and converted to binary data structures the program can use natively. In this gem, we examine the creation and usage of a tokenizer: the module responsible for converting textual data into discrete units, ready for interpretation and consolidation into valid game information.

### Before We Start

For clarification, a token is sometimes referred to as a lexeme, and the tokenizer the lexical analyzer (a word analyzer). We will use the terms token and tokenizer for this gem. Many free tokenizers are on the Internet, and you should check them out, particularly one of the more popular tokenizers, Lex (with Yacc) [Lex & Yacc], which is open source and can function as a valuable learning tool. Tokenizer and parser theory is an enormous field, and this gem will not attempt to cover every last facet. Instead, the purpose of this gem is to serve as an introduction and explanation on the usefulness of a tokenizer in game production, and how to approach implementing and using one in a practical manner. For more information on the history and theory behind tokenizers and parsers, there is a “References” section at the end of this gem.

### So What Is a Token, Anyway?

A token is basically an indivisible grouping of characters used to represent individual basic symbols. Basically, it is a grouping of characters that form a special “word.” As an example, examine the small C++ program segment in Listing 1:
