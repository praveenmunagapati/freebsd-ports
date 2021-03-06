# Created by: David O'Brien <obrien@cs.ucdavis.edu>
# $FreeBSD$

PORTNAME=	vim
PORTVERSION=	8.0.1231
DISTVERSIONPREFIX=	v
PORTREVISION=	2
CATEGORIES=	editors

MAINTAINER=	adamw@FreeBSD.org
COMMENT?=	Improved version of the vi editor

LICENSE=	VIM
LICENSE_NAME=	VIM License
LICENSE_FILE=	${WRKSRC}/runtime/doc/uganda.txt
LICENSE_PERMS=	dist-mirror dist-sell pkg-mirror pkg-sell auto-accept

CONFLICTS_INSTALL?=	vim-lite-[0-9]*

USES=		cpe iconv ncurses pkgconfig shebangfix
MAKE_JOBS_UNSAFE=	yes

USE_GITHUB=	yes
SHEBANG_FILES=	runtime/tools/demoserver.py runtime/tools/efm_perl.pl
CPE_VERSION=	${PORTVERSION:R}
PORTSCOUT=	site:https://github.com/vim/vim/releases

PLIST_SUB=	VIM_VER=${VIM_VER}
PORTDATA=	${VIM_VER}
SLAVEDIRS=	editors/vim-lite
REINPLACE_ARGS=	-i ''
VIM_VER=	${PORTNAME}${PORTVERSION:R:S|.||g}

ALL_TARGET=	# empty
MAKE_ARGS+=	CC="${CC}" \
		CONF_ARGS="--prefix=${PREFIX}" \
		STRIP="${STRIP_CMD}" \
		VIMRUNTIMEDIR=${PREFIX}/share/vim/${VIM_VER} \
		VIMRCLOC=${ETCDIR} \
		CONF_OPT_MULTIBYTE=--enable-multibyte \
		CONF_TERM_LIB=--with-tlib=ncurses \
		CONF_OPT_PYTHON="${CONF_OPT_PYTHON}"

# OPTIONS
OPTIONS_DEFAULT=	CSCOPE DEFAULT_VIMRC EXUBERANT_CTAGS GTK2 PERL PYTHON2 RUBY
OPTIONS_DEFINE=		CSCOPE DEFAULT_VIMRC EXUBERANT_CTAGS NLS XTERM_SAVE
OPTIONS_SINGLE=		UI
OPTIONS_SINGLE_UI=	ATHENA CONSOLE GNOME GTK2 GTK3 MOTIF X11
OPTIONS_GROUP=		LANGBIND
OPTIONS_GROUP_LANGBIND=	LUA PERL PYTHON2 PYTHON3 RUBY TCL
OPTIONS_SUB=		yes

.if defined(LITE)
OPTIONS_DEFAULT=	DEFAULT_VIMRC
OPTIONS_SLAVE=		CONSOLE
# Exclude everything except the two options above
OPTIONS_EXCLUDE:=	${OPTIONS_DEFINE:NDEFAULT_VIMRC} \
			${OPTIONS_SINGLE_UI:NCONSOLE} \
			${OPTIONS_GROUP_LANGBIND}
.endif

DEFAULT_VIMRC_DESC=	Install bundled vimrc as default setting
EXUBERANT_CTAGS_DESC=	Use exctags instead of ctags
XTERM_SAVE_DESC=	Restore xterm screen after exit

UI_DESC=		User interface
ATHENA_DESC=		Athena GUI toolkit
CSCOPE_DESC=		cscope support
CONSOLE_DESC=		Console/terminal mode

LANGBIND_DESC=		Optional language bindings

# BROKEN: ruby.h: error: wrong number of arguments specified for 'deprecated' attribute
OPTIONS_EXCLUDE_powerpc64=	RUBY

# GENERAL OPTIONS
CSCOPE_MAKE_ARGS=	CONF_OPT_CSCOPE=--enable-cscope
CSCOPE_MAKE_ARGS_OFF=	CONF_OPT_CSCOPE=--disable-cscope
CSCOPE_RUN_DEPENDS=	cscope:devel/cscope

