# ADB_Commands
# Introduction
### Android Debug Bridge is command line utility to communicate with the Android device that is connected either via USB or Wi-Fi, or with an emulator(Android virtual device) running on the development machine.


# Generic ADB Commands
### Below is list of most widely used ADB commands when while working with Android platform.

List devices with name, serial number<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb devices –l`

Clear logcat<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb logcat –c`

Collect logcat continuously and save to a file  (-v time, logs time. -b all, logs all buffers)<br>  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb logcat –v time –b all > my-logcat.txt`	It should be stopped explicitly.


Dump existing logs into a file<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb logcat –v time –b all –d > dump-logcat.txt`	Stops after existing logs are dumped

Collect bugreport<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb bugreport > bugreport.txt` (older versions of adb, only .txt is saved) <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb bugreport` (newer versions of adb, all files put into a zip)

Change logcat buffer size to maximum <em>16MB</em><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb logcat -b all -G 16777216`

List applications installed in the device<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell pm list packages`

List third party apps only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell pm list packages -3`

List system apps only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell pm list packages -s`

List enabled packages only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell pm list packages -e`


List disabled packages only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell pm list packages -d`

Disable an application, in eng buildsn only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell pm disable <package_name>`

Enable an application, in eng buildsn only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell pm enable <package_name>`

Get build type<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell getprop ro.build.type`

Get build display id<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell getprop ro.build.display.id`

Get build fingerprint<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell getprop ro.build.fingerprint`

Press any key on device<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell input keyevent <KEYCODE>`<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Keycodes are<br/>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell input keyevent  KEYCODE_MENU`<br/>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell input keyevent  KEYCODE_HOME`<br/>
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell input keyevent  KEYCODE_BACK`<br/>

Push file to the device <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb push <path_to_src_file_in_pc> <path_to_dest_file_in_device>`

Pull a file from the device<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb pull <path_to_src_file_in_device> <path_to_dest_file_in_pc>`

Reboot the device<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb reboot`

Reboot into bootloader<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb reboot bootloader`

Reboot into recovery<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb reboot recovery`

Take a screenshot<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell screencap /sdcard/my_snap.png`	Image will be stored in sdcard, it needs to be pulled into the PC by using `adb pull` command

Record screen<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb screenrecord /sdcard/my_video.mp4`	Records for a maximum(default) 3 minutes

Enter text on the focussed edit text<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell input text <mytext>`	<em>Spaces are not allowed in text</em>

Install an app <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb install <path_to_apk_in_pc>`

Re-install an app . If the app is already installed , it will uninstalled before installing again)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb install –r <path_to_apk_in_pc>`

Install an app in external storage<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb install –s <path_to_apk_in_pc>`

Uninstall an app<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb uninstall <package_name_of_the_application>`

Get android version<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell getprop ro.build.version.sdk`

Force stop an application<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell am force-stop <package_name_of_the_application>`

Remount system partition as read write, ENG build only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb remount`

Get selinux state<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell getenforce`

Set selinux state, ENG build only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell setenforce 1`

Remove selinux enforcement, ENG build only<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`adb shell setenforce 0`
