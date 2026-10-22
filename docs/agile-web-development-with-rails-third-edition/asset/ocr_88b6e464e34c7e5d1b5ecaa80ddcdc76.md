# A Friendlier Login System

As the code stands now, if an administrator tries to access a restricted page before they are logged in, they are taken to the login page. When they then log in, the standard status page is displayed—their original request is forgotten. If you want, you can change the application to forward them to their originally requested page once they log in.

First, in the authorize method, remember the incoming request’s URI in the session if you need to log the user in:

```
def authorize
  unless User.find_by_id(session[:user_id])
    session[:original_uri] = request.request_uri
    flash[:notice] = "Please log in"
    redirect_to(:controller => "admin", :action => "login")
  end
end
```

Once we log someone in, we can then check to see whether there’s a URI stored in the session and redirect to it if so. We also need to clear that stored URI once used.

```
def login
  session[:user_id] = nil
  if request.post?
    user = User.authenticate(params[:name], params[:password])
    if user
      session[:user_id] = user.id
      uri = session[:original_uri]
      session[:original_uri] = nil
      redirect_to(uri || { :action => "index" })
    else
      flash.now[:notice] = "Invalid user/password combination"
    end
  end
end
```

the login method. We do this simply by providing an override for the authorize method within the StoreController class:

```
Download depot_q/app/controllers/store_controller.rb
```

```
class StoreController < ApplicationController
  #...
  protected

  def authorize
  end
end
```