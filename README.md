## Build

### Sync

```bash
repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs --no-clone-bundle
mkdir -p .repo/local_manifests
curl -L https://raw.githubusercontent.com/Weijcc/manifests_macanc/lineage-24.0/macanc.xml \
  -o .repo/local_manifests/macanc.xml
repo sync -c -j8 --force-sync --no-tags --no-clone-bundle
```

### Blobs

Get the full OTA zip for PLR110, version 16.0.10.500 (CN01), and
extract only the `macanc` blobs (the common ones come from TheMuppets):

```bash
sudo apt install erofs-utils
cd device/oneplus/macanc
./extract-files.py /path/to/PLR110_16.0.10.500_CN01.zip --only-target
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
lunch lineage_macanc-${aosp_target_release}-userdebug
m bacon target-files-package otatools
```
