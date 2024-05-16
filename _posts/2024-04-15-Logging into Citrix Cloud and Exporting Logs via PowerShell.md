---
Title: Logging into Citrix Cloud and Exporting Logs via PowerShell
date: 2024-04-15- 20:14 +0300
categories: [Blogging,Citrix,scripting]
tags: [blog, scripting,IT, tools,Citrix]
author: Dinusha Tharindu
---
## Logging into Citrix Cloud and Exporting Logs via PowerShell

In this article, we will cover the steps to log in to Citrix Cloud using a PowerShell script and the process for exporting configuration logging data into HTML reports.

### Logging into Citrix Cloud

To run the script, follow these steps to log in to Citrix Cloud via PowerShell:

1. **Open PowerShell.**

2. **Add the Citrix snap-ins:**
   ```powershell
   asnp citrix*
   ```

3. **Authenticate to Citrix Cloud:**
   ```powershell
   Get-XDAuthentication
   ```
   The `Get-XDAuthentication` cmdlet will prompt you to authenticate to Citrix Cloud using your Citrix Cloud identity or Azure AD credentials. It generates an interactive prompt to sign in to Citrix Cloud and complete multi-factor authentication (MFA).

4. **Create an authentication profile:**
   ```powershell
   Set-XdCredentials
   ```
   You can use the `Set-XdCredentials` cmdlet to create an authentication profile to connect to the Citrix Cloud API using a client ID and secret created in the Citrix Cloud portal.

5. **Customer-specific authentication:**
   ```powershell
   Get-XDAuthentication -CustomerId CUSTOMERID
   ```
   This command is used for customer-specific authentication, requiring the `CUSTOMERID` parameter.

### Exporting Logs in HTML

To export configuration logging data into an HTML report, use the following syntax and examples:

#### Description
The `Export-LogReportHtml` cmdlet exports Configuration Logging data into an HTML report. The report consists of two HTML files:
- **Summary.html**: Displays summary information from the high-level operation logs.
- **Details.html**: Shows additional logging data from the low-level operation and operation detail logs.

Hyperlinks in `Summary.html` allow for drill-down into the associated low-level logging data contained within `Details.html`.

#### Examples

1. **Export all logged operations to HTML:**
   ```powershell
   Export-LogReportHtml -OutputDirectory "c:\MyReports"
   ```

2. **Export logged operations started on or after a specified datetime:**
   ```powershell
   Export-LogReportHtml -OutputDirectory "c:\MyReports" -StartDateRange "2012-12-21 09:00"
   ```

3. **Export logged operations started and completed between a date range:**
   ```powershell
   Export-LogReportHtml -OutputDirectory "c:\MyReports" -StartDateRange "2012-12-21 09:00" -EndDateRange "2012-12-31 18:00"
   ```

By following these steps, you can effectively log in to Citrix Cloud and export configuration logging data into detailed HTML reports for analysis and record-keeping.