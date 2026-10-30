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

# 26.7 Deadlocks

A deadlock is a technical term used to describe a system in which one entity e₁ is waiting to reserve a resource held by entity e₂ which in turn is waiting to reserve a resource held by and entity e₃ and so on, till some entity eₙ in this sequence is waiting to reserve a resource held by e₁. Notice that in this case no entity can make progress, because all are waiting for each other. As an example, Figure 26.7 shows cars deadlocked on roads in a city. Note that the roads are one ways, as shown. The cars in the top road are waiting for the space ahead