---
title:  Starting Windows PowerShell
ms.date:  2016-05-11
keywords:  powershell,cmdlet
description:  
ms.topic:  article
author:  jpjofre
manager:  dongill
ms.prod:  powershell
ms.assetid:  59b649a2-c90c-4cf4-bf95-a740c59148e7
---

# Starting Windows PowerShell
**ToDo: Explain how to start Windows PowerShell**

## Starting the 32-Bit Version of Windows PowerShell on 64-bit Windows operating system
When you install Windows PowerShell on a 64\-bit computer, **Windows PowerShell (x86)**, a 32\-bit version of Windows PowerShell is installed in addition to the 64\-bit version. When you run Windows PowerShell, the 64\-bit version runs by default.

However, you might occasionally need to run **Windows PowerShell (x86)**, such as when you are using a module that requires the 32\-bit version or when you are connecting remotely to a 32\-bit computer.

To start a 32\-bit version of Windows PowerShell, use any of the following procedures.

### In Windows Server® 2012 and Windows Server® 2012 R2

1.   On the **Start** screen, type **Windows PowerShell (x86)**. Click the **Windows PowerShell x86** tile.

2.  In **Server Manager**, from the **Tools** menu, select **Windows PowerShell (x86)**.

3.  On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.

### In Windows 8.1

-   On the **Start** screen, type **Windows PowerShell (x86)**. Click the **Windows PowerShell x86** tile.

-   If you are running [Remote Server Administration Tools](http://go.microsoft.com/fwlink/?LinkID=304145) for Windows 8.1, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu. Select **Windows PowerShell (x86)**.

-   On the desktop, move the cursor to the upper right corner, click **Search**, type **PowerShell x86** and then click **Windows PowerShell (x86)**.

### In Windows 8
1. On the **Start** screen, move the cursor to the upper right corner, click **Settings**, click **Tiles**, and then move the **Show Administrative Tools** slider to Yes. Then, type **PowerShell** and click **Windows PowerShell (x86)**.

2. If you are running [Remote Server Administration Tools](http://www.microsoft.com/download/details.aspx?id=28972) for Windows 8, you can also open Windows PowerShell x86 from the **Server ManagerTools** menu. Select **Windows PowerShell (x86)**.

3.  On the **Start** screen or the desktop, type **PowerShell (x86)** and then click **Windows PowerShell (x86)**.

## Starting Windows PowerShell on Earlier Versions of Windows
This section explains how to start Windows PowerShell and Windows PowerShell Integrated Scripting Environment (ISE) on Windows® 7, Windows Server® 2008 R2, and Windows Server 2008. It also explains how to enable the optional feature for Windows PowerShell ISE in Windows PowerShell 2.0 on Windows Server® 2008 R2 and Windows Server 2008.

Use any of the following methods to start the installed version of Windows PowerShell 3.0, or Windows PowerShell 4.0, where applicable.

### From the Start Menu

1. Click **Start**, type **PowerShell**, and then click **Windows PowerShell**.

2. From the **Start** menu, click **Start**, click **All Programs**, click **Accessories**, click the **Windows PowerShell** folder, and then click **Windows PowerShell**.

### At the Command Prompt

1. In Cmd.exe, Windows PowerShell, or Windows PowerShell ISE, to start Windows PowerShell, type:

    ```
    PowerShell
    ```

    You can also use the parameters of the PowerShell.exe program to customize the session. For more information, see [PowerShell.exe Command-Line Help](../core-powershell/console/PowerShell.exe-Command-Line-Help.md).

#### With Administrative privileges ("Run as administrator")

1.  Click **Start**, type **PowerShell**, right\-click **Windows PowerShell**, and then click **Run as administrator**.

## See Also
[Windows PowerShell System Requirements](Windows-PowerShell-System-Requirements.md)
[Installing Windows PowerShell](Installing-Windows-PowerShell.md)
