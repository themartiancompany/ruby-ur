# Maintainer: Anatol Pomozov <anatol.pomozov@gmail.com>
# Maintainer: Andreas 'Segaja' Schleifer <segaja at archlinux dot org>
# Maintainer: Tim Meusel <tim@bastelfreak.de>
# Contributor: Thomas Dziedzic <gostrc@gmail.com>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: John Proctor <jproctor@prium.net>
# Contributor: Jeramy Rutley <jrutley@gmail.com>

# Do not re-package default gems (see https://stdgems.org/). Trying to do that will lead to multiple problems

pkgname=(
  'ruby'
  'ruby-docs'
)
pkgver=3.2.3
pkgrel=1
arch=('x86_64')
url='https://www.ruby-lang.org/en/'
license=('BSD' 'custom')
makedepends=('doxygen' 'graphviz' 'libyaml' 'rust' 'tk')
checkdepends=('inetutils' 'procps-ng')
provides=('libruby.so')
options=('!emptydirs')
source=(
  "https://cache.ruby-lang.org/pub/ruby/${pkgver:0:3}/ruby-${pkgver}.tar.xz"
  "ruby_stop_so_duplication.patch"
  "gemrc"
)
sha512sums=('d2a1897c2f4e801a28acb869322abfee76775115016252cecad90639485ed51deda1446cb16edb387f10a2e188602d646ef9b008b57f27bd745071277c535f3b'
            '9919490bbf7dba979a1df7543e62eb3fca48e8a516e6b6ab0a73080952e1b58599b7f233259d122dc66bf93f032b434d70e0dd448a1cb86513f01acb51b2120e'
            '8cafd14d414ee3c16aa94f79072bc6c100262f925dc1300e785846c3fabbbbffc1356b8e2223af5684e3340c55032d41231179ffa948bb12e01dbae0f4131911')
b2sums=('e2cfa215b2cb910bac5f3b58edcdece91b21ffcfb6b4c183eec0c8502c320b78e7a8732c393b6e6a38dc9cfd81e129c00562d9be45f0deb36306ac81f96dcdc1'
        '8f9687ece02c0558fe485f48d1ab80cee9afee588edc94042bca27b6fefcab6cbe653c767bea9494e15d22fd6af3ea9e69d6a867a0d3c47ffb0533e92dc99693'
        'f90b5e5491dce39c9c1a0d473fdc896d67154fd781f5c7cca676d8081d3d9cef037d9c50cd8738cdf3b407300feacc9f05564424bfd9ec8ceacef58d24a399f6')
_rubyver="${pkgver:0:3}.0"

prepare() {
  cd "ruby-${pkgver}"

  patch --verbose --strip=1 --input="../ruby_stop_so_duplication.patch"

  # ignore test for openssl version 3.2.1
  sed -i "s/3.2.0/3.2.1/g" test/net/http/test_https.rb
}

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
}

check() {
  cd "ruby-${pkgver}"

  # this uses malloc_usable_size, which is incompatible with fortification level 3
  export CFLAGS="${CFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"
  export CXXFLAGS="${CXXFLAGS/_FORTIFY_SOURCE=3/_FORTIFY_SOURCE=2}"

  make check
}

