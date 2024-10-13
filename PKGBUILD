# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer:  Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer:  Truocolo <truocolo@aol.com>
# Maintainer:  Christian Hesse <mail@eworm.de>
# Maintainer:  Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Ronald van Haren <ronald.archlinux.org>
# Contributor: Keshav Amburay <(the ddoott ridikulus ddoott rat) (aatt) (gemmaeiil) (ddoott) (ccoomm)>

_os="$( \
  uname \
    -o)"
## "1" to enable IA32-EFI build in Arch x86_64
#"0" to disable
_IA32_EFI_IN_ARCH_X64="1"

## "1" to enable EMU build, "0" to disable
_GRUB_EMU_BUILD="0"

if [[ "${CARCH}" == 'x86_64' ]]; then
  _EFI_ARCH='x86_64'
  _GRUB_EMU_BUILD="1"
fi
[[ "${CARCH}" == 'i686' ]] && \
  _EFI_ARCH='i386'
[[ "${CARCH}" == 'arm' ]] && \
  _EFI_ARCH='arm'
  # _EFI_ARCH='arm-linux-androideabi'
  # _EFI_ARCH='arm-linux-gnueabihf'
[[ "${CARCH}" == 'x86_64' ]] && \
  _EMU_ARCH='x86_64'
[[ "${CARCH}" == 'i686' ]] && \
  _EMU_ARCH='i386'
[[ "${CARCH}" == 'arm' ]] && \
  _EMU_ARCH='arm-linux-gnueabihf'

_offline="false"
_git="true"
if [[ "${_os}" == "Android" ]]; then
  _git="false"
fi
pkgname='grub'
pkgdesc='GNU GRand Unified Bootloader (2)'
epoch=2
_commit='03e6ea18f6f834f177cad017279bedbb0a3de594' # git rev-parse grub-${_pkgver}
_gnulib_commit="22711ba820cf78dd8f8eea04f6073fcec7ab987b"
_pkgver=2.12
_unifont_ver='15.1.04'
pkgver=${_pkgver/-/}
pkgrel=1
url="https://www.gnu.org/software/${pkgname}"
arch=(
  'x86_64'
  'arm'
  'armv7h'
  'aarch64'
  'i686'
  'powerpc'
)
license=(
  'GPL-3.0-or-later'
)
backup=(
  "etc/default/${pkgname}"
  'etc/grub.d/40_custom'
)
install="${pkgname}.install"
options=(
  '!makeflags'
)
conflicts=(
  'grub-common'
  'grub-bios'
  "grub-efi-${_EFI_ARCH}"
  'grub-legacy'
)
replaces=(
  "grub-common"
  'grub-bios'
  "grub-efi-${_EFI_ARCH}"
)
provides=(
  "grub-common=${pkgver}"
  "grub-bios=${pkgver}"
  "grub-efi-${_EFI_ARCH}"
)
[[ "${_GRUB_EMU_BUILD}" == "1" ]] && \
  conflicts+=(
    'grub-emu'
  ) && \
  provides+=(
    'grub-emu'
  ) && \
  replaces+=(
    'grub-emu'
  )
makedepends=(
  'autogen'
  'device-mapper'
  'gettext'
  'git'
  'help2man'
  'freetype2'
  'fuse3'
  'python'
  'rsync'
  'texinfo'
  'ttf-dejavu'
  'xz'
)
[[ "${CARCH}" == 'arm' ]] && \
  makedepends+=(
    clang
  )
depends=(
  'device-mapper'
  'gettext'
  'sh'
  'xz'
)
optdepends=(
  'freetype2: For grub-mkfont usage'
  'fuse3: For grub-mount usage'
  'dosfstools: For grub-mkrescue FAT FS and EFI support'
  'lzop: For grub-mkrescue LZO support'
  'efibootmgr: For grub-install EFI support'
  'libisoburn: Provides xorriso for generating grub rescue iso using grub-mkrescue'
  'os-prober: To detect other OSes when generating grub.cfg in BIOS systems'
  'mtools: For grub-mkrescue FAT FS support')
[[ "${_GRUB_EMU_BUILD}" == "1" ]] && \
  makedepends+=(
    'libusb'
    'sdl'
  ) && \
  optdepends+=(
    'libusb: For grub-emu USB support'
    'sdl: For grub-emu SDL support'
  )
