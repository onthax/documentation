---
---

The **Sessions** widget displays a list of all active sessions, including the user who initiated the session and what time it started.
It also displays the **Token Lifetime** setting for your current session.
It allows administrators to manage other active sessions and to configure the token lifetime for their account.

{{< trueimage src="/images/SCALE/23.10/AdvancedSystemSettingsSessionsWidget.png" alt="Sessions Widget" id="7: Sessions Widget" >}}

The **Terminate Other Sessions** button ends all sessions except for the one you are currently using.
You can also end individual sessions by clicking the logout <span class="iconify" data-icon="bi:box-arrow-in-right"></span> button next to that session.
You must check a confirmation box before the system allows you to end sessions.

The logout button is inactive for your current session and active for all other current sessions.
It cannot be used to terminate your current session.

**Token Lifetime** displays the configured token duration for your current session (default five minutes).
TrueNAS SCALE logs out user sessions that are inactive for longer than that user's configured token setting.
New activity resets the token counter.

If the configured token lifetime is exceeded, TrueNAS SCALE displays a **Logout** dialog with the exceeded ticket lifetime value and the time that the session is scheduled to terminate.

{{< trueimage src="/images/SCALE/23.10/TimeoutDialog.png" alt="Logout Dialog" id="8: Logout Dialog" >}}

Click **Extend Session** to reset the token counter.
If the button is not clicked, the TrueNAS SCALE terminates the session automatically and returns to the log in screen.

Click **Configure** to open the **Token Settings** screen and configure  **Token Lifetime** for the current account.

{{< trueimage src="/images/SCALE/23.10/TokenSettingsScreen.png" alt="Token Settings Screen" id="9: Token Settings Screen" >}}

Select a value that fits your needs and security requirements.
Enter the value in seconds.

{{< hint type=tip >}}
The default lifetime setting is 300 seconds, or five minutes.

The minimum value allowed is 30 seconds.

The maximum is 2147482 seconds, or 20 hours, 31 minutes, and 22 seconds.
{{< /hint >}}

Click **Save**.
