# Handling View Activation

When you switch to a view that already exists, you need to ensure that the recordset is refreshed and that the dialog is re-initialized so that the correct information is displayed. When an existing view is activated or deactivated, the framework calls the OnActivateView() member of the class, so this is a good place to take care of refreshing the recordset and the dialog box. You can override this function in each of the view classes. You can do this by selecting the Overrides button in the Properties window for a view class and selecting OnActivateView from the list. Make sure you add the override to both view classes.

You can add the following code to complete the implementation of the OnActivateView() function override for the COrderView class:

```
void COrderView::OnActivateView(BOOL bActivate,
    CView* pActivateView, CView* pDeactiveView)
{
    if(bActivate)
    {
        // Get a pointer to the document
        CDBSampleDoc* pDoc = GetDocument();

        // Get a pointer to the frame window
        CMainFrame* pMFrame = static_cast<CMainFrame*>(GetParentFrame());

        // If the last view was the product view, we must re-query
        // the recordset with the product ID from the product recordset
        if(pMFrame->m_CurrentViewID==PRODUCT_VIEW)
        {
            if(!m_pSet->IsOpen())      // Make sure the recordset is open
                return;
            // Set current product ID as parameter
            m_pSet->m_ProductIDparam = pDoc->m_DBSampleSet.m_ProductID;
            m_pSet->Requery();         // Get data from the DB

            // If we are past the EOF there are no records
            if(m_pSet->IsEOF())
                AfxMessageBox(L"No orders for the current product ID");
        }

        // Set the window caption
        CString strTitle = _T("Table Name: ");
        CString strTable = m_pSet->GetTableName();
        if(!strTable.IsEmpty())
            strTitle += strTable;
        else
            strTitle += _T("Orders - Multiple Tables");
        pDoc->SetTitle(strTitle);
        CRecordView::OnInitialUpdate();    // Update values in dialog
    }

    CRecordView::OnActivateView(bActivate, pActivateView, pDeactiveView);
}
```

You execute the code only if the view is being activated, and when this is the case, the bActivate argument will be TRUE. After getting pointers to the document and the parent frame, you verify that the previous view was the Product View before re-querying the order set. This check is not necessary at