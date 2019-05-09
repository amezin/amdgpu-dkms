# Maintainer: Aleksandr Mezin <mezin.alexander@gmail.com>

pkgname=amdgpu-dkms
pkgver=19.10
pkgrel=1
pkgdesc="amdgpu driver dkms package"
arch=('x86_64')
url="https://cgit.freedesktop.org/~agd5f/linux"
license=('GPL2')
depends=('dkms')
source=(
  "git+git://people.freedesktop.org/~agd5f/linux#branch=amd-${pkgver}"
  "drm_ver_unknown.patch"
  "build_exclusive_kernel.patch"
  "drm_mode_connector.patch"
)
md5sums=('SKIP'
         'd3383fbff45a0e2af94241353123ef3a'
         '49e20200bce770a3b0cd5d272609167f'
         '99b1c43cf9f80502df3747658f086fef')

prepare() {
  cd "${srcdir}"/linux
  patch -p1 -i ../drm_ver_unknown.patch
  patch -p1 -i ../build_exclusive_kernel.patch
  patch -p1 -i ../drm_mode_connector.patch
}

package() {
  install_src_dir="${pkgdir}"/usr/src/${pkgname}-${pkgver}

  mkdir -p "${install_src_dir}"
  cp -r "${srcdir}"/linux/drivers/gpu/drm/amd/dkms/* "${install_src_dir}"

  while read -r line
  do
    src_path=$(echo "${line}" | cut -d' ' -f1)
    dst_path=$(echo "${line}" | cut -d' ' -f2)

    mkdir -p "${install_src_dir}"/"${dst_path}"
    cp -r "${srcdir}"/linux/"${src_path}" "${install_src_dir}"/"${dst_path}"
  done < "${install_src_dir}"/sources
}
