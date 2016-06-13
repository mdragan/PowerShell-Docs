---
external help file: PSITPro4_Utility.xml
online version: http://go.microsoft.com/fwlink/p/?linkid=294030
schema: 2.0.0
---

# Write-Output
## SYNOPSIS
Sends the specified objects to the next command in the pipeline.
If the command is the last command in the pipeline, the objects are displayed in the console.

## SYNTAX

```
Write-Output [-InputObject] <PSObject[]> [-NoEnumerate]
```

## DESCRIPTION
The Write-Output cmdlet sends the specified object down the pipeline to the next command.
If the command is the last command in the pipeline, the object is displayed in the console.

Write-Output sends objects down the primary pipeline, also known as the "output stream" or the "success pipeline." To send error objects down the error pipeline, use Write-Error.

This cmdlet is typically used in scripts to display strings and other objects on the console.
However, because the default behavior is to display the objects at the end of a pipeline, it is generally not necessary to use the cmdlet.
For example, "get-process | write-output" is equivalent to "get-process".

## EXAMPLES

### -------------------------- EXAMPLE 1 --------------------------
```
PS C:\>$p = get-process
PS C:\>write-output $p
PS C:\>$p
```

These commands get objects representing the processes running on the computer and display the objects on the console.

### -------------------------- EXAMPLE 2 --------------------------
```
PS C:\>write-output "test output" | get-member
```

This command pipes the "test output" string to the Get-Member cmdlet, which displays the members of the String class, demonstrating that the string was passed along the pipeline.

### -------------------------- EXAMPLE 3 --------------------------
```
PS C:\>write-output @(1,2,3) | measure

Count    : 3
...

PS C:\>write-output @(1,2,3) -NoEnumerate | measure

Count    : 1
```

This command adds the NoEnumerate parameter to treat a collection or array as a single object through the pipeline.

## PARAMETERS

### -InputObject
Specifies the objects to send down the pipeline.
Enter a variable that contains the objects, or type a command or expression that gets the objects.

```yaml
Type: PSObject[]
Parameter Sets: (All)
Aliases: 

Required: True
Position: 1
Default value: 
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -NoEnumerate
By default, the Write-Output cmdlet always enumerates its output.
The NoEnumerate parameter suppresses the default behavior, and prevents Write-Output from enumerating output.
The NoEnumerate parameter has no effect on collections that were created by wrapping commands in parentheses, because the parentheses force enumeration.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: True
Position: 1
Default value: 
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

## INPUTS

### System.Management.Automation.PSObject
You can pipe objects to Write-Output.

## OUTPUTS

### System.Management.Automation.PSObject
Write-Output returns the objects that are submitted as input.

## NOTES

## RELATED LINKS

[Tee-Object](ae5c403c-6a21-430e-a94a-74a1edee149a)

[Write-Debug](fb95cfe7-8a21-4b6a-9e00-0205a6b74c41)

[Write-Error](eedfea70-5aa7-4d20-b87d-f8e1147b1b42)

[Write-Host](023e670a-cfda-4e8c-af8f-c2b2d9ee5612)

[Write-Progress](3e78a07f-87ae-4bc2-ac28-b0163831fd80)

[Write-Verbose](d17c2519-dae0-4142-a506-9acfb79b72e7)

[Write-Warning](8e53946e-1762-40e6-ab70-5307f6fc2a98)
