| Display | Controls |
| :--- | :--- |
| Show the position of the look_at point | Zooming in and out (i.e., altering FOV) |
| Show the positions of the different viewports cameras in the other viewports, where visible | Panning in two dimensions |
| Render the "document" (3D model) | Rotation about three axes |
| Render world-landmarks (primary Cartesian axes, positive/negative axis directions, etc.) | Translation in three dimensions |
| Render the precise Cartesian coordinates of each salient item, at least the camera and the look_at point | Select each and every option to act upon EITHER the camera OR the look_at point OR both of them |

So, for an "editor" that lets you do nothing more than move the cameras about (and without any fancy controls for doing so; just the basics!). We have five separate things that have to be displayed and five separate sets of controls to provide. These 10 items each requires unique algorithms, and although the algorithms themselves are simple to implement, they still need to be written. Already, we have enough separate algorithms (each of which we want to maintain, update, replace, and/or remove separately) that it would be nontrivial to maintain, and we haven't yet added essential features such as object selection and basic editing.

Typical game content editors consist of perhaps 50 unique display algorithms and 30 or more control algorithms, with continuous extension. This can be a nightmare to maintain, and most editors soon become so unwieldy (in terms of both code and architecture) that adding even the simplest of functionality incurs considerable cost. This is especially hard to justify when the end consumers (players) are often not even going to see the tool.

# Users

The end users of content-editing tools are rarely the programmers. Although programmers do develop and use editors (including IDEs, of course) such tools are usually developed to make it easy for nontechnical people to create or customize content for the game. On large projects, the primary users are usually artists (creating 2D and 3D graphical content), writers (creating quests, subplots, game-logic widgets, etc.), and interpreted/proprietary-language programmers (e.g., developing AI scripts).

The main requirements for this set of users are:.

+   • A powerful, feature-rich graphical user interface (GUI)
+   • Extendible, with the ability to add new features over time (an iterative process of end users' feedback to the tools' developer(s) resulting in new functionality)
+   • Reliable; most editing should be quick and easy for the end user, and the tool(s) must be stable