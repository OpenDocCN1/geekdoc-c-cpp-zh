
If you notice that the text on your PC looks significantly smaller than the text in the book, make the screen text larger. Keep in mind, though, that the same font size can appear to be larger or smaller on screens with lower or higher resolutions.

Of course, if you're creating content for a cell phone, the situation reverses. People typically hold their phones reasonably close to their eyes, so you can get away with smaller font sizes.

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_55_0.png)

*Pick a readable typeface.* There is a great difference in legibility between different typefaces and even between different members of the same type family. Choosing a good typeface matters.¹⁵

## Takeaway Points

- Avoid text if you can.
- If you can't avoid text, keep it succinct, clear, and scannable.
- Keep paragraphs short, and convey one idea per paragraph.
- Be engaging and personal, rather than boring and professional.
- Use pictures to illustrate your points and make your text look more approachable.
- Use large font sizes and readable typefaces.

> 15. Note that studies show that whether a typeface has serifs or not probably doesn't make a difference in terms of legibility. If you are interested in reading studies on this topic, you can find out more at http://www.alexpoole.info/academic/literaturereview.html.

## Further Reading

Jakob Nielsen has a number of good essays on the topic of writing for the Web.16 If you're writing a manual, Patricia Wright's Quality of Technical Documentation [SJ94] contains a ton of useful information. Joel Spolsky tackles reading in User Interface Design for Programmers [Spo11].

Science author Carl Zimmer has written an essay about good science writing.17 Tim Radford has compiled a set of rules for good writing based on his experience as a journalist.18 If you're interested in good writing in general, I really liked Stephen King's On Writing [Kin00].

You should also read Angela Colter's essay on testing content.19

- 16. At http://www.useit.com/papers/webwriting/.
- 17. At http://blogs.discovermagazine.com/loom/2011/01/12/death-to-obfuscation/.
- 18. Read the rules at http://www.guardian.co.uk/science/blog/2011/jan/19/manifesto-simple-scribe-commandments-journalists.
- 19. At http://www.alistapart.com/articles/testing-content/.

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_57_0.png)

## Chapter 7

## Hierarchies in
User Interface Design

In thinking about how websites are organized, you’ll find that they often make use of hierarchies. Sometimes, these hierarchies are even used as explicit user interface elements. Here is an example of a “breadcrumbs” navigation element as it appears on sites like Google Directory:

## Software

Science > Biology > Bioinformatics > Software

This navigation element tells people where in a hierarchy the current page is and allows them to “jump up the hierarchy.”

The headers of many news sites also show a hierarchy of sorts but often use two or three levels of tabs instead of breadcrumbs:

| U.S. | World | Europe | Technology | Business | Science | Opinion |
| Africa | Asia | Middle East | Japan | | | |

These two examples show how whole websites or products in general can be organized into hierarchical structures. But the individual screens themselves also use hierarchies to structure their content. Check out this screenshot from Google’s Chrome browser:

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_58_0.png)

This is a very simple user interface, but even so, it implies a hierarchical structure. For example, buttons inside a tab only apply to other things inside that tab. If you hit the “back” button, anything outside of the currently active tab won’t be affected. But if you hit the window’s “close” button, the whole window will be closed, including both open tabs. Buttons affect only things that are on the same or on a lower hierarchical level.

### 7.1 Creating Hierarchical Structure Visually

If you look at any user interface, usually you can discern a hierarchy of user interface elements relatively quickly. Most Western users understand intuitively that hierarchies go from left to right, from top to bottom, and from outside to inside. Here are several examples showing representations of A hierarchically above B:

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_58_1.png)

For example, take an MP3 player that shows the currently playing track of an audio book. How would you arrange the following elements: track number, chapter number inside a track for audiobooks, or podcasts with chapter markers, and the playhead’s current position in the chapter? Obviously, the relationship between these elements is as follows:

Track→Chapter of current track→Playhead position in current chapter

Here's how this is arranged in the iPod app on iPhones:

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_59_0.png)

The chapter number and track number are shown in “reverse” order, with the current track's chapter number appearing above the track number:

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_59_1.png)

This visual arrangement implies the following, wrong hierarchy:

Chapter of current track→Track→Playhead position in current chapter

This trips me up every time and makes me think that the number next to the playhead is the chapter number, rather than the track number.

The Audible app for iPhones solves this problem by not showing the track number at all and moving the chapter number next to the playhead, which fixes the misleading arrangement:

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_59_2.png)

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_61_0.png)

Interacting with a user interface element shouldn't affect things that are placed above it in the visual hierarchy.

Hierarchies are everywhere, and they affect how people expect your product to behave. By using hierarchies properly, you can give people hints that allow them to figure out how to use your product.

## Takeaway Points

- Think about how the elements of your product can be arranged hierarchically.
- Use hierarchies to give your users hints about how your product works. Individual screens convey implicit or explicit hierarchies to the user.

## Further Reading

What most people call “organizing things,” designers call *information architecture*. There are a number of great books on the topic. Donna Spencer has written one called *A Practical Guide to Information Architecture* [Spe10]. The book *Information Architecture for the World Wide Web* [MR06] by Peter Morville and Louis Rosenfeld is another good place to get started.

## 8.1 Designing Hierarchies

In the previous chapter, we saw that products are often organized using hierarchies. Here’s another example.

Open any website, and it’s likely to be arranged in a hierarchy. Let’s say your laptop’s internal camera doesn’t work anymore, and you need help. You open the manufacturer’s website in your browser. Where do you go to find help? If your computer is from a big electronics manufacturer, you probably start by clicking “Computers” and then “Notebooks.” Here you’ll see a list of laptop lines from your manufacturer. Clicking the proper line of notebooks should take you to a list of laptop models, and you should be able to find yours in that list. On the page for the specific model, you’ll probably look for “Support.” Ideally, this will show a support page for your model, with a number of potential laptop issues. With some luck, you’ll find your problem and a solution to it in that list.

Here’s the path you took through the site’s hierarchy:

Computers → Notebooks → Notebook Line → Notebook Model → Notebook Model Support → Answer to a specific question

But that’s not the only way you could have arrived there. You could also have gone straight to the Support section of the website. The question is, if you are designing this website, how do you know what path the user will take? And how do you know where people expect to find the individual pages of your site?

## Card Sorting

A common way of finding answers to these questions is to use card sorting—a great way to determine where people expect to find things. Card sorting is really easy. In her book *Card Sorting: Designing Usable Categories* [Spe09], Donna Spencer explains that “at its core, card sorting is a pretty simple technique—write things on index cards and ask people to sort the cards into groups.”

Of course, there are nuances, so let’s look at some of the details of how to do this.
