## Convert To Debuggable

```
apktool d -s UnCrackable-Level2.apk -o decoded 
```

d - decode
-s means ==do not decode resources== (we don’t need them. All we need is a manifest);
-o – output directory.

Now, repack with `-d` option, that will automatically add `debuggable = "true"` to the `AndroidManifest.xml`:

```
apktool b decoded -d -o Uncrackable-Level1-repackaged.apk
```

where `b` stands for `build`.
Option `-d` is very useful, as one would have to alter `AndroidManifest.xml` manually to add `app:debuggable=true` attribute to `<application>` tag.

## Sign the app

The app needs to be signed, otherwise the installation of the unsigned app will fail. Use `apksigner` to check whether the app will pass the verification process during installation:

```
apksigner verify --print-certs --verbose Uncrackable-Level1-repackaged.apk
```

To sign the app, first create a keystore:

```
keytool -genkey -v -keystore <keystore-file>.keystore -alias <key-alias> -keyalg RSA -keysize 2048 -validity 10000

```

Now, Sign with apksigner:

```
apksigner sign --ks apk1.keystore --ks-key-alias apk1-key-alias Uncrackable-1-rebuild.apk
```

## Decompile the app – see the source code

First, convert `.apk` to `.jar`:

```
dex2jar -f UnCrackable-Level2.apk
```

Open Java Decompiler GUI tool:

```
java -jar jd-gui.jar
```

## Route the APK Traffic to Debugger

Run the app in “wait for debugger” mode:

```
adb shell am start -D -n "owasp.mstg.uncrackable1/sg.vantagepoint.uncrackable1.MainActivity"
```

where `am` is an `ActivityManager`;

`start` starts a component;

`-D` enables debugging;

-n: don't read from stdin

```
adb forward tcp:4321 jdwp:PID
```

tcp - LOCAL; jdwp - REMOTE (Emulator)

`jdwp:PID` stand for “use process id of the app and a `JDWP` as a transport protocol”.

Find `PID` by running:

```
adb shell ps | grep mstg
```

In order to ==suspend the execution of the app ==upon debugger connecting to it, pipe down `suspend` command to the `jdb`:

```
(echo suspend && cat) | jdb -connect com.sun.jdi.SocketAttach:hostname=localhost,port=4321
```

## Basic Debugging Commands

```
stop in android.app.Dialog.setCancelable
```

It sets a breakpoint in android.app.Dialog.setCancelable function and let's you change local variables in between.

```
resume
```

Resumes the execution of the app.

```
locals
```

Check the local variables in the app at that point of execution.The address of the entered password string and the address of the calculated password string is passed to _strncmp_ as two paramterers