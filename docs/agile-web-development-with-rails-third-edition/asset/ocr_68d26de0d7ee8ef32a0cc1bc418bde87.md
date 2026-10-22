405 ActiveResource::MethodNotAllowed
409 ActiveResource::ResourceConflict
422 ActiveResource::ResourceInvalid
401..499 ActiveResource::ClientError

+   - You can provide client-side validations by overriding validation methods in the ActiveResource base class. This behaves the same as validation does in ActiveRecord. Server-side validations failures result in a response code of 422, and you can access such failures in the same manner. See Section 20.1, Validation, on page 397 for more details.
+   - Although the default format is XML, you can also use JSON as an alternative. Simply set self.format to :json in your client classes. Be aware that your client will see dates as ISO 8601/RFC 3339-formatted strings and will see decimals as instances of Float if you do so.
+   - In addition to self.site, you can separately set self.user and self.password.
+   - self.timeout enables you to specify how long a web service request should wait, in seconds, before giving up and raising a Timeout::Error.