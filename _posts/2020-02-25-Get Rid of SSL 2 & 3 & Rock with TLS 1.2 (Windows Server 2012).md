
---
title: Get Rid of SSL 2 & 3 & Rock with TLS 1.2 (Windows Server 2012)
date: 2020-02-25 20:14 +0300
categories: [Blogging, Srilankan_IT_industry, SriLanka]
tags: [blog, security, ssl,IT, industry]
author: Dinusha Tharindu
---
   
  
  
  

![](https://static.wixstatic.com/media/e54cd3_27ab46c2e7dd4d14a601c35d611f9bdd~mv2.jpg/v1/fill/w_360,h_225,al_c,q_90,usm_0.66_1.00_0.01/e54cd3_27ab46c2e7dd4d14a601c35d611f9bdd~mv2.webp)

  
  
  
  

SSL 2 & 3 protocols no longer will be safe to use since it can be break through the POODLE technique.

  
  
  
  

if you're using any vulnerability scanning tool you may already came across with the massage " SSL Version 2 and 3 Protocol Detection "

  
  
  
  

so in order to be safe use at least TLS 1.2 on your servers.

  
  
  
  

1.  before changing any registry values , take backup using export option in regedit.
2.  Save below registry information as a reg File "XXX.REG " and import it to registry.

  
  
  
  

Windows Registry Editor Version 5.00  
  
\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\SecurityProviders\\SCHANNEL\\Protocols\\TLS 1.2\\Client\]  
"DisabledByDefault"=dword:00000000  
  
\[HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\SecurityProviders\\SCHANNEL\\Protocols\\TLS 1.2\\Server\]  
"DisabledByDefault"=dword:00000000

  
  
  
  

After that you can disable SSL Section by Deleting Registry Keys !.

  
  
  
  

Path :

  
  
  
  

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\SecurityProviders\\SCHANNEL\\Protocols

  
  
  
  

![](https://static.wixstatic.com/media/e54cd3_51b46efd912d46d4b3e588ed006760f6~mv2.jpg/v1/fill/w_360,h_226,al_c,q_90,usm_0.66_1.00_0.01/e54cd3_51b46efd912d46d4b3e588ed006760f6~mv2.webp)

  

  
  
  
  

restart the Server &

  
  
  
  

A tool available to rectified this issue in automated manner.

  
  
  
  

IIS Crypto is a free tool that gives administrators the ability to enable or disable protocols, ciphers, hashes and key exchange algorithms on Windows Server 2008, 2012, 2016 and 2019. It also lets you reorder SSL/TLS cipher suites offered by IIS, change advanced settings, implement Best Practices with a single click, create custom templates and test your website.

  
  
  
  

Get the tool from below Link

  
  
  
  

https://www.nartac.com/Products/IISCrypto/

  
  
  
  

1 - Run the Tool

  
  
  
  

2 - Click on Best Practices(it will choose best scenarios for the server automatically )

  
  
  
  

  
  
  
  

3 - Tick Reboot and Apply

  
  
  
  

![](https://static.wixstatic.com/media/e54cd3_f3fb03504a014198ad37790919305aa1~mv2.png/v1/fill/w_740,h_615,al_c,q_90,usm_0.66_1.00_0.01/e54cd3_f3fb03504a014198ad37790919305aa1~mv2.webp)

  
  
  
  

Enjoy the Vulnerability scanning again !

  
  
  
  

[#SSL3](https://social-blog.wix.com/search/.hash.ssl3) [#SSL2](https://social-blog.wix.com/search/.hash.ssl2) [#TLS1](https://social-blog.wix.com/search/.hash.tls1) [#POODLE](https://social-blog.wix.com/search/.hash.poodle) [#VULNERABLE](https://social-blog.wix.com/search/.hash.vulnerable) [#WINDOWSSERVER](https://social-blog.wix.com/search/.hash.windowsserver) [#SSL](https://social-blog.wix.com/search/.hash.ssl) 

  
  
  
  
