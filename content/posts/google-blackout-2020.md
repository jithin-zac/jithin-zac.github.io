---
author: "Jithin Zachariah"
title: "Google Went Down for an Hour"
date: "2020-12-20"
ShowToc: true
---

### Outage

On December 14, 2020, around 04:00 PST All the major Google services had service disruption. All the major services including Gmail, Youtube, Drive, etc were unavailable to the users across the globe. Users were unable to login into their Google account. Logged in users were unable to access various Google services.

### Root Cause

According to the statement released by Google, The Central Identity Management System (CIMS) used by Google was unable to neither authenticate user login requests nor was unable to authorize the request from existing logged-in users. Users have reported that Youtube was accessible in private/incognito mode as it may not have the involvement of the identity management system. All other Non-Google services which had a provision to sign in with the google option also were facing these issues when the users exercised those option.

As per the report, The root cause was an issue in the automated quota management system which reduced capacity for Google’s central identity management system, causing it to return errors globally. Various speculations have been raised regarding the storage quota issue(reduced storage quota) of the CIMS which is dependent on AQMS. Google is yet to release the complete technical details about what caused the AQMS to reduce the capacity of the CIMS.

### Conclusion

Even though the outage lasted only for an hour, millions of users were affected as all the google services and services that exercised sign in with google option faced disruption. Impacts like this show us how much we are dependent on Google services in our daily life. Technically incidents like these alert the engineers to the importance of handling a single point of failure in the system design.

Thank you!
