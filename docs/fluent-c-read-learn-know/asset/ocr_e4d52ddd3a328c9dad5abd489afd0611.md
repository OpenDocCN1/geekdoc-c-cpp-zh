![](bbox=[0.09, 0.06, 0.2, 0.21])

# REVIEW

Here's a real test for you. You know that events often come in tunnel/bubble pairs, and that by convention the name of the tunnelling version is prefaced with the word “Preview”. You also know about the `Handled` property. Now, there’s a convention in the Framework that if the `Handled` property of the tunneling event is set to `true`, the bubbling event isn’t raised. So, here’s your job: Write a pair of events, one tunneling and one bubbling, and then write the method that raises the events. Include the check that doesn’t raise the bubbling event if the tunneling event is handled.