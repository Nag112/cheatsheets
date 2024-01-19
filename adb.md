---
title: adb (Android Debug Bridge)
category: CLI
layout: 2017/sheet
weight: -1
authors:
  - github: ZackNeyland
updated: 2018-03-06
---

### Device Basics

| Command                           | Description                                 |
| ---                               | ---                                         |
| `adb devices`                     | Lists connected devices                     |
| `adb devices -l`                  | Lists connected devices and kind            |
| `adb root`                        | Restarts adbd with root permissions         |
| `adb start-server`                | Starts the adb server                       |
| `adb kill-server`                 | Kills the adb server                        |
| `adb remount`                     | Remounts file system with read/write access |
| `adb reboot`                      | Reboots the device                          |
| `adb reboot bootloader`           | Reboots the device into fastboot            |
| `adb disable-verity`              | Reboots the device into fastboot            |

`wait-for-device` can be specified after `adb` to ensure that the command will run once the device is connected.

`-s` can be used to send the commands to a specific device when multiple are connected.

#### Examples

```
$ adb wait-for-device devices
 List of devices attached
 somedevice-1234 device
 someotherdevice-1234 device
```

```
$ adb -s somedevice-1234 root
```

### Logcat

| Command                              | Description                            |
| ---                                  | ---                                    |
| `adb logcat`                         | Starts printing log messages to stdout |
| `adb logcat -g`                      | Displays current log buffer sizes      |
| `adb logcat -G <size>`               | Sets the buffer size (K or M)          |
| `adb logcat -c`                      | Clears the log buffers                 |
| `adb logcat *:V`                     | Enables ALL log messages (verbose)     |
| `adb logcat -f <filename>`           | Dumps to specified file                |

#### Examples
```
$ adb logcat -G 16M
$ adb logcat *:V > output.log
```

### File Management

| Command                              | Description                       |
| ---                                  | ---                               |
| `adb push <local> <remote>` | Copies the local to the device at remote   |
| `adb pull <remote> <local>` | Copies the remote from the device to local |

#### Examples

```
$ echo "This is a test" > test.txt
$ adb push  test.txt /sdcard/test.txt
$ adb pull /sdcard/test.txt pulledTest.txt
```

### Remote Shell

| Command                                | Description                                                           |
| ---                                    | ---                                                                   |
| `adb shell [command]`                  | Runs the specified command on device (most unix commands work here), interactive shell if no command given   |
| `adb shell wm size`                    | Displays the current screen resolution                                |
| `adb shell wm size WxH`                | Sets the resolution to WxH                                            |
| `adb shell pm list packages`           | Lists all installed packages                                          |
| `adb shell pm list packages -3`        | Lists all installed 3rd-party packages                                |
| `adb shell pm uninstall --user 0 <package>`        | Removes a package for primary user                                |
| `adb shell monkey -p app.package.name` | Starts the specified package                                          |

# Removing Bloatware/Unwanted Apps from Android using ADB

If you want to clean up your Android device by removing bloatware or unwanted apps, you can use the Android Debug Bridge (ADB) with the following commands:

## Steps to remove bloatware

1. ### `List devices`

> This command checks for connected Android devices via ADB.
```shell
adb devices
```

2. ### `Start shell session`

> This command opens a shell session on your connected Android device.

```bash
adb shell
```

3. ### `List packages`

> This command lists all installed system apps on your Android device.

```bash
pm list packages -s
```

4. ### `Remove package`

> This command uninstalls a specific package (app) from the device.

```bash
pm uninstall --user 0 <package_name>
```

**Usage:** Replace `<package_name>` with the package name of the app you want to remove. The `--user 0` flag indicates that you want to uninstall it for the primary user.


### Example

To remove a system app named "ExampleApp," you would execute:

```bash
pm uninstall --user 0 com.example.exampleapp
```