# ADB_Commands
# Introduction
### Android Debug Bridge is command line utility to communicate with the Android device that is connected either via USB or Wi-Fi, or with an emulator(Android virtual device) running on the development machine.


# Generic ADB Commands
### Below is list of adb commands used widely while working with Android platform.

#### List devices with name, serial number
	adb devices –l

#### Clear logcat
	adb logcat –c

#### Send a command to a specific device when multiple devices are connected
	adb -s <serial_number_of_device> <command>

#### Collect logcat continuously and save to a file  (-v time, logs the time. -b all, logs all buffers). It should be stopped explicitly.
	adb logcat –v time –b all > my-logcat.txt


#### Dump existing logs into a file. It stops automatically.
	adb logcat –v time –b all –d > dump-logcat.txt

#### Collect bugreport
##### Older versions of adb, only .txt is saved
	adb bugreport > bugreport.txt
##### newer versions of adb, all files put into a zip
	adb bugreport

#### Change logcat buffer size to maximum <em>16MB</em>
	adb logcat -b all -G 16777216

#### List applications installed in the device
	adb shell pm list packages

#### List third party apps only
	adb shell pm list packages -3

#### List system apps only
	adb shell pm list packages -s

#### List enabled packages only
	adb shell pm list packages -e

#### List disabled packages only
	adb shell pm list packages -d

#### Disable an application, in eng builds only
	adb shell pm disable <package_name>

#### Enable an application, in eng builds only
	adb shell pm enable <package_name>

#### Get build type
	adb shell getprop ro.build.type

#### Get build display id
	adb shell getprop ro.build.display.id

#### Get build fingerprint
	adb shell getprop ro.build.fingerprint

#### Press any key on device
	adb shell input keyevent <KEYCODE>
	Keycodes are
		adb shell input keyevent  KEYCODE_MENU
		adb shell input keyevent  KEYCODE_HOME
		adb shell input keyevent  KEYCODE_BACK
##### [All keycodes can be found here](https://developer.android.com/reference/android/view/KeyEvent#constants_2)

#### Push file to the device
	adb push <path_to_src_file_in_pc> <path_to_dest_file_in_device>

#### Pull a file from the device
	adb pull <path_to_src_file_in_device> <path_to_dest_file_in_pc>

#### Reboot the device
	adb reboot

#### Reboot into bootloader
	adb reboot bootloader

#### Reboot into recovery
	adb reboot recovery

#### Take a screenshot
	adb shell screencap /sdcard/my_snap.png

	Image will be stored in sdcard, it needs to be pulled into the PC by using adb pull command

#### Record screen
	adb screenrecord /sdcard/my_video.mp4

	Records for a maximum(default) 3 minutes

#### Enter text on the focussed edit text
	adb shell input text <mytext>

	//Spaces are not allowed in text

#### Install an app
	adb install <path_to_apk_in_pc>

#### Re-install an app . If the app is already installed , it will be uninstalled before installing again
	adb install –r <path_to_apk_in_pc>

#### Install an app in external storage
	adb install –s <path_to_apk_in_pc>

#### Uninstall an app
	adb uninstall <package_name_of_the_application>

#### Get android version
	adb shell getprop ro.build.version.sdk

#### Force stop an application
	adb shell am force-stop <package_name_of_the_application>

#### Remount system partition as read write, engineering build only
	adb remount

#### Get selinux state
	adb shell getenforce

#### Set selinux state, engineering build only
	adb shell setenforce 1

#### Remove selinux enforcement, engineering build only
	adb shell setenforce 0

<details><summary>Connect ADB over WiFi</summary>
<p>

##### When device is connected over WiFi, all adb commands can be sent over WiFi.

```
1. Connect device and PC to the same network
2. Connect device over USB cable and Enable USB Debugging in device
3. Once detected over USB, run
	adb tcpip 5555
	// this restarts adb in device
4. Disconnect USB cable now, and run
	adb connect <device_ip_address>:5555
	//this restarts adb to communicate over WiFi with input IP address
5. To disconnect adb from WiFi mode run
	adb disconnect <device_ip_address>:5555
```

</p>
</details>

<br/>
<details><summary>Start an actiivty from adb</summary>
<p>

##### We can start any activity from adb commands either explicitly by mentioning the name of the package and name of the class, or implicitly by just the name of intent action.

```
Implicit intent to launch settings application
	adb shell am start -a android.settings.SETTINGS
Launch Bluetooth settings
	adb shell am start -a android.settings.BLUETOOTH_SETTINGS
```
```
Explicit intent to launch settings app using name of the package and activity class. You must know the name of activity class to launch it via adb
	adb shell am start -n com.android.settings/.Settings
```
```
Pass extras for the intent via adb to start an activity.
1. Open google.com by sending an adb command
	adb shell am start -a android.intent.action.VIEW -t text/html -d http://www.google.com
	// Here android.intent.action.VIEW is standard intent action, -t text/html is the mimetype of the data sent with intent, -d <url> is the data to be used by the intent.

2. Open an image in Photos application
	adb shell am start -a android.intent.action.VIEW -t image/* -d /sdcard/abc.png
	// ensure you have abc.png in /sdcard/

3. Open camera application to capture an image
	adb shell am start -a android.media.action.IMAGE_CAPTURE
```
Intent actions for all settings can be [found here](https://developer.android.com/reference/android/provider/Settings#constants_2)


</details>

#### Enable data saver mode
	adb shell cmd netpolicy set restrict-background true

#### Disable data saver mode
	adb shell cmd netpolicy set restrict-background false

#### Add an app to data saver mode whitelist
	adb shell cmd netpolicy add restrict-background-whitelist <package_name>

#### Remove an app from data saver mode whitelist
	adb shell cmd netpolicy add restrict-background-whitelist <package_name>

#### List all WiFi networks
	adb shell cmd netpolicy list wifi-networks

#### Make a non-metered WiFI newtork into a metered one
	adb shell cmd netpolicy set metered-network <WIFI_SSID> true

#### Simulate unplug battery event
	adb shell dumpsys battery unplug

#### Reset battery unplug
	adb shell dumpsys battery reset

#### Send app to stand by state
	adb shell dumpsys battery unplug
	adb shell am set-inactive <package_name> true

#### Remove app from stand by state
	adb shell am set-inactive <package_name> false
