```
/* fsm.h */
#ifndef fsm_h
#define fsm_h

// Call states.
enum fsm_states { IDLE = 1, CALL_INIT, ACTIVIVE, RELEASE_INIT};

// Return values.
const int CLEAR_CALL = 1;
const int UNKNOWN_MSG = 2;
const int UNKNOWN_STATE = 3;

#endif
```

Next file is the send.cpp. Each message is created according to the protocol specification and it is passed to the lower layer. This lower layer must be the driver of the network card which forwards the message to the card for transmission in the network. As we said, for simplicity, we assume that each message contains only its code and the CRV.

```
#include "general.h"

extern Prtcl prtcl;
int Call::send_msg(Msg *p) {
    int data[2]; /* Since the message contains only its code and the CRV,
    its size is set to 2. The exercise C.11.22 shows an example of how to create
    message. */
    data[0] = CRV;
    data[1] = p->code;

    switch(data[1]) {
        case SETUP:
            break;
        case RELEASE:
            break;
        default:
            cout << "Unexpected message_" << data[1] << " for\ntransmission\n";
            return -1;
    }
#ifndef LOOPBACK_MODE
/* In a real application, here is the place where we typically call a
function of the lower layer (e.g., a function of the driver) with arguments
data array and its length for transmission in the network. */
    cout << "Only loopback tests are supported\n";
#else
    switch(data[1]) {
        case SETUP:
            data[0] = CRV;
            data[1] = CONNECT; /* We simulate the scenario that the
other party accepted the call and the message CONNECT is received to complete
the call establishment. */
            break;
    }
```