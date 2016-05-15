# PowerOPS
PowerShell Runspace Portable Post Exploitation Tool aimed at making Penetration Testing with PowerShell "easier"

### What is it:

PowerOPS is an application written in C# that does not rely on powershell.exe but runs PowerShell commands and functions within a powershell runspace environment (.NET). It intends to include multiple offensive PowerShell modules to make the process of Post Exploitation easier.

It tries to follow the KISS principle, being as simple as possible. The main goal is to make it easy to use PowerShell offensively and help to evade antivirus and other mitigations solutions. It does this by:

1. Doesn't rely on powershell.exe, it calls PowerShell directly through the .NET framework, which might help bypassing security controls like GPO, SRP, App Locker.
2. The payloads are executed from memory and never touch disk, evading most antivirus engines.

PowerOPS was inspired by [Cn33liz/p0wnedShell](https://github.com/Cn33liz/p0wnedShell). However I was only interested in PowerShell modules and I was looking for more flexibility. Since PowerOPS offers basically an interactive PowerShell command prompt you are free to use the PowerShell tools included the way you want, and additionally execute any valid PowerShell command.

### What's inside the runspace:

#### The following PowerShell tools/functions are included:

* [Powersploit](https://github.com/PowerShellMafia/PowerSploit)
  - Invoke-Mimikatz
  - Invoke-Shellcode
  - Invoke-ReflectivePEInjection
  - Invoke-TokenManipulation
  - Invoke-NinjaCopy
  - Invoke-WMICommand
* [PowerTools](https://github.com/PowerShellEmpire/PowerTools)
  - PowerUp
  - PowerView
* [Nishang](https://github.com/samratashok/nishang)
  - Get-Infromation
  - Port-Scan
  - Get-PassHashes
* [Auto-GPPPassword](https://github.com/roo7break/PowerShell-Scripts/blob/master/auto-gpppassword/auto-gpppassword.ps1)
* [PowerCat](https://github.com/besimorhino/powercat)
* [Empire](https://github.com/PowerShellEmpire/)
  - Invoke-Psexec

Additionally you can run any valid PowerShell command.

Powershell functions within the Runspace are loaded in memory from Base64 Encoded Strings.

### How to Compile it:

To compile PowerOPS you need to import this project within Microsoft Visual Studio or if you don't have access to a Visual Studio installation, you can compile it as follows:

To Compile as x86 binary:

```
cd C:\Windows\Microsoft.NET\Framework64\v4.0.30319 (Or newer .NET version folder)

csc.exe /unsafe /reference:"C:\path\to\System.Management.Automation.dll" /reference:System.IO.Compression.dll /out:C:\users\username\PowerOPS_x86.exe /platform:x86 "C:\path\to\PowerOPS\PowerOPS\*.cs"
```

To Compile as x64 binary:

```
cd C:\Windows\Microsoft.NET\Framework64\v4.0.30319 (Or newer .NET version folder)

csc.exe /unsafe /reference:"C:\path\to\System.Management.Automation.dll" /reference:System.IO.Compression.dll /out:C:\users\username\PowerOPS_x64.exe /platform:x64 "C:\path\to\PowerOPS\PowerOPS\*.cs"
```

PowerOPS uses the System.Management.Automation namespace, so make sure you have the System.Management.Automation.dll within your source path when compiling outside of Visual Studio.

### How to use it:

Just run the executables.

### Credits:

PowerOPS was inspired by [Cn33liz/p0wnedShell](https://github.com/Cn33liz/p0wnedShell), and basically consists of work from [Nikhil Mittal] (http://www.labofapenetrationtester.com/) of Nishang, [mattifiestation](https://twitter.com/mattifestation) of PowerSploit and [sixdub](https://twitter.com/sixdub), [engima0x3](https://twitter.com/enigma0x3) and [harmj0y](https://twitter.com/HarmJ0y) of Empire. 

### TODO:

Improve "How to use it" section. Add more attacks and test!