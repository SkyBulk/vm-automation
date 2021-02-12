# Content
* [VirtualBox VM automation in Python](#about)
* [Downloads](#downloads)
* [Host configuration](#host-configuration)
* [Guest configuration](#guest-configuration)
* [Usage](#usage)
* [TODO](#todo)
* [Example videos](#example-videos)
* [Useful links](#useful-links)
* [Donations](#donations)

# About
Python script that can be used to automate dynamic testing of binaries/scripts/documents on VMs (currently only VirtualBox is supported).
Based on VBoxManage command-line interface and does not require VirtualBox SDK.

Both Windows and Linux are tested as host OS. May work on other platforms, supported by VirtualBox and Python.

# Downloads
Latest stable version and Windows binaries are available in <a href="https://github.com/Pernat1y/vm-automation/releases" target="_blank">Releases</a>.

# Host configuration
* Both Windows and Linux are tested as host OS. May work on other platforms, supported by VirtualBox and Python.
* You need VirtualBox (the newer the better). Proprietary Oracle VM VirtualBox Extension Pack is *not* required.
* It is recommended to have folder with 'vboxmanage' binary in the environment variables.
* You need a recent version of Python (3.7+).

# Guest configuration
* You must have Windows as the guest OS with auto login configured (or have a snapshot with a user logged in).
* You must have VirtualBox guest additions installed.
* It is strongly recommended to have live snapshots to restore to (otherwise it will be *much* slower).
* VM disk encryption is *not* supported.

# Usage:
Essential commands:
```
python demo_cli.py \
    file.exe \
    --vms windows10 windows8 windows7 \
    --snapshots firefox chrome ie
```
or 
```
python demo_cli.py \
    file.exe \
    --config config.json
```

All options (AKA --help):
```
Required options:
  file                  Path to file
  --vms [VMS [VMS ...]], -v [VMS [VMS ...]]
                        Space-separated list of VMs to use
  --snapshots [SNAPSHOTS [SNAPSHOTS ...]], -s [SNAPSHOTS [SNAPSHOTS ...]]
                        Space-separated list of snapshots to use

Main options:
  --vboxmanage [VBOXMANAGE]
                        Path to vboxmanage binary (default: vboxmanage)
  --check_version       Check for latest VirtualBox version online (default: False)
  --timeout [TIMEOUT]   Timeout in seconds for both commands and VM (default: 60)
  --delay [DELAY]       Delay in seconds before/after starting VMs (default: 7)
  --threads [{0,1,2,3,4,5,6,7,8}]
                        Number of concurrent threads to run (0=number of VMs, default: 2)
  --verbosity [{debug,info,error,off}]
                        Log verbosity level (default: info)
  --debug               Print all messages. Alias for "--verbosity debug" (default: False)
  --log [LOG]           Path to log file (default: None) (console)
  --report              Generate html report (default: False)
  --record              Record guest' OS screen (default: False)
  --pcap                Enable recording of VM's traffic (default: False)
  --memdump             Dump memory VM (default: False)
  --no_time_sync        Disable host-guest time sync for VM (default: False)

Guests options:
  --ui [{1,0,gui,headless}]
                        Start VMs in GUI or headless mode (default: gui)
  --login [LOGIN], --user [LOGIN]
                        Login for guest OS (default: user)
  --password [PASSWORD]
                        Password for guest OS (default: 12345678)
  --remote_folder [{desktop,downloads,documents,temp}]
                        Destination folder in guest OS to place file (default: desktop)
  --uac_parent [UAC_PARENT]
                        Path for parent app, which will start main file (default: C:\Windows\Explorer.exe)
  --network [{on,off}]  State of network adapter of guest OS (default: None)
  --resolution [RESOLUTION]
                        Screen resolution for guest OS. Can be set to "random" (default: None)
  --mac [MAC]           Set MAC address for guest OS. Can be set to "random" (default: None)
  --get_file [GET_FILE]
                        Get specific file from guest OS before stopping VM (default: None)
  --pre [PRE]           Script to run before main file (default: None)
  --post [POST]         Script to run after main file (default: None)
```

# TODO
* Small improvements.
* Code optimization and fixes.
* Better tests coverage.

# Example videos
* Windows host (version 0.9.2):

<a href="http://www.youtube.com/watch?feature=player_embedded&v=t6AWew06rxo" target="_blank"><img src="http://img.youtube.com/vi/t6AWew06rxo/0.jpg" width="320" height="240" border="10" /></a>

* Linux host (version 0.7.3):

<a href="http://www.youtube.com/watch?feature=player_embedded&v=QnXfmPVbmlo" target="_blank"><img src="http://img.youtube.com/vi/QnXfmPVbmlo/0.jpg" width="320" height="240" border="10" /></a>

# Useful links
<a href="https://github.com/hfiref0x/VBoxHardenedLoader" target="_blank">VirtualBox Hardened VM detection mitigation loader - VBoxHardenedLoader</a>

# Changelog
Version 0.11:
* Added support for configuration files. Usage: '--config config.json'.
  See 'config-example.json' for example. 
  If 'config.json' file is present, all options, except file name, are optional.
* Added '--group' option. All VMs from this group will be used for analysis.
  Can be used in place of '--vms' argument.
* Added '--file_args' option to pass arguments to the main file/executable.
* '--uac_parent' option renamed to '--open_with' as it may be used with any type of files, not only the executables.
* Added colors to command line output. Enable with '--colors'.
* Updated tests

For complete changelog see <a href="CHANGELOG.md" target="_blank">CHANGELOG.md</a>

# Donations
You can support further development with a donation (Thanks!).

Bitcoin: bc1q9jfne8r64k8gudu6layjfsqasd7507mnv6d4fr

Bitcoin (legacy): 1JeFmnk9PMjazXk6pL6mbhDJ3JheXgMXhp

Monero: 48md2A642KBhge7MN8AWBngsUK6btRcV3B7zJmPzPmn6a4nAKjPWZHf8cPEQ5R9t4QcKUSonaPd79eJkJTb2QXLxMtiJQyG
