# TWRP build repository for Samsung Galaxy Tab 3 Lite 7.0

## `WORK IN PROGRESS. WILL EAT YOUR CAT.`

## Disclaimer

These are steps for Ubuntu 20.04 and Ubuntu 18.04.

## Prerequisites

- Oracle JDK 7 *(installation steps can be found [here](#downloading-oracle-jdk-7))*
- Android build tools *(installation steps can be found [here](https://source.android.com/setup/build/initializing?hl=en#installing-required-packages-ubuntu-1804))*

## Syncing TWRP sources

```bash
mkdir ~/TWRP
cd ~/TWRP

mkdir ~/.bin
curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
python3 ~/.bin/repo init --depth=1 -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-5.1
git clone --branch twrp-5.1 --single-branch https://github.com/T11x-TWRP/twrp_device_samsung_goya.git ~/TWRP/device/samsung/goya
python3 ~/.bin/repo sync -c --force-sync --optimized-fetch --no-tags --no-clone-bun --prune -j$(nproc --all)
```

## Downloading Oracle JDK 7

```bash
mkdir ~/.jdk_7
cd ~/.jdk_7
wget https://download.java.net/openjdk/jdk7u75/ri/openjdk-7u75-b13-linux-x64-18_dec_2014.tar.gz
tar -xzf openjdk-7u75-b13-linux-x64-18_dec_2014.tar.gz
```

## Building TWRP
```bash
OLDPATH=$PATH
OLDJAVAHOME=$JAVA_HOME
export PATH="$HOME/.jdk_7/java-se-7u75-ri/bin:$PATH"
export JAVA_HOME="$HOME/.jdk_7/java-se-7u75-ri"
cd ~/TWRP
source build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch omni_goya-eng
mka recoveryimage
export PATH=$OLDPATH
export JAVA_HOME=$OLDJAVAHOME
```
