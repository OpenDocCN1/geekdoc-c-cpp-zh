added the appropriate controls to the dialog template resource, add a DDX variable of type CString called m_strMessage. Then, add a message handler for the OK button. After you've done that, modify the CQCClientVCDlg::OnOk function so that when finished, it looks like the code in Listing 27.3.

# LISTING 27.3  Visual C++ Client Code to Use a Queued Component

```
```cpp
void CQCClientVCDlg::OnOk()
{
    if (UpdateData(TRUE))
    {
        m_strMessage.TrimLeft();
        m_strMessage.TrimRight();

        if (0 < m_strMessage.GetLength())
        {
            IInteraction* pInteraction = NULL;
            HRESULT hr;

            BSTR bstrMessage;
            bstrMessage = m_strMessage.AllocSysString();

            ::CoInitialize(NULL);

            hr = ::CoGetObject(L"queue:/new:qCCCompVC.Interaction.1",
                NULL,
                IID_IInteraction,
                (void**)&pInteraction);

            if (FAILED(hr))
            {
                if (MK_E_CONNECTMANUALLY == hr)
                {
                    AfxMessageBox("Operation requires manual intervention");
                }
                else if (MK_E_EXCEEDEDDEADLINE == hr)
                {
                    AfxMessageBox("Object creating timed out");
                }
                else if (MK_E_NEEDGENERIC == hr)
                {
                    AfxMessageBox("Moniker needs to be generic");
                }
                else if (MK_E_UNAVAILABLE == hr)
                {
                    AfxMessageBox("The request operation is unavailable");
                }
                else if (MK_E_SYNTAX == hr)
                {
```
```