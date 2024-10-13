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
_git="false"
if [[ "${_os}" == "Android" ]]; then
  _git="false"
fi
_pkg=grub
pkgname="${_pkg}"
pkgdesc='GNU GRand Unified Bootloader (2)'
epoch=2
_commit='03e6ea18f6f834f177cad017279bedbb0a3de594' # git rev-parse grub-${_pkgver}
_gnulib_commit="22711ba820cf78dd8f8eea04f6073fcec7ab987b"
_pkgver=2.12
_unifont_ver='16.0.01'
pkgver=${_pkgver/-/}
pkgrel=4
url="https://www.gnu.org/software/${_pkg}"
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
  "etc/default/${_pkg}"
  "etc/${_pkg}.d/40_custom"
)
install="${_pkg}.install"
options=(
  '!makeflags'
)
conflicts=(
  "${_pkg}-common"
  "${_pkg}-bios"
  "${_pkg}-efi-${_EFI_ARCH}"
  "${_pkg}-legacy"
)
replaces=(
  "${_pkg}-common"
  "${_pkg}-bios"
  "${_pkg}-efi-${_EFI_ARCH}"
)
provides=(
  "${_pkg}-common=${pkgver}"
  "${_pkg}-bios=${pkgver}"
  "${_pkg}-efi-${_EFI_ARCH}"
)
[[ "${_GRUB_EMU_BUILD}" == "1" ]] && \
  conflicts+=(
    "${_pkg}-emu"
  ) && \
  provides+=(
    "${_pkg}-emu"
  ) && \
  replaces+=(
    "${_pkg}-emu"
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
  "freetype2: For ${_pkg}-mkfont usage"
  "fuse3: For ${_pkg}-mount usage"
  "dosfstools: For ${_pkg}-mkrescue FAT FS and EFI support"
  "lzop: For ${_pkg}-mkrescue LZO support"
  "efibootmgr: For ${_pkg}-install EFI support"
  "libisoburn: Provides xorriso for generating ${_pkg} rescue iso using ${_pkg}-mkrescue"
  "os-prober: To detect other OSes when generating ${_pkg}.cfg in BIOS systems"
  "mtools: For ${_pkg}-mkrescue FAT FS support"
)
[[ "${_GRUB_EMU_BUILD}" == "1" ]] && \
  makedepends+=(
    'libusb'
    'sdl'
  ) && \
  optdepends+=(
    "libusb: For ${_pkg}-emu USB support"
    "sdl: For ${_pkg}-emu SDL support"
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
_url="${_http}/${_pkg}.git"
_gnulib="${_http}/gnulib.git"
_local="file://${HOME}/${_pkg}"
_local_gnulib="file://${HOME}/gnulib"
_tag_name="commit"
_tag="${_commit}"
source=()
sha256sums=()
b2sums=()
if [[ "${_offline}" == true ]]; then
  _url="${_local}"
  _gnulib="${_local_gnulib}"
fi
if [[ "${_git}" == "true" ]]; then
  _src="${_pkg}-${pkgver}::git+${_url}#${_tag_name}=${_tag}?signed"
  _gnulib="gnulib-${_gnulib_commit}::git+${_gnulib}"
  _sum="SKIP"
  _bsum='a6cec7271c3ea54a99f02ee6bc0a5825c8be657af68ba9a32b39a5fe8bcb571fb1ba39210426f6bf6a48d913e6e00df37dc2123ea1b39330f4c47bd9dbac9ae3'
  _gnulib_sum="SKIP"
  _gnulib_bsum="SKIP"
elif [[ "${_git}" == "false" ]]; then
  _src_url="${_savannah}/cgit/${_pkg}.git/snapshot/${_pkg}-${pkgver}.tar.gz"
  _src="${_pkg}-${pkgver}.tar.gz::${_src_url}"
  _gnulib_url="${_savannah}/gitweb/?p=gnulib.git;a=snapshot;h=${_gnulib_commit};sf=tgz"
  _gnulib="gnulib-${_gnulib_commit}.tar.gz::${_gnulib_url}"
  _sum="af4d58df3024988799225e94bc1cfaccdeaa9d5725b4ad5517f3b6cf2ee9ed78"
  _bsum="be5d3209371fd206687742de988e0531897afb4a3e0643ba001f306a8fe7a02e3448341e2802f17090874338a319c7ede4d59e50a37a84152830204b18864366"
  _gnulib_sum="f3e6628b392b8a6829cfa4837db7cc7d3f9f1984a8ea4e653f9c0ce000a8eb2c"
  _gnulib_bsum="a4d1cded4ed90736aff031bc6037f7affc0ec8ab5f91e029fc1b4481349deddebd3cdb27a2a36ca987789424befe25b7f6386ada128dfeb1ccdf16f79222293e"
fi
source+=(
  "${_src}"
  "${_gnulib}"
  "https://ftp.gnu.org/gnu/unifont/unifont-${_unifont_ver}/unifont-${_unifont_ver}.bdf.gz"{,.sig}
  '0001-00_header-add-GRUB_COLOR_-variables.patch'
  '0002-10_linux-detect-archlinux-initramfs.patch'
  '0003-support-dropins-for-default-configuration.patch'
  "${_pkg}.default"
  'sbat.csv'
)
sha256sums+=(
  "${_sum}"
  "${_gnulib_sum}"
  "230a0959aa50778b68239c88ad3c2d53abde58be0932b14a379a3869118aca33"
  'SKIP'
  '5dee6628c48eef79812bb9e86ee772068d85e7fcebbd2b2b8d1e19d24eda9dab'
  '8488aec30a93e8fe66c23ef8c23aefda39c38389530e9e73ba3fbcc8315d244d'
  'b5d9fcd62ffb3c3950fdeb7089ec2dc2294ac52e9861980ad90a437dedbd3d47'
  '7df3f5cb5df7d2dfb17f4c9b5c5dedc9519ddce6f8d2c6cd43d1be17cecb65cb'
  'f34c2b0aa2ed4ab9c7e7bcab5197470c30fedc6c2148f337839dd24bceae35fd'
)
b2sums+=(
  "${_bsum}"
  'SKIP'
  '9f306564a63961f3a9f7a45f3f3363b1cc44a1651c3fb858ca4e87cdad79668f9aaa4b2989f91032cd614e37a98e5ca5eda2e2b0315d99deab6d0732b6f57a0d'
  'SKIP'
  '992c71790785304c28fbaf0dba21dab3e283b199509f0e7e1aa0df08126da75e15b6626c3638279ff2ecaa59b925096d7dbd67d6a53cebd0ce4326ff3719d25b'
  'b4cd9ac976a579eca19d54c0b31c8d6324525fe5a0b9f5405deb63845367ac1adaa80ece4c166dfd5304608c41aa44b4f64efe235c03f437523b993be06e06e3'
  'a7820bfe9bddc34af49de63222b3d2a9788367083e29db13b33120269adbfa1619ac421d8597f662f756592889f5cc5538544a17d9936d1420bd5742282c710c'
  '5e42db2161e8f594b82005b26e590a20a0e8d32b01119bdd7b1a7f7c4b0f3360e8730a3ecdd5912a4dc7af5bd9aed1c3e780965ad6747d831b470158da19388d'
  '052b55f53ec82d805f952afcd485bfc21623e0e427fc449f29208fecf5c321b9503d33e9025fef34ef3211b60043acfe5db08b057baaf72542a1c48cdc89b3c2'
)

_backports=(
)

_reverts=(
)

if [[ "${CARCH}" == 'x86_64' ]]; then
  _cflags+=(
    -Wno-implicit-function-declaration
    -Wno-int-conversion
  )
fi

_configure_options=(
  PACKAGE_VERSION="${epoch}:${pkgver}-${pkgrel}"
  FREETYPE="pkg-config freetype2"
  BUILD_FREETYPE="pkg-config freetype2"
  --enable-nls
  --enable-device-mapper
  --enable-cache-stats
  --"enable-${_pkg}-mkfont"
  --"enable-${_pkg}-mount"
  --prefix="/usr"
  --bindir="/usr/bin"
  --sbindir="/usr/bin"
  --mandir="/usr/share/man"
  --infodir="/usr/share/info"
  --datarootdir="/usr/share"
  --sysconfdir="/etc"
  --program-prefix=""
  --with-bootdir="/boot"
  --"with-${_pkg}dir"="${srcdir}/${_pkg}-${pkgver}"
  --disable-silent-rules
  --disable-werror
)

_git_prepare() {
  local \
    _c
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
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
    _gnulib_dir
  cd \
    "${srcdir}/${_pkg}-${pkgver}"
  if [[ "${_git}" == "true" ]]; then
    _git_prepare
  fi
  echo \
    "Patch to enable GRUB_COLOR_* variables in ${_pkg}-mkconfig..."
  # Based on 
  # http://lists.gnu.org/archive/html/grub-devel/2012-02/msg00021.html
  patch \
    -Np1 \
    -i \
    "${srcdir}/0001-00_header-add-GRUB_COLOR_-variables.patch"
  echo \
    "Patch to detect of Arch Linux initramfs images by ${_pkg}-mkconfig..."
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
    "Fix DejaVuSans.ttf location so that ${_pkg}-mkfont can create *.pf2 files for starfield theme..."
  sed \
    's|/usr/share/fonts/dejavu|/usr/share/fonts/dejavu /usr/share/fonts/TTF|g' \
    -i \
    "configure.ac"
  echo \
    "Fix mkinitcpio 'rw' FS#36275..."
  sed \
    's| ro | rw |g' \
    -i \
    "util/${_pkg}.d/10_linux.in"
  echo \
    "Fix OS naming FS#33393..."
  sed \
    's|GNU/Linux|Linux|' \
    -i \
    "util/${_pkg}.d/10_linux.in"
  echo \
    "Pull in latest language files..."
  ./linguas.sh
  echo \
    "Avoid problem with unifont during compile of ${_pkg}..."
  # http://savannah.gnu.org/bugs/?40330 and https://bugs.archlinux.org/task/37847
  gzip \
    -cd \
      "${srcdir}/unifont-${_unifont_ver}.bdf.gz" > \
    "unifont.bdf"
  _gnulib_dir="${srcdir}/gnulib-${_gnulib_commit::-33}"
  echo \
    "Run bootstrap with GNULib dir '${_gnulib_dir}'..."
  ./bootstrap \
    --no-git \
    --gnulib-srcdir="${_gnulib_dir}/"
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
    "${srcdir}/${_pkg}-${pkgver}/" \
    "${srcdir}/${_pkg}-bios/"
  cd \
    "${srcdir}/${_pkg}-bios/"
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
  CFLAGS="${_cflags[*]}" \
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
      "${srcdir}/${_pkg}-${pkgver}/" \
      "${srcdir}/${_pkg}-efi-${_EFI_ARCH}/"
  cd \
    "${srcdir}/${_pkg}-efi-${_EFI_ARCH}/"
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
  CFLAGS="${_cflags[*]}" \
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
    --"enable-${_pkg}-emu-usb"=no
    --"enable-${_pkg}-emu-sdl"=no
    --"disable-${_pkg}-emu-pci"
    "${_configure_options[@]}"
  )
  echo \
    "Copy the source for building the emu part..."
  cp \
    -r \
    "${srcdir}/${_pkg}/" \
    "${srcdir}/${_pkg}-emu/"
  cd \
    "${srcdir}/${_pkg}-emu/"
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
  CFLAGS="${_cflags[*]}" \
  ./configure \
    "${_configure_opts[@]}"
  echo \
    "Run make for emu build..."
  CFLAGS="${_cflags[*]}" \
  make
}

build() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}/"
  [[ "${CARCH}" != 'arm' ]] && \
    echo \
      "Build ${_pkg} bios stuff..." && \
    "_build_${_pkg}-common_and_bios"
  echo \
    "Build ${_pkg} ${_EFI_ARCH} efi stuff..."
  "_build_${_pkg}-efi"
  if \
    [[ "${CARCH}" == "x86_64" ]] && \
    [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
      echo \
        "Build ${_pkg} i386 efi stuff..."
      _EFI_ARCH="i386" \
      "_build_${_pkg}-efi"
  fi
  if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    echo \
      "Build ${_pkg} emu stuff..."
    "_build_${_pkg}-emu"
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
    "${srcdir}/${_pkg}-bios/"
  echo \
    "Run make install for bios build..."
  CFLAGS="${_cflags[*]}" \
  make \
    "${_make_opts[@]}" \
    install
  echo \
    "Remove gdb debugging related files for bios build..."
  rm \
    -f \
    "${pkgdir}/usr/lib/${_pkg}/i386-pc"/*.module || \
    true
  rm \
    -f \
      "${pkgdir}/usr/lib/${_pkg}/i386-pc"/*.image || \
      true
  rm \
    -f \
      "${pkgdir}/usr/lib/${_pkg}/i386-pc"/{kernel.exec,"gdb_${_pkg}",gmodule.pl} || \
    true
}

_package_grub-common() {
  echo \
    "Install /etc/default/${_pkg} (used by ${_pkg}-mkconfig)..."
  install \
    -D \
    -m0644 \
    "${srcdir}/${_pkg}.default" \
    "${pkgdir}/etc/default/${_pkg}"
}

_package_grub-efi() {
  local \
    _make_opts=()
  _make_opts=(
    DESTDIR="${pkgdir}/"
    bashcompletiondir="/usr/share/bash-completion/completions"
  )
  cd \
    "${srcdir}/${_pkg}-efi-${_EFI_ARCH}/"
  echo \
    "Run make install for ${_EFI_ARCH} efi build..."
  CFLAGS="${_cflags[*]}" \
  make \
    "${_make_opts[@]}" \
    install
  echo \
    "Remove gdb debugging related files for ${_EFI_ARCH} efi build..."
  rm \
    -f \
      "${pkgdir}/usr/lib/${_pkg}/${_EFI_ARCH}-efi"/*.module || \
    true
  rm \
    -f \
      "${pkgdir}/usr/lib/${_pkg}/${_EFI_ARCH}-efi"/*.image || \
    true
  rm \
    -f "${pkgdir}/usr/lib/${_pkg}/${_EFI_ARCH}-efi"/{kernel.exec,"gdb_${_pkg}",gmodule.pl} || \
    true
  sed \
    -e \
      "s/%PKGVER%/${epoch}:${pkgver}-${pkgrel}/" < \
        "${srcdir}/sbat.csv" > \
          "${pkgdir}/usr/share/${_pkg}/sbat.csv"
}

_package_grub-emu() {
  local \
    _make_opts=()
  _make_opts=(
    DESTDIR="${pkgdir}"
    bashcompletiondir="/usr/share/bash-completion/completions"
  )
  cd \
    "${srcdir}/${_pkg}-emu"
  echo \
    "Run make install for emu build..."
  CFLAGS="${_cflags[*]}" \
  make \
    "${_make_opts[@]}" \
    install
  echo \
    "Remove gdb debugging related files for emu build..."
  rm \
    -f \
      "${pkgdir}/usr/lib/${_pkg}/${_EMU_ARCH}-emu"/*.module || \
    true
  rm \
    -f \
      "${pkgdir}/usr/lib/${_pkg}/${_EMU_ARCH}-emu"/*.image || \
    true
  rm \
    -f "${pkgdir}/usr/lib/${_pkg}/${_EMU_ARCH}-emu"/{kernel.exec,"gdb_${_pkg}",gmodule.pl} || \
    true
}

package() {
  cd \
    "${srcdir}/${_pkg}-${pkgver}/"
  echo \
    "Package ${_pkg} ${_EFI_ARCH} efi stuff..."
  "_package_${_pkg}-efi"
  if \
    [[ "${CARCH}" == "x86_64" ]] && \
    [[ "${_IA32_EFI_IN_ARCH_X64}" == "1" ]]; then
    echo \
      "Package ${_pkg} i386 efi stuff..."
      _EFI_ARCH="i386" \
      "_package_${_pkg}-efi"
  fi
  if [[ "${_GRUB_EMU_BUILD}" == "1" ]]; then
    echo \
      "Package ${_pkg} emu stuff..."
    "_package_${_pkg}-emu"
  fi
  [[ "${CARCH}" != 'arm' ]] && \
    echo \
      "Package ${_pkg} bios stuff..." && \
    "_package_${_pkg}-bios"
  "_package_${_pkg}-common"
}

# vim: ft=sh syn=sh et
