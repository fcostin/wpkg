# WPKG package recipes

A lot of it is inspired by (and copied from) the [WPKG
wiki](http://wpkg.org) so much gratitude is owed.

The following criteria must be fulfilled before the recipe is included
here:

- 32-bit and 64-bit safe
- Uses "msiexec /x package_file.msi" for uninstallations whenever
  possible to avoid knowing CLSIDs that change

## Requirements

- WPKG 1.3 as it supports nested variables and chained commands

## Branches

All development takes place in 'master'. This isn't great and should
change.

## Notes

### Regular expressions

WPKG supports regular expressions however various parts do it
differently.

- <host> use + for matching multiple characters
- <check> use * for matching multiple characters

### Versions

- If there are multiple references to the current version (file name,
  uninstall check, etc), then it should be included as a variable
  named 'version'
- All revisions should be written out WITH dots. Examples:
 - 4.65
 - 9.2.0.61
- All revision should have an additional identifier. This allows
  overriding the central version. Examples:
 - 4.65-0
 - 9.2.0.61-3
- The additional revision identifier should be incremented when needed
  and reset to 0 when a new version is added
- Priorities are set as follows
 - 10 - most normal applications
 - 50 - system applications (IE8 and others)
 - 100 - critical install first apps (Windows Installer 4.5)
- Rebooting - all should have their reboot priority set to "false" and
  only reboot (postponed) in case of 3010 or similar return codes and
  ONLY if absolutely needed
- Ensure that the following variables are defined in your WPKG
  settings.xml file
 - *NOTE* more will be added for other installers such as
   InstallShield, InnoSetup, etc
 - MSI - set to "/quiet /norestart" (without quotes)
 - MSP - set to "REINSTALL=ALL REINSTALLMODE=omus" (without quotes)
 - SOFTWARE - set to root of the application store without trailing
   backslash
 - WPKG - set to root of server WPKG installation without trailing
   backslash
