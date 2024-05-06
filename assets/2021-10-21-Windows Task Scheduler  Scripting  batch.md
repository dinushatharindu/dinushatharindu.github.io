---
title: Windows Task Scheduler  Scripting  batch
date: 2021-10-21 20:14 +0300
categories: [Blogging, windows, SriLanka]
tags: [blog, security, taskscheduler,IT, industry]
author: Dinusha Tharindu
---
   
![Desktop View](https://i.stack.imgur.com/FTZrw.png)


I have come across a scenario where there is batch script need to be run daily, recurring in every 15 min without any human interaction using the windows task scheduler.

  
  
  
  

a typical script , path has been pointed to correct location.  
  
as per the requirement script has been been added to the task scheduler and all the settings been configured correctly. but in the #1 attempt script run with out any errors and complete it's intended tasks but when it's come to it's #2 attempt in next 15 min script run and finished without any errors , but it's not completing it's expected tasks on the script it self.

  
  
  
  

![](https://cybertuxlk.files.wordpress.com/2020/02/2020-02-11_13-26-21-2.png?w=1024)

  
  
  
  

I tried to go through task sheduler events , but there's no any faliures , warning events or anything to isolate this issue , so tried to manuelly run this script , and noticed.

  
  
  
  

*   running the script manually , it execute it's all tasks successfully , but when it's come to run the script with task scheduler only, script start to fail in it's second attempt and continued.

  
  
  
  

After spending some time on troubleshooting , I noticed the root cause for script to fail and the resolution to fix.

  
  
  
  

The primary problem was, ones the task started it's #1 attempt and finished , it should be mentioned the object residing place to for next scheduler task occurrence to find the path. if it's not mentioned on " Start in(Optional)" the script won't execute , but task scheduler will mark as that task has been performed successfully .

  
  
  
  

so the resolution is :

  
  
  
  

*   Select the action as "Start Program".
*   Brows the path to script ( "path\\file to script with in quotation mark " )
*   mention the folder path ( C:\\Folder\\script\\ )

  
  
  
  

![](https://cybertuxlk.files.wordpress.com/2020/02/2020-02-11_14-08-51.png?w=1024)

  
  
  
  

After configuring above setting , the script and scheduler started working the was it expected.

  
  
  
  

I hope this will save some ones Day or time :) !

