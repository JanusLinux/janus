### Installing build dependencies
We need specific packages to build this Linux distribution. Without them you can't perform the required tasks. To install required build dependencies:
#### Debian or Ubuntu (and derivatives):
```
apt-get install build-essential m4 bison flex texinfo python3 python perl libtool autoconf automake autopoint gperf libarchive-tools xorriso curl git mtools pigz zstd rsync pcregrep pkg-config liblzma-dev libgmp-dev libmpfr-dev libmpc-dev libelf-dev libssl-dev zlib1g-dev libarchive-dev libzstd-dev libfreetype6-dev libpopt-dev libacl1-dev libcap-dev libmagic-dev libdb-dev libreadline-dev libffi-dev libsqlite3-dev
```
#### Fedora
```
dnf groupinstall "Development Tools" "C Development Tools and Libraries"
dnf install gcc gcc-g++ libstdc++-static glibc-static mtools libisoburn python3 pigz libarchive curl bsdtar xorriso autoconf automake libtool which pcre-tools freetype-devel zlib-devel xz-devel libzstd-devel libarchive-devel elfutils-libelf-devel openssl-devel libdb-devel popt-devel file file-devel libacl-devel libcap-devel gettext-devel gcc-plugin-devel gmp-devel mpfr-devel libmpc-devel readline-devel libffi-devel sqlite-devel
```
#### Arch Linux (and derivatives):
```
pacman -S base-devel xorriso mtools git pigz python rsync freetype2
```
#### Ataraxia Linux:
```
neko emerge libisoburn python mtools freetype isomd5sum
```

### Compiling package manager
Ataraxia Linux uses `neko` as its package manager. You should do this commands to install pkgutils (**AS ROOT**):
```
cd /tmp
git clone https://github.com/ataraxialinux/neko.git --depth 1
cd neko
autoreconf -vif
./configure
make
make install
```

### Building
Arguments supported by "build script":
```
stage		- Select stage for build
image		- Build image to deploy to hard drive or sdcard
installer	- Build installer image
archive		- Build stage archive
```
Sub-arguments supported by "build script":
```
 -a <Architecture>		- Select architecture for build
 -j <number of core>		- Specify number of cores/threads for build
 -g <Options for gcc>		- Specify options for GCC
 -l <Linux kernel package>	- Specify your custom Linux kernel package
 -d <desktop environment>       - Specify your desktop environment (gnome, sway, xfce, mate, budgie)
```
We have seperated the build process into seperate "stages":
```
 * meta-toolchain         - This stage intended to compile cross-toolchain
 * core-image-minimal     - This stage intended to compile basic target system with cross-compiler (You don't need to compile stage 0)
```
To begin the bootstrap process, **as root**:
See [supported platforms and architecures.](platforms.md)
```
./build stage -a [supported architecture] [stage name]
```
After bootstrap you can build target images
```
./build [image|installer|live|archive] -a [supported architecture]
```
And magic happens!
