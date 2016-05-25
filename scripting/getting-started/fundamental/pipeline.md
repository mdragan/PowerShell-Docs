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

In PowerShell, as in most other shells (i.e. [bash](https://www.gnu.org/software/bash/)), the results of the execution of a command can be passed as input to the next command. This allows to create lines of work, like an assembly line, where the output result is improved at each station.

For two commands to benefit from the pipeline, they need to be connected when issued; the connection between commands is made through the vertical bar '&#x007c;' character. Here is an example of two piped commands: `Get-ChildItem | Sort`. Pipelines can be as long as desired; there's no limit on home many commands can be connected. However, when connecting many commands to the pipeline, it is important to understand that the output of one command goes to the next one; there is no way to pick up the results from the command executed two pipes before (those results were available only to the command right after the one that issued the results).

To make sure that everything in the pipeline gets picked up, if there are no piped commands, an implicit Write-Output is added at the end of each line in the script or with each <*ENTER*> key in the console. This explains why is it that everything we do in the console or in the execution of the script appears on the screen. A few things can change this behavior, the most notable are:  
-  The assignment operator '**=**'; the results of evaluating the expression to right hand side of '=' operator gets assigned to the left hand side variable without being sent to the output. So, `$files = Get-ChildItem | Sort` will not show the sorted files; but, `$files` will allow you to see the content of the variable on output.  
-  The redirection operator '**&gt;**'; that takes whatever is in the pipeline and sends it to wherever the redirection is pointing at. So, `Get-ChildItem | Sort > C:\tmp\foo.txt` will sent everything to the *foo.txt* file in *C:\tmp* folder (assuming that 'C:\tmp' already exists).

Also, very important to the pipeline is the fact that results are passed as objects to the receiving command. This means: the receiving command can start working immediately with the results, without having to do any parsing of the input to find the needed piece of data. For example, the following line `Get-ChildItem | Where-Object { $_.Length -gt 0 }` will get all files (in the current executing folder) that have length greater that 0 (zero); here, the `Where-Object` or filter command is processing each result (object) from `Get-ChildItem` using the *Length* property of the object. The **`$_`** variable represents the current object picked up in the pipeline. A good introduction to objects in PowerShell can be found in [Objects, not text](objects-not-text.md).

Finally, to understand what gets send to the output, at the end of the pipeline, or how is it that one command picks up the right thing from the previous one see [Implicit and Explicit Output Formatting](implicit-and-explicit-output-formatting.md)
