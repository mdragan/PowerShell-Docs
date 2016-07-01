---
description:  
manager:  dongill
ms.topic:  article
author:  jpjofre
ms.prod:  powershell
keywords:  powershell,cmdlet
ms.date:  2016-07-01
title:  about_Data_Sections
ms.technology:  powershell
ms.assetid:  d2d76c2d-ad7c-41fb-b745-7bdda8df131e
---

# about_Data_Sections
Insert introduction here.  
  
## TOPIC  
 about\_Data\_Sections  
  
## SHORT DESCRIPTION  
 Explains Data sections, which isolate text strings and other read\-only data from script logic.  
  
## LONG DESCRIPTION  
 Scripts that are designed for [!INCLUDE[wps_1]()] can have one or more Data sections that contain only data. You can include one or more Data sections in any script, function, or advanced function. The content of the Data section is restricted to a specified subset of the [!INCLUDE[wps_2]()] scripting language.  
  
 Separating data from code logic makes it easier to identify and manage both logic and data. It lets you have separate string resource files for text, such as error messages and Help strings. It also isolates the code logic, which facilitates security and validation tests.  
  
 In [!INCLUDE[wps_2]()], the Data section is used to support script internationalization. You can use Data sections to make it easier to isolate, locate, and process strings that will be translated into many user interface \(UI\) languages.  
  
 The Data section is a [!INCLUDE[wps_2]()] 2.0 feature. Scripts with Data sections will not run in [!INCLUDE[wps_2]()] 1.0 without revision.  
  
### SYNTAX  
 The syntax for a Data section is as follows:  
  
```  
DATA [-supportedCommand <cmdlet-name>] {  
  
            <Permitted content>  
        }  
```  
  
 The Data keyword is required. It is not case\-sensitive.  
  
 The permitted content is limited to the following elements:  
  
```  
- All Windows PowerShell operators, except -match   
  
        - If, Else, and ElseIf statements  
  
- The following automatic variables: $PsCulture,  $PsUICulture,  $True,  
          $False, and $Null  
  
        - Comments  
  
        - Pipelines  
  
        - Statements separated by semicolons (;)  
  
        - Literals, such as the following:  
  
            a  
  
            1  
  
            1,2,3  
  
            "Windows PowerShell 2.0"  
  
            @( "red", "green", "blue" )  
  
            @{ a = 0x1; b = "great"; c ="script" }  
  
            [XML] @'  
             <p> Hello, World </p>  
            '@  
  
        - Cmdlets that are permitted in a Data section. By default, only the   
          ConvertFrom-StringData cmdlet is permitted.  
  
        - Cmdlets that you permit in a Data section by using the   
          SupportedCommand parameter.  
  
```  
  
 When you use the ConvertFrom\-StringData cmdlet in a Data section, you can enclose the key\/value pairs in single\-quoted or double\-quoted strings or in single\-quoted or double\-quoted here\-strings. However, strings that contain variables and subexpressions must be enclosed in single\-quoted strings or in single\-quoted here\-strings so that the variables are not expanded and the subexpressions are not executable.  
  
### SUPPORTEDCOMMAND  
 The SupportedCommand parameter allows you to indicate that a cmdlet or function generates only data. It is designed to allow users to include cmdlets and functions in a data section that they have written or tested.  
  
 The value of SupportedCommand is a comma\-separated list of one or more cmdlet or function names.  
  
 For example, the following data section includes a user\-written cmdlet, Format\-XML, that formats data in an XML file:  
  
```  
DATA -supportedCommand Format-XML   
        {      
           Format-XML -strings string1, string2, string3  
        }  
  
```  
  
### USING A DATA SECTION  
 To use the content of a Data section, assign it to a variable and use variable notation to access the content.  
  
 For example, the following data section contains a ConvertFrom\-StringData command that converts the here\-string into a hash table. The hash table is assigned to the $TextMsgs variable.  
  
 The $TextMsgs variable is not part of the data section.  
  
```  
$TextMsgs = DATA {  
              ConvertFrom-StringData -stringdata @'  
                Text001 = Windows 7  
                Text002 = Windows Server 2008 R2  
          '@  
          }  
  
```  
  
 To access the keys and values in hash table in $TextMsgs, use the following commands.  
  
```  
$TextMsgs.Text001        
          $TextMsgs.Text002  
  
```  
  
## EXAMPLES  
 Simple data strings.  
  
```  
DATA {  
    "Thank you for using my Windows PowerShell Organize.pst script."  
    "It is provided free of charge to the community."  
    "I appreciate your comments and feedback."  
}  
  
```  
  
 Strings that include permitted variables.  
  
```  
 DATA {  
     if ($null) {  
"To get help for this cmdlet, type get-help new-dictionary."  
     }  
 }  
  
```  
  
 A single\-quoted here\-string that uses the ConvertFrom\-StringData cmdlet:  
  
```  
DATA {  
  ConvertFrom-StringData -stringdata @'  
    Text001 = Windows 7  
    Text002 = Windows Server 2008 R2  
'@  
}  
  
```  
  
 A double\-quoted here\-string that uses the ConvertFrom\-StringData cmdlet:  
  
```  
DATA  {  
  ConvertFrom-StringData -stringdata @"  
    Msg1 = To start, press any key.  
    Msg2 = To exit, type "quit".  
"@  
}  
  
```  
  
 A data section that includes a user\-written cmdlet that generates data:  
  
```  
DATA -supportedCommand Format-XML {      
           Format-XML -strings string1, string2, string3  
        }  
  
```  
  
## SEE ALSO  
 about\_Automatic\_Variables  
  
 about\_Comparison\_Operators  
  
 about\_Hash\_Tables  
  
 about\_If  
  
 about\_Operators  
  
 about\_Quoting\_Rules  
  
 about\_Script\_Internationalization  
  
 ConvertFrom\-StringData  
  
 Import\-LocalizedData

