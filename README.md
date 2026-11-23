# open-boot-programs

A curated list of programs that deal with booting: how long boots take, what starts at boot or
sign-in, what changed or is waiting for the next restart, and boot media and boot managers.

Sorted into **works on both**, **Windows** and **Linux**. Each entry says what kind of program it
is: GUI, CLI, library, or built in (comes with the system).

## Contents

- [Works on both](#works-on-both)
- [Windows](#windows)
- [Linux](#linux)

---

## Works on both

### Boot times and uptime

- [osquery](https://osquery.io): CLI. Query the system with SQL. The `uptime` and `startup_items`
  tables cover boot time and what starts at boot. Windows, Linux and macOS.
- [systeminformation](https://systeminformation.io): library (npm). System and OS information for
  Node.js; `si.time()` includes uptime.
- [os-uptime](https://www.npmjs.com/package/os-uptime): library (npm). Gives the moment the OS
  booted as a `Date`.

### Choosing what starts at boot or sign-in

- [auto-launch](https://www.npmjs.com/package/auto-launch): library (npm). Makes a Node app or any
  program launch at login on Windows, macOS and Linux.
- [pm2](https://pm2.keymetrics.io/docs/usage/startup/): CLI (npm). Process manager; `pm2 startup`
  brings your Node apps back after a reboot (systemd and others on Linux; see
  [pm2-windows-startup](#windows) for Windows).
- [node-windows](https://github.com/coreybutler/node-windows) /
  [node-linux](https://github.com/coreybutler/node-linux) /
  [node-mac](https://github.com/coreybutler/node-mac): libraries (npm). Install a Node script as a
  service that starts at boot, with the same style of API on each system.

### Boot media

- [Ventoy](https://www.ventoy.net): GUI and CLI, open source. Copy ISO files onto a USB stick and
  pick which one to boot from a menu; the stick still works for normal files. Runs on Windows and
  Linux.
- [balenaEtcher](https://etcher.balena.io): GUI, open source. Writes one image to a USB stick or
  SD card. Windows, macOS and Linux.

---

## Windows

### Boot times and history

- [boot-times](https://github.com/buggypather/boot-times): CLI (npm and PowerShell Gallery). Your last boots with total, until
  desktop and desktop settling times, plus what slowed them down, from the boot record Windows
  already keeps.
- [BootPerformanceView](https://www.nirsoft.net/utils/boot_performance_view.html): GUI, free
  (NirSoft). Reads the same boot record and shows every stage (kernel, drivers, devices, user
  profile and more). Can save to CSV from the command line.
- [BootRacer](https://www.greatis.com/bootracer/): GUI, free for personal use. Times each boot without counting
  the time you spend typing your password, warns when boots get slower, and shows which startup
  programs cost the most.
- [TurnedOnTimesView](https://www.nirsoft.net/utils/computer_turned_on_times.html): GUI, free
  (NirSoft). When the PC was turned on and off, and why it shut down, from the event logs.
- [Windows Performance Recorder and Analyzer](https://learn.microsoft.com/windows-hardware/test/wpt/recording-onoff-transitions):
  GUI and CLI, free (Microsoft). Records a full trace of a boot (`On/Off - Boot`, or
  `wpr -addboot`) and lets you dig through it second by second. For deep troubleshooting.
- [Dargslan.WinBootAnalyzer](https://www.powershellgallery.com/packages/Dargslan.WinBootAnalyzer/):
  PowerShell module. One command that mixes boot events, startup programs and tips. New and small.

### Choosing what starts at boot or sign-in

- [Autoruns](https://learn.microsoft.com/sysinternals/downloads/autoruns): GUI and CLI
  (`autorunsc`), free (Microsoft Sysinternals). The most complete list of everything that starts
  automatically: startup folder, Run keys, services, drivers, scheduled tasks, Explorer add-ons and
  more. Untick an entry to turn it off.
- [WhatInStartup](https://www.nirsoft.net/utils/what_run_in_startup.html): GUI, free (NirSoft).
  Lists startup programs and can disable them "permanently", turning one off again if it adds
  itself back.
- [Startup Delayer](https://www.r2.com.au/page/products/download/startup-delayer/): GUI, free with
  a paid upgrade. Starts sign-in programs one after another with delays instead of all at once.
  Last updated in 2015.
- [start-on-windows-boot](https://github.com/marklagendijk/node-start-on-windows-boot): library
  (npm). Turns starting a program at Windows boot on or off.
- [pm2-windows-startup](https://github.com/marklagendijk/node-pm2-windows-startup): CLI (npm).
  Brings pm2 and its apps back after a Windows restart.
- Task Manager → Startup apps: built in. Turn sign-in programs on or off and see Windows' "startup
  impact" estimate for each.

### What changed, or what's waiting for the next restart

- [since-last-boot](https://www.npmjs.com/package/since-last-boot): PowerShell toolset (npm). HTML
  report of system and file changes since the last boot. Aimed at headless Windows machines you
  reach over SSH.
- [PendingReboot](https://www.powershellgallery.com/packages/PendingReboot): PowerShell module.
  `Test-PendingReboot` says whether Windows is waiting for a restart, and why with `-Detailed`.
- [PendMoves](https://learn.microsoft.com/sysinternals/downloads/pendmoves): CLI, free (Microsoft
  Sysinternals). Lists the file renames and deletes Windows will carry out at the next boot.
- [Process Monitor](https://learn.microsoft.com/sysinternals/downloads/procmon): GUI, free
  (Microsoft Sysinternals). Its boot logging records every file, registry and process event from
  early in the next boot.

### Boot media

- [Rufus](https://rufus.ie): GUI, open source. Makes bootable USB sticks from ISO files, with
  BIOS and UEFI options. Windows only.

---

## Linux

### Boot times and history

- [systemd-analyze](https://www.freedesktop.org/software/systemd/man/latest/systemd-analyze.html):
  CLI, built in on systemd systems. `systemd-analyze` splits the last boot into firmware, loader,
  kernel, initrd and userspace. `blame` lists services by start-up time, `critical-chain` shows
  what actually held the boot up, and `plot > boot.svg` draws a chart.
- `journalctl --list-boots` and `last reboot`: built in. A list of past boots, and the log for
  any one of them (`journalctl -b -1` is the previous boot).
- [systemd-bootchart](https://github.com/systemd/systemd-bootchart): CLI. Records CPU, disk,
  memory and per-process activity during boot and draws it as an SVG.
- [bootchart2](https://github.com/xrmx/bootchart): CLI. The older boot charting tool, for
  systems not using systemd-bootchart.
- [tuptime](https://github.com/rfmoz/tuptime): CLI. Like `uptime`, but it keeps history between
  restarts: number of boots, good and bad shutdowns, and uptime and downtime for each boot.
- [uptimed](https://github.com/rpodgorny/uptimed): daemon and CLI (`uprecords`). Keeps a table of
  your longest uptimes.

### Choosing what starts at boot or sign-in

- [systemd user services](https://wiki.archlinux.org/title/Systemd/User): built in. Run your own
  programs at sign-in with `systemctl --user enable`.
- [XDG autostart](https://wiki.archlinux.org/title/XDG_Autostart): built in on most desktops.
  `.desktop` files in `~/.config/autostart` start at sign-in; desktops show them under "Startup
  Applications".
- [dex](https://github.com/jceb/dex): CLI. Runs XDG autostart entries for window managers that
  don't do it themselves, and `dex -ad` previews what would start.
- [Stacer](https://github.com/oguzhaninan/Stacer): GUI, open source. System optimizer with a
  Startup Apps tab to turn sign-in programs on, off or add new ones, and a Services tab.
  Development has been on and off.

### What changed, or what's waiting for the next restart

- [needrestart](https://github.com/liske/needrestart): CLI (Debian, Ubuntu and others). After
  updates, lists services still running old libraries and whether a newer kernel is waiting for a
  reboot.
- [needs-restarting](https://dnf-plugins-core.readthedocs.io/en/latest/needs_restarting.html): CLI
  (Fedora, RHEL and others via dnf). `needs-restarting -r` says whether a reboot is needed, with an
  exit code to match.
- `/var/run/reboot-required`: built in on Debian and Ubuntu. Exists when an update wants a
  reboot; `/var/run/reboot-required.pkgs` names the packages.

### Boot managers and UEFI

- [efibootmgr](https://github.com/rhboot/efibootmgr): CLI. List, add, remove and reorder UEFI boot
  entries, or pick the one to use on the next boot only (`--bootnext`).
- [rEFInd](https://www.rodsbooks.com/refind/): boot manager, open source. A graphical UEFI menu
  that finds your installed systems and kernels on its own.

---

## Contributing

Suggestions are welcome: open an issue or a pull request. Please add one line per program, in the
section where it fits, saying what kind of program it is and what it does in plain words.

## License

[CC0 1.0](LICENSE): this list is in the public domain.
