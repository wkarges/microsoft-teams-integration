# Microsoft Teams Integration
Tutorial to setup OpsRamp integration with Microsoft Teams.

## Prerequisites

* Must have (or know who has) administrative privileges within the Azure/O365 tenant associated with the desired Teams Environment.
    * *Must be using a Work or School O365 tenant, personal environments will no work.*
	* *If you just need an account for testing purposes, you can sign up [here](https://developer.microsoft.com/en-us/microsoft-365/dev-program).*
* Must obtain O365 admin credentials or setup an administrative service account and retain those credentials.
* Make sure you've signed into (and downloaded) the [Postman Desktop App](https://www.postman.com/).

## Step 1 - Create an Azure AD Application

1. Go to [portal.azure.com](https://portal.azure.com/) and sign in wih your developer tenant administrator account.
1. Navigate to **Azure Active Directory**.
1. On the left menu, click **App registrations**, the click **New registration**.
![app-registrations](images/appregistrations.png)
1. Set the **Application name** to `Teams Integration` or something similar.
1. Set the **Redirect URI** to `https://oauth.pstmn.io/v1/browser-callback` and click **Register**.
1. In the left menu, click **API Permissions**.
1. Click **Add a permission**, select **Microsoft Graph**, then add permissions from the following table.
    * *Note: I have not yet identified the minimum privileges required, this is simply the list I used to get the integration working*
	
| Type        | Permissions Name  |
| ------------- | ------------- |
| Delegated | ChannelMessage.Edit |
| Application | ChannelMember.Read.All |
| Both | Channel.ReadBasic.All |
| Both | ChannelMessage.Read.All |
| Delegated | ChannelMessage.Send |
| Application | ChannelSettings.Read.All |

1.

## Reference Documentation

* [Microsoft Graph in Postman](https://docs.microsoft.com/en-us/graph/use-postman).
* [Send chatMessage in Teams Channel](https://docs.microsoft.com/en-us/graph/api/channel-post-messages?view=graph-rest-1.0&tabs=http).
* [Custom Integrations in OpsRamp](https://docs.opsramp.com/integrations/a2r/custom-integration/custom-integration/)