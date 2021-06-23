# Microsoft Teams Integration
Instructions to setup OpsRamp integration with Microsoft Teams.

## Prerequisites

* Must have (or know who has) administrative privileges within the Azure/O365 tenant associated with the desired Teams Environment.
    * *Must be using a Work or School O365 tenant, personal environments will no work.*
	* *If you just need an account for testing purposes, you can sign up [here](https://developer.microsoft.com/en-us/microsoft-365/dev-program).*
* Must obtain O365 admin credentials or setup an administrative service account and retain those credentials.
* Make sure you've signed into (and downloaded) the [Postman Desktop App](https://www.postman.com/).

## Step 1 - Create an Azure AD Application

1. Go to [portal.azure.com](https://portal.azure.com/) and sign in wih your developer tenant administrator account.
2. Navigate to **Azure Active Directory**.
3. On the left menu, click **App registrations**, the click **New registration**.
![app-registrations](images/appregistrations.png)
4. Set the **Application name** to `Teams Integration` or something similar.
5. Set the **Redirect URI** to `https://oauth.pstmn.io/v1/browser-callback` and click **Register**.
6. In the left menu, click **API Permissions**.
7. Click **Add a permission**, select **Microsoft Graph**, then add permissions from the following table.
    * *Note: I have not yet identified the minimum privileges required, this is simply the list I used to get the integration working*
	
| Type        | Permissions Name  |
| ------------- | ------------- |
| Delegated | ChannelMessage.Edit |
| Application | ChannelMember.Read.All |
| Both | Channel.ReadBasic.All |
| Both | ChannelMessage.Read.All |
| Delegated | ChannelMessage.Send |
| Application | ChannelSettings.Read.All |
| Delegated | Directory.AccessAsUser.All |
| Both | Directory.Read.All |
| Both | Directory.ReadWrite.All |
| Application | Group.Create |
| Both | Group.Read.All |
| Both | Group.ReadWrite.All |
| Both | GroupMember.Read.All |
| Application | GroupMember.ReadWrite.All |
| Both | TeamMember.Read.All |
| Application | Teamwork.Migrate.All |
| Delegated | User.Read |
| Application | User.Read.All |

![app-permissions](images/apppermissions.png)

8. Click **Grant admin consent for** and click **Yes**
    * *Note: If you are not logged in as an administrator you will need an Admin to login and grant consent.*
9. In the left menu click **Overview**.  Here you can obtain your **Application (client)** and **Directory (tenant) IDs**.  Copy them down and store them somewhere secure, you will need them in the next section.
10. In the left menu, click **Certificates & Secrets**.  Click **New client secret**, enter a description, and click **Add**.  Again copy and securely store your `client secret`, you will need it in the next section.

## Step 2 - Authenticate through Postman

1. Fork the Postman collection labeled [Microsoft Graph](https://www.postman.com/microsoftgraph/workspace/microsoft-graph/environment/455214-efbc69b2-69bd-402e-9e72-850b3a49bb21/fork).
1. Give your fork a unique label, this can be anything you want.
1. **IMPORTANT** - Make sure you select **M365 Environment** in the top-right environment drop-down, not **No environment**.
1. Click **Fork Environment**
![forkenvironment.png](images/forkenvironment.png)
1. In `ClientID`, set the **current value** to the **application (client) ID** from step 1.9.
1. In `TenantID`, set the **current value** to the **directory (tenant) ID** from step 1.9.
1. In `ClientSecret`, set the **current value** to the **client secret** value from step 1.10.
1. Click **Save**.

## Step 3 - Obtaining your Access Token

1. Right click the **Delegated** folder and select **Edit**
1. Click the **Authorization** tab.
    * Assuming you've correctly entered your credentials in the previous section, the default settings should all work.
![postmanaccesstoken.png](images/postmanaccesstoken.png)
1. Scroll down and click, **Get New Access Token**.
1. An O365 login pop-up should appear, sign in with your developer tenant administrator account.
1. Click **Proceed**, and then click the **Use Token** button.
1. On the bottom right of the dialog, click **Update**.

## Step 4 - Obtaining the necessary request parameters through Postman.

1. 

## Reference Documentation

* [Microsoft Graph in Postman](https://docs.microsoft.com/en-us/graph/use-postman).
* [Send chatMessage in Teams Channel](https://docs.microsoft.com/en-us/graph/api/channel-post-messages?view=graph-rest-1.0&tabs=http).
* [Custom Integrations in OpsRamp](https://docs.opsramp.com/integrations/a2r/custom-integration/custom-integration/).