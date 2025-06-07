# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
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
#   Anatol Pomozov
#     <anatol.pomozov@gmail.com>
# Maintainer:
#   Andreas 'Segaja' Schleifer
#     <segaja at archlinux dot org>
# Maintainer:
#   Tim Meusel
#     <tim@bastelfreak.de>
# Contributor:
#   Thomas Dziedzic
#     <gostrc@gmail.com>
# Contributor:
#   Allan McRae
#     <allan@archlinux.org>
# Contributor:
#   John Proctor
#     <jproctor@prium.net>
# Contributor:
#   Jeramy Rutley
#     <jrutley@gmail.com>

# Do not re-package default gems
# (see https://stdgems.org).
# Trying to do that will lead
# to multiple problems.

_os="$( \
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _libcompiler="libllvm"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _libcompiler="gcc-libs"
fi
_pkg=ruby
pkgname=(
  "${_pkg}"
  "${_pkg}-docs"
  "${_pkg}-default-gems"
  "${_pkg}-bundled-gems"
  "${_pkg}-stdlib"
)
pkgver="3.4.4"
pkgrel="2"
_pkgdesc=(
  'An object-oriented language'
  'for quick and easy programming.'
)
_domain="${_pkg}-lang.org"
url="https://www.${_domain}/en"
arch=(
  'arm'
  'armv6l'
  'armv7l'
  'aarch64'
  'i686'
  'mips'
  'pentium4'
  'powerpc'
  'x86_64'
)
license=(
  'BSD-2-Clause'
)
makedepends=(
  'doxygen'
  "${_libc}"
  "${_libcompiler}"
  'gdbm'
  'gmp'
  'graphviz'
  'libffi'
  'libxcrypt'
  'libyaml'
  'openssl'
  'readline'
  'rust'
  'tk'
  'zlib'
)
checkdepends=(
  'procps-ng'
)
options=(
  '!emptydirs'
)
_http="https://cache.${_domain}"
_ns="pub"
_url="${_http}/${_ns}/${_pkg}"
_tag_name="pkgver"
_tag="${pkgver}"
_tarname="${_pkg}-${_tag}"
_src="${_url}/${pkgver:0:3}/${_tarname}.tar.xz"
source=(
  "${_src}"
)
sha512sums=(
  '0d258cf790daad424c866404b5cbdc8adba0e4e13764847a89adf2335229e5184095c9f3e9594705897697e48bcc322d9a9f919b04047abb2075daca9fce8871'
)
b2sums=(
  '0c9b61784beb6c6f8b082cad4299f52de994ecb49e6bf5e9ac263c1d4fc2618119ddb1276d7060772856d297d9c2765590b54972fa2234738b3dd5c4020332f8'
)

_bootstrap=0
_rubyver="${pkgver:0:3}.0"
_bundled_gems=(
  "abbrev"
  "base64"
  "bigdecimal"
  "csv"
  "debug"
  "drb"
  "getoptlong"
  "matrix"
  "minitest"
  "mutex_m"
  "net-ftp"
  "net-imap"
  "net-pop"
  "net-smtp"
  "nkf"
  "observer"
  "power_assert"
  "prime"
  "racc"
  "rake"
  "rbs"
  "repl_type_completor"
  "resolv-replace"
  "rexml"
  "rinda"
  "rss"
  "test-unit"
  "syslog"
  "typeprof"
)
_bundled_gems_bins=(
  "racc"
  "rake"
  "rbs"
  "rdbg"
  "typeprof"
)
_default_gems=(
  "benchmark"
  "cgi"
  "date"
  "delegate"
  "did_you_mean"
  "digest"
  "english"
  "error_highlight"
  "etc"
  "fcntl"
  "fiddle"
  "fileutils"
  "find"
  "forwardable"
  "io-console"
  "io-nonblock"
  "io-wait"
  "ipaddr"
  "json"
  "logger"
  "net-http"
  "net-protocol"
  "open-uri"
  "open3"
  "openssl"
  "optparse"
  "ostruct"
  "pathname"
  "prism"
  "pp"
  "prettyprint"
  "pstore"
  "psych"
  "readline"
  "reline"
  "resolv"
  "ruby2_keywords"
  "securerandom"
  "set"
  "shellwords"
  "singleton"
  "stringio"
  "strscan"
  "syntax_suggest"
  "tempfile"
  "time"
  "timeout"
  "tmpdir"
  "tsort"
  "un"
  "uri"
  "weakref"
  "yaml"
  "zlib"
)
_default_tool_gems=(
  "bundler"
  "erb"
  "irb"
  "rdoc"
  "rubygems"
)
_default_tool_gems_bins=(
  "bundle"
  "bundler"
  "erb"
  "gem"
  "irb"
  "rdoc"
  "ri"
)

