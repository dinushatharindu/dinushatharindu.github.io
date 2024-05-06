---
title: SMB Signing not required
date: 2020-02-02 20:14 +0300
categories: [Blogging, Srilankan_IT_industry, SriLanka]
tags: [blog, smb, ssl,IT, security]
author: Dinusha Tharindu
---
  

you may have came across above statement specially when vulnerability scanning. nessus scanner identified above issue by the plugin ID 57608 as below

  
  
  
  

**Severity:** Medium.

  
  
  
  

**ID:** 57608

  
  
  
  

**File Name:** smb\_signing\_disabled.nasl

  
  
  
  

**Version:** 1.18

  
  
  
  

**Type:** remote

  
  
  
  

**Family:** [Misc.](https://www.tenable.com/plugins/nessus/families/Misc)

  
  
  
  

this issue occurred when SMB traffic or server is not signed so an unauthenticated remote attacker can exploit or launch a MIM or Man -in- Middle attack against the SMB server.

  
  
  
  

the vulnerability can be fixed by enforcing SMB signing from a Group policy for Clinet and server.

  
  
  
  

GPO Location : Computer Configuration\\Windows Settings\\Security Settings\\Local Policies\\Security Options

  
  
  
  

![](https://static.wixstatic.com/media/e54cd3_09013e640c9b46549acb4398cdd817db~mv2.jpg/v1/fill/w_740,h_262,al_c,q_90,usm_0.66_1.00_0.01/e54cd3_09013e640c9b46549acb4398cdd817db~mv2.webp)

  
  
  
  

Fore more Details read below.

  
  
  
  

[https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/smbv1-microsoft-network-server-digitally-sign-communications-always](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/smbv1-microsoft-network-server-digitally-sign-communications-always)

  
  
  
  

[https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/microsoft-network-server-digitally-sign-communications-always](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/microsoft-network-server-digitally-sign-communications-always)

  
  
  
  

Happy Fixing :)

 
