# LISTING 27.3 Continued

```
```cpp
AfxMessageBox("The display name param is invalid");
}
else if (MK_E_NOBJECT == hr)
{
    AfxMessageBox("Object could not be found");
}
else if (MK_E_INTERMEDIATEINTERFACENOTSUPPORTED == hr)
{
    AfxMessageBox("Object does not support required interface");
}
else if (ERROR_NOT_AUTHENTICATED == hr)
{
    AfxMessageBox("auth");
}
else
{
    AfxMessageBox("Unknown error occurred");
}

return;
}

pInteraction->DisplayMessage(bstrMessage);
pInteraction->Release();
pInteraction = NULL;

::CoUninitialize();

AfxMessageBox("Your message has been queued");
}
else
{
    AfxMessageBox("please enter a string to send to the queued component.");
}
}
```
```

Because some of this code is not very obvious, take a minute to walk through it to understand what is required on the client side.

The first thing the function does is to call UpdateData(FALSE) in order to retrieve the value that is entered on the dialog into the m_strMessage member variable. When that is done, a simple trimming of white space and verification that the string wasn't NULL takes place.

Now, we get to some basic COM stuff. A pointer to the IInteraction interface is declared as well as an HRESULT variable. After that is done, the m_strMessage member