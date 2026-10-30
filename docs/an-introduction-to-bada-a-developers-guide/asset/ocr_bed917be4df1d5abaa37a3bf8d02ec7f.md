![](bbox=[0.22, 0.12, 0.82, 0.42])

# Figure 5.2 UML sequence diagram – User A.

There are two classes used in this use-case: PrivacyManager and MyListener. Let’s start from User A’s PrivacyManager class, which allows the user to send a privacy control related event to the bada Server, such as set profile exposure level (PEL). The code snippet below demonstrates how to use the PrivacyManager class to set User A’s profile searchable, and how to assign the listener object to this class.

```
MyListener* pMyListener;
pMyListener = new MyListener();
pMyListener->Construct();

pMyPrivacyManager = new PrivacyManager();
pMyPrivacyManager->Construct(*pMyListener);
//Register/assign the listener to PrivacyManager

RequestId reqId;
pMyPrivacyManager->SetProfileExposureLevel(PROFILE_SEARCHABLE, reqId);
```

Another class from User A’s side is the MyListener class, which is the essential class for handling the asynchronous event sent by the bada Server. The following code snippet shows you how to implement the MyListener class.

```
// implementation of MyListener class
class MyListener :
{ public IPrivacyManagerListener
{ };

void
MyListener::OnProfileExposureLevelUpdated(RequestsId reqId, result r,
 const String &errorCode, const String &errorMsg)
{
 //Your implementations for this virtual method
}
```