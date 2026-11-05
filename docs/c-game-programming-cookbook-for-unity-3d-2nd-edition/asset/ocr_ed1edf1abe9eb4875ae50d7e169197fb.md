# # 3 Building the Core Game Framework

This chapter will give context to the design decisions made in the core framework as well as providing a good base for understanding how the individual code recipes work together and why they may sometimes have dependencies on other Components.

The framework for this book (as seen in Figure 3.1) features six main areas:

+   1. Game Manager  
+      The Game Manager acts like a central communication script for all parts of the game and oversees game state.
+   2. Players  
+      Players may already be present in the game scene or instantiated by the Game Manager. The players structure will be explored later in Chapter 4 of this book.
+   3. AI and enemies  
+      As with players, AI controlled characters, or enemies may already be present in the scene at load time or created at runtime. We look at AI in full in Chapter 10.
+   4. UI Manager  
+      The UI Manager draws all the main in game user interface elements, such as score display, and lives. We look at UI in Chapter 11.
+   5. Sound Manager  
+      The Sound Manager handles sound playback. Sound is in Chapter 9.