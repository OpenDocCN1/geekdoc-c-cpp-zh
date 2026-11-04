
## Appendix G: Colors

The Windows Forms colors are based on the Alpha-Blending Red Green Blue (ARGB) model. There are 140 predefined colors and one user-defined color. To use a color it must first be defined as an instance, and then assigned to as a specific brush/pen (see Example G.1). For a complete list of colors, see Table G.1.

### Example G.1.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;
namespace Appendix_G {
    public class Form1 : System.Windows.Forms.Form {
        public Form1() {InitializeComponent();}
        private void InitializeComponent() {}
        protected override void OnPaint(PaintEventArgs e) {
            Graphics test = e.Graphics;
            Font AlgerianFont = new Font("Algerian", 10);
            SolidBrush MyBrush = new SolidBrush(Color.Red);
            test.DrawString("Salvatore A. Buono", AlgerianFont,
                MyBrush, 60, 25);
        }
        static void Main() {
            Application.Run(new Form1());
        }
    }
}
```

We can also define our own colors using the static methods Color.FromArgb(int ARGB); Color.FromArgb(int alpha, Color color); Color.FromArgb(int red, int green, int blue); and Color.FromArgb(int alpha, int red, int green, int blue) (see Example G.2).

### Example G.2.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;
namespace Appendix_F {
    public class Form1 : System.Windows.Forms.Form {
        public Form1() {InitializeComponent();}
        private void InitializeComponent() {}
        protected override void OnPaint(PaintEventArgs e) {
            Graphics test = e.Graphics;
            Font AlgerianFont = new Font("Algerian", 10);
            SolidBrush MyBrush = new SolidBrush(Color.FromArgb(255, 0, 0));
            test.DrawString("Salvatore A. Buono",
                AlgerianFont, MyBrush, 60, 25);
        }
        static void Main() {
            Application.Run(new Form1());
        }
    }
}
```

|  |  |  |  |  |
|---|---|---|---|---|
| AliceBlue | DarkOliveGreen | Indigo | MediumPurple | Purple |
| AntiqueWhite | DarkOrange | Ivory | MediumSeaGreen | Red |
| Aqua | DarkOrchid | Khaki | MediumSlateBlue | RosyBrown |
| Aquamarine | DarkRed | Lavender | MediumSpringGreen | RoyalBlue |
| Azure | DarkSalmon | LavenderBlush | MediumTurquoise | SaddleBrown |
| Beige | DarkSeaGreen | LawnGreen | MediumVioletRed | Salmon |
| Bisque | DarkSlateBlue | LemonChiffon | MediumBlue | SandyBrown |
| Black | DarkSlateGray | LightBlue | MistyRose | SeaGreen |
| BlanchedAlmond | DarkTurquoise | LightCoral | Moccasin | SeaShell |
| Blue | DarkViolet | LightCyan | NavajoWhite | Sienna |
| BlueViolet | DeepPink | LightYellow | Navy | Silver |
| Brown | DeepSkyBlue | LightGray | OldLace | SkyBlue |
| BurlyWood | DimGray | LightGreen | Olive | SlateBlue |
| CadetBlue | DodgerBlue | LightPink | OliveDrab | Snow |
| Chartreuse | Firebrick | LightSalmon | Orange | SpringGreen |
| Chocolate | FloralWhite | LightSeaGreen | OrangeRed | SteelBlue |
| Coral | ForestGreen | LightSkyBlue | Orchid | Tan |
| CornflowerBlue | Fuchsia | LightSlateGray | PaleGoldenrod | Teal |
| Cornsilk | Gainsboro | LightSteelBlue | PaleGreen | Thistle |
| Crimson | GhostWhite | LightYellow | PaleTurquoise | Tomato |
| Cyan | Gold | Lime | PaleVioletRed | Turquoise |
| DarkBlue | Goldenrod | Linen | PapayaWhip | Violet |
| DarkCyan | Gray | Magenta | Peachpuff | Wheat |
| DarkGoldenrod | Green | Maroon | Pink | White |
| DarkGray | GreenYellow | MediumAquamarine | Plum | WhiteSmoke |
| DarkGreen | HotPink | IndianRed | PowderBlue | Yellow |
| DarkKhaki | HotPink | IndianRed | MediumBlue | PowderBlue | YellowGreen |

