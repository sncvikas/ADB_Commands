# ADB_Commands
# Introduction
### Android Debug Bridge is command line utility to communicate with the Android device that is connected either via USB or Wi-Fi, or with an emulator(Android virtual device) running on the development machine.


# Generic ADB Commands
### Below is list of most widely used ADB commands while working with Android platform.

#### List devices with name, serial number<br/>
	adb devices –l

#### Clear logcat<br/>
	adb logcat –c

#### Collect logcat continuously and save to a file  (-v time, logs time. -b all, logs all buffers). It should be stopped explicitly.<br>
	adb logcat –v time –b all > my-logcat.txt


#### Dump existing logs into a file. It should be stopped explicitly.<br/>
	adb logcat –v time –b all –d > dump-logcat.txtx

#### Collect bugreport<br/>
##### Older versions of adb, only .txt is saved
	adb bugreport > bugreport.txt <br>
##### newer versions of adb, all files put into a zip
	adb bugreport

#### Change logcat buffer size to maximum <em>16MB</em><br/>
	adb logcat -b all -G 16777216

#### List applications installed in the device<br/>
	adb shell pm list packages

#### List third party apps only<br/>
	adb shell pm list packages -3

#### List system apps only<br/>
	adb shell pm list packages -s

#### List enabled packages only<br/>
	adb shell pm list packages -e


#### List disabled packages only<br/>
	adb shell pm list packages -d

#### Disable an application, in eng buildsn only<br/>
	adb shell pm disable <package_name>

#### Enable an application, in eng buildsn only<br/>
	adb shell pm enable <package_name>

#### Get build type<br/>
	adb shell getprop ro.build.type

#### Get build display id<br/>
	adb shell getprop ro.build.display.id

#### Get build fingerprint<br/>
	adb shell getprop ro.build.fingerprint

#### Press any key on device<br/>
	adb shell input keyevent <KEYCODE>
	Keycodes are
		adb shell input keyevent  KEYCODE_MENU
		adb shell input keyevent  KEYCODE_HOME
		adb shell input keyevent  KEYCODE_BACK
	All keycodes can be found here https://developer.android.com/reference/android/view/KeyEvent#constants_2

#### Push file to the device <br/>
	adb push <path_to_src_file_in_pc> <path_to_dest_file_in_device>

#### Pull a file from the device<br/>
	adb pull <path_to_src_file_in_device> <path_to_dest_file_in_pc>

#### Reboot the device<br/>
	adb reboot

#### Reboot into bootloader<br/>
	adb reboot bootloader

#### Reboot into recovery<br/>
	adb reboot recovery

#### Take a screenshot<br/>
	adb shell screencap /sdcard/my_snap.png

	Image will be stored in sdcard, it needs to be pulled into the PC by using adb pull command

#### Record screen<br/>
	adb screenrecord /sdcard/my_video.mp4

	Records for a maximum(default) 3 minutes

#### Enter text on the focussed edit text<br/>
	adb shell input text <mytext>

	Spaces are not allowed in text

#### Install an app <br/>
	adb install <path_to_apk_in_pc>

#### Re-install an app . If the app is already installed , it will uninstalled before installing again)<br/>
	adb install –r <path_to_apk_in_pc>

#### Install an app in external storage<br/>
	adb install –s <path_to_apk_in_pc>

#### Uninstall an app<br/>
	adb uninstall <package_name_of_the_application>

#### Get android version<br/>
	adb shell getprop ro.build.version.sdk

#### Force stop an application<br/>
	adb shell am force-stop <package_name_of_the_application>

#### Remount system partition as read write, ENG build only<br/>
	adb remount

#### Get selinux state<br/>
	adb shell getenforce

#### Set selinux state, ENG build only<br/>
	adb shell setenforce 1

#### Remove selinux enforcement, ENG build only<br/>
	adb shell setenforce 0
