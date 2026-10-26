## Build

### Sync

```bash
repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs --no-clone-bundle
mkdir -p .repo/local_manifests
curl -L https://raw.githubusercontent.com/cfernande1408/local_manifests_macan/lineage-24.0/macan.xml \
  -o .repo/local_manifests/macan.xml
repo sync -c -j8 --force-sync --no-tags --no-clone-bundle
```

### Blobs

Get the full OxygenOS OTA zip for CPH2769, version 16.0.10.600 (EX01), and
extract only the `macan` blobs (the common ones come from TheMuppets):

```bash
sudo apt install erofs-utils
cd device/oneplus/macan
./extract-files.py /path/to/CPH2769_16.0.10.600_EX01.zip --only-target
cd -
```

### Pending changes

```bash
source build/envsetup.sh
repopick -t icnss2-dms-mac
```

### Compile

```bash
source build/envsetup.sh
source vendor/lineage/vars/aosp_target_release
lunch lineage_macan-${aosp_target_release}-userdebug
m bacon target-files-package otatools
```
