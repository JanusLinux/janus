### Installing build dependencies
We need specific packages to build this Linux distribution. Without them you can't perform the required tasks. To install required build dependencies:
#### Fedora
```
dnf groupinstall "Development Tools" "C Development Tools and Libraries"
dnf install clang libcxx-devel glibc-static libcxx-static libunwind-devel jq zstd bsdcpio bsdtar curl mtools libisoburn which python3 texinfo meson freetype-devel zlib-devel xz-devel libzstd-devel libarchive-devel elfutils-libelf-devel openssl-devel readline-devel libffi-devel sqlite-devel
```
### Debian/Ubuntu:
```
apt install build-essential clang lld libunwind-dev libc++-dev jq zstd libarchive-tools curl mtools xorriso python3 meson libfreetype-dev zlib1g-dev liblzma-dev libzstd-dev libarchive-dev libelf-dev libssl-dev libreadline-dev libffi-dev libsqlite-dev
```
#### Ataraxia GNU/Linux:
```
tsukuri emerge libisoburn mtools freetype
```

### Compiling package manager
Ataraxia GNU/Linux uses `tsukuri` as its package manager. You should do this commands to install `tsukuri` (**AS ROOT**):
```
cd /tmp
git clone https://github.com/ataraxialinux/tsukuri.git --depth 1
cd tsukuri
mkdir build
cd build
meson --prefix=/usr -Dsystemd=false ..
ninja
ninja install
```

### Building
Arguments supported by "build script":
```
target		- Select target for build
```
Sub-arguments supported by "build script":
```
 -a <Architecture>		- Select architecture for build
 -k <Kernel>			- Select kernel for target OS
 -b <Board>			- Build OS for specific board
```
We have seperated the build process into seperate "targets":
```
 * toolchain              - This stage intended to compile cross-toolchain
 * system                 - This stage intended to compile basic target system with cross-compiler (You don't need to compile stage 0)
 * image                  - This stage intended to generate virtual disk image
 * installer              - This stage intended to generate installer .iso image
 * live                   - This stage intended to generate live .iso image
 * stage                  - This stage intended to generate archive with pre-compiled OS
```
To begin the bootstrap process, **as root**:
See [supported platforms and architecures.](platforms.md)
```
./build target -a [supported architecture] -k [kernel] -b [supported board] [target name]
```
And magic happens!
