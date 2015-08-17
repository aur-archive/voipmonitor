# Maintainer: Andrey Mivrenik <gim at fastmail dot fm>
# Contributor: Lex Black <autumn-wind at web dot de>
# Contributor: Xavier Devlamynck <magicrhesus@ouranos.be>
pkgname=voipmonitor
pkgver=11.0.6
pkgrel=1
pkgdesc="Live network packet sniffer and call recorder which analyzes SIP/RTP/RTCP protocols."
arch=('i686' 'x86_64')
url="http://www.voipmonitor.org/"
license=('GPL2')
depends=('libogg' 'libpcap' 'libvorbis' 'snappy' 'libssh' 'json-c' 'zlib' 'unixodbc' 'rrdtool' 'mysql++' 'asterisk')
backup=('etc/voipmonitor.conf')
source=("http://downloads.sourceforge.net/project/$pkgname/${pkgver%.*}/$pkgname-$pkgver-src.tar.gz"
        "$pkgname.service")
install="$pkgname.install"
changelog="ChangeLog"
sha256sums=('2e8b4a9255dd2f74c72cef0e06b267f41077b7ed0e38e50f55b035f65c712a2f'
            '13c3dc76199a3e8b5e0922f00064899070bceb77318bdc6c3ed8627b3c94db30')

prepare() {
  cd "${srcdir}/${pkgname}-${pkgver}-src"
  sed -i "s/-ljson/-ljson-c/g" configure
  sed -i "s/-ljson/-ljson-c/g" Makefile.in
  sed -i "s/<json/<json-c/g" tools.cpp
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}-src"
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}-src"

  # installing voipmonitor
  install -d "$pkgdir/usr/bin/"
  install -Dm755 "voipmonitor" "$pkgdir/usr/bin/"

  # installing config file
  install -d "$pkgdir/etc/"
  install -Dm644 "config/voipmonitor.conf" "$pkgdir/etc/"
  
  # installing service file
  install -d "$pkgdir/usr/lib/systemd/system/"
  install -Dm644 "$srcdir/$pkgname.service" "$pkgdir/usr/lib/systemd/system/$pkgname.service"
  
  # installing additional directories
  install -d "$pkgdir/var/spool/voipmonitor"
}

# vim:set ts=2 sw=2 et:
