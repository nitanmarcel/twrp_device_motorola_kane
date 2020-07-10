# Device Tree for Motorola One Action/One Vision (kane) Fixed Android 9

The Motorola One Action/One Vision (codenamed _"troika/kane"_) is a flagship smartphone from motorola.

## Compile

First download omni-9.0 tree:

```
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-9.0
```
Then add these string to .repo/manifests/remove.xml


Then add these projects to .repo/local_manifests/roomservice.xml (If you don't have it, you can add them to .repo/manifest.xml): 

```xml
<project name="nitanmarcel/twrp_device_motorola_kane" path="device/motorola/kane" remote="github" revision="android-9.0-stricted" />
```

Now you can sync your source:

```
repo sync
```

To automatically make the twrp installer, you need to import this commit in the build/make path: https://gerrit.omnirom.org/#/c/android_build/+/33182/

Finally execute these:

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch omni_kane-eng 
mka adbd recoveryimage 
```

To test it:

```
fastboot boot out/target/product/kane/recovery.img
```

Kernel Source: https://github.com/nitanmarcel/android_kernel_motorola_exynos9610
## Credits
Thanks to @dianlujitao for the base multidevice commit: https://github.com/TeamWin/android_device_motorola_motorola3/tree/android-9.0/init
