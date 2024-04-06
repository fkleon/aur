# Maintainer: Frederik Leonhardt <frederik at leonhardt dot co dot nz>
pkgname=('bluebrick-extras-official'
		 'bluebrick-extras-thirdparty')
pkgbase=bluebrick-extras
pkgver=1.1
pkgrel=2
pkgdesc="Extra parts for BlueBrick Lego Layout Planer"
arch=('any')
url="https://bluebrick.lswproject.com"
license=('GPL-3.0-only')
depends=('bluebrick')
source=("https://bluebrick.lswproject.com/download/package/Train.1.0.zip"
        "https://bluebrick.lswproject.com/download/package/Town.1.1.zip"
        "https://bluebrick.lswproject.com/download/package/Vehicle.1.0.zip"
        "https://bluebrick.lswproject.com/download/package/Space.1.0.zip"
        "https://bluebrick.lswproject.com/download/package/Castle.1.1.zip"
        "https://bluebrick.lswproject.com/download/package/Duplo.1.0.zip"
        "https://bluebrick.lswproject.com/download/package/TrixBrix.1.7.0.zip"
        "https://bluebrick.lswproject.com/download/package/BrickTracks.1.1.zip"
        "10246-1.set.xml.patch")
sha256sums=('0602ab842f851594cd9e6d0b913a02fcdb2bc4265fb4471203b8a86692488a8f'
            'cdd2ff12cb1974e76c5fc94f4826828b641dfe90132e4a831e77849e973ed645'
            'b6b96342586907a0f787653ff01000ecfe9c8bff62de0cd5d169c0bb29a647e1'
            'eecedeed95f9312b1506561fcfa99e102e39b62458188293ad38db0ffed1102a'
            '02d910a7f37760b6b6fb0be561c14284ef6734dcb26acb78520bc2896a00b286'
            '0b3029d9dfbe8602f77ef3845e5e27a9f145764301bcb1ae32202f139e44a6e8'
            'b401b0307e651caaba1dd8ee86458f897c81404cda2c12bed1c9cba9cafd7856'
            'e25ab99a02fcd6ae02828fc00e7bc8b00cedcb52778f25940da36fbfc269aac4'
            'fbb7ad0a0bd5aa84f5cc2837b52035a9215bfea91e433f03420f9a8189dacc0f')

prepare() {
    # Fix encoding of file contents
    patch --forward --strip=0 --input=10246-1.set.xml.patch
}

package_bluebrick-extras-official() {
	pkgdesc="BlueBrick Lego Layout Planer - Official Extra Parts"

	local partsdir='/opt/bluebrick/parts/'
	local item
	local extras=(
		Train/
		Town/
		Vehicle/
		Space/
		Castle/
		Duplo/
	)

	install -Ddm757 "$pkgdir/$partsdir"

	for item in "${extras[@]}" ; do
		cp -r "$srcdir/$item" "$pkgdir/$partsdir/"
	done
}

package_bluebrick-extras-thirdparty() {
	pkgdesc="BlueBrick Lego Layout Planer - Third Party Extra Parts"
	license=('unknown')

	local partsdir='/opt/bluebrick/parts/'
	local item
	local extras=(
    	TrixBrix/
    	BrickTracks/
  	)

	install -Ddm757 "$pkgdir/$partsdir"

	for item in "${extras[@]}" ; do
		cp -r "$srcdir/$item" "$pkgdir/$partsdir/"
	done
}
