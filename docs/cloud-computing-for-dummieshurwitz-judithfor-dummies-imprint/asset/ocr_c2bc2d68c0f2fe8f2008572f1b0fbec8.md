Therefore, before any part of the data center moves to the cloud, it needs to be separated from dependencies that already exist. For a gradual move into the cloud, the full inventory of applications and systems needs to be considered in terms of which ones *must* — or at least *should* — move together. The interdependencies determine this, whatever their perspective:

+   - Hardware perspective (for example, a specific clustering of processors is required)
+   - Platform perspective (say, the provider must use a given OS and a given middleware product)
+   - Software perspective (maybe the specific services need to be closely coupled with related applications)
+   - From any mixture of these

![](bbox=[0.122, 0.391, 0.207, 0.463])

Removing the dependencies among various applications and systems helps an organization evolve the data center into a more flexible, modular environment. Establishing this architectural approach, in effect, creates containers of functionality within the data center that ease the transition to the cloud.