---
{"dg-publish":true,"permalink":"/examples/working-with-dates-and-a-database/","dgHomeLink":true}
---

# Working with Dates and a Database

Dates are tricky for a variety of reasons.

In short, when building a SwiftUI app, you should always use the `Date` data type when storing a date, a time, or a date and a time, like this:

![Screenshot 2024-06-12 at 8.17.16 PM.png](/img/user/Media/Screenshot%202024-06-12%20at%208.17.16%E2%80%AFPM.png)

When defining a database [hosted at Supabase](https://supabase.com) be sure to use the `timestamptz` data type.

Like this:

![Screenshot 2024-06-12 at 6.42.24 PM.png](/img/user/Media/Screenshot%202024-06-12%20at%206.42.24%E2%80%AFPM.png)

... and this:

![Screenshot 2024-06-12 at 6.42.19 PM.png](/img/user/Media/Screenshot%202024-06-12%20at%206.42.19%E2%80%AFPM.png)

That database table matches the Swift structure shared above.

Here is an example app that shows data that contains a date being created, added to the database table, and then refreshed to show in the app:

![Screen Recording 2024-06-12 at 8.18.26 PM.gif](/img/user/Media/Screen%20Recording%202024-06-12%20at%208.18.26%E2%80%AFPM.gif)

You can view [the commit history for this app here](https://github.com/lcs-rgordon/DatesExample/commits/main/), or [download it to try it out here](https://github.com/lcs-rgordon/DatesExample/archive/refs/heads/main.zip). Feel free to use or adapt this in your own work.