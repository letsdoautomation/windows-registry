# Active Setup
Active Setup allows us to execute commands once per user after successful sign-in to the computer.

## Registry key locations
#### Machine
* <b>HKEY_LOCAL_MACHINE</b>\SOFTWARE\Microsoft\Active Setup\\<b>Installed Components</b>
* <b>HKEY_LOCAL_MACHINE</b>\SOFTWARE\WOW6432Node\Microsoft\Active Setup\\<b>Installed Components</b>
#### Current user
* <b>HKEY_CURRENT_USER</b>\SOFTWARE\Microsoft\Active Setup\\<b>Installed Components</b>
* <b>HKEY_CURRENT_USER</b>\Software\Wow6432Node\Microsoft\Active Setup\\<b>Installed Components</b>

## Active Setup flow
```mermaid
flowchart TD
    a["User sign-in to the computer"] --> b["Computer compares Active Setup registry keys that are in HKLM <br />to keys that are under HKCU"] --> c["Computer runs values in StubPath for keys that are in HKLM and dont have a copy in HKCU"] --> w["Computer waits for the processes from Active Setup to finish"] --> g["Computer creates a copy of the key under HKCU"] --> d["Computer loads explorer.exe"]
```

## Running cmd commands from Active Setup
```powershell
REG ADD "HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\RunCMD" /v StubPath /t REG_SZ /d "cmd /c echo Running from HKLM\Active Setup && whoami && pause"
```

```powershell
REG ADD "HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\RunCMD" /v Version /t REG_SZ /d "1,1,1,1"
```

## Running cmd commands from Active Setup and RunOnce registry

```mermaid
flowchart TD
    a["User sign-in to the computer"] --> b["Computer compares Active Setup registry keys that are in HKLM <br />to keys that are under HKCU"] --> c["Computer runs values in StubPath for keys that are in HKLM and dont have a copy in HKCU"] --> w["Computer waits for the processes from Active Setup to finish"] --> g["Computer creates a copy of the key under HKCU"] --> d["Computer loads explorer.exe"] --> e["Computer runs entries in Run and RunOnce keys"]
```

```powershell
ni "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\RunCMDFromRunOnce" | New-ItemProperty -Name "StubPath" -Value 'REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v RunCMD /t REG_SZ /d "cmd /c echo Running from HKCU\RunOnce && whoami && pause"'
```

## Installing Brave with Active Setup and Run Once
Download link: [Brave](https://github.com/brave/brave-browser) <br />

```powershell
ni "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\InstallBraveFromRunOnce" | New-ItemProperty -Name "StubPath" -Value 'REG ADD "HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce" /v InstallBrave /t REG_SZ /d "cmd /c echo installing software.. && cmd /c C:\BraveBrowserStandaloneSilentSetup.exe"'
```