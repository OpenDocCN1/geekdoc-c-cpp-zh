
![](img/8edd7838aa9e4a0d883fcf44f4b667a0_204_0.png)

**FIGURE 8.1** *(See color insert.)* Typical *iTron* game.

### 8.2.1 *iTron*

*iTron* [3] is a real-world “snake” game. Essentially, players must move around in the real world; while doing so, they leave a trail of “walls” in the virtual world (Figure 8.1). Players must avoid running into walls by moving so that their represented position crosses a wall on the display. Figure 8.1 shows real-world and virtual-world views of a three-person *iTron* game in progress. One player has crashed into the tail of another early on, whereas one is in danger of hitting the area boundary. The object is to be the last one remaining after all others have crashed. The game is both a strategy game in which one tries to surround and cut off one's opponents from territory and an athletic game involving running fast enough and accurately enough to carry out these strategies.

Note also the player using an inexpensive Kyle Wrist Mount to convert the smart phone into a hands-free wearable, a key innovation that reduces risk to the device and allows more freedom for the athletic activities of the game.

This game was played in a relatively small, clear area like a parking lot or football field. *iTron* can also be played in larger areas having complex terrain, such that climbing and terrain traversal become a significant part of the planning and athleticism. This style of *iTron* game is termed *iTron/Parkour*. The final state of such a game is shown in Figure 8.2.

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_205_0.png)

**FIGURE 8.2** Final state of an *iTron/Parkour* game.

### 8.2.2 *iTESS*

*iTESS* [4] is a hide-and-seek conflict game that provides virtual weaponry and intelligence assets to players in the real world. The object of the game is for a player to last as long as possible without being hit by a weapon shot (either artillery or shotgun weapon), with one's score being the maximum of such interval achieved during an extended game session. One searches for one's opponents either in the real world or by commanding a virtual unmanned aerial vehicle (UAV) on the screen of the smart phone that “flies” over the map and paints red dots if it spots opponents (see Figure 8.3). The green-shaded (lightly shaded circle in lower right corner) circle is the UAV lookdown region. The blue dot with compass arrow is the location of the player of the device shown, and the red dot represents the enemy players spotted by the UAV. The red-shaded circles are warnings for incoming artillery rounds, whereas the blue circle is the effect area of one's own round.

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_206_0.png)

**FIGURE 8.3** Screen capture from *iTESS* showing artillery shots. Upper right numeric display shows top three scores in game at any time.

One targets artillery by moving a crosshair and then tapping the fire button. By contrast, one targets the shotgun by physically pointing the device and then doing a screen drag to pull the trigger (see Figure 8.4).

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_207_0.png)

**FIGURE 8.4** *(See color insert.)* (a) Point-and-shoot interface for the *iTESS* shotgun weapon and (b) screen display during a shotgun shot animation.

In either case, shotgun shot or artillery shot, opponents in the effect area of the weapon are notified and shown the area they must escape in the brief time before the round reaches them. *iTESS* is designed to have slow weapon effects to encourage and allow rapid reactions and fast running to save players (see Reference [4] for details).

*iTESS* operates using *ad hoc* networking to transfer geographically addressed messages among devices. Once a player is hit, his or her interval time restarts from 0.

### 8.2.3 *Butterflies*

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_208_0.png)

**FIGURE 8.5** Screenshot of a *Butterflies* game. Blue (larger) butterflies are good, red (smaller) ones are bad, blue dot is my position, and red dots are other players’ positions. Green lollipop symbols are positions at which a player can obtain butterfly nets.

*Butterflies* provides virtual creatures interacting with human players in the real world. Figure 8.5 shows a game situation, with blue dot (dark dot with arrow through it) being one's own position on the map, red dots being other human players' positions, and the other symbols representing butterflies and butterfly net acquisition areas. Essentially, the human's goal is to collect as many good butterflies as possible by running so as to move onto the butterflies without being touched by the running within bad butterflies. A butterfly net (if one has one available) can extend one's reach to capture hard to reach or fast butterflies, such as those that fly on top of buildings. As game level increases, butterflies gain more and more complex behaviors. At lowest levels, they move randomly in predetermined pseudorandom patterns. At higher levels, they can run away from humans or chase them, at varying speeds. Humans can find butterfly nets that help catch or defend against them. This game therefore involves a lot of movement, planning, and social interaction as, for example, some butterflies are so fast and clever that often the only way to catch them is for humans to coordinate their actions.

## 8.3 ENGINEERING CHALLENGES

Outdoor multiplayer games as discussed earlier bring challenges to software engineering in at least five phases: architecture, design, coding, validation, and requirements.

### 8.3.1 Architecture

Outdoor play in natural environments such as parks, beaches, and remote camps will often involve play without or with weak network coverage, with no WiFi hot spots or even 3G coverage available. The devices, however, are capable of device-to-device *ad hoc* networking. This will generally mean that communications between distant players will become disconnected unpredictably and for extended periods. For example, two *iTESS* players might run off into a valley while continuing to shoot at each other, yet still be out of network contact with the other players due to terrain. Similarly, subsets of *iTron* or *Butterflies* players can move apart, to opposite sides of a building, for example. Because to be successful the game experience must continue (to the extent physically possible) even when out of infrastructure coverage areas and even when partitioned from distant players, I term this first major problem in architecting an outdoor smart phone game the *communication problem*.

Following from this first problem is the fact that any two devices can become unpredictably partitioned from one another for extended periods. This means that *game experience must not require a central controller*. That is, for games intended for play in remote areas, not only can we not require a console or Internet game server in the architecture of the game, but also we cannot even designate one of the smart phones as the controller. If we did so, any time devices become partitioned away from it, they lose game experience until contact is reestablished. I term this the *full distribution problem*.

Finally, another architecture issue, the *long-range play problem* concerns games playable at long distances. It makes perfect sense for a group in California to play *iTESS* against groups in New Jersey, the United Kingdom, and Tokyo. Obviously, this requires Internet connectivity, because device-to-device relaying is clearly inadequate. If we assume that enough players have devices that are in coverage of an Internet access point (e.g., receiving 3G/GSM coverage), we would like our game architecture to support the communications necessary as seamlessly as possible.

My initial progress on attacking these problems is captured in the *Geocast Games Architecture* (GGA) (see Section 8.4).

### 8.3.2 Design

When designing games involving virtual structures, objects, or creatures that can have evolving states, there is a need for the game system to manage state evolution in a way that yields the desired game experience to all players. As an example, consider virtual creature control. A butterfly that reacts to human proximity by flying away changes state in response to environment events. But how do players located away from this butterfly's location, maybe even network partitioned from the area, gain a coherent view of its state? The problem is compounded when events from *multiple* different devices cause state changes, as we must be concerned with how the different players view the creature, given that different subsets of players will have been made aware of different subsets of the events. Figure 8.6 shows screen captures from two *Butterflies* players at nearly the same time; the two players have been out of network contact due to being on opposite sides of a building. Consequently, their devices have different views of what the butterflies have been doing. Positions of butterflies and even positions of other players are significantly different. This

![](img/8edd7838aa9e4a0d883fcf44f4b667a0_210_0.png)

**FIGURE 8.6** (a,b) Two device screens at nearly the same time (13 seconds apart) in a *Butterflies* game with radio obstacles.