package_ruby() {
  pkgdesc='An object-oriented language for quick and easy programming'
  depends=(
    'gdbm'
    'glibc'
    'gmp'
    'libffi'
    'libxcrypt'
    'libyaml'
    'openssl'
    'readline'
    'zlib'
  )
  optdepends=(
    'tk: for Ruby/TK'

    'ruby-debug'
    'ruby-matrix'
    'ruby-minitest'
    'ruby-net-ftp'
    'ruby-net-imap'
    'ruby-net-pop'
    'ruby-net-smtp'
    'ruby-power_assert'
    'ruby-prime'
    'ruby-rake'
    'ruby-rbs'
    'ruby-rexml'
    'ruby-rss'
    'ruby-test-unit'
    'ruby-typeprof'
  )
  replaces=(
    'ruby-bundledgems'
    'ruby-stdlib'

    'ruby-abbrev'
    'ruby-base64'
    'ruby-benchmark'
    'ruby-bigdecimal'
    'ruby-bundler'
    'ruby-cgi'
    'ruby-csv'
    'ruby-date'
    'ruby-delegate'
    'ruby-did_you_mean'
    'ruby-digest'
    'ruby-drb'
    'ruby-english'
    'ruby-erb'
    'ruby-etc'
    'ruby-fcntl'
    'ruby-fiddle'
    'ruby-fileutils'
    'ruby-find'
    'ruby-forwardable'
    'ruby-getoptlong'
    'ruby-io-console'
    'ruby-io-nonblock'
    'ruby-io-wait'
    'ruby-ipaddr'
    'ruby-irb'
    'ruby-json'
    'ruby-logger'
    'ruby-mutex_m'
    'ruby-net-http'
    'ruby-open-uri'
    'ruby-psych'
    'ruby-racc'
    'ruby-rdoc'
    'ruby-reline'
    'ruby-ruby2_keywords'
    'ruby-set'
    'ruby-stringio'
    'ruby-time'
    'ruby-tmpdir'
    'ruby-uri'
    'rubygems'
  )
  provides=(
    'ruby-abbrev'
    'ruby-base64'
    'ruby-benchmark'
    'ruby-bigdecimal'
    'ruby-bundler'
    'ruby-cgi'
    'ruby-csv'
    'ruby-date'
    'ruby-delegate'
    'ruby-did_you_mean'
    'ruby-digest'
    'ruby-drb'
    'ruby-english'
    'ruby-erb'
    'ruby-error_highlight'
    'ruby-etc'
    'ruby-fcntl'
    'ruby-fiddle'
    'ruby-fileutils'
    'ruby-find'
    'ruby-forwardable'
    'ruby-getoptlong'
    'ruby-io-console'
    'ruby-io-nonblock'
    'ruby-io-wait'
    'ruby-ipaddr'
    'ruby-irb'
    'ruby-json'
    'ruby-logger'
    'ruby-mutex_m'
    'ruby-net-http'
    'ruby-net-protocol'
    'ruby-nkf'
    'ruby-observer'
    'ruby-open-uri'
    'ruby-open3'
    'ruby-openssl'
    'ruby-optparse'
    'ruby-ostruct'
    'ruby-pathname'
    'ruby-pp'
    'ruby-prettyprint'
    'ruby-pstore'
    'ruby-psych'
    'ruby-racc'
    'ruby-rdoc'
    'ruby-readline'
    'ruby-readline-ext'
    'ruby-reline'
    'ruby-resolv'
    'ruby-resolv-replace'
    'ruby-rinda'
    'ruby-ruby2_keywords'
    'ruby-securerandom'
    'ruby-set'
    'ruby-shellwords'
    'ruby-singleton'
    'ruby-stringio'
    'ruby-strscan'
    'ruby-syntax_suggest'
    'ruby-syslog'
    'ruby-tempfile'
    'ruby-time'
    'ruby-timeout'
    'ruby-tmpdir'
    'ruby-tsort'
    'ruby-un'
    'ruby-uri'
    'ruby-weakref'
    'ruby-yaml'
    'ruby-zlib'
    'rubygems'
  )

  cd "ruby-${pkgver}"

  make DESTDIR="${pkgdir}" install-nodoc

  install --verbose -D --mode=0644 ../gemrc "${pkgdir}/etc/gemrc"
  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
  install --verbose -D --mode=0644 *.md --target-directory "${pkgdir}/usr/share/doc/${pkgname}"

  # remove unrepreducible files
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/cache"

  # remove bundled gems - they are provided as dedicated packages
  ## debug
  rm --recursive --verbose \
    "${pkgdir}/usr/bin/rdbg" \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/extensions/x86_64-linux/${_rubyver}"/debug-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/debug-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/debug-*.gemspec

  ## matrix
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/matrix-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/matrix-*.gemspec

  ## minitest
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/minitest-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/minitest-*.gemspec

  ## net-ftp
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/net-ftp-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/net-ftp-*.gemspec

  ## net-imap
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/net-imap-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/net-imap-*.gemspec

  ## net-pop
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/net-pop-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/net-pop-*.gemspec

  ## net-smtp
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/net-smtp-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/net-smtp-*.gemspec

  ## power_assert
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/power_assert-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/power_assert-*.gemspec

  ## prime
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/prime-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/prime-*.gemspec

  ## rake
  rm --recursive --verbose \
    "${pkgdir}/usr/bin/rake" \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/rake-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/rake-*.gemspec

  ## rbs
  rm --recursive --verbose \
    "${pkgdir}/usr/bin/rbs" \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/extensions/x86_64-linux/${_rubyver}"/rbs-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/rbs-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/rbs-*.gemspec

  ## rexml
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/rexml-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/rexml-*.gemspec

  ## rss
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/rss-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/rss-*.gemspec

  ## test-unit
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/test-unit-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/test-unit-*.gemspec

  ## typeprof
  rm --recursive --verbose \
    "${pkgdir}/usr/bin/typeprof" \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/typeprof-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/typeprof-*.gemspec
}

package_ruby-docs() {
  pkgdesc='Documentation files for ruby'

  cd "ruby-${pkgver}"

  make DESTDIR="${pkgdir}" install-doc install-capi

  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: tabstop=2 shiftwidth=2 expandtab:
