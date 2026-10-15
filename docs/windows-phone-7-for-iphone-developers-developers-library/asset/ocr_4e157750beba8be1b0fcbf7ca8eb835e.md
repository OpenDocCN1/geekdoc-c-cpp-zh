thing from killing a certain number of enemies, dying in a spectacular fashion, or finding a hidden area on the map.

An API that is part of GameKit allows you to query for the list of achievements a player has already unlocked within your game. You can also programmatically grant or revoke achievements. The list of achievements that are possible in your game, including the culture-localized descriptions of those achievements, are all defined by logging into the iTunes Connect portal and modifying the Game Center settings for your application. To unlock an achievement, just pass the unique ID of the achievement to the appropriate method in the GameKit API.

The GameKit API is isolated. This means that you are limited by the API to only reading and writing data that pertains to your application. You cannot query the list of achievements earned from other applications, nor is there a global achievement list. This view differs from the classic Xbox Live view, where you can navigate to a list of every unlocked achievement in every game by viewing the game’s profile.

# Leaderboards

Leaderboards, also configurable through iTunes Connect, allow your application to keep track of statistics of players and make those statistics available globally. Any device running your application can access the global leaderboards. All you need to do is set the numeric value for a particular player’s profile, and the leaderboard configuration does the rest.

You can rank players by kill count, experience points, levels, or any other arbitrary value that is representable as some number. Again, the leaderboards are sandboxed to your application so that your code has access only to leaderboards belonging to your application. Your app can access the leaderboards programmatically to provide a custom or themed UI, or it can launch the standard Game Center Leaderboard UI.

# Networking API

Just providing unfettered access to leaderboards and achievements makes writing Game Center games with GameKit a compelling proposition. Add the fact that GameKit also comes with a robust set of networking APIs, and Game Center games become a nearly irresistible target for independent and, in many cases, commercial game developers.

The GameKit APIs provide the capability to find friends and other nearby players through a number of means. First, the application can use stock UI dialogs provided by Apple to find players nearby through either Bluetooth or on the local Wi-Fi network. If this isn’t enough, the game can use custom services written by the game developer or global services provided by Apple for finding connected friends, regardless of the means by which those friends are connected.

Once in the game, GameKit provides developers with the capability to halt game sessions programmatically. They can also send messages containing arbitrary data to individual players or all connected players, facilitating both direct and broadcast data.