look at the API documentation for ActiveRecord::Errors, you'll find a number of other methods. Most of these have been superseded by higher-level validation helper methods.

# Validation Helpers

Some validations are common: this attribute must not be empty, that other attribute must be between 18 and 65, and so on. Active Record has a set of standard helper methods that will add these validations to your model. Each is a class-level method, and all have names that start validates_. Each method takes a list of attribute names optionally followed by a hash of configuration options for the validation.

For example, we could have written the previous validation as follows:

```
class User < ActiveRecord::Base
  validates_format_of :name,
    :with     => /\A\w+$/,
    :message => "is missing or invalid"

  validates_uniqueness_of :name,
    :on       => :create,
    :message => "is already being used"
end
```

The majority of the validates_ methods accept :on and :message options. The :on option determines when the validation is applied and takes one of the values :save (the default), :create, or :update. The :message parameter can be used to override the generated error message.

When validation fails, the helpers add an error object to the Active Record model object. This will be associated with the field being validated. After validation, you can access the list of errors by looking at the errors attribute of the model object. When Active Record is used as part of a Rails application, this checking is often done in two steps:

+   1. The controller attempts to save an Active Record object, but the save fails because of validation problems (returning false). The controller redisplays the form containing the bad data.
+   2. The view template uses the error_messages_for method to display the error list for the model object, and the user has the opportunity to fix the fields.

We cover the interactions of forms and models in Section 23.5, Error Handling and Model Objects, on page 536.

The pages that follow contain a list of the validation helpers you can use in model objects.