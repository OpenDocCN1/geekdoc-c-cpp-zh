# 7.2 Use the bada SNS Gateway to Access a Social Network Service such as Facebook

# Problem Description

You need an easy way to use a social networking service like Facebook from your bada app. You can use the bada SNS Gateway.

# The Recipe

The following configuration is required for this recipe:

**Namespaces used:**
Osp::Social::Services, Osp::Base::Collection

**Header files to #include:**
FSocial.h, FBase.h

**Required libraries:**
FSocial, FSocialServices, FSocialServicesSnsAuth

**Required privilege level:**
System

**Required privilege groups:**
SNS_SERVICE

The bada SNS Gateway provides a unified API that enables easy access to social networking services (SNS), such as Facebook, Twitter, and MySpace. The Gateway supports many basic use-cases, and also provides simple authentication that can be used for subsequent interaction with the services’ own RESTful APIs if you need more complex interactions.

The API is asynchronous, and uses listener methods of interface classes to enable call-backs to be received from the framework when events of interest occur. To use a listener, an app derives a suitable object, for example a Form, from the appropriate interface class, and implements a listener method to handle events of interest.

The SNS Gateway provides listeners for four different kinds of event:

+   - nsActivityListener: receives responses to activity requests made to the Gateway.

+   - nsGatewayListener: receives events related to the login status of the client app.