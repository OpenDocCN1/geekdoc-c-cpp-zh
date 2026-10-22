```
config.action_mailer.default_content_type = "text/plain"
```

This is the default content type for e-mails.

```
config.action_mailer.default_implicit_parts_order =
%w( text/html text/enriched text/plain)
```

We saw on page 616 how Rails will automatically generate multipart messages if it finds template files named xxx.text.plain.rhtml, xxx.text.html.rhtml, and so on. This parameter determines the order in which these parts are added to the e-mail and hence the priority given to them by an e-mail client.

```
config.action_mailer.default_mime_version = "1.0"
```

This is the default mime version for e-mails.

```
config.action_mailer.delivery_method = :smtp | :sendmail | :test
```

This determines the delivery method for e-mail. Use with smtp settings. See the description starting on page 610.

```
config.action_mailer.logger = logger
```

Set this to override the default logger used by the mailer. (If it’s not set, the overall application logger is used.)

```
config.action_mailer.perform_deliveries = true | false
```

If this is false, the mailer will not deliver e-mail.

```
config.action_mailer.raise_delivery_errors = true | false
```

If this is true, an exception will be raised if e-mail delivery fails. Note that Rails knows only about the initial handoff of e-mail to a mail transfer agent. It cannot tell whether mail actually reached its recipient. This parameter is true in the test environment but by default is false in the others.

```
config.action_mailer.register_template_extension extension
```

This registers a template extension so mailer templates written in a templating language other than ERb or Builder are supported.

```
config.action_mailer.sendmail_settings = hash
```

This is a hash containing the following settings:

+   :location This is the location of the sendmail executable. This defaults to /usr/sbin/sendmail.

+   :arguments This contains the command line arguments. This defaults to -i -t.

```
config.action_mailer.smtp_settings = hash
```

See the description starting on page 610.