can be called again.

The function grantClearance determines where to direct the plane next and what resources to reserve for it, based upon the plane position, i.e. the segment on which the plane is, and which gate the plane has been allocated.

```
void ATC::grantClearance(plane *p){
    if(p->segment == rightTaxiway)
        allocateGate(p);
    else if(p->segment == rightTaxiway + 1 + p->gate){
        taxiways[p->segment]->release();
        p->prepareToMove(toGates + p->gate);
    }
    else if(p->segment == toGates + p->gate){
        sim::log() << " Plane " << p->id << " at gate " << p->gate << " will wait for " << p->serviceT << endl;
        sim::post(p->serviceT, [=](){
            // wait for service
            p->prepareToMove(fromGates + p->gate);
        });
    }
    else if(p->segment == fromGates + p->gate){
        taxiways[rightTaxiway + 2 + p->gate]->acquire([=](){
            taxiways[toGates + p->gate]->release();
            p->prepareToMove(rightTaxiway + 2 + p->gate);
        });
    }
    else if(p->segment == leftTaxiway){
        taxiways[takeOff]->acquire([=](){
            taxiways[halfRW]->acquire([=](){
                taxiways[leftTaxiway]->release();
                p->prepareToMove(takeOff);
            });
        });
    }
    else if(p->segment == takeOff){
        taxiways[takeOff]->release();
        p->hide();
        sim::log() << " plane " << p->id << " left." << endl;
        delete p;
    }
    else {
        // default case
        taxiways[p->segment+1]->acquire([=](){
            taxiways[p->segment]->release();
            p->prepareToMove(p->segment+1);
        });
    }
}
```