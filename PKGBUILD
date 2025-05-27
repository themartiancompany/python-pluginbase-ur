# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer:
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer:
#   Mohamed Tarek
#     <Mokhamed_tarek@mail.ru>
# Contributor:
#   Tomislav Ivek
#     <tomislav.ivek@gmail.com>
# Contributor:
#   Carl George
#     < arch at cgtx dot us >

_evmfs_available="$( \
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
_pkg="pluginbase"
_name="${_pkg}"
_module="${_name}"
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
pkgname=(
  "${_py}-${_module}"
)
pkgver=1.0.1
pkgrel=0
_pkgdesc=(
  "A support library for building"
  "plugins systems in Python."
)
arch=(
  "any"
)
url="https://pypi.org/project/${_pkg}"
license=(
  "BSD-3-Clause"
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-setuptools"
)
_pypi="https://files.pythonhosted.org/packages"
_tarname="${_pkg}-${pkgver}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_archive_sum="ff6c33a98fce232e9c73841d787a643de574937069f0d18147028d70d7dee287"
_evmfs_archive_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sum}"
_evmfs_archive_src="${_tarname}.zip::${_evmfs_archive_uri}"
_archive_sig_sum="aa179698830c84608cef0717d1fbd03271c509a6d86f43455c6061b9049555f2"
_archive_sig_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sig_sum}"
_archive_sig_src="${_tarname}.zip.sig::${_archive_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
  _src="${_evmfs_archive_src}"
  source+=(
    "${_archive_sig_src}"
  )
  sha256sums+=(
    "${_archive_sig_sum}"
  )
elif [[ "${_evmfs}" == "false" ]]; then
  uri="${_pypi}/f3/07/753451e80d2b0bf3bceec1162e8d23638ac3cb18d1c38ad340c586e90b42/${_tarname}.tar.gz"
  _src="${_tarname}.zip::${_uri}"
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_archive_sum}"
)
_src="${_tarname}.tar.gz::${_uri}"
source=(
  "${_src}"
)
sha256sums=(
  'ff6c33a98fce232e9c73841d787a643de574937069f0d18147028d70d7dee287'
)
validpgpkeys=(
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

build() {
  cd \
    "${_tarname}"
  "${_py}" \
    "setup.py" \
      build
}

package_python-pluginbase() {
  cd \
    "${_tarname}"
  "${_py}" \
    "setup.py" \
      install \
        --skip-build \
	--root="${pkgdir}" \
	--optimize=1
  install \
    -vDm644 \
    --target-directory \
      "${pkgdir}/usr/share/licenses/${pkgname}" \
    "LICENSE"
}
