# Implementing-Conditional-Access-Policy
Implementing Conditional Access Policy

Phase 1: Create the "Break-Glass" Account
A break-glass account is a highly privileged, cloud-only emergency account excluded from all Conditional Access policies.

1. Create a new user
2. **Name:** `Emergency Access`
3. **User Principal Name:** `breakglass@sajemaph.onmicrosoft.com`
4. **Password:** Qoxu390523
5. **Roles:** Assign this user the **Global Administrator** role.
6. Create the user. *Do not set up MFA for this specific account.*

Phase 2: Building the Conditional Access Policy
*This will enforce enforce Multi-Factor Authentication (MFA) for everyone else in SajemaPH whenever they try to access any corporate application.

1. In the Azure Portal search bar, type **Conditional Access** and select it.
2. Click **Create new policy**.
3. **Name your policy:** `CA-01-RequireMFA-AllUsers-AllApps`.

**Configure the Assignments:**
•	Users: Click the link under Users.
•	Under the **Include** tab, select **All users**.
•	Under the **Exclude** tab, select **Users and groups**, and search for your `Emergency Access` break-glass account.
•	**Target resources:** * Click the link.
•	Under the **Include** tab, select ** All resources (formerly 'All cloud apps') **.
•	**Conditions:** * We will leave this blank for this specific policy, meaning it applies regardless of location, device, or risk.

**Configure the Access Controls:**
•	**Grant:** * Click the link.
•	Select **Grant access**.
•	Check the box for **Require multifactor authentication**.
•	Click **Select**.

**Enable the Policy:**
•	Under **Enable policy**, you will see three options: *Report-only*, *On*, and *Off*.
It is best practice to always start with **Report-only**. This allows you to check the sign-in logs to see what *would* have happened without actually blocking anyone.
•	For this lab, toggled it to **On** and click **Create**.

<img width="339" height="409" alt="image" src="https://github.com/user-attachments/assets/1424bb2d-7337-4d02-8df7-58ee3c7ea942" />

Phase 3: Testing the User Experience (UX)

1. Open a fresh **Incognito/Private browsing window**. Go to `myapps.microsoft.com` and log in as Kobe.
2. The Trigger: After entering the password, Kobe will be immediately stopped by a prompt stating: **"More information required"** or **"Help us protect your account."**

<img width="289" height="324" alt="image" src="https://github.com/user-attachments/assets/20531d2e-3e09-4fa6-9ce5-81fb77ec82b9" />

4.	This is the Conditional Access policy stepping in. Kobe is now forced to register for MFA (typically using the Microsoft Authenticator app or a phone number) before they are allowed to see the WorkDay app.

Phase 4: Logging and Auditing
1. Go back to your admin portal and navigate to **Entra ID > Monitoring & health > Sign-in logs**.
2. Find Kobe’s recent sign-in attempt.
3. Click on the log entry and navigate to the **Conditional Access** tab.
4. You will see `CA-01-RequireMFA-AllUsers-AllApps` listed with a result of **Success** (meaning the policy successfully applied and evaluated the login).

<img width="975" height="264" alt="image" src="https://github.com/user-attachments/assets/34a9ffa3-950d-4f1b-872b-afe8d975cc58" />
