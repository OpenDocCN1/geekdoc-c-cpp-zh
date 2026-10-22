The first thing we need to do is make the SESSION_KEY a constant that can be referred to later in the application. In your config/environment.rb file, this value is currently hardcoded in the assignment to config.action_controller.session. We need to refactor that out:

```
Download e1/cookies/cookie2/config/environment.rb
# Be sure to restart your server when you modify this file

# Uncomment below to force Rails into production mode when
# you don't control web/app server and can't set it the proper way
# ENV['RAILS_ENV'] ||= 'production'

# Specifies gem version of Rails to use when vendor/rails is not present
RAILS_GEM_VERSION = '2.2.2' unless defined? RAILS_GEM_VERSION

# Bootstrap the Rails environment, frameworks, and default configuration
require File.join(File.dirname(__FILE__), 'boot')

# Define session key as a constant
SESSION_KEY = '_cookie2_session'

Rails::Initializer.run do |config|
  # ...

  # Your secret key for verifying cookie session data integrity.
  # If you change this key, all old sessions will become invalid!
  # Make sure the secret is at least 30 characters and all random,
  # no regular words or you'll be exposed to dictionary attacks.
  config.action_controller.session = {
    :session_key => SESSION_KEY,
    :secret      => 'cbd4061f23fe1dfeb087dd38c...888cdd186e23c9d7137606801cb7665'
  }

  # ...
end
```

Now we need to do two things.

First, we need to define a cookies_required filter that we apply to all actions in our application that require cookies. For simplicity, we will do it for all actions except for the cookies test itself. If your application has different needs, adjust accordingly. This method does nothing if the session is already defined; otherwise, it attempts to save the request URI in a new session and redirect to the cookies test.

Then we need to define the cookies_test method itself. It, too, is straightforward: if there is no session, we log that fact and render a simple template that will inform the user that enabling cookies is required in order to use this application. If there is a session at this point, we simply redirect back, taking care to provide a default destination in case some joker decides to directly access this