
SCRIPTSDIR?=	${PREFIX}/sbin

BUILDDIR=	.build

SCRIPTS=	${BUILDDIR}/pkg_fetch \
		${BUILDDIR}/pkg_glob \
		${BUILDDIR}/pkg_sort \
		${BUILDDIR}/pkgdb \
		${BUILDDIR}/pkgdu \
		${BUILDDIR}/portcvsweb \
		${BUILDDIR}/portsclean \
		${BUILDDIR}/portsdb \
		${BUILDDIR}/portupgrade \
		${BUILDDIR}/portversion
LINKS=		${SCRIPTSDIR}/pkg_glob		${SCRIPTSDIR}/pkg_deinstall \
		${SCRIPTSDIR}/pkgdb		${SCRIPTSDIR}/pkg_which \
		${SCRIPTSDIR}/portupgrade	${SCRIPTSDIR}/portinstall \
		${SCRIPTSDIR}/portcvsweb	${SCRIPTSDIR}/portsvnweb \
		${SCRIPTSDIR}/portsdb		${SCRIPTSDIR}/ports_glob

CLEANDIRS=	${BUILDDIR}

.for script in ${SCRIPTS}
${script}: ${script:T}
	${RUBY} -wc ${.ALLSRC}
	@${MKDIR} ${BUILDDIR}
	${RUBY} -pe ' \
		if $$. == 1; \
		 if /^#!/; \
		  $$_.sub!(/^#!\s*\S*(\benv\s+)?\bruby/, "#!${RUBY}"); \
		 else; \
		  $$_ = "#!${RUBY}\n" + $$_; \
		 end; \
		end' \
		${.ALLSRC} > ${.TARGET}
.endfor

.include <bsd.prog.mk>

.include "${.CURDIR}/../Makefile.compat"