prepare() {
  cd \
    "${_tarname}"
  autoreconf \
    -fiv
}

build() {
  local \
    _configure_opts=()
  _configure_opts+=(
    --prefix="/usr"
    --sysconfdir="/etc"
    --localstatedir="/var"
    --sharedstatedir="/var/lib"
    --libexecdir="/usr/lib/ruby"
    --enable-shared
    --disable-rpath
    --with-dbm-type="gdbm_compat"
  )
  cd \
    "${_tarname}"
  # This uses malloc_usable_size,
  # which is incompatible with
  # fortification level 3.
  export \
    CFLAGS="${CFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}" \
    CXXFLAGS="${CXXFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"
  ./configure \
    "${_configure_opts[@]}"
  make
  make \
    "rdoc" \
    "capi"
}

check() {
  cd \
    "${_tarname}"
  # This uses malloc_usable_size,
  # which is incompatible with
  # fortification level 3.
  export \
    CFLAGS="${CFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}" \
    CXXFLAGS="${CXXFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"
  make \
    check
}

package_ruby() {
  depends=(
    "${_libcompiler}"
    "gdbm"
    "${_libc}"
    "gmp"
    "libffi"
    "libxcrypt"
    "libyaml"
    "openssl"
    "readline"
    "zlib"
  )
  optdepends=(
    'tk: for Ruby/TK'
    "${_pkg}-docs: Documentation for Ruby"
    "${_pkg}-default-gems: Default gems which are part of Ruby StdLib"
    "${_pkg}-bundled-gems: Bundled gems which are part of Ruby StdLib"
    "${_pkg}-stdlib: Full Ruby StdLib including default gems, bundled gems and tools"
  )
  provides=(
    "lib${_pkg}=${pkgver}"
    "lib${_pkg}.so=${pkgver}"
  )
  conflicts=(
    "lib${_pkg}=${pkgver}"
    "lib${_pkg}.so=${pkgver}"
  )
  replaces=(
    "${_pkg}-benchmark"
    "${_pkg}-cgi"
    "${_pkg}-date"
    "${_pkg}-delegate"
    "${_pkg}-did_you_mean"
    "${_pkg}-digest"
    "${_pkg}-english"
    "${_pkg}-etc"
    "${_pkg}-fcntl"
    "${_pkg}-fiddle"
    "${_pkg}-fileutils"
    "${_pkg}-find"
    "${_pkg}-forwardable"
    "${_pkg}-io-console"
    "${_pkg}-io-nonblock"
    "${_pkg}-io-wait"
    "${_pkg}-ipaddr"
    "${_pkg}-json"
    "${_pkg}-logger"
    "${_pkg}-net-http"
    "${_pkg}-open-uri"
    "${_pkg}-prism"
    "${_pkg}-psych"
    "${_pkg}-reline"
    "${_pkg}-ruby2_keywords"
    "${_pkg}-set"
    "${_pkg}-stringio"
    "${_pkg}-time"
    "${_pkg}-tmpdir"
    "${_pkg}-uri"
  )
  conflicts=(
    "${replaces[@]}"
  )
  provides+=(
    "${_default_gems[@]/#/ruby-}"
  )
  cd \
    "${_tarname}"
  make \
    DESTDIR="${pkgdir}" \
    install-nodoc
  install \
    -vDm0644 \
    "BSDL" \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  install \
    -vDm0644 \
    *".md" \
    -t \
    "${pkgdir}/usr/share/doc/${pkgname}"
  # Remove unrepreducible files.
  rm \
    -rv \
    "${pkgdir}/usr/lib/${_pkg}/gems/${_rubyver}/cache"
  # Bootstrap switch.
  if (( _bootstrap )); then
    # provide everything for a bootstrap build
    # use a reference to provides to srcinfo generation isn't confused
    declare \
      -n \
      bootstrap_provides=provides
    bootstrap_provides+=(
      "${_default_tool_gems[@]/#/ruby-}"
      "${_pkg}gems"
    )
    bootstrap_provides+=(
      "${_bundled_gems[@]/#/ruby-}"
    )
    declare \
      -n \
      bootstrap_conflicts=conflicts
    bootstrap_conflicts+=(
      "${_default_tool_gems[@]/#/ruby-}"
      "${_pkg}gems"
    )
    bootstrap_conflicts+=(
      "${_bundled_gems[@]/#/ruby-}"
    )
  else
    # remove de-vendored parts
    _remove_default_tool_gems
    _remove_bundled_gems
    # add standard dependencies
    depends+=(
      "${_pkg}gems"
    )
  fi
}

