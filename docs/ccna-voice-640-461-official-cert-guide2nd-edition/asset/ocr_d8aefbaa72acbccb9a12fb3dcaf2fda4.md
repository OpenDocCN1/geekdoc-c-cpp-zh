the extension his phone should have; in a new deployment, this may be provided to Bob on an information sheet, or it may simply be the same extension (let's assume 5309 in this case) that he had on the old phone system that is being migrated to CUCM.

+   6. When Bob enters the extension, the IP-IVR records his input of "5309" and captures the MAC address of the phone Bob is using. The IP-IVR sends all this information to CUCM.

+   7. CUCM looks up the extension of 5309 in the database, and finds it in the record for the newly-added BAT job phones—one that will become Bob’s phone. CUCM replaces the dummy MAC address in the BAT record with the real MAC captured and forwarded by the IP-IVR. The database record now is complete and accurate, using the real MAC address of the phone that sits on Bob's desk.

+   8. CUCM restarts Bob’s phone, and when it comes online, it is fully configured with all of the specific details from the BAT record for Bob's phone.

This is an exceptionally powerful way to deploy thousands of IP Phones. With some minor tweaks and some training of the users, it requires minimal administrator involvement in the phone deployment. The downside is that it requires the IP-IVR hardware and software and a capable administrator to configure it, and still involves either trainers to set up their own phones or using administrators to perform repetitive tasks, which are not cost-effective uses of their time.

# Describe End Users in CUCM

It is technically true that a phone system doesn't need End Users. A person parks himself in front of a phone and starts using it; it doesn't really matter who the person is as long as the phone does what that person needs it to do. But a Unified Communications system provides far more than phone functionality; it has a massive array of features that can be provided and customized by individual users. Converged networks are increasingly complex, and End Users expect an increasing simplicity of use. The configuration of End Users is an integral part of a full-featured system.

# End Users Versus Application Users

> Key Topic

CUCM makes a clear distinction between End Users and Application Users. The distinction is simple: End Users are typically people who type in a username and password to a login screen (usually a Web page) to access features or controls. An Application User is typically an application that sends authentication inline with a request to read or write information to a system (perhaps a third-party billing application accessing the CDR/CAR database, for example). Table 9-2 lists some of the characteristics and limitations of End Users versus Application Users.