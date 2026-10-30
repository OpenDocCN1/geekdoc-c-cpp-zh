```
if (IsFailed(r))
{
    AppLog("Sorry, can't update status text.");
}
```

# Hints, Pitfalls, and Related Topics

Make sure that the correct event handler is registered when constructing the SnsGateway instance (see step 2). Otherwise, your app will not receive the expected call-back.

An alternative approach to using Twitter from your applications is to use Twitter's own RESTful APIs directly. You can use bada's HTTP API to achieve this. Using Twitter APIs directly gives you greater flexibility, but is of course more complex.

# Related Recipe

+   - Use the bada SNS Gateway to Access a Social Network Service such as Facebook

# 7.4 Upload a Photo to Facebook

# Problem Description

You want to upload a photo to Facebook from your app.

# The Recipe

The following configuration is required for this recipe:

| Namespaces used: | Osp::Social::Services |
| Header files to #include: | FS ocial.h |
| Required libraries: | FS ocial, FS ocialServices, FS ocialServicesSnsAuth |
| Required privilege level: | System |
| Required privilege groups: | SNS_SERVICE |