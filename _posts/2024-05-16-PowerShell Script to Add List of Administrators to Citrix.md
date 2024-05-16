---
Title: Powershell script to add list of administrators to citrix
date: 2024-05-15- 20:14 +0300
categories: [Blogging,Citrix,scripting]
tags: [blog, scripting,IT, tools,Citrix]
author: Dinusha Tharindu
---

# PowerShell Script to Add List of Administrators to Citrix

## Script Description

This script uses the `Add-AdminRight` cmdlet to add rights (role and scope pairs) to an administrator in Citrix. For convenience, the `-All` parameter can be used to specify the 'All' scope. The `Get-AdminAdministrator` cmdlet is used to determine what rights an administrator has.

## Prerequisites: Authenticate to Citrix Cloud

To run this script, you need to log in to Citrix Cloud via PowerShell. Assume that the PowerShell SDK for Citrix is already installed. Here is the process:

1. **Open PowerShell**

2. **Load Citrix Snap-ins**
    ```powershell
    asnp citrix*
    ```

3. **Authenticate to Citrix Cloud**
    ```powershell
    Get-XDAuthentication
    ```
    `Get-XDAuthentication` will prompt you to authenticate to Citrix Cloud using your Citrix Cloud identity or Azure AD credentials. It will generate an interactive prompt to sign in to Citrix Cloud and complete MFA.

4. **Set Credentials for Citrix Cloud API**
    ```powershell
    Set-XdCredentials
    ```
    You can use `Set-XdCredentials` to create an authentication profile to connect to Citrix Cloud API using a client ID and secret created in the Citrix Cloud portal.

5. **Authenticate with Customer ID**
    ```powershell
    Get-XDAuthentication -CustomerId CUSTOMERID
    ```

## Script

```powershell
# Define the path to the CSV file
$csvFilePath = "path\to\administrators.csv"

# Import the CSV file
$admins = Import-Csv -Path $csvFilePath

# Iterate through each row in the CSV
foreach ($admin in $admins) {
    $administrator = $admin.Administrator
    $role = $admin.Role
    $scope = $admin.Scope

    # Check if the scope is 'All'
    if ($scope -eq 'All') {
        # Add the role with 'All' scope
        Add-AdminRight -Role $role -All -Administrator $administrator
    } else {
        # Add the role with specific scope
        Add-AdminRight -Role $role -Scope $scope -Administrator $administrator
    }

    # Output the assigned rights for verification
    $assignedRights = Get-AdminAdministrator -Name $administrator
    Write-Output "$administrator has been assigned the following rights:"
    $assignedRights.Rights | ForEach-Object { Write-Output "Role: $_.Role, Scope: $_.Scope" }
}
```

## Example CSV File (`administrators.csv`)

```plaintext
Administrator,Role,Scope
DOMAIN\Admin1,Help Desk Administrator,London
DOMAIN\Admin2,Full Administrator,All
DOMAIN\Admin3,Read Only Administrator,New York
```

## Explanation

1. **CSV File Path**: Set the `$csvFilePath` variable to the path where your CSV file is located.
2. **Import-Csv**: The `Import-Csv` cmdlet is used to import the list of administrators from the CSV file.
3. **Iteration**: The `foreach` loop iterates through each administrator entry in the CSV.
4. **Scope Check**: Inside the loop, there's a check to see if the scope is 'All'. If it is, the `-All` parameter is used. Otherwise, the `-Scope` parameter with the specific scope value is used.
5. **Add-AdminRight**: The `Add-AdminRight` cmdlet is called to assign the role and scope to the administrator.
6. **Verification**: After assigning rights, the script retrieves and outputs the assigned rights for verification purposes.

## Running the Script

1. Save the script as a `.ps1` file, for example, `Add-Admins.ps1`.
2. Ensure the CSV file is correctly formatted and saved at the specified path.
3. Open PowerShell with administrative privileges.
4. Execute the script by navigating to its directory and running:
   ```powershell
   .\Add-Admins.ps1
   ```

This script automates the process of adding roles and scopes to multiple administrators in Citrix, making it efficient to manage administrator rights.