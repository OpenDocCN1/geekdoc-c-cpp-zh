
```
if (IsFailed(r))
{
    Util::ShowMessage(L"Error!",
        L"Sorry, can't get the Albums.");
    AppLog("OnSnsPhotoAlbumsReceivedN() is failed.");
    return;
}

IEnumerator*      pEnum = null;
SnsAlbumInfo*     pAlbum = null;
String            albumId;
String            albumTitle;

//make item to add following list

Util::DeleteList(pAlbumList);
pAlbumList = pAlbumList;
pEnum = pAlbumList->GetEnumeratorN();

while ((pEnum->MoveNext() != E_OUT_OF_RANGE))
{
    pAlbum = static_cast<SnsAlbumInfo*>(pEnum->GetCurrent());

    albumId = pAlbum->GetAlbumId();

    pAlbum->GetValue(SNS_ALBUM_PID_TITLE, albumTitle);
    //You can use this value as per the requirement
}
delete pEnum;
}
```

## Hints, Pitfalls, and Related Topics

Be sure to register the appropriate event handlers during construction of the SnsGateway instance, in step 4 above. Each type of listener has a different position in the argument list to the Constructor.

Remember, also, to add SnsAuthResult to the SnsGateway instance. This authentication result is crucial, especially if you want to incorporate other features that are not supported out of the box by the bada SNS Gateway; in this case, you can interact with the RESTful API's provided by the service provider using the token key and token secret, which are generated as part of the application authentication process.

Follow the steps 1–7 in the recipe ‘Use the bada SNS Gateway to Access a Social Network Service such as Facebook’ to set up and authenticate with the SNS Gateway. To do so your requesting class should inherit from ISnsAuthenticatorListener and ISnsGatewayListener

After your app has successfully authenticated with the bada Server, you can go on to post tweets. To do so, you use the ISnsPeopleListener interface.

Figure R7.2 shows an app that provides users with a simple editable control to write text in, and an update button that sends the text as a tweet from the user’s Twitter account.

![](img/a257d5fd53a79a244a20e587cd2f08f6_454_0.png)

Figure R7.2 Writing and posting a tweet to a Twitter account. The Update button posts the tweet, which you can see displayed in the Twitter stream below.

Let’s see how this looks in code.

- 1. Derive your class from ISnsAuthenticatorListener for authentication via SnsAuthenticator, from ISnsGatewayListener for SnsGateway functions, and from ISnsPeopleListener for the interaction with Twitter. Note that your implementations of unused interface methods can be empty.

```
#include <FSocial.h>

class MyTwitterClass :
    public Osp::Social::Services::ISnsAuthenticatorListener,
    public Osp::Social::Services::ISnsGatewayListener,
    public Osp::Social::Services::ISnsPeopleListener
{
    Osp::Social::Services::SnsGateway* pSnsGateway;
    Osp::Social::Services::SnsAuthenticator* pSNSAuthenticator;
    Osp::Social::Services::SnsAuthResult* pSNSAuthResult;

    result Initialize(void);

    result SubmitTweet(const Osp::Base::String tweet);

    // ISnsAuthenticatorListener function
    void OnSnsAuthenticated(Osp::Social::Services::SnsAuthResult &snsAuthResult, result r,
        const Osp::Base::String& errorCode,
        const Osp::Base::String& errorMsg);

    // ISnsGatewayListener
    void OnSnsLoggedInStatusReceived(RequestId reqId,
        Osp::Base::String& serviceProvider,
        bool isLoggedIn, result r,
        const Osp::Base::String& errorCode,
        const Osp::Base::String& errorMsg);

    // ISnsPeopleListener
    void OnMySnsBuddiesReceivedN(RequestId reqId,
        Osp::Base::Collection::IList *pBuddyProfileList,
        bool hasNext,
        Osp::Social::Services::SnsPagingParam &pagingParam,
        result r, const Osp::Base::String &errorCode,
        const Osp::Base::String& errorMsg);
    void OnSnsStatusTextReceived(RequestId reqId,
        Osp::Social::Services::SnsStatusText *pStatusText,
        result r,
        const Osp::Base::String errorCode,
        const Osp::Base::String& errorMsg);
    void OnSnsProfileReceived(RequestId reqId,
        Osp::Social::Services::SnsProfile *pProfile,
        result r,
        const Osp::Base::String errorCode,
        const Osp::Base::String& errorMsg);
```

```
void OnMySnsStatusTextUpdated(RequestId reqId,
    Osp::Base::String &serviceProvider,
    result r,
    const Osp::Base::String &errorCode,
    const Osp::Base::String &errorMsg);
```

