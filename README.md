# Yocto scarthgap manifest

This is Linux manifest for raspberry pi Yocto development.

#### Build environment setup

First, we need to install the host packages. these packages.

```bash
sudo apt-get update && sudo apt-get install -y gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint3 xterm python3-subunit mesa-common-dev zstd liblz4-tool
```
It will install all the host packages.

***Note: These host dependence packages are for scarthgap version and also test on ubuntu-18.04 & 20.04 LTS distro.***

Once the environment setup done. we need to do repo init by using the below cmd.

#### Install repo tool
```bash
mkdir -p ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

```bash
echo 'export PATH=${HOME}/bin:${PATH}' >> ${HOME}/.profile
```

Note: Add the above cmd in profile file so the repo tool will be available always on PATH environment

#### Sync source
```bash
repo init -u https://github.com/spikynavin/linux-manifest -b main -m raspberry-platform-sys-mainline.xml --repo-url=https://github.com/GerritCodeReview/git-repo  --repo-branch=stable --no-repo-verify
```
```bash
repo sync -c --no-tags
```
Once source synced try the below cmd.

#### Yocto build for raspberrypi
```bash
cd workspace
source build.sh -f
bitbake core-image-minimal
bitbake core-image-minimal -c populate_sdk
```
Once the build done. check the image in
```bash
ls workspace/build-sdk/tmp/deploy/image/
ls workspace/build-sdk/tmp/deploy/sdk/
```
There we can find the image and sdk.
