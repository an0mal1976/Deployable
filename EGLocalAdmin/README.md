# EGLocalAdmin

EGLocalAdmin is a backend service and frontend application which enables granting of local group rigths including local administrators via a policy drive by Microsoft Entra ID (formally Azure AD).

#### 1. Create a Entra ID Application.

Full documenation can be found [here](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app "here") on registering applications in the Microsoft Identity Platform.

### Create Application.
![](https://github.com/an0mal1976/Deployable/blob/main/EGLocalAdmin/content/CreateApp.png?raw=true)



### Grant Permissions
![](https://github.com/an0mal1976/Deployable/blob/main/EGLocalAdmin/content/GrantPermissions.png?raw=true)




#### 2. Grant the required Deletegated Rights

#### 3. Install application

Download the application. [EG_LocalAdmin_Setup.msi](https://github.com/an0mal1976/Deployable/blob/main/EGLocalAdmin/EG_LocalAdmin_Setup.msi?raw=true)

Install application via intune or other means with parameters below.

msiexec /i EG_LocalAdmin_Setup.msi APPID={GUIDOFAPP} TENANTID={GUIDOFTENANT} APPURI={REDIRECTURI e.g. myapp://EGLocalAdmin}


