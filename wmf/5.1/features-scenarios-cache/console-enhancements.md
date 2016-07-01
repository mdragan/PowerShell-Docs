---
title: Enhancements to the console experience
author: jasonsh
---

>Note: provide a proposed descriptive title and a brief description

## PowerShell Console Enhancements

The following changes have been made to powershell.exe to improve the console experience:

1. VT100 support

Windows 10 added support for [VT100 escape sequences](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).
PowerShell will ignore certain VT100 formatting escape sequences when calculating table widths.

PowerShell also added a new api that can be used in formatting code to determine if VT100 is supported.  For example:

```
if ($host.UI.SupportsVirtualTerminal)
{
    $esc = [char]0x1b
    "A yellow ${esc}[93mhello${esc}[0m"
}
else
{
    "A default hello"
}
```
Here is a complete [example](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) that can be used to highlight matches from Select-String.
Save the example in a file named `MatchInfo.format.ps1xml`, the to use it, in your profile or elsewhere, run `Update-FormatData -Prepend MatchInfo.format.ps1xml`.

Note that VT100 escape sequences are only supported starting with the Aniversary update to Windows 10, they are not supported on earlier systems.   

2. Vi mode support in PSReadline

[PSReadline](https://github.com/lzybkr/PSReadLine) adds support for vi mode. To use vi mode, run `Set-PSReadline -EditMode vi`.

3. Redirected stdin w/ interactive input 

In earlier versions, starting PowerShell with `powershell -File -` was required when stdin was redirected and
you wanted to enter commands interactively.

With WMF 5.1, this hard to discover option is no longer necessary, you can start powershell without any options, e.g. `powershell`.

Note that PSReadline does not currently supported redirected stdin, and the builtin commanding line editing experience with redirected
stdin is extremely limited, e.g. arrow keys don't work.  A future release of PSReadline should address this issue.   