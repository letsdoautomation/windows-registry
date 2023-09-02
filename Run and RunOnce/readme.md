# Run and RunOnce

<b>Documentation:</b> [Run and RunOnce Registry Keys](https://learn.microsoft.com/en-us/windows/win32/setupapi/run-and-runonce-registry-keys) <br />

# Examples
## Runing CMD in HKCU
```powershell
# HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
# HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce

REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v RunCMD /t REG_SZ /d "cmd /c echo Running from HKCU\RunOnce && whoami && pause"

REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v RunCMD /t REG_SZ /d "cmd /c echo Running from HKCU\Run && whoami && pause"
```

## Installing Brave using RunOnce
Download link: [Brave](https://github.com/brave/brave-browser) <br />

```powershell
REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v InstallBrave /t REG_SZ /d "cmd /c echo installing software.. && cmd /c C:\BraveBrowserStandaloneSilentSetup.exe"
```

## Uninstalling Brave using RunOnce
```powershell
REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v RemoveBrave /t REG_SZ /d "cmd /c echo removing software.. && cmd /c powershell.exe -Command ""& {$remove = Get-ItemPropertyValue -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Uninstall\BraveSoftware Brave-Browser' -Name UninstallString; cmd /c $($remove) --force-uninstall}"""
```

## Runing CMD in HKLM
```powershell
# HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
# HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce

# RunOnce in HKLM works only on administrator accounts
REG ADD "HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v RunCMD /t REG_SZ /d "cmd /c echo Running from HKLM\RunOnce && whoami && pause"

REG ADD "HKLM\Software\Microsoft\Windows\CurrentVersion\Run" /v RunCMD /t REG_SZ /d "cmd /c echo Running from HKLM\Run && whoami && pause"
```