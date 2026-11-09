Listing 25.8 demonstrates the process of enlisting an OLEDB provider session in a DTC transaction. This code is from the internal ChargeAccount() method of the Order class in the OrderEntry project. The sample application accesses a single table in a SQL Server database containing balance, account number, and email address fields. The application uses the ATL consumer templates to simplify the management of the several OLEDB interfaces involved.

# **LISTING 25.8**  Enlisting an OLEDB Session to an External DTC Transaction

```
CDataSource OrderConnection;                 //Accounts database connection
CSession OrderSession;                        //Session for Order processing
HRESULT hr;                                   //Call result

//Open database and create session
hr = OrderConnection.OpenFromInitializationString(
        L"DRIVER=SQL Server;SERVER=(local);"
        L"APP=Microsoft® Windows NT (R);Operating System;"
        L"WSID=WINLAP;DATABASE=Accounts;TranslationName=Yes;"
        L"QueryLogFile=Yes;" );
if ( FAILED(hr) )
        _com_issue_error(hr);
hr = OrderSession.Open(OrderConnection);
if ( FAILED(hr) )
        _com_issue_error(hr);

//Join the external transaction
ITransactionJoin *pTJ = NULL;
hr = (OrderSession.m_spOpenRowset)->QueryInterface(
                                      IID_ITransactionJoin,
                                      (void**)&pTJ);
if ( FAILED(hr) )
        _com_issue_error(hr);
hr = pTJ->JoinTransaction(pTransaction,0,0,NULL);
if ( FAILED(hr) )
        _com_issue_error(hr);
```

Notice that the process used to join the transaction has two steps. You have probably also noticed that I reverted to direct OLEDB operations here. At this stage of the game, the ATL templates are still a bit new and have no direct support for joining explicit DTC transactions. The direct OLEDB operation is not too painful in this case. Simply query for an ITransactionJoin interface using the session IOpenRowset interface pointer and call JoinTransaction().

If you get back a NULL from your ITransactionJoin query, the provider is indicating that it cannot support external DTC transactions. I have also found that some providers which return a good interface pointer don't support external transactions either, or at least not correctly.