---
title: WSUS Nightmare
date: 2020-04-18 20:14 +0300
categories: [Blogging, Srilankan_IT_industry, SriLanka]
tags: [blog, security, ssl,IT, industry]
author: Dinusha Tharindu
---
  

  

If you ever come across with wsus server console showing that client are not reported to the server over x number of days , you'll see something like below

  
  
  
  

![](https://cybertuxlk.files.wordpress.com/2020/02/2020-02-03_13-35-17.png?w=850)

  
  
  
  

but when you really look at the client logs it shows that everything is working fine , client are reporting to WSUS server as normal , updates are downloaded from the server , even showing on the correct client targeting groups. here some logs extracted from clients.

  
  
  
  

    2020/01/23 15:17:51.1568821 9852  628   DownloadManager *FAILED* [80004001] Method failed [CAgentDownloadManager::CanRetryWithDifferentCDNForError:23980]2020/01/23 15:17:51.1568965 9852  628   DownloadManager BITS job {0A0F1B98-4B97-4FB3-A7CD-7EB5AD8B9D3E} failed, updateId = 4FED3B54-C444-49B9-950F-301402B8B6B2.200, hr = 0x80190194. File URL = http://namnzsccm.nikkoam.com:8530/Content/43/2699F66F2A4ACCB6A04A2418C94153BCBA21FA43.cab, local path = C:\windows\SoftwareDistribution\Download\60d29cc85b6a3173213aec4fbb2cb5cb\stslist-x-none.cab, The response headers = HTTP/1.1 404 Not Found  Date: Thu, 23 Jan 2020 02:17:50 GMT  Content-Length: 1245  Content-Type: text/html  Server: Microsoft-IIS/8.5  X-Powered-By: ASP.NET    2020/01/23 15:17:51.1570292 9852  628   DownloadManager   Progress failure bytes total = 0, bytes transferred = 02020/01/23 15:17:51.1570490 9852  7344  ProtocolTalker  OK to reuse existing configuration2020/01/23 15:17:51.1570523 9852  7344  ProtocolTalker  Existing cookie is valid, just use it2020/01/23 15:17:51.1570536 9852  7344  ProtocolTalker  PTInfo: Server requested registration2020/01/23 15:17:51.1590469 9852  628   DownloadManager Total download size for update 4FED3B54-C444-49B9-950F-301402B8B6B2.200 (session data: (null)) set via progress to 02020/01/23 15:17:51.1594692 9852  628   DownloadManager *FAILED* [80244019] Error occurred while downloading update 4FED3B54-C444-49B9-950F-301402B8B6B2.200; notifying dependent calls.2020/01/23 15:17:51.1665050 9852  7344  ProtocolTalker  *FAILED* [8024000B] Method failed [CAgentProtocolTalker::GetCurrentComputerInfo:4599]2020/01/23 15:17:51.1665089 9852  7344  ProtocolTalker  *FAILED* [8024000B] GetCurrentComputerInfo failed, not fatal2020/01/23 15:17:51.1665101 9852  7344  ProtocolTalker  *FAILED* [8024000B] RefreshPTState failed2020/01/23 15:17:51.1718495 9852  7344  DownloadManager * END * Download Call Complete. Call 71 for caller UpdateOrchestrator has completed; signaling completion.

  
  
  
  

after reading lot of KB articles I realized this could be due to SID duplication in Client deployment / imaging process. (If you need to detect duplication follow below blog post).  
[https://ms07.de/blog/?p=277](https://ms07.de/blog/?p=277)

  
  
  
  

Further reading of this subject , below steps need to be follow to fix the WSUS clients report back to the server.

  
  
  
  

*   Stops the wuauserv service
*   Deletes the AccountDomainSid registry key (if it exists)
*   Deletes the PingID registry key (if it exists)
*   Deletes the SusClientId registry key (if it exists)
*   Restarts the wuauserv service
*   Resets the Authorization Cookie

  
  
  
  

After checking few more hours on internet i come across a verified awesome script by "Manuel Gil" that can be achieved the same results.  
[https://gallery.technet.microsoft.com/scriptcenter/Reset-WSUS-Client-ID-90661da1](https://gallery.technet.microsoft.com/scriptcenter/Reset-WSUS-Client-ID-90661da1)  

  
  
  
  

    :: ================================================================================== :: NAME:    Reset WSUS Client ID. :: AUTHOR:    Manuel Gil. :: ==================================================================================  echo off title Reset WSUS Client ID. color 17  cls ver echo.Reset WSUS Client ID. echo.  echo.    The methods inside this tool modify files and registry settings. echo.    While you are tested and tend to work, We not take responsibility for echo.    the use of this tool. echo. echo.    This tool is provided without warranty. Any damage caused is your echo.    own responsibility. echo. echo.    As well, batch files are almost always flagged by anti-virus, feel free echo.    to review the code if you're unsure. echo.  choice /c YN /n /m "Do you want to continue with this process? (Y/N) " if %errorlevel% EQU 2 goto :eof  echo.Canceling the Windows Update process. echo.  taskkill /im wuauclt.exe /f  echo.Stopping the Windows Update services. echo.  net stop bits net stop wuauserv net stop appidsvc net stop cryptsvc  echo.Checking the services status. echo.  sc query bits | findstr /I /C:"STOPPED" if %errorlevel% NEQ 0 echo Failed to stop the bits service. & pause & goto :eof  sc query wuauserv | findstr /I /C:"STOPPED" if %errorlevel% NEQ 0 echo Failed to stop the wuauserv service. & pause & goto :eof  sc query appidsvc | findstr /I /C:"STOPPED" if %errorlevel% NEQ 0 sc query appidsvc | findstr /I /C:"OpenService FAILED 1060" if %errorlevel% NEQ 0 echo Failed to stop the appidsvc service. & pause & goto :eof  sc query cryptsvc | findstr /I /C:"STOPPED" if %errorlevel% NEQ 0 echo Failed to stop the cryptsvc service. & pause & goto :eof  echo.Deleting the qmgr*.dat files. echo.  del /s /q /f "%ALLUSERSPROFILE%\Application Data\Microsoft\Network\Downloader\qmgr*.dat" del /s /q /f "%ALLUSERSPROFILE%\Microsoft\Network\Downloader\qmgr*.dat"  echo.Renaming the softare distribution folders backup copies. echo.  rmdir /s /q "%SYSTEMROOT%\SoftwareDistribution.bak" ren "%SYSTEMROOT%\SoftwareDistribution" SoftwareDistribution.bak if exist "%SYSTEMROOT%\SoftwareDistribution" echo Failed to rename the SoftwareDistribution folder.  & pause & goto :eof  rmdir /s /q "%SYSTEMROOT%\system32\Catroot2.bak" ren "%SYSTEMROOT%\system32\Catroot2" Catroot2.bak  del /s /q /f "%SYSTEMROOT%\winsxs\pending.xml.bak" ren "%SYSTEMROOT%\winsxs\pending.xml" pending.xml.bak  del /s /q /f "%SYSTEMROOT%\WindowsUpdate.log.bak" ren "%SYSTEMROOT%\WindowsUpdate.log" WindowsUpdate.log.bak  echo.Reset the BITS service and the Windows Update service to the default security descriptor. echo.  sc.exe sdset wuauserv D:(A;;CCLCSWLOCRRC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCDCLCSWRPWPDTLCRSDRCWDWO;;;SO)(A;;CCLCSWRPWPDTLOCRRC;;;SY)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;WD) sc.exe sdset bits D:(A;;CCLCSWLOCRRC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCDCLCSWRPWPDTLCRSDRCWDWO;;;SO)(A;;CCLCSWRPWPDTLOCRRC;;;SY)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;WD) sc.exe sdset cryptsvc D:(A;;CCLCSWLOCRRC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCDCLCSWRPWPDTLCRSDRCWDWO;;;SO)(A;;CCLCSWRPWPDTLOCRRC;;;SY)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;WD) sc.exe sdset trustedinstaller D:(A;;CCLCSWLOCRRC;;;AU)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCDCLCSWRPWPDTLCRSDRCWDWO;;;SO)(A;;CCLCSWRPWPDTLOCRRC;;;SY)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;WD)  echo.Reregister the BITS files and the Windows Update files. echo.  regsvr32.exe /s atl.dll regsvr32.exe /s urlmon.dll regsvr32.exe /s mshtml.dll regsvr32.exe /s shdocvw.dll regsvr32.exe /s browseui.dll regsvr32.exe /s jscript.dll regsvr32.exe /s vbscript.dll regsvr32.exe /s scrrun.dll regsvr32.exe /s msxml.dll regsvr32.exe /s msxml3.dll regsvr32.exe /s msxml6.dll regsvr32.exe /s actxprxy.dll regsvr32.exe /s softpub.dll regsvr32.exe /s wintrust.dll regsvr32.exe /s dssenh.dll regsvr32.exe /s rsaenh.dll regsvr32.exe /s gpkcsp.dll regsvr32.exe /s sccbase.dll regsvr32.exe /s slbcsp.dll regsvr32.exe /s cryptdlg.dll regsvr32.exe /s oleaut32.dll regsvr32.exe /s ole32.dll regsvr32.exe /s shell32.dll regsvr32.exe /s initpki.dll regsvr32.exe /s wuapi.dll regsvr32.exe /s wuaueng.dll regsvr32.exe /s wuaueng1.dll regsvr32.exe /s wucltui.dll regsvr32.exe /s wups.dll regsvr32.exe /s wups2.dll regsvr32.exe /s wuweb.dll regsvr32.exe /s qmgr.dll regsvr32.exe /s qmgrprxy.dll regsvr32.exe /s wucltux.dll regsvr32.exe /s muweb.dll regsvr32.exe /s wuwebv.dll   echo.Deleting values in the Registry. echo. reg Delete HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate /v PingID /f reg Delete HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate /v AccountDomainSid /f reg Delete HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate /v SusClientId /f reg Delete HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate /v SusClientIDValidation /f  echo.Resetting Winsock and WinHTTP Proxy. echo.  netsh winsock reset netsh winhttp reset proxy  echo.Resetting the services as automatics. echo.  sc.exe config wuauserv start= auto sc.exe config bits start= delayed-auto sc.exe config cryptsvc start= auto sc.exe config TrustedInstaller start= demand sc.exe config DcomLaunch start= auto  echo.Starting the Windows Update services. echo.  net start bits net start wuauserv net start appidsvc net start cryptsvc net start DcomLaunch  echo.Forcing updates. echo. wuauclt.exe /resetauthorization /detectnow  echo.The operation completed successfully. echo.Please reboot your computer. pause goto :eof 

  
  
  
  

Executing the script, all client computers report back to the wsus server.

  
  
  
  

This Phenomenal has happened in the windows client OS deployment process , and not following the best practices for windows 10 deployment.  

  
  
  
  

in shorter terms SYSPREP tool need be executed and generalize the image ,  
  
To deploy a Windows image to different PCs, you have to first generalize the image to remove computer-specific information such as installed drivers and the computer security identifier (SID). You can either use [Sysprep](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview) by itself or Sysprep with an [unattend](https://docs.microsoft.com/windows-hardware/customize/desktop/unattend/) answer file to generalize your image and make it ready for deployment.  
  
[https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation)

  
  
  
