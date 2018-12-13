ADB Commands
============

A non-comprehensive list of generally useful `adb` commands. This document is continuously evolving and PRs are welcome! Standard Unix-like system argument conventions are followed where square brackets **[]** indicate optional arguments and angled brackets **<>** indicate a required argument.

Files
-----

- **Copy files to device**

  `adb push <source file> <destination directory>`

- **Copy files from device**
  
  `adb pull <device file> <local file path>`


Input
-----

- **Key events**

  `adb shell input keyevent [--longpress] <keycode>`
  
  Popular `<keycode>`s are:
  - `3`     Home button
  - `4`     Back button
  - `24`    Volume up
  - `25`    Volume down
  - `26`    Toggle screen on/off
  - `220`   Brightness down
  - `221`   Brightness up

Display
-------

- **Get Screen Resolution**

  `adb shell wm size`
  
- **Get Screen density**

  `adb shell wm density`
  
- **Emulate Screen Size and Density**

  `adb shell wm size <dimens>` for example `adb shell wm size 640x480`
  
  `adb shell wm density <density>` for example `adb shell wm density 288`
  
  When you are done emulating a certain screen, reset to the original settings:
  
  `adb shell wm size reset`
  
  `adb shell wm density reset`

Properties
----------

- **Get properties**

  `adb shell getprop [property]`
  
  Property name is optional if you want all properties. Popular `[property]` values:
  - `ro.build.version.release` release version of OS
  - `ro.product.cpu.abi` cpu architecture, for example arm64-v8a
  - `ro.product.cpu.abilist` all supported cpu architectures

Package Manager
---------------

- **List installed packages**

  `adb shell pm list packages [query]`

- **Grant Permissions**

  `adb shell pm grant <your.package.name> <permission>`
  
- **Revoke Permissions**

  `adb shell pm revoke <your.package.name> <permission>`
  
- **To clear Application data & Cache**
  `adb shell pm clear <your.package.name>`


Profiling
---------------------

- **Frame profiling**

  `adb shell setprop debug.hwui.profile <value>`
  
  Possible `<value>`s are:
  - `true` to enable profiling
  - `visual_bars` to enable profiling and visualize the results on screen as bars
  - `visual_lines` to enable profiling and visualize the results on screen as lines
  - `false` to disable profiling

- **Overdraw**

  `adb shell setprop debug.hwui.overdraw <value>`
  
  Possible `<value>`s are:
  - `show` to display overdraw areas on screen
  - `count` to display an overdraw counter
  - `false` to disable overdraw debugging
  
- **Graphics Rendering Performance**
  
  `adb shell dumpsys gfxinfo [your.package.name]`
  
- **Heap Dump**

  `adb shell am dumpheap <your.package.name> /sdcard/dumpheap.hprof`
  
- **Layout Borders**

  `adb shell setprop debug.layout <true/false>`
  
  You have to relaunch your application to see the borders. 
  
Miscellaneous
-------------

- **Kill Application**

  `adb shell am kill <your.package.name>`
  
  Simulates the application being killed for memory pressure. Only works if the application is placed into the background first by pressing the home button.

- **Immersive Mode**
  
  `adb shell settings put global policy_control immersive.full=[value]`
  
  Possible `[value]`s are:
  - `*` to enable immersive mode
  - leave blank to disable immersive mode
