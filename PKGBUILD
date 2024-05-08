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
  'ruby-bundledgems'
  'ruby-docs'
)
pkgver=3.2.4
pkgrel=0
arch=('x86_64')
url='https://www.ruby-lang.org/en/'
license=('BSD' 'custom')
makedepends=('doxygen' 'graphviz' 'libyaml' 'rust' 'tk')
checkdepends=('inetutils' 'procps-ng')
options=('!emptydirs')
source=(
  "https://cache.ruby-lang.org/pub/ruby/${pkgver:0:3}/ruby-${pkgver}.tar.xz"
  ruby-3.2-openssl-3.3-fix.patch::https://github.com/ruby/ruby/commit/dd5e625d7bcb7dc849fdbc2ad8053f9c2724efb4.patch
)
sha512sums=('fb0af37be4b6ad7b98ab9f8a508952238ee68b5828e3926331e4db52e2ebc1e6046f31114069322db0cd3bea7c9b82ace91c8564573ddcfa1f960877b237dbff'
            '52351374fc9aa9c3576bfb4b62df1d1d8dbe7327270a4d1c5777d247a33d6e6528b08a537fc4c87d9d0cc54b4b9183848f6c54d54fc727871b3e511b7a73ddb7')
b2sums=('9c2300a958b03528d51f0d74a069c8c538ca4009835d55377509a000bcfb43893a8a80d8fda57011e77c72e6283cb259281d5ba7b37444546e49f2a9ad515cf3'
        '1ee662e57f9f29b4ab29b391b38b988a8b5c199e62c815353c3a47e6eceea910344c7d9a00512916e05b6404efddf941313dfdcb0bec027f7f668443309228b9')
_rubyver="${pkgver:0:3}.0"
_bootstrap=1

prepare() {
  cd "ruby-${pkgver}"

  # ignore test_session_reuse_but_expire test for openssl version 3.3
  sed -i "s/3.2./3.3./g" test/net/http/test_https.rb

  patch -Np1 < ../ruby-3.2-openssl-3.3-fix.patch
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
    'ruby-bundledgems'
  )
  replaces=(
    'ruby-stdlib'

    'ruby-abbrev'
    'ruby-base64'
    'ruby-benchmark'
    'ruby-bigdecimal'
    'ruby-cgi'
    'ruby-csv'
    'ruby-date'
    'ruby-delegate'
    'ruby-did_you_mean'
    'ruby-digest'
    'ruby-drb'
    'ruby-english'
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
    'ruby-json'
    'ruby-logger'
    'ruby-mutex_m'
    'ruby-net-http'
    'ruby-open-uri'
    'ruby-psych'
    'ruby-racc'
    'ruby-reline'
    'ruby-ruby2_keywords'
    'ruby-set'
    'ruby-stringio'
    'ruby-time'
    'ruby-tmpdir'
    'ruby-uri'
  )
  provides=(
    libruby.so
    'ruby-abbrev'
    'ruby-base64'
    'ruby-benchmark'
    'ruby-bigdecimal'
    'ruby-cgi'
    'ruby-csv'
    'ruby-date'
    'ruby-delegate'
    'ruby-did_you_mean'
    'ruby-digest'
    'ruby-drb'
    'ruby-english'
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
  )
  bootstrap_gems=(
    ruby-bundler
    ruby-erb
    ruby-irb
    ruby-rdoc
    ruby-rake
    ruby-minitest
    ruby-power_assert
    ruby-test-unit
    rubygems
  )

  cd "ruby-${pkgver}"

  make DESTDIR="${pkgdir}" install-nodoc

  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
  install --verbose -D --mode=0644 *.md --target-directory "${pkgdir}/usr/share/doc/${pkgname}"

  # remove unrepreducible files
  rm --recursive --verbose \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}/cache"

  if (( _bootstrap )); then
    provides+=("${bootstrap_gems[@]}")
  else
    _remove_binary_default_gems
    _remove_bundled_gems
  fi
}

_remove_bundled_gems() {
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

_remove_binary_default_gems() {
  ## bundler
  rm --recursive --verbose \
    "${pkgdir}"/usr/bin/{bundle,bundler} \
    "${pkgdir}/usr/lib/ruby/${_rubyver}"/bundler* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/bundler-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/default/bundler-*.gemspec

  ## erb
  rm --recursive --verbose \
    "${pkgdir}/usr/bin/erb" \
    "${pkgdir}/usr/lib/ruby/${_rubyver}"/erb* \
    "${pkgdir}/usr/lib/ruby/${_rubyver}/x86_64-linux/erb" \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/erb-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/default/erb-*.gemspec \
    "${pkgdir}/usr/share/man/man1/erb.1"

  ## irb
  rm --recursive --verbose \
    "${pkgdir}/usr/bin/irb" \
    "${pkgdir}/usr/lib/ruby/${_rubyver}"/irb* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/irb-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/default/irb-*.gemspec \
    "${pkgdir}/usr/share/man/man1/irb.1"

  ## rdoc
  rm --recursive --verbose \
    "${pkgdir}"/usr/bin/{rdoc,ri} \
    "${pkgdir}/usr/lib/ruby/${_rubyver}"/rdoc* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/gems/rdoc-* \
    "${pkgdir}/usr/lib/ruby/gems/${_rubyver}"/specifications/default/rdoc-*.gemspec \
    "${pkgdir}/usr/share/man/man1/ri.1"

  ## rubygems
  rm --recursive --verbose \
    "${pkgdir}/usr/bin/gem" \
    "${pkgdir}/usr/lib/ruby/${_rubyver}"/rubygems*
}

package_ruby-docs() {
  pkgdesc='Documentation files for ruby'

  cd "ruby-${pkgver}"

  make DESTDIR="${pkgdir}" install-doc install-capi

  install --verbose -D --mode=0644 BSDL COPYING --target-directory "${pkgdir}/usr/share/licenses/${pkgname}"
}

package_ruby-bundledgems() {
  pkgdesc='Ruby Gems (third-party libraries) that are installed by default when Ruby is installed'

  depends=(
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
}

# vim: tabstop=2 shiftwidth=2 expandtab:
