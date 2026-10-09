```
public static void StopFetch()
{
    started = false;
    Fetch.Stop();
}

public static void Fetch_Elapsed(object sender,
    ElapsedEventArgs e)
{
    if (!started)
    {
        started = true;
        Console.WriteLine(
            "Fetching Oldest Appointment...");

        using (Appointment a = new Appointment(PhoneNumber))
        {
            AppointmentData ad = a.Get();

            if (ad != null)
            {
                using (TwilioCore t = new
                    TwilioCore(cStrTwilioSid, cStrTwilioAuthTk))
                {
                    t.SendSms(cStrTwilioSender, PhoneNumber,
                        $"Reminder of appointment {ad.Id} -
                        {ad.Name} on: {a.FormatTime(ad.Time)}");

                    Console.WriteLine(
                        $"Reminder of appointment
                        {ad.Id} - {ad.Name} on:
                        {a.FormatTime(ad.Time)}");

                    ad.Sent = true;
                }

                a.MarkAssent(ad);
            }
        }

        started = false;
    }
}

public static bool Create(string id, string n, string pn,
    DateTime t)
```