validpgpkeys=(
  # Vladimir 'phcoder' Serbinenko <phcoder@gmail.com>
  'E53D497F3FA42AD8C9B4D1E835A93B74E82E4209'
  # Daniel Kiper <dkiper@net-space.pl>
  'BE5C23209ACDDACEB20DB0A28C8189F1988C2166'
  # Paul Hardy <unifoundry@unifoundry.com>
  '95D2E9AB8740D8046387FD151A09227B1F435A33'
)
_savannah="https://git.savannah.gnu.org"
_http="${_savannah}/git"
_url="${_http}/${pkgname}.git"
_gnulib="${_http}/gnulib.git"
_local="file://${HOME}/${pkgname}"
_local_gnulib="file://${HOME}/gnulib"
_tag_name="commit"
_tag="${_commit}"
source=()
sha256sums=()
if [[ "${_offline}" == true ]]; then
  _url="${_local}"
  _gnulib="${_local_gnulib}"
fi
if [[ "${_git}" == "true" ]]; then
  _src="${pkgname}-${_tag}::git+${_url}#${_tag_name}=${_tag}?signed"
  _gnulib="gnulib-${_gnulib_commit}::git+${_gnulib}"
  _sum="SKIP"
  _gnulib_sum="SKIP"
elif [[ "${_git}" == "false" ]]; then
  _src="${_savannah}/cgit/${pkgname}.git/snapshot/${pkgname}-${pkgver}.tar.gz"
  _gnulib_url="${_savannah}/gitweb/?p=gnulib.git;a=snapshot;h=${_gnulib_commit};sf=tgz"
  _gnulib="gnulib-${_gnulib_commit}.tar.gz::${_gnulib_url}"
  _sum="ciao"
  _gnulib_sum="ciao"
fi
source=(
  "${_src}"
  "${_gnulib}"
  "https://ftp.gnu.org/gnu/unifont/unifont-${_unifont_ver}/unifont-${_unifont_ver}.bdf.gz"{,.sig}
  '0001-00_header-add-GRUB_COLOR_-variables.patch'
  '0002-10_linux-detect-archlinux-initramfs.patch'
  '0003-support-dropins-for-default-configuration.patch'
  "${pkgname}.default"
  'sbat.csv'
)

sha256sums=(
  "${_sum}"
  "${_gnulib_sum}"
  '88e00954b10528407e62e97ce6eaa88c847ebfd9a464cafde6bf55c7e4eeed54'
  'SKIP'
  '5dee6628c48eef79812bb9e86ee772068d85e7fcebbd2b2b8d1e19d24eda9dab'
  '8488aec30a93e8fe66c23ef8c23aefda39c38389530e9e73ba3fbcc8315d244d'
  'b5d9fcd62ffb3c3950fdeb7089ec2dc2294ac52e9861980ad90a437dedbd3d47'
  '7df3f5cb5df7d2dfb17f4c9b5c5dedc9519ddce6f8d2c6cd43d1be17cecb65cb'
  'f34c2b0aa2ed4ab9c7e7bcab5197470c30fedc6c2148f337839dd24bceae35fd'
)

_backports=(
)

_reverts=(
)

_configure_options=(
  PACKAGE_VERSION="${epoch}:${pkgver}-${pkgrel}"
  FREETYPE="pkg-config freetype2"
  BUILD_FREETYPE="pkg-config freetype2"
  --enable-nls
  --enable-device-mapper
  --enable-cache-stats
  --enable-grub-mkfont
  --enable-grub-mount
  --prefix="/usr"
  --bindir="/usr/bin"
  --sbindir="/usr/bin"
  --mandir="/usr/share/man"
  --infodir="/usr/share/info"
  --datarootdir="/usr/share"
  --sysconfdir="/etc"
  --program-prefix=""
  --with-bootdir="/boot"
  --with-grubdir="grub"
  --disable-silent-rules
  --disable-werror
)

_git_prepare() {
  local \
    _c
  cd \
    "${srcdir}/${pkgname}/"
  echo \
    "Apply backports..."
  for _c in \
    "${_backports[@]}"; do
    git \
      log \
        --oneline \
	-1 \
	"${_c}"
    git \
      cherry-pick \
        -n \
	"${_c}"
  done
  echo \
    "Apply reverts..."
  _c=""
  for _c in \
    "${_reverts[@]}"; do
    git \
      log \
        --oneline \
	-1 \
	"${_c}"
    git \
      revert \
        -n \
	"${_c}"
  done
}

