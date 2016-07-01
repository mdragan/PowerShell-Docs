---
description:  
manager:  dongill
ms.topic:  article
author:  jpjofre
ms.prod:  powershell
keywords:  powershell,cmdlet
ms.date:  2016-07-01
title:  about_Debuggers
ms.technology:  powershell
ms.assetid:  2b2ce8b3-f881-4528-bd30-f453dea06755
---

# about_Debuggers
```  
TOPIC  
    about_Debuggers  
  
SHORT DESCRIPTION  
    Describes the Windows PowerShell debugger.  
  
LONG DESCRIPTION  
    Debugging is the process of examining a script while it is running in  
    order to identify and correct errors in the script instructions. The  
    Windows PowerShell debugger is designed to help you examine and identify  
    errors and inefficiencies in your scripts.  
  
    Note: The Windows PowerShell debugger does not run remotely. To debug  
          a script on a remote computer, copy the script to the local  
          computer.  
  
    You can use the features of the Windows PowerShell debugger to examine a   
    Windows PowerShell script, function, command, or expression while it is  
    running. The Windows PowerShell debugger includes a set of cmdlets that  
    let you set breakpoints, manage breakpoints, and view the call stack.  
  
  Debugger Cmdlets  
      The Windows PowerShell debugger includes the following set of cmdlets:  
  
          Set-PsBreakpoint:     Sets breakpoints on lines, variables, and  
                                commands.   
  
          Get-PsBreakpoint:     Gets breakpoints in the current session.  
  
          Disable-PsBreakpoint: Turns off breakpoints in the current session.  
  
          Enable-PsBreakpoint:  Re-enables breakpoints in the current session.  
  
          Remove-PsBreakpoint:  Deletes breakpoints from the current session.  
  
          Get-PsCallStack:      Displays the current call stack.  
  
  Starting and Stopping the Debugger  
      To start the debugger, set one or more breakpoints. Then, run the script,  
      command, or function that you want to debug.  
  
      When you reach a breakpoint, execution stops, and control is turned over   
      to the debugger.  
  
      To stop the debugger, run the script, command, or function until it is   
      complete. Or, type "stop" or "t".  
  
  Debugger Commands  
      When you use the debugger in the Windows PowerShell console, use the   
      following commands to control the execution.  
  
      Note: For information about how to use the debugger in other host  
          applications, see the host application documentation.  
  
 s, Step-into        Executes the next statement and then stops.  
  
 v, Step-over        Executes the next statement, but skips functions  
                            and invocations. The skipped statements are  
                            executed, but not stepped through.  
  
 o, Step-out         Steps out of the current function; up one level  
                            if nested. If in the main body, it continues to  
                            the end or the next breakpoint. The skipped  
                            statements are executed, but not stepped through.  
  
 c, Continue         Continues to run until the script is complete or  
                            until the next breakpoint is reached. The skipped  
                            statements are executed, but not stepped through.  
  
        l, List             Displays the part of the script that is executing.  
                            By default, it displays the current line, five  
                            previous lines, and 10 subsequent lines. To continue  
                            listing the script, press ENTER.  
  
        l <m>, List         Displays 16 lines of the script beginning with the  
                            line number specified by <m>.                             
  
        l <m> <n>, List     Displays <n> lines of the script, beginning with the  
                            line number specified by <m>.                             
  
        q, Stop             Stops executing the script, and exits the debugger.  
  
        k, Get-PsCallStack  Displays the current call stack.  
  
<Enter>             Repeats the last command if it was Step (s),   
                            Step-over (v), or List (l). Otherwise, represents a  
                            submit action.  
  
?, h                Displays the debugger command Help.  
  
      To exit the debugger, use Stop (q).  
  
      By using these debugger commands, you can run a script, stop on a point  
      of concern, examine the values of variables and the state of the system,  
      and continue running the script until you have identified a problem.   
  
      NOTE:  If you step into a statement with a redirection operator,   
             such as ">", the Windows PowerShell debugger steps over all  
             remaining statements in the script.  
  
  Displaying the Values of script Variables  
  
      While you are in the debugger, you can also enter commands, display the  
      value of variables, use cmdlets, and run scripts at the command line.  
  
      You can display the current value of all variables in the script that is  
      being debugged, except for the following automatic variables:   
  
          $_  
          $Args  
          $Input  
          $MyInvocation  
          $PSBoundParameters  
  
      If you try to display the value of any of these variables, you get the   
      value of that variable for in an internal pipeline the debugger uses, not  
      the value of the variable in the script.  
  
      To display the value these variables for the script that is being debugged,  
      in the script, assign the value of the automatic variable to a new variable.  
      Then you can display the value of the new variable.  
  
      For example,  
  
          $scriptArgs = $Args  
          $scriptArgs  
  
      In the example in this topic, the value of the $MyInvocation variable is  
      reassigned as follows:  
  
          $scriptname = $MyInvocation.MyCommand.Path  
  
  The Debugger Environment  
      When you reach a breakpoint, you enter the debugger environment. The  
      command prompt changes so that it begins with "[DBG]:". You can customize  
      the prompt.  
  
      Also, in some host applications, such as the Windows PowerShell console,  
      (but not in Windows PowerShell Integrated Scripting Environment [ISE]),   
      a nested prompt opens for debugging. You can detect the nested prompt by  
      the repeating greater-than characters (ASCII 62) that appear at the  
      command prompt.  
  
      For example, the following is the default debugging prompt in the  
      Windows PowerShell console:  
  
          [DBG]: PS (get-location)>>>  
  
      You can find the nesting level by using the $NestedPromptLevel   
      automatic variable.  
  
      Additionally, an automatic variable, $PSDebugContext, is defined in   
      the local scope. You can use the presence of the $PsDebugContext   
      variable to determine whether you are in the debugger.  
  
      For example:  
  
          if ($psdebugcontext) {"Debugging"} else {"Not Debugging"}  
  
      You can use the value of the $PSDebugContext variable in your  
      debugging.  
  
[DBG]: PS>>> $psdebugcontext.invocationinfo  
  
        Name   CommandLineParameters  UnboundArguments  Location  
        ----   ---------------------  ----------------  --------  
        =      {}                     {}                C:\ps-test\vote.ps1 (1)  
  
  Debugging and Scope  
      Breaking into the debugger does not change the scope in which  
      you are operating, but when you reach a breakpoint in a script,  
      you move into the script scope. The script scope is a child   
      of the scope in which you ran the debugger.  
  
      To find the variables and aliases that are defined in the   
      script scope, use the Scope parameter of the Get-Alias or  
      Get-Variable cmdlets.  
  
      For example, the following command gets the variables in the  
      local (script) scope:  
  
  get-variable -scope 0  
  
      You can abbreviate the command as:  
  
gv -s 0  
  
      This is a useful way to see only the variables that you defined in the  
      script and that you defined while debugging.  
  
  Debugging at the Command Line  
      When you set a variable breakpoint or a command breakpoint, you can set  
      the breakpoint only in a script file. However, by default, the breakpoint  
      is set on anything that runs in the current session.  
  
      For example, if you set a breakpoint on the $name variable, the debugger  
      breaks on any $name variable in any script, command, function, script   
      cmdlet or expression that you run until you disable or remove the   
      breakpoint.  
  
      This allows you to debug your scripts in a more realistic context in   
      which they might be affected by functions, variables, and other scripts  
      in the session and in the user's profile.  
  
      Line breakpoints are specific to script files, so they are set only in  
      script files.  
  
  Debugging Functions  
      When you set a breakpoint on a function that has Begin, Process, and  
      End sections, the debugger breaks at the first line of each section.  
  
      For example:  
  
              function test-cmdlet  
              {  
                  begin  
                  {  
                      write-output "Begin"  
                  }  
                  process  
                  {  
                      write-output "Process"  
                  }  
                  end  
                  {  
                      write-output "End"  
                  }  
              }  
  
          C:\PS> set-psbreakpoint -command test-cmdlet  
  
          C:\PS> test-cmdlet  
  
          Begin  
          Entering debug mode. Use h or ? for help.  
  
          Hit Command breakpoint on 'prompt:test-cmdlet'  
  
          test-cmdlet  
  
          [DBG]: C:\PS> c  
          Process  
          Entering debug mode. Use h or ? for help.  
  
          Hit Command breakpoint on 'prompt:test-cmdlet'  
  
          test-cmdlet  
  
          [DBG]: C:\PS> c  
          End  
          Entering debug mode. Use h or ? for help.  
  
          Hit Command breakpoint on 'prompt:test-cmdlet'  
  
          test-cmdlet  
  
          [DBG]: C:\PS>  
  
  Debugging Remote Scripts  
      You cannot run the Windows PowerShell debugger in a remote session. To   
      debug a script on a remote computer, copy the script to the local   
      computer.  
  
      The following command copies the Test.ps1 script from the Server01 remote  
      computer to the local computer:  
  
          invoke-command -computername Server01 `  
          {get-content c:\ps-test\test.ps1} | set-content c:\ps-test\test.ps1  
  
  Examples  
      This test script detects the version of the operating system and   
      displays a system-appropriate message. It includes a function, a function  
      call, and a variable.  
  
      The following command displays the contents of the test script file:  
  
  c:>\PS-test>  get-content test.ps1  
  
  function psversion {  
             "Windows PowerShell " + $psversiontable.psversion  
              if ($psversiontable.psversion.major -lt 2) {  
                  "Upgrade to Windows PowerShell 2.0!"  
              }  
              else {  
                  "Have you run a background job today (start-job)?"  
              }  
          }  
  
  $scriptname = $MyInvocation.MyCommand.Path  
  psversion  
  "Done $scriptname."  
  
      To start, set a breakpoint at a point of interest in the script, such  
      as a line, command, variable, or function.  
  
      Start by creating a line breakpoint on the first line of the Test.ps1  
      script in the current directory.  
  
          PS C:\ps-test> set-psbreakpoint -line 1 -script test.ps1  
  
      You can abbreviate this command as:  
  
          PS C:\ps-test> spb 1 -s test.ps1  
  
      The command returns a line-breakpoint object  
      (System.Management.Automation.LineBreakpoint).  
  
      Column     : 0  
            Line       : 1  
            Action     :  
            Enabled    : True  
            HitCount   : 0  
            Id         : 0  
            Script     : C:\ps-test\test.ps1  
            ScriptName : C:\ps-test\test.ps1  
  
      Now, start the script.  
  
  PS C:\ps-test> .\test.ps1  
  
      When the script reaches the first breakpoint, the breakpoint message  
      indicates that the debugger is active. It describes the breakpoint and   
      previews the first line of the script, which is a function declaration.   
      The command prompt also changes to indicate that the debugger has   
      control.  
  
      The preview line includes the script name and the line number of the  
      previewed command.  
  
          Entering debug mode. Use h or ? for help.  
  
          Hit Line breakpoint on 'C:\ps-test\test.ps1:1'  
  
          test.ps1:1   function psversion {  
          DBG>  
  
      Use the Step command (s) to execute the first statement in the script  
      and to preview the next statement. The next statement uses the   
      $MyInvocation automatic variable to set the value of the $ScriptName   
      variable to the path and file name of the script file.  
  
          DBG> s  
          test.ps1:11  $scriptname = $MyInvocation.MyCommand.Path  
  
      At this point, the $ScriptName variable is not populated, but you can  
      verify the value of the variable by displaying its value. In this case,  
      the value is $null.  
  
          DBG> $scriptname  
          DBG>  
  
      Use another Step command (s) to execute the current statement and to   
      preview the next statement in the script. The next statement calls the   
      PsVersion function.  
  
  DBG> s  
  test.ps1:12  psversion  
  
      At this point, the $ScriptName variable is populated, but you verify the  
      value of the variable by displaying its value. In this case, the value  
      is set to the script path.  
  
          DBG> $scriptname  
          C:\ps-test\test.ps1  
  
      Use another Step command to execute the function call. Press ENTER,  
      or type "s" for Step.  
  
  DBG> s  
  test.ps1:2       "Windows PowerShell " + $psversiontable.psversion  
  
      The debug message includes a preview of the statement in the function.  
      To execute this statement and to preview the next statement in the   
      function, you can use a Step command. But, in this case, use a Step-Out   
      command (o). It completes the execution of the function (unless it   
      reaches a breakpoint) and steps to the next statement in the script.  
  
  DBG> o  
  Windows PowerShell 2.0  
  Have you run a background job today (start-job)?  
  test.ps1:13  "Done $scriptname"  
  
      Because we are on the last statement in the script, the Step, Step-Out,   
      and Continue commands have the same effect. In this case, use   
      Step-Out (o).  
  
  Done C:\ps-test\test.ps1  
  PS C:\ps-test>  
  
      The Step-Out command executes the last command. The standard command   
      prompt indicates that the debugger has exited and returned control to the  
      command processor.  
  
      Now, run the debugger again. First, to delete the current   
      breakpoint, use the Get-PsBreakpoint and Remove-PsBreakpoint cmdlets.  
      (If you think you might reuse the breakpoint, use the   
      Disable-PsBreakpoint cmdlet instead of Remove-PsBreakpoint.)  
  
  PS C:\ps-test> Get-PsBreakpoint | Remove-PSBreakpoint  
  
      You can abbreviate this command as:  
  
  PS C:\ps-test> gbp | rbp  
  
      Or, run the command by writing a function, such as the following   
      function:  
  
  function delbr { gbp | rbp }  
  
      Now, create a breakpoint on the $scriptname variable.  
  
  PS C:\ps-test> set-psbreakpoint -variable scriptname -script test.ps1  
  
      You can abbreviate the command as:  
  
  PS C:\ps-test> sbp -v scriptname -s test.ps1  
  
      Now, start the script. The script reaches the variable breakpoint. The   
      default mode is Write, so execution stops just before the statement  
      that changes the value of the variable.  
  
  PS C:\ps-test> .\test.ps1  
  Hit Variable breakpoint on 'C:\ps-test\test.ps1:$scriptname'  
          (Write access)  
  
  test.ps1:11  $scriptname = $MyInvocation.mycommand.path  
  DBG>  
  
      Display the current value of the $scriptname variable, which  
      is $null.  
  
          DBG> $scriptname  
          DBG>  
  
      Use a Step command (s) to execute the statement that populates  
      the variable. Then, display the new value of the $scriptname  
      variable.  
  
  DBG> $scriptname  
  C:\ps-test\test.ps1  
  
      Use a Step command (s) to preview the next statement in the script.  
  
  DBG> s  
  test.ps1:12  psversion  
  
      The next statement is a call to the PsVersion function. To skip the  
      function but still execute it, use a Step-Over command (v). If you are  
      already in the function when you use Step-Over, it is not effective. The   
      function call is displayed, but it is not executed.  
  
  DBG> v  
  Windows PowerShell 2.0  
  Have you run a background job today (start-job)?  
  test.ps1:13  "Done $scriptname"  
  
      The Step-Over command executes the function, and it previews the next  
      statement in the script, which prints the final line.  
  
      Use a Stop command (t) to exit the debugger. The command prompt   
      reverts to the standard command prompt.  
  
  C:\ps-test>  
  
      To delete the breakpoints, use the Get-PsBreakpoint and  
      Remove-PsBreakpoint cmdlets.  
  
  PS C:\ps-test> Get-PsBreakpoint | Remove-PSBreakpoint  
  
      Create a new command breakpoint on the PsVersion function.  
  
          PS C:\ps-test> Set-PsBreakpoint -command psversion -script test.ps1  
  
      You can abbreviate this command to:  
  
          PS C:\ps-test> sbp -c psversion -s test.ps1  
  
      Now, run the script.  
  
          PS C:\ps-test> .\test.ps1  
          Hit Command breakpoint on 'C:\ps-test\test.ps1:psversion'  
  
          test.ps1:12  psversion  
          DBG>  
  
      The script reaches the breakpoint at the function call. At this point,   
      the function has not yet been called. This gives you the opportunity  
      to use the Action parameter of Set-PsBreakpoint to set conditions for  
      the execution of the breakpoint or to perform preparatory or diagnostic  
      tasks, such as starting a log or invoking a diagnostic or security  
      script.  
  
      To set an action, use a Continue command (c) to exit the script, and a  
      Remove-PsBreakpoint command to delete the current breakpoint.   
      (Breakpoints are read-only, so you cannot add an action to the current  
      breakpoint.)  
  
  DBG> c  
  Windows PowerShell 2.0  
  Have you run a background job today (start-job)?  
  Done C:\ps-test\test.ps1  
  
  PS C:\ps-test> get-psbreakpoint | remove-psbreakpoint  
  PS C:\ps-test>  
  
      Now, create a new command breakpoint with an action. The following  
      command sets a command breakpoint with an action that logs the value  
      of the $scriptname variable when the function is called. Because the  
      Break keyword is not used in the action, execution does not stop. (The  
      backtick (`) is the line-continuation character.)  
  
         PS C:\ps-test> set-psbreakpoint -command psversion -script test.ps1  `  
         -action { add-content "The value of `$scriptname is $scriptname." `  
         -path action.log}  
  
      You can also add actions that set conditions for the breakpoint. In  
      the following command, the command breakpoint is executed only if the  
      execution policy is set to RemoteSigned, the most restrictive policy  
      that still permits you to run scripts. (The backtick (`) is the  
      continuation character.)  
  
          PS C:\ps-test> set-psbreakpoint -script test.ps1 -command psversion `  
          -action { if ((get-executionpolicy) -eq "RemoteSigned") { break }}  
  
      The Break keyword in the action directs the debugger to execute the  
      breakpoint. You can also use the Continue keyword to direct the debugger  
      to execute without breaking. Because the default keyword is Continue,   
      you must specify Break to stop execution.  
  
      Now, run the script.  
  
  PS C:\ps-test> .\test.ps1  
  Hit Command breakpoint on 'C:\ps-test\test.ps1:psversion'  
  
  test.ps1:12  psversion  
  
      Because the execution policy is set to RemoteSigned, execution stops  
      at the function call.  
  
      At this point, you might want to check the call stack. Use the  
      Get-PsCallStack cmdlet or the Get-PsCallStack debugger command (k).  
      The following command gets the current call stack.  
  
  DBG> k  
  2: prompt  
  1: .\test.ps1: $args=[]  
  0: prompt: $args=[]  
  
      This example demonstrates just a few of the many ways to use the Windows  
      PowerShell debugger.  
  
      For more information about the debugger cmdlets, type the following  
      command:  
  
          help <cmdlet-name> -full  
  
      For example, type:  
  
          help set-psbreakpoint -full  
  
  Other Debugging Features in Windows PowerShell  
  
    In addition to the Windows PowerShell debugger, Windows PowerShell includes  
    several other features that you can use to debug scripts and functions.  
  
    -- Windows PowerShell Interactive Scripting Environment (ISE) includes  
       an interactive graphical debugger. For more information, start Windows  
       PowerShell ISE and press F1.  
  
    -- The Set-PSDebug cmdlet offers very basic script debugging features,  
       including stepping and tracing.   
  
    -- Use the Set-StrictMode cmdlet to detect references to   
       uninitialized variables, to references to non-existent properties  
       of an object, and to function syntax that is not valid.   
  
    -- Add diagnostic statements to a script, such as statements that  
       display the value of variables, statements that read input from  
       the command line, or statements that report the current   
       instruction. Use the cmdlets that contain the Write verb for   
       this task, such as Write-Host, Write-Debug, Write-Warning, and  
       Write-Verbose.  
  
SEE ALSO  
    Disable-PsBreakpoint  
    Enable-PsBreakpoint  
    Get-PsBreakpoint     
    Get-PsCallStack  
    Remove-PsBreakpoint  
    Set-PsBreakpoint   
    Set-PsDebug  
    Set-Strictmode  
    Write-Debug  
    Write-Verbose      
```

