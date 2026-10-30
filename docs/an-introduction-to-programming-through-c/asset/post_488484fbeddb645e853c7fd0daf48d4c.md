
The gate allocation procedure as discussed earlier is simple: we reserve the smallest numbered unreserved gate. If reservation is successful, then we try to move forward. For this, we acquire the next segment. When that is acquired, we release the current segment, and then try to move on the new segment. If gate reservation is not successful, then we try reservation again after one step.

## 26.6 The plane class

The aircraft are implemented using a plane class. An aircraft must appear on the screen as a part of the animation. So we inherit from the Turtle class. Indeed, our aircraft appear on the screen as turtles. We could have defined a more aircraft like visual appearance by using the polygon class, but that is left for the exercises. To keep track of which taxiway segment the plane is on at any time instant we will have a data member segment. We will have another data member timeToSegmentEnd, in which we keep track of the number of steps we need to move forward in order to reach the end of the current segment. In addition, we need to note the gate allocated for the aircraft. For this we use an integer data member gate. Finally, the plane will need to know about the taxiways and the atc, so we have data members to hold those references.

```
class plane : public Turtle {
public:
    int id;                 // identifying number for plane
    int arrivalT;           // arrival time
    int serviceT;           // how long the aircraft waits at the gate
    int segment;            // index of taxiway segment the aircraft is on
    int timeToSegmentEnd;   // how far from the end of the segment
    int gate;               // id of allocated gate
    vector<taxiway*> &taxiways;
    ATC &atc;
public:
    plane(int i, int at, int st, vector<taxiway*> &tw, ATC &atc0)
        : id(i), arrivalT(at), serviceT(st), taxiways(tw), atc(atc0) {
        hide();
        penUp();
        gate = -1;          // indicates gate not allocated
    }
    void prepareToMove(int newsegment);
    void moveOnSegment();
    friend class ATC;
};
```

Note that we have made the ATC class a friend because it needs to know where a plane is etc. A plane is created in the ATC class as discussed earlier.

The basic action performed by a plane is moving on a taxiway. When the atc determines that a plane must move on certain segment of the taxiway, it calls the prepareToMove

member function of the plane class. This does minor housekeeping and aligns the plane with the direction of the taxiway. The data member timeToSegmentEnd is also set to the number of steps in which the current segment is to be traversed. After that the plane is ready to move.

```
void plane::prepareToMove(int newSegment){
    segment = newSegment;
    Position linestart = taxiways[segment]->getStart();
    moveTo(linestart.getX(), linestart.getY());
    Position lineend = taxiways[segment]->getEnd();
    face(lineend.getX(), lineend.getY());
    timeToSegmentEnd = taxiways[segment]->traversalT;
    sim::post(0, [=](){this->moveOnSegment();});
}
```

At the end, the moveOnSegment member function is called. This causes the plane to take one step on the segment taxiway. To traverse the entire segment, the function is called repeatedly, for each value of timeToSegmentEnd as it is decremented down to 0. At the end, the plane has reached the end of the segment, and so clearance must be sought from the air traffic controllers for future action. So atc.grantClearance is called.

There is one slight complication to be handled: when the plane is taking off or landing, then the taxiway halfRW must be released when the plane has reached the middle of the segment.

```
void plane::moveOnSegment(){
    if(timeToSegmentEnd != 0){
        if((segment == landing || segment == takeOff)
           && timeToSegmentEnd == taxiways[segment]->traversalT/2){
            taxiways[halfRW]->release();
        }
        forward(taxiways[segment]->stepsize);
        --timeToSegmentEnd;
        sim::post(1, [=](){moveOnSegment();});
    }
    else
        atc.grantClearance(this);
}
```

## 26.7 Deadlocks