prepare() {
  local \
    _c
  cd \
    "${srcdir}/${pkgname}/"
  if [[ "${_git}" == "true" ]]; then
    _git_prepare
  fi
  echo \
    "Patch to enable GRUB_COLOR_* variables in grub-mkconfig..."
  # Based on 
  # http://lists.gnu.org/archive/html/grub-devel/2012-02/msg00021.html
  patch \
    -Np1 \
    -i \
    "${srcdir}/0001-00_header-add-GRUB_COLOR_-variables.patch"
  echo \
    "Patch to detect of Arch Linux initramfs images by grub-mkconfig..."
  patch \
    -Np1 \
    -i \
    "${srcdir}/0002-10_linux-detect-archlinux-initramfs.patch"
  echo \
    "Patch to support dropins for default configuration..."
  patch \
    -Np1 \
    -i \
      "${srcdir}/0003-support-dropins-for-default-configuration.patch"
  echo \
    "Fix DejaVuSans.ttf location so that grub-mkfont can create *.pf2 files for starfield theme..."
  sed \
    's|/usr/share/fonts/dejavu|/usr/share/fonts/dejavu /usr/share/fonts/TTF|g' \
    -i \
    "configure.ac"
  echo \
    "Fix mkinitcpio 'rw' FS#36275..."
  sed \
    's| ro | rw |g' \
    -i \
    "util/grub.d/10_linux.in"
  echo \
    "Fix OS naming FS#33393..."
  sed \
    's|GNU/Linux|Linux|' \
    -i \
    "util/grub.d/10_linux.in"
  echo \
    "Pull in latest language files..."
  ./linguas.sh
  echo \
    "Avoid problem with unifont during compile of grub..."
  # http://savannah.gnu.org/bugs/?40330 and https://bugs.archlinux.org/task/37847
  gzip \
    -cd \
      "${srcdir}/unifont-${_unifont_ver}.bdf.gz" > \
    "unifont.bdf"
  echo \
    "Run bootstrap..."
  ./bootstrap \
    --gnulib-srcdir="${srcdir}/gnulib/" \
    --no-git
  echo \
    "Make translations reproducible..."
  sed \
    -i \
      '1i /^PO-Revision-Date:/ d' \
    po/*.sed
}

_build_grub-common_and_bios() {
  local \
    _configure_opts=()
  echo \
    "Set ARCH dependent variables for bios build..."
  if [[ "${CARCH}" == 'x86_64' ]]; then
    _EFIEMU="--enable-efiemu"
  else
    _EFIEMU="--disable-efiemu"
  fi
  _configure_opts=(
    --with-platform="pc"
    --target="i386"
    "${_EFIEMU}"
    --enable-boot-time
    "${_configure_options[@]}"
  )
  echo \
    "Copy the source for building the bios part..."
  cp \
    -r \
    "${srcdir}/grub/" \
    "${srcdir}/grub-bios/"
  cd \
    "${srcdir}/grub-bios/"
  echo \
    "Unset all compiler FLAGS for bios build..."
  unset \
    CFLAGS \
    CPPFLAGS \
    CXXFLAGS \
    LDFLAGS \
    MAKEFLAGS
  echo \
    "Run ./configure for bios build..."
  ./configure \
    "${_configure_opts[@]}"
  if [ ! -z "${SOURCE_DATE_EPOCH}" ]; then
    echo \
      "Make info pages reproducible..."
  touch \
    -d \
      "@${SOURCE_DATE_EPOCH}" \
      $(find \
          -name \
            '*.texi')
  fi
  
  echo \
    "Run make for bios build..."
  make
}

_build_grub-efi() {
  local \
    _configure_opts=()
  _configure_opts=(
    --with-platform="efi"
    --target="${_EFI_ARCH}"
    --disable-efiemu
    --enable-boot-time
    "${_configure_options[@]}"
  )
  echo \
    "Copy the source for building the ${_EFI_ARCH} efi part..."
  cp \
    -r \
      "${srcdir}/grub/" \
      "${srcdir}/grub-efi-${_EFI_ARCH}/"
  cd \
    "${srcdir}/grub-efi-${_EFI_ARCH}/"
  echo \
    "Unset all compiler FLAGS for ${_EFI_ARCH} efi build..."
  unset \
    CFLAGS \
    CPPFLAGS \
    CXXFLAGS \
    LDFLAGS \
    MAKEFLAGS
  echo \
    "Run ./configure for ${_EFI_ARCH} efi build..."
  ./configure \
    "${_configure_opts[@]}"
  echo \
    "Run make for ${_EFI_ARCH} efi build..."
  make
}

_build_grub-emu() {
  local \
    _configure_opts=()
  _configure_opts=(
    --with-platform="emu"
    --target="${_EMU_ARCH}"
    --enable-grub-emu-usb=no
    --enable-grub-emu-sdl=no
    --disable-grub-emu-pci
    "${_configure_options[@]}"
  )
  echo \
    "Copy the source for building the emu part..."
  cp \
    -r \
    "${srcdir}/grub/" \
    "${srcdir}/grub-emu/"
  cd \
    "${srcdir}/grub-emu/"
  echo \
    "Unset all compiler FLAGS for emu build..."
  unset \
    CFLAGS \
    CPPFLAGS \
    CXXFLAGS \
    LDFLAGS \
    MAKEFLAGS
  
  echo \
    "Run ./configure for emu build..."
  ./configure \
    "${_configure_opts[@]}"
  echo \
    "Run make for emu build..."
  make
}

build() {
  cd \
    "${srcdir}/grub/"
  [[ "${CARCH}" != 'arm' ]] && \
    echo \
      "Build grub bios stuff..." && \
    _build_grub-common_and_bios
  echo \
    "Build grub ${_EFI_ARCH} efi stuff..."
  _build_grub-efi
  
  if \
    [[ "${CARCH}" == "x86_64" ]] && \
    [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
      echo "Build grub i386 efi stuff..."
      _EFI_ARCH="i386" _build_grub-efi
  fi
  if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    echo \
      "Build grub emu stuff..."
    _build_grub-emu
  fi
}

_package_grub-bios() {
  local \
    _make_opts=()
  _make_opts=(
    DESTDIR="${pkgdir}"
    bashcompletiondir="/usr/share/bash-completion/completions"
  )
  cd \
    "${srcdir}/grub-bios/"
  echo \
    "Run make install for bios build..."
  make \
    "${_make_opts[@]}" \
    install
  echo \
    "Remove gdb debugging related files for bios build..."
  rm \
    -f \
    "${pkgdir}/usr/lib/grub/i386-pc"/*.module || \
    true
  rm \
    -f \
      "${pkgdir}/usr/lib/grub/i386-pc"/*.image || \
      true
  rm \
    -f \
      "${pkgdir}/usr/lib/grub/i386-pc"/{kernel.exec,gdb_grub,gmodule.pl} || \
    true
}

_package_grub-common() {
  echo \
    "Install /etc/default/grub (used by grub-mkconfig)..."
  install \
    -D \
    -m0644 \
    "${srcdir}/grub.default" \
    "${pkgdir}/etc/default/grub"
}

_package_grub-efi() {
  local \
    _make_opts=()
  _make_opts=(
    DESTDIR="${pkgdir}/"
    bashcompletiondir="/usr/share/bash-completion/completions"
  )
  cd \
    "${srcdir}/grub-efi-${_EFI_ARCH}/"
  echo \
    "Run make install for ${_EFI_ARCH} efi build..."
  make \
    "${_make_opts[@]}" \
    install
  echo \
    "Remove gdb debugging related files for ${_EFI_ARCH} efi build..."
  rm \
    -f \
      "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/*.module || \
    true
  rm \
    -f \
      "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/*.image || \
    true
  rm \
    -f "${pkgdir}/usr/lib/grub/${_EFI_ARCH}-efi"/{kernel.exec,gdb_grub,gmodule.pl} || \
    true
  
  sed \
    -e \
      "s/%PKGVER%/${epoch}:${pkgver}-${pkgrel}/" < \
        "${srcdir}/sbat.csv" > \
          "${pkgdir}/usr/share/grub/sbat.csv"
}

_package_grub-emu() {
  local \
    _make_opts=()
  _make_opts=(
    DESTDIR="${pkgdir}"
    bashcompletiondir="/usr/share/bash-completion/completions"
  )
  cd \
    "${srcdir}/grub-emu"

  echo \
    "Run make install for emu build..."
  make \
    "${_make_opts[@]}" \
    install
  echo \
    "Remove gdb debugging related files for emu build..."
  rm \
    -f \
      "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/*.module || \
    true
  rm \
    -f \
      "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/*.image || \
    true
  rm \
    -f "${pkgdir}/usr/lib/grub/${_EMU_ARCH}-emu"/{kernel.exec,gdb_grub,gmodule.pl} || \
    true
}

package() {
  cd \
    "${srcdir}/grub/"
  echo \
    "Package grub ${_EFI_ARCH} efi stuff..."
  _package_grub-efi
  if \
    [[ "${CARCH}" == "x86_64" ]] && \
    [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
    echo \
      "Package grub i386 efi stuff..."
      _EFI_ARCH="i386" \
      _package_grub-efi
  fi
  if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    echo \
      "Package grub emu stuff..."
    _package_grub-emu
  fi
  [[ "${CARCH}" != 'arm' ]] && \
    echo \
      "Package grub bios stuff..." && \
    _package_grub-bios
  _package_grub-common
}

# vim: ft=sh syn=sh et
