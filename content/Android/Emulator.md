# Starting an emulator

1. Install Android studio.
2. open virtual device manager in more actions.
3. Install a new device with OS not latest and not oldest.
4. Use RootAVD to install Magisk.
5. It will root the device too.
6. Install Burp certificate.
7. Add Alwaystrustusercert.zip in magisk module.
8. add proxy in emulator network.
9. Now try to intercept the request using burp.
10. If not, install frida. frida version and frida server version should be same.
11. put frida-server in /data/local/tmp and run.
12. you can hook frida scripts using frida-tools (pip install frida-tools)

Reference: https://youtu.be/QzsNn3GhYYk?si=8oJoicIq21IRq-hz

## To install and run a rooted AVD in android studio

https://infosecwriteups.com/get-yourself-a-rooted-android-virtual-device-avd-fb443d590dfa

## To root a AVD 

https://proandroiddev.com/root-an-android-emulator-avd-9f912328ca08

## [Using Magisc](https://book.hacktricks.wiki/en/mobile-pentesting/android-app-pentesting/install-burp-certificate.html#using-magisc)

If you **rooted your device with Magisc** (maybe an emulator), and you **can't follow** the previous **steps** to install the Burp cert because the **filesystem is read-only** and you cannot remount it writable, there is another way.
