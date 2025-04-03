How to use Power Platform Custom Connector to Retrieve Secrets from Azure Key Vault using OAuth2 Client Credential Flow (Service Principal).

Create a new app registration in Microsoft Entra ID and record the below information. We will need this information to configure OAuth2 settings.

Display name:powerplatformtestapp
Application (client) ID:
Object ID:
Directory (tenant) ID:
Secret: 

Login to Power Apps: https://make.powerapps.com/environments/your-environment-name/customconnectors
Create a new custom connector

Overview tab:
Add description that is more than 30 characters
Scheme: HTTPS
Host: your-keyvalut-fqdn from Azure
Base URL: /

Security Tab:
Select OAuth 2.0 from Authentication type
Identity provider: Azure Active Directory
Check - Enable Service Principal support
Enter Client ID:
Enter Client secret:
Authorization URL: https://login.microsoftonline.com (auto populated when you select Azure Active Directory as Identity provider)
Enter Tenant ID:
Enter Resource URL: example, https://ppkv2966.vault.azure.net
Enable on-behalf-of login: false
Scope: leave it empty
Redirect URL: will be auto created after you save/create the connector
** Note: Client ID and Client secret are not saved in the definition**

Definition tab:
Summary: GetSecret
Description: GetSecret
Operation ID: GetSecret
Visibility: none
Request: + Import from sample
Add: GET https://ppkv2966.vault.azure.net/secrets/ppsecret1/6fa00508f0424a8ca919faa1f100b992?api-version=7.4 (change to your key vault)

You don't have to do anything at AI Plugin(preview) and/or Code tabs.

Save/update connector

Before you can Test, you must create a Connection. You can do so at Test Tab itself or you can go to Connections tab and create new connection. I would rather do at Test tab.
Create/Edit Connection:
Display name: KeyVaultAccess or anything you like
Authentication Type: Service Principal Connection
Client ID:
Client Secret:
Tenant:

Once connection is created successfully, you can go back to Custom connector and jump to Test tab directly
Make sure Selected connection is populated with the connection name that you just created (along with created at date/time)
You would see GetSecret under Operations
Enter api-version: 7.4
Hit Test operation

You should get valid response header and body. Secret value would be in the response body.
