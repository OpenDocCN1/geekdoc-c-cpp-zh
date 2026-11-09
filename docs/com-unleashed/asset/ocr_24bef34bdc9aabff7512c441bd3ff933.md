# **LISTING 24.7 Continued**

```
~~~cpp
vtBody.vt = VT_BSTR;
vtBody.bstrVal = BSTR(MessageBody);

//Set up the message and send it
IMSMQMessagePtr pMsg("MSMQ.MSMQMessage");
pMsg->PutLabel(wcsLabel);
pMsg->PutBody(vtBody);
pMsg->Send( pQueue );
wprintf(L"Message sent!\n\n");
~~~
```

# ## Receiving a Message

Receiving a message with smart pointers is actually easier than sending one. Once again, you will need to create a MSMQMessage object. In receive mode, you use the IMSMQQueue::Receive() method to retrieve the message:

```
~~~cpp
//Set up the message and send it
IMSMQMessagePtr pMsg("MSMQ.MSMQMessage");
VARIANT vtTimeout;
vtTimeout.vt = VT_I4;
vtTimeout.lVal = 0;
pMsg = pQueue->Receive( &vtMissing,
                        &vtMissing,
                        &vtMissing,
                        &vtTimeout );
wprintf(L"Retrieved message label:\n\t%s\n",
        (const wchar_t *)pMsg->Label);
wprintf(L"Retrieved message body:\n\t%s\n\n",
        (pMsg->Body).bstrVal );
~~~
```

Notice that you can use vtMissing to take the place of ignored arguments leading up to our field of interest, which is the timeout value. Because you want nonblocking behavior, you supply a four-byte integer variant with a value of zero. Note that C++ allows you to completely leave out trailing parameters that you're not interested in. As you can see, the smart pointer property accessors make this block of code very easy to put together. I should mention the fragile nature of your last print statement. You are making the strong assumption that the message body is a BSTR. You could avoid the danger inherent in assumptions by simply checking the variant type to be sure that it is a BSTR.

![](bbox=[0.84, 0.57, 0.97, 0.84])

# ## Closing a Queue

As you might expect, there's nothing to do here, but I'm a fan of symmetry. The smart pointer destructors handle the entire shutdown behavior involved with releasing interface pointers