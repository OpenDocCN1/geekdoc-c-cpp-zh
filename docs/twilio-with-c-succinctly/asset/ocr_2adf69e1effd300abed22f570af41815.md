![](bbox=[0.26, 0.09, 0.73, 0.34])

*Figure 32: Azure Storage Explorer Add Account Settings*

After entering the requested details, you should click Test Access in order to check if the connection works. If that is successful, you can click Save.

With these details stored, the next time you open the Azure Storage Explorer application, you’ll be able to access your Storage account from the dropdown next to the Add Account button.

With our Storage account wired up, let’s now explore how we can do some SMS automation with Twilio and use Table Storage as our backend.

# Appointment reminders

Keeping customers happy is probably the biggest challenge any company faces today. Fortunately, the right attitude and a bit of automation can make customer satisfaction an achievable goal.

Appointment reminders are a simple and effective way of automating the process of reaching out to customers before an upcoming appointment. We can write code that will allow us to accomplish this—we’ll use the `TwilioCore` class we’ve already written.

Let’s first think for a bit about how we can architect this solution. We’ll need to be able to create appointments with a future `DateTime` that we can store on Azure Table Storage. This future `DateTime` will be the appointment’s scheduled date. We’ll also need a process in place that watches when an appointment is scheduled, retrieves the information from Table Storage, and sends out an SMS to the registered phone number for that appointment.

We’ll initially explore the first action that allows us to interact with Azure Table Storage. In order to do that, let’s get the WindowsAzure.Storage NuGet package installed, then create an **Appointment** class.