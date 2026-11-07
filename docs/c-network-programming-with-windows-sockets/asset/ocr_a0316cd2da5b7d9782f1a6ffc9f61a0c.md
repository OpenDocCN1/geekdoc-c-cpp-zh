# Stream Echo Client SECLIENT

The stream echo client, SECLIENT, follows the same basic outline as DECLIENT. The primary difference lies in the implementation of the CMainView object. The header file for the CMainView object is shown in Listing 8.20. Its implementation is shown in Listing 8.21. This object performs most of the work for the SECLIENT application. CMainView::OnInitialUpdate() is called soon after the object is created. This function is responsible for creating a socket, connecting to the server, waiting to send and receive data, and setting a timer to be used for sending data. When the connection with the server is made, data is ready to be received, or data can be sent, the CMainView::OnAsyncSelect() member function is called due to the message mapping of the user-defined message WM_USER_ASYNC_SELECT. The CMainView::OnTimer() function is called every five seconds to format a string to send to the echo server.

# Listing 8.20. MAINVIEW.H for SECLIENT.

```
```cpp
// mainview.h : header file
//
/////////////////////////////////////////////////////////////////////////////
// CMainView form view

#ifndef __AFXEXT_H_
#include <afxext.h>
#endif

class CMainView : public CFormView
{
    DECLARE_DYNCREATE(CMainView)

public:
    SOCKET m_s;                  // socket
    SOCKADDR_IN m_addr;          // address of server
    IN_ADDR m_in;                // IP address of server
    int m_nBytesToSend;          // bytes left to send in the buffer
    int m_nTotalBytesToSend;     // total bytes in the buffer
    char m_pBuf[61];             // buffer to send

protected:
    CMainView();                 // protected constructor used by dynamic creation

// Form Data
public:
    //{{AFX_DATA(CMainView)
    enum { IDD = IDD_DIALOG_MAIN };
    // NOTE: the ClassWizard will add data members here
    //}}AFX_DATA

// Attributes
public:
```
```