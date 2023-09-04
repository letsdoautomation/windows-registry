#### Paths to registry
```
# Machine
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Active Setup\Installed Components

# Current user
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Active Setup\Installed Components
HKEY_CURRENT_USER\Software\Wow6432Node\Microsoft\Active Setup\Installed Components
```

#### Message command from active setup only
```powershell
REG ADD "HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\RunCMD" /v StubPath /t REG_SZ /d "cmd /c echo Running from HKLM\Active Setup && whoami && pause"
```

```powershell
REG ADD "HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\RunCMD" /v Version /t REG_SZ /d "1,1,1,1"
```

#### Message command from active setup and then RunOnce registry
```powershell
ni "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\RunCMDFromRunOnce" | New-ItemProperty -Name "StubPath" -Value 'REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v RunCMD /t REG_SZ /d "cmd /c echo Running from HKCU\RunOnce && whoami && pause"'
```

#### Download Brave
Download link: [Brave](https://github.com/brave/brave-browser) <br />

## Install Brave from Active Setup and then Run Once
```powershell
ni "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\InstallBraveFromRunOnce" | New-ItemProperty -Name "StubPath" -Value 'REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v InstallBrave /t REG_SZ /d "cmd /c echo installing software.. && cmd /c C:\BraveBrowserStandaloneSilentSetup.exe"'
```