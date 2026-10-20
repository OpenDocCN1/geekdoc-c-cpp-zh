# 21 Validating Forms: The Basics

Client-side validation is a must-have. Seriously. Regardless of your users’ connection throughput, having to do a round-trip on the server for any validations that could be done straight in the browser is a crying shame. You don’t want to feel anything but pride about your web pages, so let’s dive in!

This first task focuses on the most basic type of validation: required fields, that is, verifying that specific fields have nonblank text or are checked, and so on. We’ll use a convention of tagging such fields with the required CSS class and rely on styling for visual feedback on missing fields.

First, be sure to intercept the form’s submit event, not the submit button’s click or text fields’ Return keys. The only surefire way of catching a form before it goes to the server is its submit event. It even fires on programmatic submissions (form.submit() calls).

Once hooked in, we just need to grab all elements in the form tagged as required and verify that they have a nonblank value. Prototype’s blank() extension on String is convenient here. Strings containing nothing but whitespace are deemed blank, and from a semantic point of view, they sure are no better than actual empty strings. Note, however, that if you have a field where whitespace-only is considered all right, you can just use if (field.getValue())—in JavaScript, empty strings are false-equivalent.

Our code maintains a firstOffender reference so we can help the user correct input by autofocusing the first problematic field. Last but certainly not least, once we’re done with our checks, if there is at least one problem, we stop() the event, effectively preventing the current form from being submitted.

As a final reminder, out of the box, submit events do not bubble in Internet Explorer. So if your code needs to run in IE too, you would have to attach an event listener for every single form on the page you want to check, including dynamically inserted forms obtained after initial DOM loading. jQuery simulates bubbling for submit in IE since version 1.4 but at the cost of somewhat heavy monitoring of all clicks and keypresses within all forms.