Table G.1. Complete list of ARGB colors.

## Appendix H: Algorithms

I'd like to take a moment to demonstrate a more explicit version of an algorithm. Here, every detail must be documented and made as vivid as possible, with no assumptions placed on the part of the programmer(s). Reasonable timelines should be developed with additional exit strategies placed on optional material and research. A text outline, drawings, and even some suggestive coding could be included with this model, but it should remain only a model.

### Introduction

Pawns is a game I developed back in the late 1980s as an alternative to a traditional Chess game. It resembles Chess down to its very last detail, but there's one key difference: In my version, the players are no longer considered to be the Kings and instead are forced to choose alternative persona. They can select their own Queen, a Rook, Bishop, Knight, or any of their pawns, but if their player is captured, they're captured, meaning that the game is over and the other player wins. Thus, the true purpose of the game is not to capture the King, but instead to attempt to capture the other player's piece. Both sides should try their best to avoid revealing their identities, but at the same time they must defend the King and play the traditional game.

### Basic Rules

The game is played on an eight by eight checkered board with all sixty-four squares open for play (see Figure H.1). Two players, one lighter and the other darker, rotate between moves with the lighter player beginning the game.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_515_0.png)

Figure H.1.

Each player begins with sixteen characters: one King, one Queen, two Rooks, two Bishops, two Knights and eight Pawns. The players are lined up on opposite sides of the board with the lighter side placing its right-hand, or King-side Rook, on a lighter square. The arrangement of the key pieces is from left to right and is listed as follows: Queen-side Rook, Queen-side Knight, Queen-side Bishop, The Queen, The King, King-side Bishop, King-side Knight, and King-side Rook. The Pawns are then placed in the squares directly in front of them with their positions defining their identities, i.e., Queen-Rook's Pawn, Queen-Knight's Pawn, Queen-Bishop's Pawn, Queen's Pawn, King's Pawn, King-Bishop's Pawn, King-Knight Pawn, King-Rook's Pawn. The darker side mirrors these positions (see Figure H.2). Note: The Queens of each side should be lined up vertically with the lighter Queen placed on a lighter square and the darker Queen placed on a darker square.

Figure H.2.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_516_0.png)

Each player is only allowed one move per turn; no two pieces may occupy the same square at any one time; and a player can only capture pieces from the opponent's side. Once a piece is captured, the attacking piece takes that square and the turn is complete. At the beginning of the game, each player is instructed to secretly choose a piece from their own set of characters which will represent them. The King is not considered a valid choice, nor are any of the opponent's pieces; if a player fails to select a valid character, he automatically forfeits the game.

Once the game is in play, it can only be terminated by one of six situations:
- A player's chosen piece is captured, which immediately ends the game giving the win to the player that captured the piece;
- A King is placed in checkmate, which also immediately terminates the game, but this time it is considered to be a draw;
- A player cannot move any piece without placing his king in check, which would count as a draw;
- A player resigns, forfeiting the game, with the win going to the remaining player.
- Both players agree to withdraw (in this case, the player who was ahead wins the game).
- All players on either side have been captured except for King and the player's choice—the game is then considered a victory for the player with the fewest pieces.

### The King

Each piece has its own set of movements. Beginning with the King, we find that he is subject to several limitations and one key exception: The King is only able to step a distance of one space, but he can move in any direction (see Figure H.3). He is not able to step onto a square controlled by his enemy, nor can he remain on a square that his enemy has taken control over; this second situation is known as checking the King.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_517_0.png)

Figure H.3.

If the King is placed in check, there are three potential solutions:
- He can move to an alternative space, assuming there is one that is available that doesn't break the rules listed above;
- He or another same-side piece can capture the opposing piece, assuming this move can be done without leaving the King in any additional checks;
- It may be possible to block the opposing player's line of attack, by placing a lesser piece between the King and his opponent.

It is against the rules to cause a check by moving one's own pieces if they inadvertently reveal a check. However, if an opponent can open a path by removing one of his own obstacles, it would be considered legal, or what is called a revealed check. If two or more piece are threatening the King (a double check) this second choice will be
