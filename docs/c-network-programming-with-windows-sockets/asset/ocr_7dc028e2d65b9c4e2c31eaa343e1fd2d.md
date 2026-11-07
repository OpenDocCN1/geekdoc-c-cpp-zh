```
```cpp
////////////////////////////////////////////////////////////////
// CMainView

IMPLEMENT_DYNCREATE(CMainView, CFormView)

CMainView::CMainView()
    : CFormView(CMainView::IDD)
{
    //{{AFX_DATA_INIT(CMainView)
    // NOTE: the ClassWizard will add member initialization here
    //}}AFX_DATA_INIT

    // initialize class variables

    m_pWinSock = NULL;
    g_pStreamSrv = NULL;
}

CMainView::~CMainView()
{
    // free the stream and WinSock objects

    if (g_pStreamSrv)
    {
        g_pStreamSrv->DestroySocket();
        delete g_pStreamSrv;
        g_pStreamSrv = NULL;
    }

    if (m_pWinSock)
    {
        m_pWinSock->Shutdown();
        delete m_pWinSock;
        m_pWinSock = NULL;
    }
}

void CMainView::DoDataExchange(CDataExchange* pDX)
{
    CFormView::DoDataExchange(pDX);
    //{{AFX_DATA_MAP(CMainView)
    // NOTE: the ClassWizard will add DDX and DDV calls here
    //}}AFX_DATA_MAP
}

void CMainView::OnInitialUpdate()
{
    // get pointer to list box used for status messages

    CListBox* plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // initialize the WinSock object

    m_pWinSock = new CWinSock;
    if (m_pWinSock->Startup() == CWinSock::WINSOCK_NOERROR)
        plb->InsertString(0, "WinSock initialized");
    else
    {
```
```