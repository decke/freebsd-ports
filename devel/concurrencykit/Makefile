PORTNAME=	concurrencykit
PORTVERSION=	0.6.0
CATEGORIES=	devel
MASTER_SITES=	http://concurrencykit.org/releases/ \
		http://repnop.org/releases/
DISTNAME=	ck-${PORTVERSION}

PATCH_SITES=	https://github.com/${PORTNAME}/ck/commit/
PATCHFILES=	999d4612e873bb19867ad1d7043c9c18c7c4d3b9.patch:-p1

MAINTAINER=	bofh@FreeBSD.org
COMMENT=	Lock-free data structures for high performance concurrent systems
WWW=		http://concurrencykit.org

LICENSE=	BSD2CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

ONLY_FOR_ARCHS=	aarch64 amd64 armv6 armv7 i386 powerpc powerpc64 powerpc64le

OPTIONS_DEFINE=		RTM VMAPACK
OPTIONS_DEFAULT=	VMAPACK

RTM_DESC=	Restricted Transactional Memory (x86_64 only)
VMAPACK_DESC=	Enable pointer packing

RTM_CONFIGURE_ON=	--enable-rtm
VMAPACK_CONFIGURE_ON=	--enable-pointer-packing

USES=		pkgconfig
USE_LDCONFIG=	yes
HAS_CONFIGURE=	yes

CONFIGURE_ARGS+=	--mandir=${PREFIX}/man

TEST_TARGET=	check

PLIST_SUB+=	VERSION=${PORTVERSION}

post-extract:
	${REINPLACE_CMD} -e 's|PKGCONFIG_DATA=@LIBRARY@|PKGCONFIG_DATA=${PREFIX}/libdata/|g' \
	${WRKSRC}/Makefile.in

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libck.so.${PORTVERSION}

.include <bsd.port.mk>
