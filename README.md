# How to build AOSP Marshmallow for Nexus 5  including its kernel
it describes how to build marshmallow mr2 for the Nexus 5  including kernel-3.4 and provides few patches.

## Find right version
setting up a right version of Android is the key to successful build the android source.

I chose m_mr2 for my Nexus 5 with no paticular reason :) and `MOB31E` seems right choice which I can see rigth version information as follows on google groups:

**Android version**
Build  Branch  Version Supported devices
MOB31E, **android-6.0.1_r66**, Nexus 5, Nexus 6, Nexus 9 (volantisg)

**Kernel version**
**android-6.0.1_r0.124** kernel/msm **android-msm-hammerhead-3.4-marshmallow-mr2** Nexus 5 (hammerhead)

## Setup sources

### android m-mr2
Firstly sync the m_mr2 branch `marshmallow-mr2-release`
```
repo init -u https://android.googlesource.com/platform/manifest -b marshmallow-mr2-release
repo sync -j8
```
and checkout MOB31E, I used `reset`.
```
repo start m_mr2 --all
repo forall -c 'pwd;git reset --hard android-6.0.1_r66
```

### kernel
sync and checkout the branch for Nexus5
```  
git clone https://android.googlesource.com/kernel/msm kernel-3.4
cd kernel-3.4
git fetch origin android-msm-hammerhead-3.4-marshmallow-mr2
git checkout -b android-msm-hammerhead-3.4-marshmallow-mr2 origin/android-msm-hammerhead-3.4-marshmallow-mr2
```
and finally reset the commits
```
git reset --hard android-6.0.1_r0.124
```

### patching files
I've attached 3 patches as follows:
- `build.diff` for build/
- `device_lge_hammerhead.diff` for /device/lge/hammerhead
- `kernel.diff` for kernel-3.4/
apply them at its directories.

### vendor driver files
- download all vendor driver files for M`OB31E` from google at
https://developers.google.com/android/drivers#hammerheadmob31e
- and unzip and execute them, now you have the all patches under `vendor`
- finally copy `vendor` to android
```
cp -r vendor <your android root>/vendor
```

### missing libraries(optional)
  TBD

## Build
Now you are ready to build, I know you know how to build :)

## Flashing
TBD
