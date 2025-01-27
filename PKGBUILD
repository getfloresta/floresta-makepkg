pkgbase=Floresta
pkgname=('florestad')
pkgver=0.7.0
pkgrel=1
arch=('x86_64')
url="https://github.com/vinteumorg/floresta"
makedepends=(cargo clang cmake ffmpeg git mold)

license=('MIT')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/vinteumorg/Floresta/archive/refs/tags/$pkgver.tar.gz"
        "SHA256SUMS::https://github.com/vinteumorg/Floresta/releases/download/$pkgver/SHA256SUMS"
	      "SHA256SUMS.asc::https://github.com/vinteumorg/Floresta/releases/download/$pkgver/SHA256SUMS.asc"
        "floresta.sysusers"
        "floresta.tmpfiles"
        "floresta.service")

sha256sums=('733b1e2bcecfdf5ab552b81db428b125e6f8154cccfda69b5e746da7a4a0a322'
	    'd343ea63bbaba5e28d20f9074d42e59f63fdd1912a0151e6eb0bd1f2e93b8a50'
	    'aab81663ed2ff0c27b9e201a26bae323f6c257342be8ce6efc38350588e1c587'
	    'b142df68404b453c9c0c45937e1036dab09900fa23f9ccdf1ae307129eb83de9'
      '559e4fa9467603123aa513e8a4bb1e052757f5a55e9999ac324394bbbb4d5528'
      'e03b37517c949c013e32ac184139249b22b0f98c4bfcfa62cda6e47bf97b7929'
    )

validpgpkeys=('2C8E0F836FD7DBBBB9E9B2EF89964EC3AB22B2E3')
changelog=Changelog

build() {
  cd $pkgbase-$pkgver
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  RUSTFLAGS="-C link-arg=-fuse-ld=mold -C target-cpu=native"
  cargo build --release --bin florestad --bin floresta_cli --locked
}

package() {
  pkgdesc="Floresta is a lightweight, secure, and fast Bitcoin Implementation, written in Rust"
  backup=('etc/floresta/config.toml')
  provides=('floresta-cli')
  replaces=('floresta-cli')

  cd $pkgbase-$pkgver
  install -Dm755 -t "$pkgdir/usr/bin" \
    target/release/florestad \
    target/release/floresta_cli

  install -Dm644 $srcdir/floresta.service \
    "$pkgdir/usr/lib/systemd/system/floresta.service"
  install -Dm644 "$srcdir/floresta.sysusers" \
    "$pkgdir/usr/lib/sysusers.d/floresta.conf"
  install -Dm644 "$srcdir/floresta.tmpfiles" \
    "$pkgdir/usr/lib/tmpfiles.d/floresta.conf"
  install -Dm644 config.toml.sample \
    "$pkgdir/etc/florestad/config.toml"

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

