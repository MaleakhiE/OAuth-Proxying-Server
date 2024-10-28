Features

Basic Authentication to OAuth Transformation: Converts Basic Auth headers into OAuth tokens to authenticate requests with Microsoft Graph API.
Email Sending and Reading: Users can send and read emails via Microsoft Graph API, using Azure AD OAuth tokens obtained by the proxy server.
Interactive Frontend: A Streamlit interface for easy user interaction, including email fields and real-time loading indicators.
Project Structure


.
├── flask_proxy_server.py       # Flask server code
├── streamlit_app.py            # Streamlit frontend application
└── README.md                   # Project documentation
Prerequisites

Python 3.7+
Microsoft Azure AD Application with permissions to use Microsoft Graph API.
Microsoft Graph API permissions to Mail.Send and Mail.Read.
Setup

1. Clone the Repository


git clone https://github.com/MaleakhiE/OAuth-Proxying-Server.git
cd oauth-email-proxy-app
2. Install Required Packages


pip install -r requirements.txt
3. Configure Azure AD Application
Go to the Azure AD portal and create an application.
Note down the Client ID, Client Secret, and Tenant ID.
Assign the application permissions for Mail.Send and Mail.Read under Microsoft Graph API.
Grant admin consent for these permissions.
4. Add Configuration in streamlit_app.py
Edit streamlit_app.py to add the Client ID, Client Secret, and Tenant ID you obtained from Azure AD.

5. Start the Flask Proxy Server
Run the Flask server to handle requests:



python flask_proxy_server.py
This server will run on http://localhost:5000 by default.

6. Start the Streamlit Application
Run the Streamlit app:



streamlit run streamlit_app.py
The Streamlit app will open in a web browser, allowing you to input email details and interact with the Flask proxy server.

Usage

1. Sending an Email
Open the Streamlit app in your browser.
Fill in the Azure AD credentials (Client ID, Client Secret, Tenant ID).
Enter your email address and password in Basic Auth format.
Provide recipient email, subject, and email body.
Click Send Email. The Streamlit app will display a loading spinner until the email is sent successfully or an error occurs.
2. Reading Recent Emails
In the Streamlit app, ensure Azure AD credentials, email address, and password are filled.
Click Read Emails. The app will display a loading spinner and fetch recent emails from your inbox.
Emails will be displayed in the Streamlit app with details like subject, sender, and received date.
Code Overview

Flask Proxy Server (flask_proxy_server.py)
The Flask server handles two main routes:

/send_email: Receives Basic Auth credentials and Azure AD information, obtains an OAuth token, and sends an email through Microsoft Graph API.
/read_emails: Receives Basic Auth credentials and Azure AD information, obtains an OAuth token, and retrieves recent emails from Microsoft Graph API.
Streamlit Application (streamlit_app.py)
The Streamlit app provides a user-friendly interface to input email and Azure AD credentials, as well as send or read emails. It communicates with the Flask server using HTTP POST requests.

Troubleshooting

HTTP 400 Errors: Ensure that all required fields (Client ID, Client Secret, Tenant ID, email, and password) are correctly filled.
HTTP 404 Errors: Confirm that the Flask server is running and accessible at the URL specified in streamlit_app.py.
Microsoft Graph API Permissions: Ensure that your Azure AD app has the necessary permissions (Mail.Send and Mail.Read) and that admin consent has been granted.
Security Considerations

Do not hardcode sensitive information (e.g., client secrets) in your source files for production environments.
This application is designed for demo purposes. Implement secure token storage, HTTPS, and other security measures for production use.
