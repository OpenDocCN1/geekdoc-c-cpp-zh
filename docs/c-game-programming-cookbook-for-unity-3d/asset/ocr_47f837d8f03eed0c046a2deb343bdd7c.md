they can do with them." With this approach, Apple stores attempted to convey the lifestyle just much as the product, using clear layout and styling to reinforce the key themes of the experience, such as using natural materials to bring a more earthy, organic feel to their casual and clutter-free open plans.

Just like the exterior and layout of a high-end store, your menus and interface can affect how people feel about the game "inside." The unthinkable graphics, or a difficult menu flow can frustrate players before the game starts, leading to a heightened sense of frustration during initial gameplay. Anpolished interface may lower expectations or change the perception of quality of work that has gone into the game. We want to avoid these situations and set the user to feel as good as possible. To encourage a positive start, we should try to make sure that menu systems are tidy and functional, and they attempt to reinforce the main themes of the game world in every aspect.

If you look at most modern videogames, the menus and screens are filled with little touches that developers would notice, like particle effects, transitions, and animations. Most games have dedicated teams for building the menus and interface systems. Artists work hand in hand with developers to build new experiences. All this (sometimes 2D and 3D) comes at a cost, and it may take months of work for just the main menu screen of a commercial title.

Some studios reuse their menu and interface code from game to game, changing the layout and graphics but keeping the underlying code and/or structure. Reuse of menu code makes a lot of sense in an industry where we need to pack in as much gameplay possible and where customers demand a lot more bang for their buck.

The menu system we will be building in this chapter will not be winning awards or enticing players to play. But it will serve as a structural beginning and a functional method for configuring the example games and getting them started. The great thing about this menu is that it's completely open to interpretation. It could be built out for just about any kind of game with the addition of some graphics and sounds. As you develop your games and your style, having an operational menu will help during testing.

The main menu system is used by all of the example games in this book. It is easy to port between games and have submenus for audio and graphics options. The full screen flow for the entire main menu and its submenus is shown in Figure 10.1.

The flow requirements are almost identical for each game, although there are a few that need to be variable. These are

+   1. Game name.
2. Which scene to load when we start the game button.
3. The filename of the prefs we save to store options (volume and graphics levels).
4. In the case of Interstellar Paranoia, the menu needs to have a Start Co-Op Game button, too.

Options menu use PlayerPrefs to save and load any information we need to store or retrieve related to audio and graphics settings. The menu code should check to see