# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#   Felipe Contreras
#     <felipe.contreras@gmail.com>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
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
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_tag_name" ]]; then
  _tag_name="commit"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _archive_format="zip"
      elif [[ "${_tag_name}" == "pkgver" ]]; then
        _archive_format="tar.gz"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
_py="python"
_pkg=git-remote-hg
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=1.0.5
_pkgver="v${pkgver}"
_commit="16b33919e44483d1267bd2e51218a75ff1b61139"
_bundle_commit="88b2756e4383032f2d31746245c56bd69a3e861b"
pkgrel=9
_pkgdesc=(
  "Bidirectional bridge between"
  "Git and Mercurial."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://github.com"
_ns="felipec"
_ns="mnauw"
_ns="themartiancompany"
url="${_http}/${_ns}/${_pkg}"
license=(
  'GPL2'
)
depends=(
  'git'
  'mercurial'
)
makedepends=(
  'asciidoctor'
  "make"
  "mercurial"
  "${_py}"
)
if [[ "${_os}" == "Msys" ]]; then
  makedepends+=(
    "${_py}-pip"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
source=()
sha256sums=()
_url="${url}"
_tag="${_commit}"
_tarname="${pkgname}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_bundle_sum="cd8c747f5519f6269af82e90bc7fe91330252fdcfda067bf152cd217ceb100a7"
_bundle_sig_sum="1a6d941543b788748de7e217134ba4f4b4c0cb4a6012c1815090121c218eb776"
_github_sum="eed9e4b82162838216415d99a4f55993c9ea02433358002e40c1479c5abdd732"
_github_sig_sum="6d778349468a29f12b122ded3554afd6bbb7fec3ce6c50262d0bd06bace982bf"
if [[ "${_git}" == "true" ]]; then
  _sum="${_bundle_sum}"
  _sig_sum="${_bundle_sig_sum}"
elif [[ "${_git}" == "false" ]]; then
  if [[ "${_git_service}" == "github" ]]; then
    _sum="${_github_sum}"
    _sig_sum="${_github_sig_sum}"
  fi
fi
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  _src="${_evmfs_src}"
  _sig_sum="${_sig_sum}"
  source+=(
    "${_sig_src}"
  )
  sha256sums+=(
    "${_sig_sum}"
  )
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"
      elif [[ "${_tag_name}" == "pkgver" ]]; then
        _uri="${url}/archive/v${pkgver}.${_archive_format}"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

build() {
  cd \
    "${_tarname}"
  if [[ "${_os}" == "Msys" ]]; then
    pip \
      install \
      "mercurial"
  fi
  make \
    all \
    doc
}

check() {
  cd \
    "${_tarname}"
  make \
    test
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install \
    install-doc
}
