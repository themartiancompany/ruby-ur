# Maintainer: Anatol Pomozov <anatol.pomozov@gmail.com>
# Maintainer: Andreas 'Segaja' Schleifer <segaja at archlinux dot org>
# Maintainer: Tim Meusel <tim@bastelfreak.de>
# Contributor: Thomas Dziedzic <gostrc@gmail.com>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: John Proctor <jproctor@prium.net>
# Contributor: Jeramy Rutley <jrutley@gmail.com>

# Do not re-package default gems (see https://stdgems.org/). Trying to do that will lead to multiple problems

pkgname=(
  ruby
  ruby-docs
  ruby-default-gems
  ruby-bundled-gems
  ruby-stdlib
)
pkgver=3.2.5
pkgrel=2
pkgdesc='An object-oriented language for quick and easy programming'
url='https://www.ruby-lang.org/en/'
arch=(x86_64)
license=(BSD-2-Clause)
makedepends=(
  doxygen
  gcc-libs
  gdbm
  glibc
  gmp
  graphviz
  libffi
  libxcrypt
  libyaml
  openssl
  readline
  rust
  tk
  zlib
)
checkdepends=(
  inetutils
  procps-ng
)
options=('!emptydirs')
source=("https://cache.ruby-lang.org/pub/ruby/${pkgver:0:3}/ruby-${pkgver}.tar.xz")
sha512sums=('092348b84b513aec62e63ec10b326370d0e3d1fa3126c59c03c84f28e2d7741a4772c461b077ec6a7dac3964a20f434655729e1acd50a3438755d7ad64073305')
b2sums=('a37c92a0f751e81dcae328b8944c4ecf10f6aee4f4468d6d08bb924c9808c8556c5febb71a825dd62dbcccf56385138e6e306bf3efae3589bdf0512d16d99d1a')

_bootstrap=0
_rubyver="${pkgver:0:3}.0"
_bundled_gems=(
  debug
  matrix
  minitest
  net-ftp
  net-imap
  net-pop
  net-smtp
  power_assert
  prime
  rake
  rbs
  rexml
  rss
  test-unit
  typeprof
)
_bundled_gems_bins=(
  rake
  rbs
  rdbg
  typeprof
)
_default_gems=(
  abbrev
  base64
  benchmark
  bigdecimal
  cgi
  csv
  date
  delegate
  did_you_mean
  digest
  drb
  english
  error_highlight
  etc
  fcntl
  fiddle
  fileutils
  find
  forwardable
  getoptlong
  io-console
  io-nonblock
  io-wait
  ipaddr
  json
  logger
  mutex_m
  net-http
  net-protocol
  nkf
  observer
  open-uri
  open3
  openssl
  optparse
  ostruct
  pathname
  pp
  prettyprint
  pstore
  psych
  readline
  readline-ext
  reline
  resolv
  resolv-replace
  rinda
  ruby2_keywords
  securerandom
  set
  shellwords
  singleton
  stringio
  strscan
  syntax_suggest
  syslog
  tempfile
  time
  timeout
  tmpdir
  tsort
  un
  uri
  weakref
  yaml
  zlib
)
_default_tool_gems=(
  bundler
  erb
  irb
  racc
  rdoc
  rubygems
)
_default_tool_gems_bins=(
  bundle
  bundler
  erb
  gem
  irb
  racc
  rdoc
  ri
)

build() {
  cd "ruby-${pkgver}"

  # this uses malloc_usable_size, which is incompatible with fortification level 3
  export CFLAGS="${CFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"
  export CXXFLAGS="${CXXFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"

  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --sharedstatedir=/var/lib \
    --libexecdir=/usr/lib/ruby \
    --enable-shared \
    --disable-rpath \
    --with-dbm-type=gdbm_compat

  make
  make rdoc capi
}

check() {
  cd "ruby-${pkgver}"

  # this uses malloc_usable_size, which is incompatible with fortification level 3
  export CFLAGS="${CFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"
  export CXXFLAGS="${CXXFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"

  make check
}

package_ruby() {
  depends=(
    gcc-libs
    gdbm
    glibc
    gmp
    libffi
    libxcrypt
    libyaml
    openssl
    readline
    zlib
  )
  optdepends=(
    'tk: for Ruby/TK'
    'ruby-docs: Documentation for Ruby'
    'ruby-default-gems: Default gems which are part of Ruby StdLib'
    'ruby-bundled-gems: Bundled gems which are part of Ruby StdLib'
    'ruby-stdlib: Full Ruby StdLib including default gems, bundled gems and tools'
  )
  provides=(
    libruby.so
  )
  replaces=(
    ruby-abbrev
    ruby-base64
    ruby-benchmark
    ruby-bigdecimal
    ruby-cgi
    ruby-csv
    ruby-date
    ruby-delegate
    ruby-did_you_mean
    ruby-digest
    ruby-drb
    ruby-english
    ruby-etc
    ruby-fcntl
    ruby-fiddle
    ruby-fileutils
    ruby-find
    ruby-forwardable
    ruby-getoptlong
    ruby-io-console
    ruby-io-nonblock
    ruby-io-wait
    ruby-ipaddr
    ruby-json
    ruby-logger
    ruby-mutex_m
    ruby-net-http
    ruby-open-uri
    ruby-psych
    ruby-reline
    ruby-ruby2_keywords
    ruby-set
    ruby-stringio
    ruby-time
    ruby-tmpdir
    ruby-uri
  )
  conflicts=("${replaces[@]}")
  provides+=("${_default_gems[@]/#/ruby-}")

  cd "ruby-${pkgver}"

  make DESTDIR="${pkgdir}" install-nodoc

  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
  install --verbose -D --mode=0644 *.md --target-directory "${pkgdir}/usr/share/doc/${pkgname}"

  # remove unrepreducible files
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/cache"

  # bootstrap switch
  if (( _bootstrap )); then
    # provide everything for a bootstrap build
    # use a reference to provides to srcinfo generation isn't confused
    declare -n bootstrap_provides=provides
    bootstrap_provides+=("${_default_tool_gems[@]/#/ruby-}" rubygems)
    bootstrap_provides+=("${_bundled_gems[@]/#/ruby-}")
    declare -n bootstrap_conflicts=conflicts
    bootstrap_conflicts+=("${_default_tool_gems[@]/#/ruby-}" rubygems)
    bootstrap_conflicts+=("${_bundled_gems[@]/#/ruby-}")
  else
    # remove de-vendored parts
    _remove_default_tool_gems
    _remove_bundled_gems
    # add standard dependencies
    depends+=(
      rubygems
    )
  fi
}

# remove bundled gems - they are provided as dedicated packages
_remove_bundled_gems() {
  local gem bin
  for gem in "${_bundled_gems[@]}"; do
    msg2 "removing bundled gem ${gem}"
    rm --recursive --verbose \
      "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/gems/${gem}"-* \
      "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/specifications/${gem}"-*.gemspec
    rm --recursive --verbose --force \
      "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/extensions"/*-linux/"${_rubyver}/${gem}"-*
  done
  for bin in "${_bundled_gems_bins[@]}"; do
    rm --recursive --verbose "${pkgdir}/usr/bin/${bin}"
    rm --recursive --verbose --force "${pkgdir}/usr/share/man/man1/${bin}.1"
  done

}

# remove default tool gems - they are provided as dedicated packages
_remove_default_tool_gems() {
  local gem bin
  for gem in "${_default_tool_gems[@]}"; do
    msg2 "removing default gem ${gem}"
    rm --recursive --verbose \
      "${pkgdir}/usr/lib/ruby/${_rubyver}/${gem}"*
    if [[ ${gem} != rubygems ]]; then
      rm --recursive --verbose \
        "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/gems/${gem}"-* \
        "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/specifications/default/${gem}"-*.gemspec
    fi
    rm --recursive --verbose --force \
      "${pkgdir}/usr/lib/ruby/${_rubyver}"/*-linux/"${gem}"
  done
  for bin in "${_default_tool_gems_bins[@]}"; do
    rm --recursive --verbose "${pkgdir}/usr/bin/${bin}"
    rm --recursive --verbose --force "${pkgdir}/usr/share/man/man1/${bin}.1"
  done
}

package_ruby-docs() {
  pkgdesc='Documentation files for Ruby'

  cd "ruby-${pkgver}"
  make DESTDIR="${pkgdir}" install-doc install-capi
  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_ruby-bundled-gems() {
  pkgdesc='Bundled gems which are part of Ruby StdLib'
  replaces=(ruby-bundledgems)
  conflicts=(ruby-bundledgems)
  depends=("${_bundled_gems[@]/#/ruby-}")

  cd "ruby-${pkgver}"
  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_ruby-default-gems() {
  pkgdesc='Default gems which are part of Ruby StdLib'
  depends=("${_default_tool_gems[@]/#/ruby-}")

  cd "ruby-${pkgver}"
  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_ruby-stdlib() {
  pkgdesc='Full Ruby StdLib including default gems, bundled gems and tools'
  depends=(ruby-default-gems ruby-bundled-gems)

  cd "ruby-${pkgver}"
  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: tabstop=2 shiftwidth=2 expandtab:
