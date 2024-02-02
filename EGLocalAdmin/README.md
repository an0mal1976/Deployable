# EGLocalAdmin

EGLocalAdmin is a backend service and frontend application which enables granting of local group rigths including local administrators via a policy drive by Microsoft Entra ID (formally Azure AD).

#### 1. Create a Entra ID Application.

Full documenation can be found [here](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app "here") on registering applications in the Microsoft Identity Platform.

### Create Application.
![](https://github.com/an0mal1976/Deployable/blob/main/EGLocalAdmin/content/CreateApp.png?raw=true)



### Grant Permissions
![](https://github.com/an0mal1976/Deployable/blob/main/EGLocalAdmin/content/GrantPermissions.png?raw=true)

### Or run on powerhsell with appropirate rigths.



Connect-AzureAD

$appName = "EGLocalAdmin"
$appURI = "myapp://EGLocalAdmin"

if(!($myApp = Get-AzureADApplication -Filter "DisplayName eq '$($appName)'"  -ErrorAction SilentlyContinue))
{
    $myApp = New-AzureADApplication -DisplayName $appName -ReplyUrls $appURI
}

$Permission1 = New-Object -TypeName "Microsoft.Open.AzureAD.Model.ResourceAccess" -ArgumentList "0e263e50-5827-48a4-b97c-d940288653c7","Scope"
$Permission2 = New-Object -TypeName "Microsoft.Open.AzureAD.Model.ResourceAccess" -ArgumentList "e1fe6dd8-ba31-4d61-89e7-88639da4683d","Scope"
$Aad = New-Object -TypeName "Microsoft.Open.AzureAD.Model.RequiredResourceAccess"
$Aad.ResourceAppId = "00000003-0000-0000-c000-000000000000"
$Aad.ResourceAccess = $Permission1, $Permission2
Set-AzureADApplication -ObjectId $myApp.ObjectID -RequiredResourceAccess $Aad

To get the AppId run the following command.

"AppID:" + $myApp.AppId

To get the tenant ID run the following command.

(Get-AzureADTenantDetail).objectId


You will still require to approve delegated permisions on behalf of the organisation.



#### 3. Install application

Download the application installer EG_LocalAdmin_Setup.msi

Install application via intune or other means with parameters below.

msiexec /i EG_LocalAdmin_Setup.msi APPID={GUIDOFAPP} TENANTID={GUIDOFTENANT} APPURI={REDIRECTURI e.g. myapp://EGLocalAdmin}


