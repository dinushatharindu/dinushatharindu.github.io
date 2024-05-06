
---
title: The Ghost Issue  port exhaustion   How to Troubleshoot
date: 2020-01-12 20:14 +0300
categories: [Blogging, Srilankan_IT_industry, SriLanka]
tags: [blog, security, ssl,IT, industry]
author: Dinusha Tharindu
---
  

Have you ever faced windows server issue with blow symptoms , still there's no where to correlate each of them ?

  
  
  
  

*   Server is unable to reach but the server is online. no issue found on the network level , or firewall side.
*   Unable to Remote but everything is fine for Remote desktop.
*   All the outgoing connections are blocked inside , and incoming connection are blocked it self .
*   none of the applications hosted on the server working.
*   Issue occurred time to time but there is no any pattern to diagnose
*   unable to find any evidence from event logs.
*   Group policy update get failed
*   network shares are unable to access.

  
  
  
  

after spending so many hours on reading different vendor article , i came cross scenario called " Port Exhaustion ". this can be happened due to the all they dynamic range ports are busy or waiting for connection to established.

  
  
  
  

If you dive deep in to the events logs you 'll notice events 4227/4231 has been triggered closed to the issue started time.

  
  
  
  

![](https://cybertuxlk.files.wordpress.com/2020/02/2020-02-07_11-53-28-1.png?w=737)

  
  
  
  

and lots of events ( ID 10028) can be triggered as results of the internal application connections are getting failed due to the port exhaustion.

  
  
  
  

![](https://cybertuxlk.files.wordpress.com/2020/02/2020-02-07_11-57-17.png?w=731)

  
  
  
  

So now we know we have port exhaustion , but how to troubleshoot ? or what's the solution ?.  
Well there no exact solution or fox for this issue , but we know one thing for sure ,

  
  
  
  

"We don't have enough ports to make connection" :)  
What can we do about it ?. as per Microsoft we can temporarily increase the number of ports while comply with [Internet Assigned Numbers Authority (IANA)](http://www.iana.org/assignments/port-numbers).

  
  
  
  

to view the existing port range you can use below commands set.

  
  
  
  

*   `netsh int ipv4 show dynamicport tcp`
*   `netsh int ipv4 show dynamicport udp`
*   `netsh int ipv6 show dynamicport tcp`
*   `netsh int ipv6 show dynamicport udp`

  
  
  
  

use below command to increase the port range

  
  
  
  

    netsh int <ipv4|ipv6> set dynamic <tcp|udp> start=number num=rangeExamples :netsh int ipv4 set dynamicport tcp start=10000 num=1000netsh int ipv4 set dynamicport udp start=10000 num=1000netsh int ipv6 set dynamicport tcp start=10000 num=1000netsh int ipv6 set dynamicport udp start=10000 num=1000

  
  
  
  

For more Details , you can refer Microsoft recommendation below.  
[https://docs.microsoft.com/en-us/windows/client-management/troubleshoot-tcpip-port-exhaust](https://docs.microsoft.com/en-us/windows/client-management/troubleshoot-tcpip-port-exhaust)

  
  
  
  

So we have increased the port range but it's temporary, because we have to dig down to the root cause and identify what's causing the this port exhausting issue. so which tool can we used for that ?.

  
  
  
  

Yes , as always Windows Sysinternals tools Save our lives Everyday. :-) Nice work by [Mark](https://blogs.technet.microsoft.com/markrussinovich/) [Russinovich](https://blogs.technet.microsoft.com/markrussinovich/)

  
  
  
  

Here you can use Sysinternals process explorer to identify which application causing the problem , here's how you do it.  
Download and install Sysinternals process explorer and open with elevated privileged, Here is the Link.  
  
[https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)

  
  
  
  

initially you'll find something like this , but you have make it's interface view that way it can help to get better view of what's happening on the system. Here how you do it.

  
  
  
  

*   Right-click > column header, then select “Choose Columns.”
*   go to Performance Tab, then add Handle Count then View > Show Lower Pane.
*   Click select View > Lower Pane View > Handles. and then Sort the handles in order.

  
  
  
  

![](https://cybertuxlk.files.wordpress.com/2020/02/2020-02-07_17-55-55.png?w=764)

  
  
  
  

If you have make it correct you'll come up something like below , where blue arrow shows which application make highest number of handlers and red arrow shows type of handles and ports or sockets.

  
  
  
  

in moment where port exhausting happening this can go up to 30,000 or more.

  
  
  
  

![](https://cybertuxlk.files.wordpress.com/2020/02/2020-02-07_18-07-28-1.png?w=895)

  
  
  
  

Even you can you deep dive up to what applications made connection to which remote IP/port. by right click on the process and click properties. there are so much of information for you to deal with.

  
  
  
  

![](https://cybertuxlk.files.wordpress.com/2020/02/2020-02-07_18-16-51-1.png?w=927)

  
  
  
  

  
  
  
  

So the conclusion Is :

  
  
  
  

Use process explorer to identify the process or application see what's causing the port exhaustion, based on your scenario work with application vendor to fix the app. or you can disable the process temporarily with causing the problem.  
  
Happy Troubleshooting :)

  
  
  
