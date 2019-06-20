# ADB_Commands
# Introduction
### Android Debug Bridge is command line utility to communicate with the Android device that is connected either via USB or Wi-Fi, or with an emulator(Android virtual device) running on the development machine.


# Generic ADB Commands
### Below is list of adb commands used widely while working with Android platform.

#### List devices with name, serial number
	adb devices –l

#### Clear logcat
	adb logcat –c

#### Collect logcat continuously and save to a file  (-v time, logs the time. -b all, logs all buffers). It should be stopped explicitly.
	adb logcat –v time –b all > my-logcat.txt


#### Dump existing logs into a file. It stops automatically.
	adb logcat –v time –b all –d > dump-logcat.txtx

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
##### All keycodes can be found here https://developer.android.com/reference/android/view/KeyEvent#constants_2

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

#### Re-install an app . If the app is already installed , it will uninstalled before installing again
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
