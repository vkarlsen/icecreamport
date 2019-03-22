# $FreeBSD$

PORTNAME=		icecream
PORTVERSION=		1.2
CATEGORIES=		devel

MAINTAINER=		vidar@karlsen.tech
COMMENT=		Distribute compilation of code acrosss machines on a network

LICENSE=		GPLv2
LICENSE_FILE=		${WRKSRC}/COPYING

BUILD_DEPENDS=		gcc:lang/gcc docbook2man:textproc/docbook2X
LIB_DEPENDS=		liblzo2.so:archivers/lzo2 #libpopt.so:devel/popt
RUN_DEPENDS=		bash:shells/bash

GNU_CONFIGURE=		yes
CONFIGURE_ARGS+=	LDFLAGS="-L/usr/lib -L${PREFIX}/lib" \
			CXXFLAGS="-I/usr/include -I${PREFIX}/include"
USES=			autoreconf libtool gmake shebangfix #alias pkgconfig
SHEBANG_FILES=		client/icecc-create-env.in client/icecc-test-env.in
USE_GITHUB=		yes
GH_ACCOUNT=		icecc

USE_GCC=		yes

GROUPS=			icecc
USERS=			icecc

MAN_FILES=		icecc-create-env.1 icecc-scheduler.1 icecc.1 iceccd.1
DOC_FILES=		AUTHORS BENCH COPYING ChangeLog INSTALL NEWS README README.md TODO

OPTIONS_DEFINE=		DOCS
OPTIONS_DEFAULT=	#########DOCS

do-install:
	# Install services/
	cd ${WRKSRC}/services && ${SH} ../libtool --mode=install /usr/bin/install -c libicecc.la '${STAGEDIR}${PREFIX}/lib'
	@${MKDIR} ${STAGEDIR}${PREFIX}/include/icecc
	cd ${WRKSRC}/services && ${INSTALL_DATA} job.h comm.h logging.h '${STAGEDIR}${PREFIX}/include/icecc'
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/pkgconfig
	cd ${WRKSRC}/services && ${INSTALL_DATA} icecc.pc '${STAGEDIR}${PREFIX}/lib/pkgconfig'

	# Install daemon/
	cd ${WRKSRC}/daemon && ${SH} ../libtool --mode=install install -s -m 555 iceccd '${STAGEDIR}${PREFIX}/sbin'

	# Install client/
	cd ${WRKSRC}/client && ${SH} ../libtool --mode=install install  -s -m 555 icecc '${STAGEDIR}${PREFIX}/bin'
	cd ${WRKSRC}/client && ${INSTALL_SCRIPT} icecc-create-env icecc-test-env ${STAGEDIR}${PREFIX}/bin

	# Install man pages
	cd ${WRKSRC}/doc && ${INSTALL_MAN} ${MAN_FILES} ${STAGEDIR}${MANPREFIX}/man/man1
	cd ${WRKSRC}/doc && ${INSTALL_MAN} icecream.7 ${STAGEDIR}${MANPREFIX}/man/man7

do-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC} && ${INSTALL_DATA} ${DOC_FILES} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