# Remove bundled gems
# -  they are provided as dedicated packages.
_remove_bundled_gems() {
  local \
    gem \
    bin
  for gem in "${_bundled_gems[@]}"; do
    msg2 \
      "Removing bundled gem ${gem}."
    rm \
      -rv \
      "${pkgdir}/usr/lib/${_pkg}/gems/${_rubyver}/gems/${gem}-"* \
      "${pkgdir}/usr/lib/${_pkg}/gems/${_rubyver}/specifications/${gem}-"*".gemspec"
    rm \
      -rvf \
      "${pkgdir}/usr/lib/${_pkg}/gems/${_rubyver}/extensions/"*"-linux/${_rubyver}/${gem}-"*
  done
  for bin in "${_bundled_gems_bins[@]}"; do
    rm \
      -rv \
      "${pkgdir}/usr/bin/${bin}"
    rm \
      -rvf \
      "${pkgdir}/usr/bin/${bin}.lock"
    rm \
      -rvf \
      "${pkgdir}/usr/share/man/man1/${bin}.1"
  done
}

# remove default tool gems - they are provided as dedicated packages
_remove_default_tool_gems() {
  local \
    gem \
    bin
  for gem in "${_default_tool_gems[@]}"; do
    msg2 \
      "Removing default gem ${gem}."
    rm \
      -rv \
      "${pkgdir}/usr/lib/${_pkg}/${_rubyver}/${gem}"*
    if [[ ${gem} != rubygems ]]; then
      rm \
        -rv \
        "${pkgdir}/usr/lib/${_pkg}/gems/${_rubyver}/gems/${gem}-"* \
        "${pkgdir}/usr/lib/${_pkg}/gems/${_rubyver}/specifications/default/${gem}-"*".gemspec"
    fi
    rm \
      -rvf \
      "${pkgdir}/usr/lib/ruby/${_rubyver}/"*"-linux/${gem}"
  done
  for bin in "${_default_tool_gems_bins[@]}"; do
    rm \
      -rv \
      "${pkgdir}/usr/bin/${bin}"
    rm \
      -rvf \
      "${pkgdir}/usr/bin/${bin}.lock"
    rm \
      -rvf \
      "${pkgdir}/usr/share/man/man1/${bin}.1"
  done
}

package_ruby-docs() {
  local \
    _pkgdesc=()
  _pkgdesc=(
    'Documentation files for Ruby.'
  )
  pkgdesc="${_pkgdesc[*]}"
  cd \
    "${_tarname}"
  make \
    DESTDIR="${pkgdir}" \
    install-doc \
    install-capi
  install \
    -vDm0644 \
    "BSDL" \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_ruby-bundled-gems() {
  local \
    _pkgdesc=()
  _pkgdesc=(
    'Bundled gems which are part of Ruby StdLib.'
  )
  pkgdesc="${_pkgdesc[*]}"
  replaces=(
    "${_pkg}-bundledgems"
  )
  conflicts=(
    "${_pkg}-bundledgems"
  )
  depends=(
    "${_bundled_gems[@]/#/ruby-}"
  )
  cd \
    "${_tarname}"
  install \
    -vDm0644 \
    "BSDL" \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_ruby-default-gems() {
  local \
    _pkgdesc=()
  _pkgdesc=(
    'Default gems which are part of Ruby StdLib.'
  )
  pkgdesc="${_pkgdesc[*]}"
  depends=(
    "${_default_tool_gems[@]/#/ruby-}"
  )
  cd \
    "${_tarname}"
  install \
    -vDm0644 \
    "BSDL" \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_ruby-stdlib() {
  local \
    _pkgdesc=()
  _pkgdesc=(
    'Full Ruby StdLib including'
    'default gems, bundled gems'
    'and tools.'
  )
  pkgdesc="${_pkgdesc[*]}"
  depends=(
    "${_pkg}-default-gems"
    "${_pkg}-bundled-gems"
  )
  cd \
    "${_tarname}"
  install \
    -vDm0644 \
    "BSDL" \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: tabstop=2 shiftwidth=2 expandtab:
