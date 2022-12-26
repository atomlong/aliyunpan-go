pkgname=aliyunpan-go
pkgver=0.2.4
pkgrel=1
pkgdesc="阿里云盘命令行客户端，支持webdav文件服务，支持JavaScript插件，支持同步备份功能。 "
arch=('x86_64')
url="https://github.com/tickstep/aliyunpan"
license=('Apache-2.0')
makedepends=('go')
source=("https://github.com/tickstep/aliyunpan/archive/refs/tags/v$pkgver.tar.gz"
        aliyunpan.env
		aliyunpan@.service)
sha256sums=('8c4339b9316a0d73fd68c03ccc1c7e4d16c6cd75249497c76853fdc0449e8855'
            'ef96c705e57b9662928e29f0a4fdb2b17053958ff9900c6fe1646a1afbdec012'
			'6e9ebfea3915ccf266e992fe776594245123f8dfbfd68d482cd3768b7fbbb1d4')

build() {
  cd "$srcdir/aliyunpan-$pkgver"
  go build \
      -trimpath \
      -buildmode=pie \
      -mod=readonly \
      -modcacherw \
      -ldflags "-linkmode external -extldflags \"${LDFLAGS}\"" \
      .
}

package() {
  cd "$srcdir/aliyunpan-$pkgver"
  install -Dm755 aliyunpan "$pkgdir"/usr/bin/aliyunpan-go
  install -Dm644 docs/manual.md "$pkgdir"/usr/share/docs/aliyunpan-go/manual.md
  install -Dm644 $srcdir/aliyunpan.env "$pkgdir"/etc/default/aliyunpan.env
  install -Dm644 $srcdir/aliyunpan@.service "$pkgdir"/usr/lib/systemd/system/aliyunpan@.service
}
