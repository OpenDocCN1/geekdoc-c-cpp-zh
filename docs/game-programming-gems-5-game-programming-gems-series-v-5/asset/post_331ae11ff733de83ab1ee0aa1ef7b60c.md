
we would be 50% complete: (175–100)/150. Using that percentage, we can determine both its position and orientation by using splines and quaternions.

## Movement of 3D Points

Think of the physics event as if you were going to play connect-the-dots. In this version of the game, the dots are already numbered in order, and you already know that the shape we’re tracing is a person’s face. Since most faces aren’t square, when you trace between the dots, you decide to put in an artistic touch by making the lines between the dots have gentle curves instead of harsh straight lines. The end result is that the curves make the face look natural and far more pleasing than if you had simply used a ruler.

Like playing connect-the-dots, the manner in which you draw the lines between the dots (or waypoints) determines the overall picture that the customer will see. Most prescribed physics engines can easily support multiple connect-the-dot movement algorithms, including basic linear methods and several implementations of splines. In this gem, we’ll focus on just using Catmull-Rom splines [Dunlop00] to move our objects from point to point.

Velocity is a great example of how topsy-turvy this new physics can be. Velocity is determined based on where we place our waypoints and how much time we allow for an object to travel between a pair of waypoints. It’s one of the many backward-thinking flurries programmers face when using this method of physics. We’re so used to giving an object acceleration and velocity, then sending it off into the world, that it can get confusing when we realize that an object traveling X distance for T amount of time plugs nicely into the old velocity formula.

Listing 4.6.1 is a basic function that uses percent complete, percent squared, percent cubed, our X, Y, or Z position for spline points at n – 2, n – 1, and n + 1 intervals, and our given X, Y, or Z position to generate our current position.

## Listing 4.6.1 Catmull-Rom Computation for a Given X, Y, or Z

```
inline float GetSpline(float inOurPoint, float inPercent,
    float inTSquared, float inTCubed,
    float inBack2, float inBack1, float inNext)
{
    return (0.5f * ((2.0f * inBack1 +
        ((-inBack2 + inOurPoint) * inPercent) +
        ((2.0f * inBack2 - 5.0f * inBack1 + 4.0f *
        inOurPoint - inNext) * inTSquared) +
        ((-inBack2 + 3.0f * inBack1 - 3.0f * inOurPoint)
        + inNext)*inTCubed)));
}
```

Listing 4.6.2 is a simplified function that advances an object to its next waypoint given a percentage. It uses the GetSpline method with this waypoint's ending world position to determine the current 3D location. For example, if inPercent is 0.5, the object’s current position will end up halfway between the last waypoint and the current waypoint.

## Listing 4.6.2 Advancing a Point Along a Spline Path

```
void AdvanceSpline(float inPercent, GE3DPoint& ioPoint, const
GE3DPoint& inBack2, const GE3DPoint& inBack1,
const GE3DPoint& inNext)
{
inPercent = min(1.0f, inPercent);
float theTSquared = inPercent * inPercent;
float theTCubed = theTSquared * inPercent;
/* Spline for X */
ioPoint.mX = ::GetSpline(ioPoint.mX,
inPercent, theTSquared, theTCubed,
inBack2.mX, inBack1.mX, inNext.mX);
/* Spline for Y */
ioPoint.mY = ::GetSpline(ioPoint.mY,
inPercent, theTSquared, theTCubed,
inBack2.mY, inBack1.mY, inNext.mY);
/* Spline for Z */
ioPoint.mZ = ::GetSpline(ioPoint.mZ,
inPercent, theTSquared, theTCubed,
inBack2.mZ, inBack1.mZ, inNext.mZ);
}
```

Listing 4.6.3 shows AdvanceSpline using mostly precomputed splines. If you want to use faster spline calculations, precompute most of the math into a look-up table as shown. (Note, you’ll see in later sections of this gem that it’s possible to affect an object’s physics path during runtime. In that case, go with the normal, slower spline calculations since you will end up recomputing the splines every time the physics path changes).)

## Listing 4.6.3 Cached Spline Calculations

