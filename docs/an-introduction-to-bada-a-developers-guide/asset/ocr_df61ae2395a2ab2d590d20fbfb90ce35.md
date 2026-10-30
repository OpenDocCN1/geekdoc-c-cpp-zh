```
pDataList->Add(*pData2);

// Start the required application with the relevant data
// As the CONTACTS app is going to return phone numbers,
// the callback listener must be sent to the
// application control.
r = pAC->Start(pDataList, this);

delete pAC;

pDataList->RemoveAll(true);
delete pDataList;
}
else
{
    r = E_OBJ_NOT_FOUND;
}

return r;
}
```

The IAppControlEventListener interface receives notification events from the Application Control when it is done (i.e. the operation has completed or has been cancelled). The type of notification data received depends on the type of Application Control started and the operation type used. For this example, the implementation of the OnAppControlCompleted() method must handle both Application Status results and multiple items of Contacts data.

The following steps describe the functionality that would be implemented in the OnAppControlCompleted() method:

+   1. Retrieve the number of result elements in the IList collection returned from the Contacts application.
+   2. Check that the application control ID and the operation ID match those requested when the Application Control was started (APPCONTROL_CONTACT and OPERATION_PICK respectively).
+   3. If they match, determine if the request was successful by retrieving the first result item from the IList collection and comparing it with the APPCONTROL_RESULT_SUCCEEDED result.
+   4. If it matches, determine if the correct return type has been set by retrieving the second result item from the IList collection and comparing it with the string ‘phone’.
+   5. If it matches, retrieve all the data values by looping through the list until the last element is reached.

The following code snippet is an example of the Application Control event handling in the MainForm’s OnAppControlCompleted() method: