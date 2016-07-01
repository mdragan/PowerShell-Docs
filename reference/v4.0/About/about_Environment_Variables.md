---
description:  
manager:  dongill
ms.topic:  article
author:  jpjofre
ms.prod:  powershell
keywords:  powershell,cmdlet
ms.date:  2016-07-01
title:  about_Environment_Variables
ms.technology:  powershell
ms.assetid:  998c8863-3794-42a8-8971-a5cadef72772
---

# about_Environment_Variables
## TOPIC  
 about\_Environment\_Variables  
  
## SHORT DESCRIPTION  
 Describes how to access Windows environment variables in [!INCLUDE[wps_1]()].  
  
## LONG DESCRIPTION  
 Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders.  
  
 The environment variables store data that is used by the operating system and other programs. For example, the WINDIR environment variable contains the location of the Windows installation directory. Programs can query the value of this variable to determine where Windows operating system files are located.  
  
 [!INCLUDE[wps_2]()] lets you view and change Windows environment variables, including the variables set in the registry, and those set for a particular session. The [!INCLUDE[wps_2]()] environment provider simplifies this process by making it easy to view and change the environment variables.  
  
 Unlike other types of variables in [!INCLUDE[wps_2]()], environment variables and their values are inherited by child sessions, such as local background jobs and the sessions in which module members run. This makes environment variables well suited to storing values that are needed in both parent and child sessions.  
  
### WINDOWS POWERSHELL ENVIRONMENT PROVIDER  
 The [!INCLUDE[wps_2]()] environment provider lets you access Windows environment variables in [!INCLUDE[wps_2]()] in a [!INCLUDE[wps_2]()] drive \(the Env: drive\). This drive looks much like a file system drive. To go to the Env: drive, type:  
  
```  
Set-Location Env:  
  
```  
  
 Then, to display the contents of the Env: drive, type:  
  
```  
Get-ChildItem  
  
```  
  
 You can view the environment variables in the Env: drive from any other [!INCLUDE[wps_2]()] drive, and you can go into the Env: drive to view and change the environment variables.  
  
### ENVIRONMENT VARIABLE OBJECTS  
 In [!INCLUDE[wps_2]()], each environment variable is represented by an object that is an instance of the System.Collections.DictionaryEntry class.  
  
 In each DictionaryEntry object, the name of the environment variable is the dictionary key. The value of the variable is the dictionary value.  
  
 To display an environment variable in [!INCLUDE[wps_2]()], get an object that represents the variable, and then display the values of the object properties. When you change an environment variable in [!INCLUDE[wps_2]()], use the methods that are associated with the DictionaryEntry object.  
  
 To display the properties and methods of the object that represents an environment variable in [!INCLUDE[wps_2]()], use the Get\-Member cmdlet. For example, to display the methods and properties of all the objects in the Env: drive, type:  
  
```  
Get-Item -Path Env:* | Get-Member  
  
```  
  
### DISPLAYING ENVIRONMENT VARIABLES  
 You can use the cmdlets that contain the Item noun \(the Item cmdlets\) to display and change the values of environment variables. Because environment variables do not have child items, the output of Get\-Item and Get\-ChildItem is the same.  
  
 When you refer to an environment variable, type the Env: drive name followed by the name of the variable. For example, to display the value of the COMPUTERNAME environment variable, type:  
  
```  
Get-Childitem Env:Computername  
  
```  
  
 To display the values of all the environment variables, type:  
  
```  
Get-ChildItem Env:  
  
```  
  
 By default, [!INCLUDE[wps_2]()] displays the environment variables in the order in which it retrieves them. To sort the list of environment variables by variable name, pipe the output of a Get\-ChildItem command to the Sort\-Object cmdlet. For example, from any [!INCLUDE[wps_2]()] drive, type:  
  
```  
Get-ChildItem Env: | Sort Name  
```  
  
 You can also go into the Env: drive by using the Set\-Location cmdlet:  
  
```  
Set-Location Env:  
```  
  
 When you are in the Env: drive, you can omit the Env: drive name from the path. For example, to display all the environment variables, type:  
  
```  
Get-ChildItem  
```  
  
 To display the value of the COMPUTERNAME variable from within the Env: drive, type:  
  
```  
Get-ChildItem ComputerName  
```  
  
 You can also display and change the values of environment variables without using a cmdlet by using the expression parser in [!INCLUDE[wps_2]()]. To display the value of an environment variable, use the following syntax:  
  
```  
$Env:<variable-name>  
```  
  
 For example, to display the value of the WINDIR environment variable, type the following command at the [!INCLUDE[wps_2]()] command prompt:  
  
```  
$Env:windir  
```  
  
 In this syntax, the dollar sign \($\) indicates a variable, and the drive name indicates an environment variable.  
  
### CHANGING ENVIRONMENT VARIABLES  
 To make a persistent change to an environment variable, use System in Control Panel \(Advanced tab or the Advanced System Settings item\) to store the change in the registry.  
  
 When you change environment variables in [!INCLUDE[wps_2]()], the change affects only the current session. This behavior resembles the behavior of the Set command in Windows\-based environments and the Setenv command in UNIX\-based environments.  
  
 You must also have permission to change the values of the variables. If you try to change a value without sufficient permission, the command fails, and [!INCLUDE[wps_2]()] displays an error.  
  
 You can change the values of variables without using a cmdlet by using the following syntax:  
  
```  
$Env:<variable-name> = "<new-value>"  
  
```  
  
 For example, to append ";c:\\temp" to the value of the Path environment variable, use the following syntax:  
  
```  
$Env:path = $env:path + ";c:\temp"  
  
```  
  
 You can also use the Item cmdlets, such as Set\-Item, Remove\-Item, and Copy\-Item to change the values of environment variables. For example, to use the Set\-Item cmdlet to append ";c:\\temp" to the value of the Path environment variable, use the following syntax:  
  
```  
Set-Item -Path Env:Path -Value ($Env:Path + ";C:\Temp")  
  
```  
  
 In this command, the value is enclosed in parentheses so that it is  interpreted as a unit.  
  
### SAVING CHANGES TO ENVIRONMENT VARIABLES  
 To create or change the value of an environment variable in every [!INCLUDE[wps_2]()] session, add the change to your [!INCLUDE[wps_2]()] profile.  
  
 For example, to add the C:\\Temp directory to the Path environment variable in every [!INCLUDE[wps_2]()] session, add the following command to your [!INCLUDE[wps_2]()] profile.  
  
```  
$Env:Path = $Env:Path + ";C:\Temp"  
  
```  
  
 To add the command to an existing profile, such as the CurrentUser,AllHosts profile, type:  
  
```  
Add-Content -Path $Profile.CurrentUserAllHosts -Value '$Env:Path = $Env:Path + ";C:\Temp"'  
  
```  
  
### ENVIRONMENT VARIABLES THAT STORE PREFERENCES  
 [!INCLUDE[wps_2]()] features can use environment variables to store user preferences. These variables work like preference variables, but they are inherited by child sessions of the sessions in which they are created. For more information about preference variables, see about\_preference\_variables.  
  
 The environment variables that store preferences include:  
  
#### PSEXECUTIONPOLICYPREFERENCE  
 Stores the execution policy set for the current session. This environment variable exists only when you set an execution policy for a single session. You can do this in two different ways.  
  
 \-\- Use PowerShell.exe to start a session at the command line and use its ExecutionPolicy parameter to set the execution policy for the session.  
  
 \-\- Use the Set\-ExecutionPolicy cmdlet. Use the Scope parameter with a value of "Process".  
  
 For more information, see about\_Execution\_Policies.  
  
#### PSMODULEPATH  
 Stores the paths to the default module directories. [!INCLUDE[wps_2]()] looks for modules in the specified directories when you do not specify a full path to a module.  
  
 The default value of $Env:PSModulePath is:  
  
```  
$home\Documents\WindowsPowerShell\Modules; $pshome\Modules  
  
```  
  
 [!INCLUDE[wps_2]()] sets the value of "$pshome\\Modules" in the registry. It sets the value of "$home\\Documents\\WindowsPowerShell\\Modules" each time you start [!INCLUDE[wps_2]()].  
  
 In addition, setup programs that install modules in other directories, such as the Program Files directory, can append their locations to the value of PSModulePath.  
  
 To change the default module directories for the current session, use the following command format to change the value of the PSModulePath environment variable.  
  
 For example, to add the "C:\\Program Files\\Fabrikam\\Modules" directory to the value of the PSModulePath environment variable, type:  
  
```  
$Env:PSModulePath = $Env:PSModulePath + ";C:\Program Files\Fabrikam\Modules"  
  
```  
  
 The semi\-colon \(;\) in the command separates the new path from the path that precedes it in the list.  
  
 To change the value of PSModulePath in every session, add the previous command to your [!INCLUDE[wps_2]()] profile or use the  SetEnvironmentVariable method of the Environment class.  
  
 The following command uses the GetEnvironmentVariable method to get the machine setting of PSModulePath and the SetEnvironmentVariable method to add the C:\\Program Files\\Fabrikam\\Modules path to the value.  
  
```  
$path = [System.Environment]::GetEnvironmentVariable("PSModulePath", "Machine")  
            [System.Environment]::SetEnvironmentVariable("PSModulePath", $path + `  
               ";C:\Program Files\Fabrikam\Modules", "Machine")  
```  
  
 To add a path to the user setting, change the target value to User.  
  
```  
$path = [System.Environment]::GetEnvironmentVariable("PSModulePath", "User")  
[System.Environment]::SetEnvironmentVariable("PSModulePath", $path + `  
   ";$home\Documents\Fabrikam\Modules", "User")  
  
```  
  
 For more information about the methods of the System.Environment class, see "Environment Methods" in MSDN at http:\/\/go.microsoft.com\/fwlink\/?LinkId\=242783.  
  
 You can add also add a command that changes the value to your profile or use System in Control Panel to change the value of the PSModulePath environment variable in the registry.  
  
 For more information, see about\_Modules.  
  
### SEE ALSO  
 Environment \(provider\)  
  
 about\_Modules

