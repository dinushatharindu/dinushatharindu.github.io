## Microsoft Teams 2.1 VDI/DaaS Compatibility

**Applicable Products**
- Citrix DaaS
- Citrix Cloud
- Citrix Virtual Apps and Desktops

**Overview**
Microsoft has introduced Microsoft Teams for Virtual Desktop Infrastructure (VDI) in early December 2023. This updated version of Teams has been re-engineered to enhance performance, reduce memory consumption, improve usability, and bolster security. For detailed information on the new Teams, refer to [Microsoft's official documentation](https://learn.microsoft.com/en-us/microsoftteams/new-teams-desktop-admin).

However, there are two significant limitations to note regarding the implementation of the new Teams within your Citrix environment:

1. The new Teams Client is incompatible with Windows Server 2016. Microsoft recommends upgrading to Server 2019 or 2022.
2. The new Teams does not support functioning as a Published (seamless) Application. This issue has been resolved in the CVAD 2402 LTSR release.

**Important Note**
Recognizing the significance of utilizing the new Teams as a published application, Citrix has addressed this concern alongside other enhancements in the CVAD 2402 LTSR release.

**Action Required:** Customers currently on 2203 LTSR seeking published application support and other enhancements introduced in 2402 LTSR are advised to raise a support ticket with Citrix.

**New Teams and VDI 1.0 (WebRTC)**
The new Microsoft Teams now supports Optimized calling and video calling via the Citrix WebRTC optimization product. It remains compatible with the existing WebRTC media engine (VDI 1.0).

Additionally, the new Teams will be compatible with a forthcoming Media Engine (VDI 2.0) being developed and tested by Microsoft. This VDI 2.0 is based on the current Media Engine powering Microsoft Teams (fat client) today.

**Installation**
Microsoft's documentation [here](https://learn.microsoft.com/en-us/microsoftteams/new-teams-vdi-requirements-deploy) outlines the installation process for the new Teams. Notably, the installation methodology differs significantly from the previous version, as the new Teams installer utilizes MSIX technology. All installation, configuration, and product documentation for the new Teams will be provided by Microsoft.

**CVAD 2402 LTSR Enhancements**

- **Published App Support:** With CVAD 2402 LTSR, publishing new Teams as a seamless application is now supported.
- **Registry Configuration Simplification:** Starting with CVAD 2402 LTSR, manual configuration of the msedgewebview2.exe registry entry is unnecessary as it is whitelisted by default.

**CWA Windows 2402 LTSR Enhancements**

- **System Audio Sharing (Technical Preview):** Users can now share the audio playing on their Virtual Delivery Agent (VDA) with meeting participants. This feature requires registry configuration and is available after a future update from Microsoft Teams.
- **Current Limitations:** 
  - Audio sharing is not compatible with certain redirected apps or tabs.
  - Echo cancellation is disabled when the Share System Audio feature is active.
  - This feature is only supported on published desktops.

**VDI 2.0 Plugin Helper Installation**
With the CWA Windows 2402 installer, users have the option to install the VDI 2.0 plugin helper. This plugin helper facilitates the download of the VDI 2.0 plugin upon detecting the new Teams installed on the VDA.

**Version Support Matrix**
For supported versions of Citrix VDA and CWA software, refer to Microsoft's official website.

**CPM Support**
Guidance on enabling roaming for the new Microsoft Teams using Profile Management is provided in this article. The process varies depending on the installer type selected:

- For per-machine installer: Profile Management requirement is 2402 or later.
- For per-user installer: Profile Management requirement is 2308 or later.

**App Layering Support**
New Teams can be layered using Citrix App Layering, simplifying management of the application. Presently, installation in the OS Layer is required, but future versions of App Layering will support installation in the App Layer.
