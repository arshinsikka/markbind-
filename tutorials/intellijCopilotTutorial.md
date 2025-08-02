<frontmatter>
title: "IntelliJ IDEA – Using GitHub Copilot"
pageNav: 2
</frontmatter>

# IntelliJ IDEA – Using GitHub Copilot


GitHub Copilot is an AI-powered code assistant that helps you write, test, and refactor code faster. In this tutorial, you’ll learn how to set up and use Copilot in IntelliJ IDEA — perfect for students in CS2103/T, CS2113, and other Java-heavy modules.

<box type="info" seamless>
To use GitHub Copilot for free as a student, you must:

1. Sign up for a GitHub account  
2. Enable two-factor authentication (2FA)  
3. Apply for the GitHub Student Developer Pack  

This guide walks you through setting up Copilot access and using it in IntelliJ IDEA.
</box>


---

## 1. Setting Up GitHub Copilot Access

### Step 1: Fill in Billing Information

1. Visit the [GitHub billing settings page](https://github.com/settings/billing).  
2. Fill in only your billing address (no charges will occur if you qualify for student access).  
3. Click **Save billing information**.

<pic src="images/intellij-copilot/billing-info.png" width="450" />

### Step 2: Enable Two-Factor Authentication (2FA)

1. Go to [GitHub security settings](https://github.com/settings/security).  
2. Click **Enable two-factor authentication** and follow the prompts.  
3. Use an authenticator app (e.g., Google Authenticator, Microsoft Authenticator) to complete setup.

<pic src="images/intellij-copilot/2fa-setup.png" width="400" />

### Step 3: Link Your University Email

1. Go to [GitHub email settings](https://github.com/settings/emails).  
2. Add your university email (e.g., `yourname@u.nus.edu`).  
3. Verify via the confirmation link sent to your inbox.

### Step 4: Apply for GitHub Student Developer Pack

1. Visit the [GitHub Education Pack page](https://education.github.com/pack).  
2. Click **Get student benefits** and complete the application.  
3. After approval, you’ll see a message like “You already have the Student Developer Pack.”

<pic src="images/intellij-copilot/student-pack-confirmed.png" width="500" />

---

## 2. Installing GitHub Copilot Plugin in IntelliJ IDEA

1. Open IntelliJ IDEA.  
2. On Mac: **IntelliJ IDEA > Preferences**. On Windows/Linux: **File > Settings**.  
3. Select **Plugins > Marketplace**.  
4. Search for **GitHub Copilot**.  
5. Click **Install**, then **Restart IDE** when prompted.

<pic src="images/intellij-copilot/plugin-marketplace.png" width="500" />  
<pic src="images/intellij-copilot/plugin-installed-popup.png" width="500" />

---

## 3. Signing In to GitHub

1. After restart, open **Settings > Languages & Frameworks > GitHub Copilot**.  
2. Under **Authentication**, click **Manage GitHub Accounts**.  
3. Sign in via your browser and authorize Copilot.  
4. Your GitHub username should appear in the **Preferred GitHub account** dropdown.

<pic src="images/intellij-copilot/copilot-settings.png" width="600" />

---

## 4. Verifying Copilot in Action

1. Create or open a Java file, e.g., `CopilotTest.java`.  
2. Inside a `main` method, type:

```java
// print Hello World
```

3. Wait 2–3 seconds — a gray suggestion appears.

4. Press Tab to accept the suggestion.

<pic src="images/intellij-copilot/suggestion-visible.png" width="600" />  
<pic src="images/intellij-copilot/suggestion-accepted.png" width="600" />

<box type="tip" seamless>
Copilot works best with clear, descriptive comments.
</box>

---

## 5. Using Copilot Chat *(if available)*

> Copilot Chat may be in beta or limited in IntelliJ.

1. Go to **View > Tool Windows > Copilot Chat**.  
2. Ask a question, e.g.:
Write a function to reverse a string in Java.


3. Review the response and insert code as needed.

<pic src="images/intellij-copilot/copilot-chat-window.png" width="600" />

---

## 6. Troubleshooting

<box type="tip" seamless>
**Common Issues & Fixes**  

- **No suggestions** → Ensure the plugin is enabled and you’re signed in.  
- **No Copilot panel** → Restart IntelliJ or reinstall the plugin.  
- **Unsupported file type** → Use `.java` or other supported languages.  
- **Authentication errors** → Re-authorize in **Settings > GitHub Copilot**.  
</box>

---

**Contributors:** Arshin Sikka (@arshinsikka)



