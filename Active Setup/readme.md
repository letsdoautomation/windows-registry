#### Paths to registry
```
# Machine
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Active Setup\Installed Components

# Current user
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Active Setup\Installed Components
HKEY_CURRENT_USER\Software\Wow6432Node\Microsoft\Active Setup\Installed Components
```

#### Message command
```powershell
cmd /c echo Running from active setup && whoami && pause
```

#### Download Brave
Download link: [Brave](https://github.com/brave/brave-browser) <br />

```powershell
C:\install\BraveBrowserStandaloneSetup.exe /silent /install
```

