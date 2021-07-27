## Prerequisites

* Must have (or know who has) administrative privileges within the Azure/O365 tenant associated with the desired Teams Environment.
    * *Must be using a Work or School O365 tenant, personal environments will not work.*
	* *If you just need an account for testing purposes, you can sign up [here](https://developer.microsoft.com/en-us/microsoft-365/dev-program).*
* Must obtain Azure admin credentials or setup an administrative service account and retain those credentials.
* Make sure you've signed into (and downloaded) the [Postman Desktop App](https://www.postman.com/).

## Step 1 - Create an Azure AD Application

1. Go to [portal.azure.com](https://portal.azure.com/) and sign in with your developer tenant administrator account.
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
| Both | Reports.Read.All |

![app-permissions](https://client-shared.s3.us-west-2.amazonaws.com/misc/apppermissions.png)

8. Click **Grant admin consent for** and click **Yes**
    * *Note: If you are not logged in as an administrator you will need an Admin to login and grant consent.*
9. In the left menu click **Overview**.  Here you can obtain your **Application (client)** and **Directory (tenant) IDs**.  Copy them down and store them somewhere secure, you will need them in the next section.
10. In the left menu, click **Certificates & Secrets**.  Click **New client secret**, enter a description, and click **Add**.  Again copy and securely store your **client secret**, you will need it in the next section.