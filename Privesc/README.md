To install this module, drop the entire Privesc folder into one of your module directories. The default PowerShell module paths are listed in the $Env:PSModulePath environment variable.

The default per-user module path is: "$Env:HomeDrive$Env:HOMEPATH\Documents\WindowsPowerShell\Modules"
The default computer-level module path is: "$Env:windir\System32\WindowsPowerShell\v1.0\Modules"

To use the module, type `Import-Module Privesc`

To see the commands imported, type `Get-Command -Module Privesc`

For help on each individual command, Get-Help is your friend.

Note: The tools contained within this module were all designed such that they can be run individually. Including them in a module simply lends itself to increased portability.


## PowerUp

PowerUp aims to be a clearinghouse of common Windows privilege escalation
vectors that rely on misconfigurations.

Running Invoke-PrivescAudit will output any identifiable vulnerabilities along
with specifications for any abuse functions. The -HTMLReport flag will also
generate a COMPUTER.username.html version of the report.

Author: @harmj0y
License: BSD 3-Clause
Required Dependencies: None
Optional Dependencies: None


### Service Enumeration:
    Get-ServiceUnquoted                 -   returns services with unquoted paths that also have a space in the name
    Get-ModifiableServiceFile           -   returns services where the current user can write to the service binary path or its config
    Get-ModifiableService               -   returns services the current user can modify
    Get-ServiceDetail                   -   returns detailed information about a specified service

### Service Abuse:
    Invoke-ServiceAbuse                 -   modifies a vulnerable service to create a local admin or execute a custom command
    Write-ServiceBinary                 -   writes out a patched C# service binary that adds a local admin or executes a custom command
    Install-ServiceBinary               -   replaces a service binary with one that adds a local admin or executes a custom command
    Restore-ServiceBinary               -   restores a replaced service binary with the original executable

### DLL Hijacking:
    Find-ProcessDLLHijack               -   finds potential DLL hijacking opportunities for currently running processes
    Find-PathDLLHijack                  -   finds service %PATH% DLL hijacking opportunities
    Write-HijackDll                     -   writes out a hijackable DLL
    
### Registry Checks:
    Get-RegistryAlwaysInstallElevated   -  checks if the AlwaysInstallElevated registry key is set
    Get-RegistryAutoLogon               -   checks for Autologon credentials in the registry
    Get-ModifiableRegistryAutoRun       -   checks for any modifiable binaries/scripts (or their configs) in HKLM autoruns

### Miscellaneous Checks:
    Get-ModifiableScheduledTaskFile     -   find schtasks with modifiable target files
    Get-UnattendedInstallFile           -   finds remaining unattended installation files
    Get-Webconfig                       -   checks for any encrypted web.config strings
    Get-ApplicationHost                 -   checks for encrypted application pool and virtual directory passwords
    Get-SiteListPassword                -   retrieves the plaintext passwords for any found McAfee's SiteList.xml files
    Get-CachedGPPPassword               -   checks for passwords in cached Group Policy Preferences files

### Other Helpers/Meta-Functions:
    Get-ModifiablePath                  -   tokenizes an input string and returns the files in it the current user can modify
    Get-CurrentUserTokenGroupSid        -   returns all SIDs that the current user is a part of, whether they are disabled or not
    Add-ServiceDacl                     -   adds a Dacl field to a service object returned by Get-Service
    Set-ServiceBinPath                  -   sets the binary path for a service to a specified value through Win32 API methods
    Test-ServiceDaclPermission          -   tests one or more passed services or service names against a given permission set
    Write-UserAddMSI                    -   write out a MSI installer that prompts for a user to be added
    Invoke-PrivescAudit                 -   runs all current escalation checks and returns a report
