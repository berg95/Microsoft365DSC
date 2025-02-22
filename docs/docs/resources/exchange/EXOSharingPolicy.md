﻿# EXOSharingPolicy

## Parameters

| Parameter | Attribute | DataType | Description | Allowed Values |
| --- | --- | --- | --- | --- |
| **Name** | Key | String | The Name parameter specifies the unique name of the sharing policy. The maximum length is 64 characters. ||
| **Default** | Write | Boolean | The Default switch specifies that the sharing policy is the default sharing policy for all mailboxes. ||
| **Enabled** | Write | Boolean | The Enabled parameter specifies whether to enable the sharing policy. Valid values for this parameter are $true or $false. ||
| **Domains** | Write | StringArray[] | The Domains parameter specifies domains to which this policy applies and the sharing policy action. ||
| **Ensure** | Write | String | Specify if the Sharing Policy should exist or not. |Present, Absent|
| **Credential** | Write | PSCredential | Credentials of the Exchange Global Admin ||
| **ApplicationId** | Write | String | Id of the Azure Active Directory application to authenticate with. ||
| **TenantId** | Write | String | Id of the Azure Active Directory tenant used for authentication. ||
| **CertificateThumbprint** | Write | String | Thumbprint of the Azure Active Directory application's authentication certificate to use for authentication. ||
| **CertificatePassword** | Write | PSCredential | Username can be made up to anything but password will be used for CertificatePassword ||
| **CertificatePath** | Write | String | Path to certificate used in service principal usually a PFX file. ||

# EXOSharingPolicy

### Description

This resource configures Sharing Policies in Exchange Online.

## Examples

### Example 1

This example is used to test new resources and showcase the usage of new resources being worked on.
It is not meant to use as a production baseline.

```powershell
Configuration Example
{
    param(
        [Parameter(Mandatory = $true)]
        [PSCredential]
        $credsGlobalAdmin
    )
    Import-DscResource -ModuleName Microsoft365DSC

    node localhost
    {
        EXOSharingPolicy 'ConfigureSharingPolicy'
        {
            Name       = "Default Sharing Policy"
            Default    = $True
            Domains    = @("Anonymous:CalendarSharingFreeBusyReviewer", "*:CalendarSharingFreeBusySimple")
            Enabled    = $True
            Ensure     = "Present"
            Credential = $credsGlobalAdmin
        }
    }
}
```

