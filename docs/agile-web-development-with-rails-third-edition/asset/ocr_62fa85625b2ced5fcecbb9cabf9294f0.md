Here's a typical e-mail unit test:

Download e1/mailer/test/unit/order_mailer_test.rb

```
require 'test_helper'

class OrderMailerTest < ActionMailer::TestCase
  tests OrderMailer

  def setup
    @order = Order.new(:name => "Dave Thomas", :email => "dave@pragprog.com")
  end

  def test_confirm
    response = OrderMailer.create_confirm(@order)
    assert_equal("Pragmatic Store Order Confirmation", response.subject)
    assert_equal("dave@pragprog.com", response.to[0])
    assert_match(/Dear Dave Thomas/, response.body)
  end
end
```

The setup method creates an order object for the mail sender to use. In the test method we get the mail class to create (but not to send) an e-mail, and we use assertions to verify that the dynamic content is what we expect. Note the use of assert_match to validate just part of the body content.

# Functional Testing of E-mail

Now that we know that e-mails can be created for orders, we'd like to make sure that our application sends the correct e-mail at the right time. This is a job for functional testing.

Let's start by generating a new controller for our application:

```
depot> ruby script/generate controller Order confirm
```

We'll implement the single action, confirm, which sends the confirmation e-mail for a new order:

Download e1/mailer/app/controllers/order_controller.rb

```
class OrderController < ApplicationController
  def confirm
    order = Order.find(params[:id])
    OrderMailer.deliver_confirm(order)
    redirect_to(:action => :index)
  end
end
```

We saw how Rails constructs a stub functional test for generated controllers back in Section 14.3, Functional Testing of Controllers, on page 224. We'll add our mail testing to this generated test.

Action Mailer does not deliver e-mail in the test environment. Instead, it adds each e-mail it generates to an array, ActionMailer::Base.deliveries. We'll use this