EXUBERANT_CTAGS_RUN_DEPENDS=	exctags:devel/ctags

NLS_MAKE_ARGS=		CONF_OPT_NLS=--enable-nls
NLS_MAKE_ARGS_OFF=	CONF_OPT_NLS=--disable-nls
NLS_USES=		gettext

# UI
ATHENA_MAKE_ARGS=	CONF_OPT_GUI=--enable-gui=athena
ATHENA_PLIST_SUB=	GUI="" DESKTOP="@comment "
ATHENA_USE=		XORG=ice,sm,x11,xaw,xmu,xpm,xt

CONSOLE_MAKE_ARGS=	CONF_OPT_GUI="--enable-gui=no --without-x"
CONSOLE_MAKE_ARGS_OFF=	CONF_OPT_INPUT=--enable-xim \
			CONF_OPT_OUTPUT=--enable-fontset
CONSOLE_PLIST_SUB=	GUI="@comment " DESKTOP="@comment "

GNOME_MAKE_ARGS=	CONF_OPT_GUI=--enable-gui=gnome2
GNOME_PLIST_SUB=	GUI="" DESKTOP=""
GNOME_IMPLIES=		NLS
GNOME_USE=		GNOME=gdkpixbuf2,libgnomeui XORG=ice,sm,glproto,x11,xpm,xt
GNOME_USES=		desktop-file-utils
GNOME_VARS=		INSTALLS_ICONS=yes

GTK2_MAKE_ARGS=		CONF_OPT_GUI=--enable-gui=gtk2
GTK2_PLIST_SUB=		GUI="" DESKTOP=""
GTK2_USE=		GNOME=gdkpixbuf2,gtk20 XORG=ice,sm,x11,xpm,xt
GTK2_USES=		desktop-file-utils
GTK2_VARS=		INSTALLS_ICONS=yes

GTK3_MAKE_ARGS=		CONF_OPT_GUI=--enable-gui=gtk3
GTK3_PLIST_SUB=		GUI="" DESKTOP=""
GTK3_USE=		GNOME=cairo,gdkpixbuf2,gtk30 XORG=ice,sm,x11,xpm,xt
GTK3_USES=		desktop-file-utils
GTK3_VARS=		INSTALLS_ICONS=yes

MOTIF_MAKE_ARGS=	CONF_OPT_GUI='--enable-gui=motif --with-motif-lib="${MOTIFLIB}"' MOTIFHOME=${LOCALBASE}
MOTIF_PLIST_SUB=	GUI="" DESKTOP="@comment "
MOTIF_USES=		motif
MOTIF_USE=		XORG=ice,sm,x11,xmu,xt

X11_MAKE_ARGS=		CONF_OPT_GUI="--enable-gui=no --with-x"
X11_PLIST_SUB=		GUI="@comment " DESKTOP="@comment "
X11_USE=		XORG=ice,sm,x11,xt

# LANGUAGE BINDINGS
LUA_MAKE_ARGS=		CONF_OPT_LUA=--enable-luainterp=dynamic CONF_OPT_LUA_PREFIX=--with-lua-prefix=${LOCALBASE}
LUA_MAKE_ARGS_OFF=	CONF_OPT_LUA=--disable-luainterp
LUA_USES=		lua

PERL_MAKE_ARGS=		CONF_OPT_PERL=--enable-perlinterp
PERL_MAKE_ARGS_OFF=	CONF_OPT_PERL=--disable-perlinterp
PERL_USES=		perl5