A deadlock is a technical term used to describe a system in which one entity e₁ is waiting to reserve a resource held by entity e₂ which in turn is waiting to reserve a resource held by and entity e₃ and so on, till some entity eₙ in this sequence is waiting to reserve a resource held by e₁. Notice that in this case no entity can make progress, because all are waiting for each other. As an example, Figure 26.7 shows cars deadlocked on roads in a city. Note that the roads are one ways, as shown. The cars in the top road are waiting for the space ahead

of them to become empty. This will happen if the cars in the right road can move down. But these can move down if the cars in the bottom road can move left. These in turn will move left only if the cars in the left road can move. But these are blocked because of the cars in the top row. The net result: no one can move. Deadlock.

![](img/c7233aedab7e4c7cad32a7615b6a4783_451_0.png)

Figure 26.3: Traffic deadlock in a city

A deadlock is possible on a circular taxiway if every segment contains a plane which wants to move forward. In our airport it would seem that the taxiways do not form a circular path. However we have to be careful in implementing the half-runway-exclusion rule.

It turns out that deadlocks will not arise because we observe the following discipline in reserving halfRW. A landing aircraft must first reserve the landing runway and only then halfRW. Similarly a plane taking off must first reserve the takeoff runway and only then halfRW. You can see that this is a good strategy: halfRW being a precious resource must be reserved last. If a plane reserves halfRW and cannot reserve the landing runway, then it prevents take offs unnecessarily until such time as it reserves the landing runway. More formally, as the exercise asks you, you should be able to prove that if this policy is used there can be no deadlock. On the other hand, if landing planes as well as planes taking off reserve halfRW first, then it is possible to create a deadlock by carefully constructing the arrival sequence of the planes. The exercises invite you to explore this possibility.

## 26.8 Concluding remarks

There are many ways in which we could have designed this program. For example, note that the class ATC does not contain any interesting data members. Thus you might choose not

to have this class at all and instead include the member functions from this class into the plane class itself. This would simplify the code a bit; you could directly access the members in plane in writing functions such as ATC::processArrival. However, we have preferred to have two classes because we felt it is better to put air traffic control actions in an ATC class.

Another possibility is to not use the sim and Resource classes at all. Write the code from the point of view of the air traffic controllers who examine the planes at each step and advance them as needed. You are asked to do this in an exercise.

## Exercises

- 1. Modify the simulation program to print out the average aircraft delay.
- 2. Define a better plane class in which the on screen image looks like an aircraft rather than a triangle.
- 3. Suppose we wish to ensure that as much as possible, an aircraft must land at its arrival time. Thus, while granting halfRW to a departing plane, we must check whether no plane will want to land during the interval in which the departing plane will use halfRW. Device a good mechanism to do this. Hint: perhaps you can reserve the landing runway and halfRW a bit earlier than needed?
- 4. The program given in the text uses so called busy waiting to allocate gates, i.e. if a gate is not currently available, the plane retries after 1 step. It will be more efficient if the plane can await the release of any gate. Develop a class to represent such a resource group. A resource group models a sequence of objects, each of which can be either reserved or unreserved. On a reserve request, one of the unreserved objects must be allocated, i.e. the requesting entity should be set as its owner. If all objects are currenly reserved, then the reserve request is deemed to fail and should thus return false. In that case the entity may await its release. When any of the objects becomes available, that should get reserved for the waiting entity. Use this in the simulation code.
- 5. Show that our strategy of reserving resources ensures that there is no deadlock. Specifically, show that at every step some aircraft will make progress, and that there will not exist entities e0,...,en−1 where ei is waiting for a resource currently held by entity ei+1 mod n.
- 6. Suppose we reserve halfRW first and then the take off or landing runways. Construct an input sequence (the file arrivals.txt) such that there is a deadlock.
- 7. Perform the airport simulation without using the sim and Resource classes, as described in Section 26.8. Do you think this will run faster than the simulation we have presented, or slower? What if there is no need to produce a graphical output, i.e. only a textual record is required?
- 8. Suppose we do not want to divide the taxiway into segments. Instead, suppose we will allow a plane to move a certain stepsize at each step while keeping a certain safe
