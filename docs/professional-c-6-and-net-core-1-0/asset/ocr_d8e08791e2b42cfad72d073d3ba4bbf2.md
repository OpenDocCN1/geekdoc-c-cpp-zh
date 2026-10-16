# Room Reservation

| Room: | |
| Begin time: | |
| End time: | |
| Contact: | |
| Event: | |

Reserve Room

# Figure 44.6

Because the service host is configured with the ServiceMetadataBehavior, it offers a MEX endpoint. After the service host is started, you can add a service reference from Visual Studio. After you add the service reference, the dialog shown in Figure 44.7 pops up. Enter the link to the service metadata with the URL http://localhost:9000/RoomReservation?wsdl, and set the namespace name to RoomReservationService. This defines the namespace of the generated proxy class.