---
title: How to Use IdFix Tool for Azure AD Synchronization Error Remediation
date: 2024-02-23 20:14 +0300
categories: [Blogging, Tutorial]
tags: [blog, azuread, tools, Effort]
author: Dinusha Tharindu
---
**How to Use IdFix Tool for Azure AD Synchronization Error Remediation**

If you're the admin of an Azure AD/Office 365 tenant and have installed AD sync on your on-prem servers, chances are you've received notification emails titled "Sync errors detected on your Azure AD Connect service."

These notifications often stem from synchronization errors between on-premises servers and Office 365, typically due to duplicate entries and formatting errors.

To address this issue, Microsoft recommends using a tool called "IdFix," designed to identify errors like duplicates and formatting problems in Active Directory Domain Services (AD DS) domains.

**What is IdFix?**

IdFix is utilized to discover and remediate identity object and attribute errors in an on-premises Active Directory environment, preparing it for migration to Azure Active Directory. You can download the tool using the link below:

[IdFix Download Link](https://www.microsoft.com/en-us/download/details.aspx?id=36832)

**Using IdFix:**

Once you've downloaded the tool, follow these steps:

1\. **Extract and Run:**

   - Download the zip file, extract it, and run the EXE called IdFix with appropriate permissions to the forest. Microsoft recommends the following permissions:

     - Permissions: The application runs in the context of the authenticated user, meaning it queries the authenticated forest and requires read rights to the directory. For applying changes to the directory, the authenticated user needs write permission to the desired objects.

2\. **Querying the Directory:**

   - Open the tool and click on "Query." This action queries the entire directory, searching for errors. The time taken depends on the size of your directory.

3\. **Identifying Errors:**

   - Once the tool completes its run, it displays various types of issues such as duplications, invalid characters, and format errors. Depending on the error type, you can take appropriate actions in the "Action" section. See below screenshot for reference.

4\. **Applying Changes:**

   - After selecting all actions, you can apply changes to the directory by clicking "Apply."

5\. **Verification and Resolution:**

   - You can reduce the number of synchronization errors by addressing the identified issues. Verify the changes by rerunning the tool. Once all entries are fixed, run a full sync using Azure AD Connect to resolve your AD sync problem.

For detailed guidance on fixing different types of attributes and errors using the IdFix tool, refer to the Microsoft article below:

[Microsoft Article: Prepare Directory Attributes for Synchronization with IdFix](https://docs.microsoft.com/en-us/office365/enterprise/prepare-directory-attributes-for-synch-with-idfix)

**Happy Fixing! :)**
