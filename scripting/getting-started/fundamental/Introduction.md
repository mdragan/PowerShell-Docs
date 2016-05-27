---
title:  Introduction
ms.date:  2016-05-23
keywords:  powershell,cmdlet
description:  
ms.topic:  article
author:  jpjofre
manager:  dongill
ms.prod:  powershell
---

# Introduction

PowerShell is a task-based command-line shell and scripting language designed especially for system administration. Built on the .NET Framework, PowerShell helps IT professionals and power users control and automate the administration of servers and computers that run on Windows. The fundamental goal of PowerShell is providing better, easier administrative control over systems, either interactively or from script.

The power in PowerShell comes from being an object oriented language; which synthesizes the code and how the results from one command execution are passed to the next one. The other pillars of PowerShell strength come from the *[pipeline](../../Windows-PowerShell-Glossary.md#pipeline)* and the fully developed scripting language. The pipeline is what connects the output from one command -*[cmdlet](../../Windows-PowerShell-Glossary.md#cmdlet)*- to the input of the following command.

Because PowerShell is object oriented, all interactions between cmdlets are clean and terse. The command, that picks up on the results of a previous command, doesn't have to guess on the contents of the data; being all objects part of .Net Framework, it's easy to know how to use the object. This is a huge differentiator with other shells, like Bash, that are string oriented; in Bash, the command picking up on the results of a previous command has to do all the heavy lifting on parsing the content, to find the piece of information that needs.

By design, all PowerShell cmdlet names follow the *verb-noun* pattern; this helps IT professionals and everyone else to easily understand the purpose of each cmdlet. This also makes all cmdlets task oriented, as the name implies the action executed. For example, if you want to send some results over the internet to a website that is expecting to receive the data, chances are the web site is expecting to receive the data in [JSON](http://www.json.org/)   `ConvertTo-Json` converts an object to a JSON-formatted string and its counterpart `ConvertFrom-Json` converts a JSON-formatted string to a custom object.

Basic system administration, usually, involves working with the file system, with system processes and services, handling printers and network resources, dealing with remote machines, scheduling and managing jobs, and much more; the [Basic Cookbooks](../basic-cookbooks.md) section takes you through the fundamentals of managing your system with PowerShell, without delay and through sample scripts that are specific to solve the task at hand; it is the hands-on approach to learn PowerShell.

If you are looking to better understand PowerShell, you can start with the fundamentals
-  [Pipeline](pipeline.md),
-  [Objects, not text](objects-not-text.md)
-  [Command parsing](command-parsing.md)
-  [Scripting Language Elements](scripting-language-elements.md)
-  [Native Application Execution and Parameter Passing](native-application-execution-and-parameter-passing.md)
-  [Implicit and Explicit Output Formatting](implicit-and-explicit-output-formatting.md)
-  [Integration with Operating System and Services](integration-with-operating-system-and-services.md)
