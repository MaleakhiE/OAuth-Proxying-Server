**Features**

Basic Authentication to OAuth Transformation: Converts Basic Auth headers into OAuth tokens to authenticate requests with Microsoft Graph API.
Email Sending and Reading: Users can send and read emails via Microsoft Graph API, using Azure AD OAuth tokens obtained by the proxy server.
Interactive Frontend: A Streamlit interface for easy user interaction, including email fields and real-time loading indicators.

**1. Sending an Email**
Open the Streamlit app in your browser.
Fill in the Azure AD credentials (Client ID, Client Secret, Tenant ID).
Enter your email address and password in Basic Auth format.
Provide recipient email, subject, and email body.
Click Send Email. The Streamlit app will display a loading spinner until the email is sent successfully or an error occurs.

**3. Reading Recent Emails**
In the Streamlit app, ensure Azure AD credentials, email address, and password are filled.
Click Read Emails. The app will display a loading spinner and fetch recent emails from your inbox.
Emails will be displayed in the Streamlit app with details like subject, sender, and received date.

**Flask Proxy Server**
The Flask server handles two main routes:

- /send_email: Receives Basic Auth credentials and Azure AD information, obtains an OAuth token, and sends an email through Microsoft Graph API.
- /read_emails: Receives Basic Auth credentials and Azure AD information, obtains an OAuth token, and retrieves recent emails from Microsoft Graph API.

**Troubleshooting**

- HTTP 400 Errors: Ensure that all required fields (Client ID, Client Secret, Tenant ID, email, and password) are correctly filled.
- HTTP 404 Errors: Confirm that the Flask server is running and accessible at the URL specified in streamlit_app.py.
- Microsoft Graph API Permissions: Ensure that your Azure AD app has the necessary permissions (Mail.Send and Mail.Read) and that admin consent has been granted.
