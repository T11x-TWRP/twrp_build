# TWRP build repository for Samsung Galaxy Tab 3 Lite 7.0 (Marvell PXA986 Edition)

## `WORK IN PROGRESS. WILL EAT YOUR CAT.`

## Prerequisites

- Oracle JDK 7 *(installation steps can be found [here](#installing-oracle-jdk-7))*
- Android build tools *(installation steps can be found [here](https://source.android.com/setup/build/initializing?hl=en#installing-required-packages-ubuntu-1804))*

## Syncing TWRP sources

```bash
mkdir ~/TWRP
cd ~/TWRP

mkdir ~/.bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
python3 ~/.bin/repo init --depth=1 -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-4.4-deprecated
git clone --branch twrp-4.4 --single-branch https://github.com/T11x-TWRP/android_platform_manifest.git .repo/local_manifests
python3 ~/.bin/repo sync -c --force-sync --optimized-fetch --no-tags --no-clone-bun --prune -j$(nproc --all)
```

## Downloading Oracle JDK 7

```bash
mkdir ~/.jdk_7
cd ~/.jdk_7
wget https://repo.huaweicloud.com/java/jdk/7u80-b15/jdk-7u80-linux-i586.tar.gz
tar -xzf jdk-7u80-linux-i586.tar.gz
```

## Building TWRP
```bash
export PATH="$HOME/.jdk_7/jdk1.7.0_80/bin:$PATH"
export JAVA_HOME="$HOME/.jdk_7/jdk1.7.0_80"
cd ~/TWRP
source build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch omni_goya-eng
mka recoveryimage
```
