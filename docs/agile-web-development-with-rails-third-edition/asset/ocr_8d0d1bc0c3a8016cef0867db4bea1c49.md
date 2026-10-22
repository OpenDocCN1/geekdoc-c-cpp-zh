Once installed, you add support to all your application’s controllers by adding an include to your application controller:

```
class ApplicationController < ActionController::Base
  include SslRequirement
end
```

Now you can set policies for individual actions in each of your controllers. The following code comes straight from the plug-in’s README file:

```
class AccountController < ApplicationController
  ssl_required :signup, :payment
  ssl_allowed :index

  def signup
    # Non-SSL access will be redirected to SSL
  end

  def payment
    # Non-SSL access will be redirected to SSL
  end

  def index
    # This action will work either with or without SSL
  end

  def other
    # SSL access will be redirected to non-SSL
  end
end
```

The ssl_required declaration lists the actions that can be invoked only by HTTPS requests. The ssl_allowed declaration lists actions that can be called with either HTTP or HTTPS.

The trick with the ssl_requirement plug-in is the way it handles requests that don’t meet the stated requirements. If a regular HTTP request comes along for a method that has been declared to require SSL, the plug-in will intercept it and immediately issue a redirect back to the same URL, but with a protocol of HTTPS. That way the user will automatically be switched to a secure connection without the need to perform any explicit protocol setting in your application’s views.⁶ Similarly, if an HTTPS request comes in for an action that shouldn’t use SSL, the plug-in will automatically redirect back to the same URL, but with a protocol of HTTP.

> 6. But, of course, that ease of use comes at the expense of having an initial redirect to get you from the HTTP to the HTTPS world. Note that this redirect happens just once. Once you’re talking HTTPS, the regular link_to helpers will automatically keep generating HTTPS protocol requests.