```
/* uses a precomputed array to compute a fast spline */
inline float GetFastSpline(float* inArray, float inSquared,
float inCubed, float inPercent)
{
return (0.5f * (inArray[0] + (inArray[1] * inPercent) +
(inArray[2] * inSquared) + (inArray[3] * inCubed)));
}
```

/* simplified Advance spline method */
void AdvanceSpline(float inPercent, GE3DPoint& ioPoint)
{
ioPoint.mX = GetFastSpline(mOptimizedSplines,
 theSqd, theCube, thePercent);
ioPoint.mY = GetFastSpline(mOptimizedSplines + 4,
 theSqd, theCube, thePercent);
ioPoint.mZ = GetFastSpline(mOptimizedSplines + 8,
 theSqd, theCube, thePercent);
}

## Orientations and Quaternions

Orientations describe an object's yaw, pitch, and roll. In short, orientation is not an object's location, but rather which direction it is facing while at that position. If the object is facing upside down, angled sideways, or head over heels, that refers to its orientation. Luckily for us, quaternions are great for orientations. Quaternions not only do an amazing job of modifying an object's orientation smoothly, they also fit neatly into the time-percent paradigm that we use with our 3D movement and splines. If that wasn't enough, using quaternions to advance orientation is so simple it should be a crime. Quaternions work their magic on an object's orientation by using a spherical linear interpolation, known as "slerping," which smoothly scales its orientation along a curve (see [Svarovsky00]).

## Start Your Engines!

Time to put all the pieces together into a roaring engine that will thrill our game fans. The heart of a basic engine is simple. Its job is to process all the physics nodes, advance object positions using splines, and then advance orientations using quaternions. Finally, the correct orientation is applied and the object's location is set.

Walking through Listing 4.6.4, we can see what the update code of the prescripted physics engine looks like. The first operation in the update is to pop off our nodes until we are in the correct time range. For example, if world time is 200 and node 3 goes from 195 to 220, we will pop off nodes 1 and 2 to ensure we are ready at node 3 for processing. Once we have the current node, we advance the orientation (using time and quaternions), followed by advancing the 3D position (using time and splines). Lastly, we ensure that we are rotating around the correct point on the object (feet, head, middle, wherever) before finishing our update. It's simple, it's fast, and it's almost too easy.

## Listing 4.6.4 Update Method of the Prescripted Physics Engine

```
float thePercent;
bool theResult = true;
bool thePointMatches;

/* Ensure our next point is the right one (time-wise) */
AdjustToCorrectPointUsingTime(inWorldTime);

/* any physics nodes? */
if(mPhysicsNodes.empty() == false)
{
    GE3DPoint thePoint;

    /* get our point */
    inCurrentLocation.GetPosition(thePoint);

    /* get the first item */
    FPNode& theNode = mPhysicsNodes.front();

    /* compute the percent(it will be 0-1.0F because
    of the "AdjustToCorrectPoint method" */
    thePercent = ((float)(inWorldTime -
    theNode.mStartTime)) * theNode.mInverseTotalTime;

    /* advance Orientation */
    theNode.mAdvanceOrientation(thePercent,
    mQuatOrientation);
    outResultOrientation = mQuatOrientation;

    /* Advance our location */
    theNode.mAdvanceSpline(thePercent, thePoint,
    theNode.mSplines[0], theNode.mSplines[1],
    theNode.mSplines[2]);

    /* Rotate it at the correct spot. (head/middle/etc) */
    ApplyRotation(theNode, outTransform, thePoint);
}
else
{
    theResult = false;
}
```

## Polish It to a Shine!

As with almost everything in the games industry, the details are where you can pull away from the crowd or fall back with the pack. Some polish items that make a large impact on how well the physics appears to our customers come from adding acceleration ramps, animations, and effects to waypoints. Other items include mapping points onto objects or terrain, rotating about an arbitrary point on the object, rewinding physics, or causing reactions to occur.

## Ramps and Rewind

At almost every turn, prescribed physics seems to be battling the traditional notion of physics. How can we possibly move an object through a series of points naturally without using acceleration? It’s lucky for us that quaternions needed a percentage
