# Changelog
All notable changes to this project will be documented in this file.
This project adheres to [Semantic Versioning](http://semver.org/).


## [0.5.0 / 5.45.0] - 2020-12-01

### Added
- added new notification window
- added user interactive control mechanism when using the new SandMan UI
-- when a file exeeds the copy limit instead of failing, the user is prompted if the file should be copied or not
-- when internet access is blocked it now can be exempted in real time by the user
- added missing file recovery and auto/quick recovery functionality
- added silent MSG_1399 boxed process start notification to keep track of short lived boxed processes
- added ability to prvent system wide process starts, sandboxie can now instead of just alerting also block processed on the alert list
-- set "StartRunAlertDenied=y" to enable prcess blocking
- the process start alert/block mechanism can now also handle folders use "AlertFolder=..." 
- added ability to merge snapshots
- added icons to the sandbox context menu in the new UI
- added more advanced options to the sandbox options window
- added file migration progress indicator
- added more run commands and custom run commands per sandbox
-- the the box settings users can now speficy programs to be available from the box run menu
-- also processes can be pinned to that list from the presets menu
- added more windows 10 specific template presets
- added ability to create desktop shortcuts to sandboxed items
- added icons to box option tabs
- added box grouping
- added new debug option "DebugTrace=y" to log debug output to the trace log

### Changed
- File migration limit can now be disabled by specifying "CopyLimitKb=-1"
- improved and refactored mesage logging mechanism, reducing memory usage by factor of 2
- terminated boxed processes are now kept listed for a coupel of seconds
- reworked sandbox dletion mechaism ofthe new UI
- restructured sandbox options window
- SbieDLL.dll can now be compiled with an up to date nitll.lib

### Fixed
- fixed issues migrating files > 4GB
- fixed a issue that would allow a maliciosue application to bypass the internet blockade
- fixed issue when logging messages from a non sandboxed process, added process_id parameter to API_LOG_MESSAGE_ARGS
- fixed issues with localization
- fixed issue using file recovery in legacy ui SbieCtrl.exe when "SeparateUserFolders=n" is set
- when a program is blocked from starting due to restrictions no redundant messages are issues anymore
- fixed UI not properly displaying async errors
- fixed issues when a snapshot operation failed
- fixed some special cases of IpcPath and WinClass in the new UI
- fixed driver issues with WHQL passing compatybility testing



## [0.4.5 / 5.44.1] - 2020-11-16

### Added
- added "Terminate all processes" and "disable forced programs" commands to tray menu in SandMan ui
- program start restrictions settings now can be switsched between a white list and a black list
-- programs can be terminated and blacklisted from the context menu
- added additional process context menu options, lingering and leader process can be now set from menu
- added option to view template presets for any given box
- added text filter to template view
- added new compatybility templates:
-- Windows 10 core UI component: OpenIpcPath=\BaseNamedObjects\[CoreUI]-* solving issues with Chinese Input and Emojis
-- FireFox Quantum, access to windows FontCachePort for compatybility with windows 7
- added experimental debug option "OriginalToken=y" which lets sandboxed processes retain their original unrestricted token
-- This option is comparable with "OpenToken=y" and is intended only for testing and debugging, it BREAKS most SECURITY guarantees (!)
- added debug option "NoSandboxieDesktop=y" it disables the desktop proxy mechanism
-- Note: without an unrestricted token with this option applications wont be able to start
- added debug option "NoSysCallHooks=y" it disables the sys call processing by the driver
-- Note: without an unrestricted token with this option applications wont be able to start
- added ability to record verbost access tracess to the resource monitor
-- use ini options "FileTrace=*", "PipeTrace=*", "KeyTrace=*", "IpcTrace=*", "GuiTrace=*" to record all events
-- replace "*" to log only: "A" - allowed, "D" - denided, or "I" - ignore events
- added ability to record debug output strings to the resource monitor,
-- use ini option DebugTrace=y to enable

### Changed
- AppUserModelID sting no longer contains sandboxie version string
- now by default sbie's application manifest hack is disabled, as it causes problems with version checking on windows 10
-- to enable old behavioure add "PreferExternalManifest=y" to the global or the box specific ini section
- the resource log mechanism can now handle multiple strings to reduce on string copy operations

### Fixed
- fixed issue with disabling some restriction settings failed
- fixed disabling of internet block from the presets menu sometimes failed
- the software compatybility list in the sandman UI now shows the proper template names
- fixed use of freed memory in the driver
- replaced swprintf with snwprintf to prevent potential buffer overflow in SbieDll.dll
- fixed bad list performance with resource log and api log in SandMan UI



## [0.4.4 / 5.44.0] - 2020-11-03

### Added
- added SbieLdr (experimental)

### Changed
- moved code injection mechanism from SbieSvc to SbieDll
- moved function hooking mechanism from SbieDrv to SbieDll
- introduced a new driverless method to resolve wow64 ntdll base address

### removed
- removed support for windows vista x64



## [0.4.3 / 5.43.7] - 2020-11-03

### Added
- added disable forced programs menu command to the sandman ui

### Fixed
- fixed file rename bug introduced with an earlier driver verifier fix
- fixed issue saving access lists
- fixed issue with program groups parsing in the SandMan UI 
- fixed issue with intrnet access restriction options
- fixed issue deleting sandbox when located on a drive directly



## [0.4.2 / 5.43.6] - 2020-10-10

### Added
- added explore box content menu option

### Fixed
- fixed thread handle leak in SbieSvc and other components
- msedge.exe is now categorized as a chromium derivate
- fixed chrome 86+ compatybility bug with chroms own sandbox



## [0.4.1 / 5.43.5] - 2020-09-12

### Added
- added core version compatybility check to sandman UI
- added shell integration options to SbiePlus

### Changed
- SbieCtrl does not longer auto show the tutorian on first start
- when hooking, the to the trampoline migrated section of the original function is not longer noped out
-- it caused issues with unity games, will be investigated and re enabled later

### Fixed
- fixed color issue with vertical tabs in dark mode
- fixed wrong path separators when adding new forced folders
- fixed directroy listing bug intriduced in 5.43
- fixed issues with settings window when not being connected to driver
- fixed issue when starting sandman ui as admin
- fixed auto content delete not working with sandman ui



## [0.4.0 / 5.43] - 2020-09-05

### Added
- added a proper custom installer to the the Plus release
- added sandbox snapshot functionality to sbie core
-- filesystem is saved incrementally, the snapshots built upon each other
-- each snapshot gets a full copy of the box registry for now
-- each snapshot can have multiple children snapshots
- added access status to resource monitor
- added setting to change border width
- added snapshot manager UI to SandMan
- added template to enable authentication with an Yubikey or comparable 2FA device
- added ui for program allert
- added software compatybility options to teh UI

### Changed
- SandMan UI now handles deletion of sandboxe content on its own
- no longer adding redundnat resource accesses as new events

### Fixed
- fixed issues when hooking functions from delay loaded libraries
- fixed issues when hooking an already hooked function 
- fixed issues with the new box settings editor

### Removed
- removes deprecated workaround in the hooking mechanism for an obsolete antimalware product



## [0.3.5 / 5.42.1] - 2020-07-19

### Added
- Added settings window
- added translationsupport
- added dark theme
- added auto start option
- added sandbox options
- added debug option "NoAddProcessToJob=y"

### Changed
- improved empty sandbox tray icon
- improved message parsing
- updated homepage links

### Fixed
- fixed ini issue with sandman.exe when renaming sandboxes
- fixed ini auto reload bug introduced in the last build
- fixed issue when hooking delayd loaded libraries



## [0.3 / 5.42] - 2020-07-04

### Added
- API_QUERY_PROCESS_INFO can be now used to get the original process token of sandboxed processes
-- Note: this capability is used by TaskExplorer to allow inspecting sandbox internal tokens
- Added option "KeepTokenIntegrity=y" to make the sbie token keep its initial integrity level (debug option)
-- Note: Do NOT USE Debug Options if you dont know their security implications (!) 
- Added process id to log messages very usefull for debugging
- Added finder to resource log
- Added option to hide host processes "HideHostProcess=[name]"
-- Note: Sbie hides by default processes from other boxes, this behavioure can now be controlled with "HideOtherBoxes=n"
- Sandboxed RpcSs and DcomLaunch can now be run as system with the option "ProtectRpcSs=y" howeever tht breaks sandboxed explorer and other
- BuiltIn Clsid whitelist can now be disabled with "OpenDefaultClsid=n"
- Processes can be now terminated with the del key, and require a confirmation
- Added sandboxed window border display to SandMan.exe
- Added notification for sbie log messages
- Added Sandbox Presets sub menu allowing to quickly change some settings
-- Enable/Disable API logging, logapi_dll's are now distributed with SbiePlus 
-- And other: Drop admin rights; Block/Allow internet access; Block/Allow access to files on te network
- Added more info to the sandbox status column
- Added path column to SbieModel
- Added info tooltips in SbieView

### Changed
- Reworked ApiLog, added pid and pid filter
- Auto config reload on in change is now delayed by 500ms to not reload multiple times on incremental changes
- Sandbox names now replace "_" witn " " for display allowing to use names that are build of separated words

### Fixed
- added mising PreferExternalManifest itialization to portable mode
- fixed permission issues with sandboxed system processes
-- Note: you can use "ExposeBoxedSystem=y" for the old behaviour (debug option)
- fixed missing SCM access check for sandboxed services
-- Note: to disable the access check use "UnrestrictedSCM=y" (debug option)
- fixed missing initialization in serviceserver that caused sandboxed programs to crash when querying service status
- fixed many bugs that caused the SbieDrv.sys to BSOD when run with MSFT Driver Verifier active
-- 0xF6 in GetThreadTokenOwnerPid and File_Api_Rename
-- missing non optional parameter for FltGetFileNameInformation in File_PreOperation
-- 0xE3 in Key_StoreValue and Key_PreDataInject



## [0.2.2 / 5.41.2] - 2020-06-19

### Added
- added option SeparateUserFolders=n to no longer have the user profile files stored separately in the sandbox
- added SandboxieLogon=y it makes processes run under the SID of the "Sandboxie" user instead of the Anonymous user
-- Note: the global option AllowSandboxieLogon=y must be enabled, the "Sandboxie" user account must be manually created first and the driver reloaded, else process start will fail
- improved debugging around process creation errors in the driver

### Fixed
- fixed some log messages going lost after driver reload
- found a workable fix for the MSI installer issue, see Proc_CreateProcessInternalW_RS5



## [0.2.1 / 5.41.1] - 2020-06-18

### Added
- added different sandbox icons for different types
-- Red LogAPI/BSA enabled
-- More to come :D
- Added progress window for async operations that take time
- added DPI awareness
- the driver file is now obfuscated to avoid false positives
- additional debug options to sandboxie.ini OpenToken=y that combines UnrestrictedToken=y and UnfilteredToken=y
-- Note: using these options weekens the sandboxing, they are intended for debugging and may be used for better application virtualization later

### Changed
- SbieDll.dll when processinh InjectDll now looks in the SbieHome folder for the Dll's if the entered path starts with a backslash
-- i.e. "InjectDll=\LogAPI\i386\logapi32v.dll" or "InjectDll64=\LogAPI\amd64\logapi64v.dll"

### Fixed
- IniWatcher did not work in portable mode
- service path fix broke other services, now properly fixed, may be
- found workaround for the msi installer issue



## [0.2 / 5.41.0] - 2020-06-08

### Added
- IniWatcher, no more clicking reload, the ini is now reloaded automatically every time it changes
- Added Mainanance menu to the Sandbox menu, allowing to install/uninstall and start/stop sandboxie driver, service
- SandMan.exe now is packed with Sbie files and when no sbie is installed acts as a portable instalation
- Added option to clean up logs

### Changed
- sbie driver now first checks the home path for the sbie ini before checking SystemRoot

### Fixed
- Fixed a resource leak when running sandboxed
- Fixed issue boxed services not starting when the path contained a space
- NtQueryInformationProcess now returns the proper sandboxed path for sandboxed processes



## [0.1 / 5.40.2] - 2020-06-01

### Added
- Created a new Qt based UI names SandMan (Sandboxie Manager)
- Resource monitor now shows the PID
- Added basic API call log using updated BSA LogApiDll


### Changed
- reworked resource monitor to work with multiple event consumers
- reworked log to work with multiple event consumers



## [5.40.1] - 2020-04-10

### Added
- "Other" type for the Resource Access Monitor
-- added call to StartService to the logged Resources

### Fixed
- fixed "Windows Installer Service could not be accessed" that got introduced with Windows 1903

