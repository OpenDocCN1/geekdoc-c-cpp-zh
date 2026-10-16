Now you can step into the implementation of the service. Create a WCF service library named RoomReservationService. By default, this library type contains both the service contract and the service implementation. If the client application just uses metadata information to create a proxy for accessing the service, this model is okay to work with. However, if the client might use the contract types directly, it is a better idea to put the contracts in a separate assembly as it was done here. With the first client that is done, a proxy is created from metadata. Later you can see how to create a client to share the contract assembly. Splitting the contracts and implementation is a good preparation for this.

The service class RoomReservationService implements the interface IRoomService. The service is implemented just by invoking the appropriate methods of the RoomReservationData class (code file RoomReservation/RoomReservationService/RoomReservationService.cs

```
using System;
using System.ServiceModel;
using Wrox.ProCSharp.WCF.Contracts;
using Wrox.ProCSharp.WCF.Data;

namespace Wrox.ProCSharp.WCF.Service
{
    [ServiceBehavior(InstanceContextMode =
    InstanceContextMode.PerCall)]
    public class RoomReservationService : IRoomService
    {
        public bool ReserveRoom(RoomReservation roomReservation)
        {
            var data = new RoomReservationRepository();
            data.ReserveRoom(roomReservation);
            return true;
        }

        public RoomReservation[] GetRoomReservations(DateTime fromTime,
            DateTime toTime)
        {
            var data = new RoomReservationRepository();
            return data.GetReservations(fromTime, toTime);
        }
    }
}
```

Figure 44.2 shows the assemblies created so far and their dependencies. The RoomReservationContracts assembly is used by both RoomReservationData and RoomReservationService.