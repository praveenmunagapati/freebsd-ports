# Created by: Mikle Davidkin <skylord@vt.net.ru>
# $FreeBSD$

PORTNAME=	isp
PORTVERSION=	1.1
PORTREVISION=	3
CATEGORIES=	net-p2p
MASTER_SITES=	SF/verlihub/VH_ISP/${DISTVERSION}

MAINTAINER=	me@skylord.ru

BROKEN_armv6=		fails to configure: checking for VERLIHUB - version >= 0... no (see config.log)

PLUGIN_DESC=	ISP

PLIST_FILES=	share/verlihub/default_pi_isp.sql

.include "../verlihub-plugins/Makefile.plugins"
.include <bsd.port.mk>
