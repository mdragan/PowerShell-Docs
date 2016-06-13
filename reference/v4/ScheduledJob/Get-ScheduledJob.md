---
external help file: PSITPro4_ScheduledJob.xml
online version: http://go.microsoft.com/fwlink/p/?linkid=290626
schema: 2.0.0
---

# Get-ScheduledJob
## SYNOPSIS
Gets scheduled jobs on the local computer.

## SYNTAX

### UNNAMED_PARAMETER_SET_1
```
Get-ScheduledJob [[-Id] <Int32[]>]
```

### UNNAMED_PARAMETER_SET_2
```
Get-ScheduledJob [-Name] <String[]>
```

## DESCRIPTION
The Get-ScheduledJob cmdlet gets scheduled jobs on the local computer.
Get-ScheduledJob gets only scheduled jobs that are created by the current user using the Register-ScheduledJob cmdlet.

Although jobs that are created by using the Register-ScheduledJob cmdlet appear in Task Scheduler, Get-ScheduledJob gets only scheduled jobs.
It does not get scheduled tasks created in Task Scheduler.

Without parameters, Get-ScheduledJob gets all scheduled jobs on the computer.
You can use the parameters of Get-ScheduledJob to get scheduled jobs by ID or name and examine them or pipe them to other cmdlets.

Get-ScheduledJob is one of a collection of job scheduling cmdlets in the PSScheduledJob module that is included in Windows PowerShell.

For more information about Scheduled Jobs, see the About topics in the PSScheduledJob module.
Import the PSScheduledJob module and then type: Get-Help about_Scheduled* or see about_Scheduled_Jobs.

This cmdlet is introduced in Windows PowerShell 3.0.

## EXAMPLES

### Example 1: Get all scheduled jobs
```
PS C:\>Get-ScheduledJob
```

This command gets all scheduled jobs on the local computer.

### Example 2: Get scheduled jobs by name
```
PS C:\>Get-ScheduledJob -Name *Backup*, *Archive*
```

This command gets all scheduled jobs on the computer that have names that include "Backup" or "Archive".
This command format lets you search for particular jobs.

### Example 3: Get scheduled jobs on remote computers
```
PS C:\>Invoke-Command -ComputerName (Get-Content Servers.txt) {Get-ScheduledJob}
```

This command gets all scheduled jobs on the computers that are listed in the Servers.txt file.
The command uses the Invoke-Command cmdlet to run a Get-ScheduleJob command on each computer.

### Example 4: Pipe scheduled jobs to other cmdlets
```
PS C:\>Get-ScheduledJob DailyBackup, WeeklyBackup | Get-JobTrigger
```

This command gets the job triggers of the DailyBackup and WeeklyBackup scheduled jobs.
It uses the Get-ScheduledJob cmdlet to get the scheduled jobs and the Get-JobTrigger cmdlet to get the job triggers of the scheduled jobs.

## PARAMETERS

### -Id
Gets only the scheduled jobs with the specified identification number (ID).
Enter one or more IDs of scheduled jobs on the computer.
By default, Get-ScheduledJob gets all scheduled jobs on the computer.

```yaml
Type: Int32[]
Parameter Sets: UNNAMED_PARAMETER_SET_1
Aliases: 

Required: False
Position: 1
Default value: All jobs
Accept pipeline input: False
Accept wildcard characters: False
```

### -Name
Gets only the scheduled jobs with the specified names.
Enter one or more names of scheduled jobs on the computer.
Wildcards are supported.
By default, Get-ScheduledJob gets all scheduled jobs on the computer.

```yaml
Type: String[]
Parameter Sets: UNNAMED_PARAMETER_SET_2
Aliases: 

Required: True
Position: 1
Default value: All jobs
Accept pipeline input: False
Accept wildcard characters: True
```

## INPUTS

### None
You cannot pipe input to Get-ScheduledJob.

## OUTPUTS

### Microsoft.PowerShell.ScheduledJob.ScheduledJobDefinition

## NOTES
Each scheduled job is saved in a subdirectory of the $home\AppData\Local\Microsoft\Windows\PowerShell\ScheduledJobs directory on the local computer.
The subdirectory is named for the scheduled job and contains the XML file for the scheduled job and records of its execution history.
For more information about scheduled jobs on disk, see about_Scheduled_Jobs_Advanced.

Scheduled jobs that you create in Windows PowerShell appear in Task Scheduler in the Task Scheduler Library\Microsoft\Windows\PowerShell\ScheduledJobs folder.
You can use Task Scheduler to view and edit the scheduled job.

You can use Task Scheduler, the SchTasks.exe command-line tool, and the Task Scheduler cmdlets to manage scheduled jobs that you create with the Scheduled Job cmdlets.
However, you cannot use the Scheduled Job cmdlets to manage tasks that you create in Task Scheduler.

## RELATED LINKS

[about_Scheduled_Jobs](3b546629-703c-4939-b44f-52dd567bce92)

[Add-JobTrigger](d0ab1b5d-ca22-4518-a3dc-88ffb4578b62)

[Disable-JobTrigger](6387c972-06c8-4f7c-a1fe-35e0ed03b3cb)

[Disable-ScheduledJob](0f633d57-fe67-4fb8-b6f1-875395c76042)

[Enable-JobTrigger](a76ca67d-298b-4674-be43-af3f781eb570)

[Enable-ScheduledJob](e61a922e-b575-4b19-b29c-2b2b6f58ebcf)

[Get-JobTrigger](60c56495-7aa1-49fd-835a-09dfad27bdf8)

[Get-ScheduledJob](ff366cbf-5e3b-49fb-b987-d1a8d9822172)

[Get-ScheduledJobOption](00b922bf-0816-4817-bd07-0534538e5d68)

[New-JobTrigger](605eb27a-e8ff-4167-b94c-988b2b893696)

[New-ScheduledJobOption](a3262ad6-5b68-452e-80da-f53173bfa89f)

[Register-ScheduledJob](47e8f0de-6a42-447b-a024-9a20da5a852f)

[Remove-JobTrigger](46cc6c3a-d929-40d7-bf3f-0eb38d203879)

[Set-JobTrigger](d79c9eef-5446-40c2-a29c-28c13dffcd7c)

[Set-ScheduledJob](f759d9ff-6807-45d5-af98-7e56efd9615c)

[Set-ScheduledJobOption](5fe666db-ceed-4261-89ec-376dd01712f9)

[Unregister-ScheduledJob](a76ff3d0-1496-46a8-885a-b54552eda897)