PYTHON2_VARS=		CONF_OPT_PYTHON+=--enable-pythoninterp
PYTHON2_VARS_OFF=	CONF_OPT_PYTHON+=--disable-pythoninterp
PYTHON2_BUILD_DEPENDS=	python${PYTHON2_DEFAULT}:lang/python${PYTHON2_DEFAULT:S/.//}
PYTHON2_RUN_DEPENDS=	${PYTHON2_BUILD_DEPENDS}

PYTHON3_VARS=		CONF_OPT_PYTHON+=--enable-python3interp
PYTHON3_VARS_OFF=	CONF_OPT_PYTHON+=--disable-python3interp
PYTHON3_USES=		python:3.4+

RUBY_MAKE_ARGS=		CONF_OPT_RUBY=--enable-rubyinterp
RUBY_MAKE_ARGS_OFF=	CONF_OPT_RUBY=--disable-rubyinterp
RUBY_USE=		RUBY=yes

TCL_MAKE_ARGS=		CONF_OPT_TCL="--enable-tclinterp --with-tclsh=tclsh${TCL_VER}"
TCL_MAKE_ARGS_OFF=	CONF_OPT_TCL=--disable-tclinterp
TCL_USES=		tcl:85+

post-extract:
	${INSTALL_DATA} ${FILESDIR}/vietnamese_viscii.vim ${WRKSRC}/runtime/keymap

post-patch:
	@${ECHO_CMD} '#define SYS_VIMRC_FILE "'${ETCDIR}'/vimrc"' >> ${WRKSRC}/src/feature.h
	@${ECHO_CMD} '#define SYS_GVIMRC_FILE "'${ETCDIR}'/gvimrc"' >> ${WRKSRC}/src/feature.h
	@${REINPLACE_CMD} -e 's|-liconv|${ICONV_LIB}|g; s|/usr/local|${LOCALBASE}|g' \
		${WRKSRC}/src/auto/configure
# Work around qa-check shebang error
	@${REINPLACE_CMD} -e 1d ${WRKSRC}/runtime/tools/demoserver.py

pre-configure:
	@${CP} ${WRKSRC}/src/config.mk.dist ${WRKSRC}/src/auto/config.mk
	@${DO_MAKE_BUILD} -C ${WRKSRC}/src distclean

post-configure:
	@${DO_MAKE_BUILD} -C ${WRKSRC}/src scratch config
# Needed when devel/libsysinfo is installed:
	@${REINPLACE_CMD} -e '/#define HAVE_SYSINFO 1/ d' ${WRKSRC}/src/auto/config.h

post-install:
	@${RM} ${STAGEDIR}${PREFIX}/bin/ex
	@${RM} ${STAGEDIR}${PREFIX}/bin/view
.for F in eview evim gview gvim gvimdiff rgview rgvim rview rvim vimdiff
	${LN} -sf vim ${STAGEDIR}${PREFIX}/bin/$F
.endfor

# OPTIONS
post-patch-EXUBERANT_CTAGS-off:
	@${FIND} ${WRKSRC}/runtime/ -name 'menu*.vim' -print0 | ${XARGS} -0 ${REINPLACE_CMD} -Ee 's!ctags -R ?\.!${FIND} . -type f \\| ${XARGS} ctags!g'

post-patch-EXUBERANT_CTAGS-on:
	@${FIND} ${WRKSRC}/runtime/ -name 'menu*.vim' -print0 | ${XARGS} -0 ${REINPLACE_CMD} -e 's|ctags -R|exctags -R|g'

post-patch-LUA-on:
	@${REINPLACE_CMD} -e 's|set dummy lua;|set dummy ${LUA_CMD};|g' ${WRKSRC}/src/auto/configure

post-patch-XTERM_SAVE-on:
	@${REINPLACE_CMD} -e '/FEAT_XTERM_SAVE/ s|.*|#define FEAT_XTERM_SAVE|' ${WRKSRC}/src/feature.h

post-install-DEFAULT_VIMRC-on:
	@${MKDIR} ${STAGEDIR}${ETCDIR}
	${SED} -e '/set nocompatible/d' ${FILESDIR}/vimrc > ${STAGEDIR}${ETCDIR}/gvimrc.sample
	${INSTALL_DATA} ${FILESDIR}/vimrc ${STAGEDIR}${ETCDIR}/vimrc.sample

post-install-NLS-off:
	@${MKDIR} ${STAGEDIR}${DATADIR}/${VIM_VER}/lang
	@${MKDIR} ${STAGEDIR}${DATADIR}/${VIM_VER}/keymap
	${INSTALL_DATA} ${WRKSRC}/runtime/keymap/* ${STAGEDIR}${DATADIR}/${VIM_VER}/keymap

.include <bsd.port.mk>
