The goal, in part, was to offer players a rare opportunity in the world of computer RPGs—to play a game master, in a manner somewhat similar to tabletop RPGs, crafting the game experience of other players.6 As in many other games, the quests of Neverwinter Nights are presented to the player in the form of a virtual journal.

Using Aurora, the first step in creating a quest is to begin a new category for entries in player journals, using the special purpose Journal Editor tool (shown in figure 3.1). Each entry in a category is designed to let the player know that the appropriate scripts have been activated to set the flags that are necessary for the next stage of the quest.7 For example, one could create a journal category with three entries:

+   - [0001] Grandfather had a signet ring that belonged to his own great-grandfather. But apparently no one has seen it since it was passed down to him—and it wasn't mentioned in his will.
+   - [0002] Grandma would treasure this ring with the rest of Grandpa's jewelry. But the carved symbol you've seen before at your Uncle's, so he might be interested in it as more than a memento. Of course, it also looks valuable, and you could use the money you'd get from selling it.
+   - [0003] You no longer have the ring.

Different events can trigger scripts that change the current state of the player journal. For instance, the first entry above could be added based on a conversation with the player character's grandmother, or finding and reading a letter sent to the player character's father. The same script could set a value of “true” for a flag with a name such as “lookingForRing” Dialogue trees for NPCs could be different based on this flag, offering the player the option

> 6. As noted in this chapter’s first sidebar, Neverwinter Nights is a licensed computer version of the tabletop game Dungeons & Dragons—which remains the most popular tabletop RPG, in addition to being the first.

> 7. In Aurora’s model, the current state of the quest journal is rarely queried by any part of the game system: it’s just a method of exposing information to the player and assiduously avoiding the perils of the Eliza effect.