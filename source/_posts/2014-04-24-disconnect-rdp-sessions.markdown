---
layout: post
title: "Disconnect RDP Sessions"
author: Matthew Pickle
date: 2014-04-24 11:34:32 -0400
comments: true
categories: [QA, Framework Utilities, Windows, RDP]
published: true
---

# Intro
If you are using RDP (Remote Desktop Protocol) to connect to your Windows test machines for UI test automation, it is crucial that you disconnect the active RDP session and pass control to the console.  This allows the automation tool to properly interact with the desktop or web application.

# Code
``` bat Disconnect RDP Session - Current User
for /f "skip=1 tokens=3 usebackq" %%sId in (
  :: Query for Current User Name
  'query user %username%'
) do (
  :: Disconnect RDP Session & Pass Control to Console
  '%windir%\System32\tscon.exe' %%sId /dest:console
)
```

# How To
> * Copy and Paste the code into a batch file (i.e. Disconnect_RDP.bat)
> * Integrate into any automation framework by calling the batch file during test setup
> * Run manually to leave the test machine in a state ready for automated testing.

# References
> <a href="http://technet.microsoft.com/en-us/library/bb490801.aspx" target="_blank">query user</a>

> <a href="http://technet.microsoft.com/en-us/library/cc770988.aspx" target="_blank">tscon</a>

*Automate Everything!*