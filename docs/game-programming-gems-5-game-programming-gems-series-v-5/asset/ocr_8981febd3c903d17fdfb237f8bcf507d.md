physics events. Instead of days implementing complicated math for new physics, most should take only a few hours and require little code from the programmer.

**Tools:** Prescribed physics can be made into a tool that artists and designers use to generate “physics files” for objects in the world. This can take the programmer completely out of the loop once the engine is built and game-ready.

**Performance:** A common barrier people face when using physics is the fear of performance. Since prescribed physics events are by definition precomputed, the real-time performance cost can be very light on the CPU.

**Replay:** The prescribed physics engine is ideal for “rewinding” an object’s movement through the game world as if it were in a sports “instant replay.”

Following is a list of the weaknesses of prescribed physics:

**Reactions:** If you want prescribed physics to interact with other objects in real time, like a baseball being interrupted by a baseball bat, then it requires extra code to support that reaction. Since this system computes the path the object will travel at the beginning of the physics event, reactions can only work if the engine supports both collision detection and the ability to morph the event into a reaction event. Coding this functionality can potentially take as much time as coding the prescribed physics engine itself.

**Unique and unfamiliar:** If a tool isn’t built for artists or designers to use, you must rely on programmers to produce the physics events. Programmers need to understand that they have to think differently to use prescribed physics. It doesn’t take a math genius to write these events, but it does take skills in observation and the ability to transfer those observations into steps. With such a foreign system of physics, it’s not surprising that some of the most mathematically gifted programmers struggle with this system at the beginning or outright refuse to use it. Once they toss aside their calculus books and think of the physics as if they were watching a movie, it generally “clicks.”

**Compound physics:** Compound physics, like reactions, requires extra effort to get right. As a general rule, when an object is under the influence of prescribed physics, no other physics in the world should be affecting the object unless you write special code to support it.

# The Engine

The most basic prescribed physics engine has two main parts: the movement of 3D points and the changing of an object’s orientation. Both the movement and orientation use a percentage value computed using time as the basis for interpolation. For location, the time converts to a percentage indicating where an object is on the spline from point A to point B. As for orientation, that same percentage is used to determine the object’s yaw, pitch, and roll. For example, if a waypoint started at world time 100 ms and went until 250 ms, giving us a total of 150 ms in length, at world time 175,