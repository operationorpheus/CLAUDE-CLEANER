---
name:Claude Cleaner
description:An easy tool for cleaning up files and bloat from your bots., temp files, cached data, or unnecessary software from a Windows or Linux system
allowed-tools: Bash

# System Cleanup — Pre-Sale / Debloat

Run these in order. Skipping steps is fine depending on OS and use case.

## Linux

```bash
sudo apt autoremove -y && sudo apt autopurge -y

sudo apt clean && sudo apt autoclean

sudo rm -rf /tmp/* /var/tmp/*

sudo journalctl --vacuum-time=1allowed-tools: Bash
d
sudo rm -rf /var/log/*.gz /var/log/*.old

history -c && rm -f ~/.bash_history ~/.zsh_history

rm -rf ~/.cache/thumbnails/*

rm -rf ~/.cache/*

sudo rm -rf /var/lib/snapd/cache/*

sudo dd if=/dev/zero of=/zerofile bs=1M; sudo rm -f /zerofile
```

## Windows (run in elevated PowerShell)

```powershell
# Clear temp files
Remove-Item -Recurse -Force $env:TEMP\*
Remove-Item -Recurse -Force C:\Windows\Temp\*

# Disk cleanup (automated)
cleanmgr /sagerun:1

Stop-Service wuauserv
Remove-Item -Recurse -Force C:\Windows\SoftwareDistribution\Download\*
Start-Service wuauserv

Remove-Item -Recurse -Force C:\Windows\Prefetch\*

Remove-Item -Recurse -Force "$env:LOCALAPPDATA\Google\Chrome\User Data\Default\Cache\*"


Remove-Item -Recurse -Force C:\Users\USERNAME\Documents\*
Remove-Item -Recurse -Force C:\Users\USERNAME\Downloads\*
Remove-Item -Recurse -Force C:\Users\USERNAME\Desktop\*

sfc /scannow


C:\Windows\System32\Sysprep\sysprep.exe /oobe /generalize /shutdown
```

## Notes

- Run sysprep LAST — it shuts down and generalizes the install. Do everything else first.
- On Linux, zeroing free space is optional but good if you're selling an SSD and want clean compression.
- Always verify nothing important is left before running the user profile wipes.
```