2. Authentication follows the steps shown in the recipe ‘Use the bada SNS Gateway to Access a Social Network Service such as Facebook’, except for the position of the intended listener method supplied as an argument when you construct the SnsGateway instance. To use Twitter the listener is ISnsPeopleListener, which is supplied as the third argument in the function call (as this, because we make the call from an ISnsContentListener -derived class):

```
pSnsGateway->Construct(this, null, this, null);
```

3. After successful authentication, post the tweet with:

```
pSnsGateway->UpdateMyStatusText(L"twitter", tweet, reqId);
```

where L"twitter" is the requested service (note use of the L macro to construct the string), tweet is the message text, and reqId is a RequestId that will be filled by the server when the request completes (you might use it to track which call completed if you are making multiple requests to the server).

```
result
MyTwitterClass:: SubmitTweet(const String tweet)
{
    result r = E_SUCCESS;

    RequestId reqId = INVALID_REQUEST_ID;

    r =pSnsGateway->UpdateMyStatusText(L"twitter", tweet, reqId);

    if (IsFailed(r))
        AppLog("Fail to . [%s]", GetErrorMessage(r));

    return r;
}
```

4. On completion, SnsGateway::OnMySnsStatusTextUpdated() is the call-back method that contains the results of the update request. Implement this method to handle any errors. The value in result r contains the result of the update request, and the errorCode and errorMsg strings give further information about any error.

```
void
MyTwitterClass::OnMySnsStatusTextUpdated (RequestId reqId,
    String &serviceProvider, result r,
    const String &errorCode, const String &errorMsg)
```

```
if (IsFailed(r))
{
    AppLog("Sorry, can't update status text.");
}
```

## Hints, Pitfalls, and Related Topics

Make sure that the correct event handler is registered when constructing the SnsGateway instance (see step 2). Otherwise, your app will not receive the expected call-back.

An alternative approach to using Twitter from your applications is to use Twitter's own RESTful APIs directly. You can use bada's HTTP API to achieve this. Using Twitter APIs directly gives you greater flexibility, but is of course more complex.

## Related Recipe

- Use the bada SNS Gateway to Access a Social Network Service such as Facebook

## 7.4 Upload a Photo to Facebook

### Problem Description

You want to upload a photo to Facebook from your app.

### The Recipe

The following configuration is required for this recipe:

| Namespaces used: | Osp::Social::Services |
| Header files to #include: | FSocial.h |
| Required libraries: | FSocial, FSocialServices, FSocialServicesSnsAuth |
| Required privilege level: | System |
| Required privilege groups: | SNS_SERVICE |

You can easily upload a photo to Facebook from your app by using the bada SNS Gateway.

The basic steps for interacting with the Gateway are described in the recipe ‘Use the bada SNS Gateway to Access a Social Network Service such as Facebook’. The steps required to use Facebook via the Gateway are similar to those for Twitter, described in the recipe ‘Send a Tweet from Twitter’. When authenticating with the Gateway to use Facebook you should specify facebook as the service provider:

```
String serviceProvider = "facebook";
r = pSNSAuthenticator->Authenticate(serviceProvider, appID, appSecret);
```

The same comments apply in this recipe as in related recipes about the keys needed to authenticate with social network services, and about required bada privileges. For more about both topics, and for Facebook-specific guidance, see the documentation at developer.bada.com.

Follow the steps 1-7 in the recipe ‘Use the bada SNS Gateway to Access a Social Network Service such as Facebook’ to set up and authenticate with the SNS Gateway. To do so your requesting class should inherit from ISnsAuthenticatorListener and ISnsGatewayListener.

In addition, to upload a photo to Facebook, inherit the ISnsContentListener interface and implement the ISnsContentListener::OnSnsPhotoUploaded() method, which will receive the response from the framework when your upload request completes.

To upload the photo, call the SnsGateway::UploadPhoto() method. Let’s see how this looks in code.

- 1. Inherit the required interface classes and provide implementations of the interface methods. Note that many of these can be empty implementations. For example, the only ISnsContentListener method we require is OnSnsPhotoUploaded().

```
#include <FSocial.h>

class MyFacebookClass :
public Osp::Social::Services::ISnsAuthenticatorListener,
public Osp::Social::Services::ISnsGatewayListener,
public Osp::Social::Services::ISnsContentListener
{
Osp::Social::Services::SnsGateway* pSnsGateway;
Osp::Social::Services::SnsAuthenticator* pSNSAuthenticator;
Osp::Social::Services::SnsAuthResult* pSNSAuthResult;

result Construct(void);

result Authenticate(void);
```
