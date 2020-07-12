pkgname=zotero
pkgver=5.0.88
pkgrel=1
pkgdesc="Zotero Standalone. Is a free, easy-to-use tool to help you collect, organize, cite, and share your research sources."
arch=('x86_64')
url="http://www.zotero.org/download"
license=('GPL3')
depends=('dbus-glib' 'gtk3' 'nss' 'libxt')

source=("Zotero-${pkgver}_linux_$CARCH.tar.bz2::https://www.zotero.org/download/client/dl?channel=release&platform=linux-$CARCH&version=${pkgver}"
	"zotero.desktop")

sha256sums=('c248bb3b5165f4b03c7e38673aa928f1f29796a8d8ba1b335699803c559529a7'
	    '2e700ebe97d332a894be80d232b037b0117d84b38c5fa99dffc727cb10918228')

package() {
  install -dDm755 "$pkgdir"/usr/{bin,lib/zotero}
  mv "$srcdir"/Zotero_linux-$CARCH/* "$pkgdir"/usr/lib/zotero
  ln -s /usr/lib/zotero/zotero "$pkgdir"/usr/bin/zotero
  install -Dm644 "$srcdir"/zotero.desktop "$pkgdir"/usr/share/applications/zotero.desktop
  # Copy zotero icons to a standard location
  install -Dm644 "$pkgdir"/usr/lib/zotero/chrome/icons/default/default16.png "$pkgdir"/usr/share/icons/hicolor/16x16/apps/zotero.png
  install -Dm644 "$pkgdir"/usr/lib/zotero/chrome/icons/default/default32.png "$pkgdir"/usr/share/icons/hicolor/32x32/apps/zotero.png
  install -Dm644 "$pkgdir"/usr/lib/zotero/chrome/icons/default/default48.png "$pkgdir"/usr/share/icons/hicolor/48x48/apps/zotero.png
  install -Dm644 "$pkgdir"/usr/lib/zotero/chrome/icons/default/default256.png "$pkgdir"/usr/share/icons/hicolor/256x256/apps/zotero.png
  # Disable APP update
  sed -i '/pref("app.update.enabled", true);/c\pref("app.update.enabled", false);' "$pkgdir"/usr/lib/zotero/defaults/preferences/prefs.js
  # No need to keep a shell around when launching Zotero
  sed -i -r 's/^("\$CALLDIR\/zotero-bin" -app "\$CALLDIR\/application.ini" "\$@")/exec \1/' "$pkgdir"/usr/lib/zotero/zotero
}
