# Finger Client Design

The Finger client application, FINGER, uses the venerable CFormView-derived object as its main interface. The header file for the CMainView object is shown in Listing 16.1. Its implementation is shown in Listing 16.2 (both of these listings appear later in this section). This object performs most of the work for the FINGER application. OnInitialUpdate() is called soon after the object is created. The first thing this function does is to force the list box used for output to use a fixed-pitch font. This ensures that any data formatted for an ASCII terminal looks appropriate. The function starts the WinSock subsystem next and then initializes the data entry field used to accept a username.

When the operator of the Finger client selects the button labeled Finger, OnClickedButtonFinger() is called. First, the host and username fields are checked to ensure that they contain valid data. If the username is valid, a Finger request string is formatted. If the wildcard asterisk character (*) is entered for the username, the request string consists of just a carriage return followed by a linefeed. Otherwise, the request string is the username followed by carriage return and linefeed. Next, a stream socket is created and the asynchronous connect is made to port 79 on the selected host. Last, the Finger button is disabled to give the user visual feedback that the program is busy.

When the connect succeeds, OnStream() is called with wParam set to CWINSOCK_YOU_ARE_CONNECTED. In response to this event, the Finger request, formatted in the OnClickedButtonFinger() function, is sent. When the Finger request is sent, OnStream() is called with wParam set to CWINSOCK_DONE_WRITING. In response to this event, the list box used for output is cleared, readying itself for the response to the Finger request.

As data arrives, OnStream() is called with wParam set to CWINSOCK_DONE_READING. The CWINSOCK_DONE_READING handler calls DisplayData() to buffer a complete line of text, denoted by a carriage return, before adding the line to the output list box. The buffering is necessary because it is possible for the data to be received in several pieces with some lines only partially received.

When the Finger server is done sending its response to the Finger request, it closes its side of the stream connection, causing OnStream() to be called with wParam set to CWINSOCK_LOST_CONNECTION. This causes the client to destroy the stream socket. The Finger button is enabled, signaling that it may be used again, with the same or a different host/username combination.

# Listing 16.1. MAINVIEW.H for FINGER.

```
```cpp
// mainview.h : header file
//
```
```