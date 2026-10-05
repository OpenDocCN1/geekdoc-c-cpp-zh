
# Make 4 Complete Unity Games from Scratch Using C#

Up to date for Unity 2018.1

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_0_0.png)

# Unity Games by Tutorials THIRD EDITION

By the raywenderlich.com Tutorial Team Brian Moakley, Mike Berg, Sean Duffy, Eric Van de Kerckhove & Anthony Uccello

# Unity Games by Tutorials Third Edition

Mike Berg, Sean Duffy, Brian Moakley, Eric Van de Kerckhove, and Anthony Uccello

Copyright ©2018 Razeware LLC.

# Notice of Rights

All rights reserved. No part of this book or corresponding materials (such as text, images, or source code) may be reproduced or distributed by any means without prior permission of the copyright owner.

# Notice of Liability

This book and all corresponding materials (such as source code) are provided on an "as is" basis, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages or other liability, whether in action of contract, tort or otherwise, arising from, out of or in connection with the software or the use of other dealing in the software.

# Trademarks

All trademarks and registered trademarks appearing in this book are the property of their own respective owners.

# Dedications

“To the experimenters, learners and creators. To those taking on the monumental task of making games, and learning to create art on top of that. To the creation of something no one has seen before.”

— Mike Berg

“To my wife Carmen, and my son Braeden, who provide inspiration every day to achieve more than I would ever think possible.”

— Sean Duffy

“To Lizzie, Fiora, and Rowan – these words exist only from your sacrifice and blessings. My others find joy in them as I find joy in you.”

— Brian Moakley

“To my loving girlfriend who has always been patient with me and respects the time I spend making and playing games. I'd also like to thank the raywenderlich.com team for allowing me to grow and give back to the community.”

— Eric Van de Kerckhove

“I dedicate this book to my wife Carrie and our 6 fur babies (Daisy, Jack, Yoshi, Bowser, Ripper, and Boo).”

— Anthony Uccello

## About the authors

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_3_0.png)

**Mike Berg** is a full-time game artist who is fortunate enough to work with many indie game developers from all over the world. When he's not manipulating pixel colors, he loves to eat good food, spend time with his family, play games and be happy. You can check out his work at [www.weheartgames.com](http://www.weheartgames.com)

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_3_1.png)

**Sean Duffy** is a software engineer by day, and hobbyist game and tools developer by night. He loves working with Unity, and is also a Unity Asset Store developer with a special focus on 2D tools to help other game developers. Some of Sean's more popular Unity Assets include his 2D Shooter Bullet and Weapon System and 2D Homing Missiles assets. You can find Sean on Twitter at [@shogan85](https://twitter.com/shogan85)

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_3_2.png)

**Brian Moakley** is an instructor who produces video tutorials on iOS, Unity, and various other topics. When not writing or coding, Brian enjoys story driven first person shooters, reading genre fiction, and epic board game sessions with friends.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_3_3.png)

**Eric Van de Kerckhove** is a Belgian hobbyist game dev and has been so for more than 15 years. He has made a fair share of games over the years, mostly free ones for fun and as learning experiences. Eric leads the Unity team.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_3_4.png)

**Anthony Ucello** is a software consultant who spends his night hours coding away making games in Unity. He is married and has 3 dogs and 3 cats.

## About the editors

Adrian Strahan is a tech editor of this book. Adrian is a full-time Product Owner and part-time iOS developer living in the South West of England. When he's not working, Adrian is either running, gardening or building Lego models.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_4_0.png)

Manda Frederick is the editor of this book. She has been involved in publishing for over years through various creative, educational, medical and technical print and digital publications, and is thrilled to bring her experience to the raywenderlich.com family as Managing Editor. In her free time, you can find her at the climbing gym, backpacking in the backcountry, hanging with her dog, working on poems, playing guitar and exploring breweries.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_4_1.png)

Brian Moakey is the final editor of this book. Brian is an instructor who produces video tutorials on iOS, Unity, and various other topics. When not writing or coding, Brian enjoys story driven first person shooters, reading genre fiction, and epic board game sessions with friends.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_4_2.png)

## About the artists

Mike Berg made all of the 3D models, animations, and textures for this book. He is a full-time game artist who is fortunate enough to work with many indie game developers from all over the world. When he's not manipulating pixel colors, he loves to eat good food, spend time with family, play games and be happy. You can check out his work at: www.weheartartgames.com

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_4_3.png)

Vinnie Prabhu created all of the music and sounds for the games in this book. Vinnie is a music composer/software engineer from Northern Virginia who has done music sound work for concerts, plays and video games. He's also a staff member on OverClocked ReMix, an online community for music and video game fans. You can find Vinnie on Twitter as @palpablevt.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_4_4.png)

## Table of Contents: Overview

- Introduction ................................................................................ 16
- Section I: Getting Started ............................................................ 23
- Chapter 1: Hello Unity ................................................................ 24
- Chapter 2: GameObjects ....................................................... 51
- Chapter 3: Components ....................................................... 73
- Chapter 4: Physics ................................................................ 96
- Chapter 5: Managers and Pathfinding ............................................ 126
- Chapter 6: Animation ............................................................ 152
- Chapter 7: Sound ................................................................. 183
- Chapter 8: Finishing Touches ............................................... 210
- Section II: First-Person Shooters .......................................... 240
- Chapter 9: The Player and Environment ................... 241
- Chapter 10: Adding Enemies ................................... 269
- Chapter 11: Introducing the UI ................................ 297
- Section III: 2D Platformers ................................................ 327
- Chapter 12: Beginning Unity 2D ................................ 328
- Chapter 13: More Unity 2D ....................................... 356
- Chapter 14: Saving Data .................................................. 385
- Section IV: Blender........................................................... 415
- Chapter 15: Modeling in Blender ................................................ 416
- Chapter 16: Texturing With Blender ........................................ 442
- Chapter 17: Animating in Blender ................................ 467
- Section V: Tower Defense Games ................................... 498
- Chapter 18: Making A Tower Defense Game.. ......... 499
- Chapter 19: Making Towers ................................... 531
- Chapter 20: Virtual Reality ................................ 569
- Chapter 21: Publishing Your Game ................... 602
- Section VI: Appendices ....................................... 619
- Chapter 22: C# Crash Course .................................. 620
- Chapter 23: Unity API ........................................ 634
- Chapter 24: Visual Studio.................................. 651
- Conclusion ................................................... 659
- More Books You Might Enjoy.................................. 660
