# TWRP Device configuration for Motorola Moto Z3 Play

## Device specifications

Basic   | Spec Sheet
-------:|:-------------------------
CPU     | Octa-core 1.8 GHz Kryo 260
CHIPSET | Qualcomm SDM636 Snapdragon 636
GPU     | Adreno 509
Memory  | 4GB
Shipped Android Version | 8.1 (Oreo)
Storage | 64GB
Battery | 3000 mAh
Dimensions | 156.5 x 76.5 x 6.75 mm
Display | 1080 x 2160 pixels, 6.0" Super AMOLED
Rear Camera  | 12 MP (f/1.7) + 5 MP (f/2.2), (PDAF, dual pixel)
Front Camera | 8 MP (f/2.2)

![Device Picture](https://i-cdn.phonearena.com//images/phones/72220-xlarge/Motorola-Moto-Z3-Play-8.jpg)

### Kernel Source
https://github.com/moto-SDM660/android_kernel_motorola_sdm660/tree/twrp-11

## Compile

First repo init the twrp-11 tree (and necessary qcom dependencies):

```
mkdir ~/android/twrp-11
cd ~/android/twrp-11
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-11
mkdir -p .repo/local_manifests
curl https://raw.githubusercontent.com/TeamWin/buildtree_manifests/master/min-aosp-11/qcom.xml > .repo/local_manifests/qcom.xml
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="osm0sis/twrp_abtemplate" path="bootable/recovery/installer" remote="github" revision="master"/>
  <project name="android_device_motorola_beckham" path="device/motorola/beckham" remote="TeamWin" revision="android-11"/>
</manifest>
```

Now you can sync your source:

```
repo sync
```

To automatically make the TWRP installer zip, you need to import this commit in the build/make path: https://gerrit.twrp.me/c/android_build/+/4964

Finally execute these:

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch twrp_beckham-eng
make adbd bootimage

```
### Copyright
 ```
  /*
  *  Copyright (C) 2013-17 The OmniROM Project
  *  Copyright 2022 - The TeamWin Recovery Project
  *
  * This program is free software: you can redistribute it and/or modify
  * it under the terms of the GNU General Public License as published by
  * the Free Software Foundation, either version 3 of the License, or
  * (at your option) any later version.
  *
  * This program is distributed in the hope that it will be useful,
  * but WITHOUT ANY WARRANTY; without even the implied warranty of
  * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  * GNU General Public License for more details.
  *
  * You should have received a copy of the GNU General Public License
  * along with this program.  If not, see <http://www.gnu.org/licenses/>.
  *
  */
  ```
