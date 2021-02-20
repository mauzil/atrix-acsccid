
pkgname=acsccid
pkgver=1.1.8
pkgrel=0
arch=('x86_64')
url="https://www.acs.com.hk/download-driver-unified/11929/ACS-Unified-PKG-Lnx-118-P.zip"
source=("https://www.acs.com.hk/download-driver-unified/12030/ACS-Unified-Driver-Lnx-Mac-118-P.zip")
sha512sums=("be8800815cfd392224c4990651bd627624a3bdd5ee1ba18f62c6302dc302256059f9fc22f922a77318562cb4f5875a8060b284e748867b6d9212a5c0f4a08d47")

ziproot="ACS-Unified-Driver-Lnx-Mac-118-P"
package="${pkgname}-${pkgver}"

prepare() {
	builddir=${srcdir}/${ziproot}
	cd ${builddir}
	tar jxfv ${package}.tar.bz2
	mkdir -p ${builddir}/build
	cd ${builddir}/build
	${builddir}/${package}/bootstrap
	${builddir}/${package}/configure

	export builddir
}

build() {
	echo "Build on ${builddir} *"
	make -C ${builddir}/build
}

package() {
	#builddir=${srcdir}/${ziproot}
	echo "Srcdir ${srcdir} *"
	echo "Pkgver ${pkgver} *"
	echo "Pkgname ${pkgname} *"
	echo "Builddir ${builddir} * "
	make -C ${builddir}/build   DESTDIR=${pkgdir} install	

	install -d -m 0755 ${pkgdir}/etc/udev/rules.d
	# srcdir /home/mauro/Progetti/BzTeam/Cards/lettori/acs122u/ACS-Unified-Driver-Lnx-Mac-118-P/src *
	#        /home/mauro/Progetti/BzTeam/Cards/lettori/acs122u/ACS-Unified-Driver-Lnx-Mac-118-P/src/ACS-Unified-Driver-Lnx-Mac-118-P/acsccid-1.1.8/src/
	#        /home/mauro/Progetti/BzTeam/Cards/lettori/acs122u/ACS-Unified-Driver-Lnx-Mac-118-P/src/ACS-Unified-Driver-Lnx-Mac-118-P
	install -m 0644 ${builddir}/${pkgname}-${pkgver}/src/92_pcscd_acsccid.rules ${pkgdir}/etc/udev/rules.d
}

