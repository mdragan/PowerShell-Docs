---
title:  Pipeline
ms.date:  2016-05-23
keywords:  powershell,cmdlet
description:  
ms.topic:  article
author:  jpjofre
manager:  dongill
ms.prod:  powershell
---

# Pipeline

In PowerShell, as in most other shells (i.e. [bash](https://www.gnu.org/software/bash/)), the results of the execution of a command can be passed as input to the next command. This allows to create lines of work, like 

For two commands to benefit from the pipeline, they need to be connected when issued; the connection between commands is made through the vertical bar '&#x007c;' character. An example of two piped commands: `Get-ChildItem | Sort`
