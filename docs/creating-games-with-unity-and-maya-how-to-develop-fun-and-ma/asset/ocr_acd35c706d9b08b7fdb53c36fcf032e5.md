+   - **Step 20:** Save and return to Unity. Fix syntax.
+   - **Step 21:** Attach this new DamagePlayerScript to the Trigger-WaterKiller GameObject in the Hierarchy.
+   - **Step 22:** Select Trigger-WaterKiller and in the Inspector under the Damage Player Script component, define the Damage Amount as 10.
+   - **Step 23:** Test and play. Jump in the water and stay there. Watch the Health meter at the top and see how it drops by 10 every 2 seconds. Eventually, the Console will throw an error because you'll be dead, but Unity won't know of any Scene-ClosingFall scene.
+   - **Step 24:** Save Scene-EntryWay.
+   - **Step 25:** Open Scene-Hallway.
+   - **Step 26:** Deactivate Hallway_Unbaked and activate Hallway_BakedGroup.

# **Why?**

I know, you're probably sick of turning these off and on, and it would have been great if the tutorials were set up so we never had to do that but alas, with the concepts we're exploring this little annoyance is necessary to allow ideas to build upon each other.

+   - **Step 27:** Create a new trigger that fits into the area between all the stairs (Figure 17.8). This needs to be very accurate because if it's too big the player will hit it running down the stairs and die, but if it's too small, he might be able to fall all the way to the ground without hitting the trigger. Name the trigger Trigger-FallDeath.

**FIGURE 17.8** Trigger-FallDeath.

![](bbox=[0.32, 0.61, 0.8, 0.825])

# **Why?**

There are different ways to handle a character falling to his death. Some are more interesting than this one and can include timing how long a character is not grounded and is falling. Others simply measure how far a