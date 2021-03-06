dnl Process this file with autoconf to produce a configure script.

AC_PREREQ(2.63)
AC_INIT(ovis-ldms, 4.3.3, ovis-help@sandia.gov)
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_SRCDIR([src/core/ldms.h])
AC_CONFIG_AUX_DIR(config)
AM_CONFIG_HEADER(config.h)
AM_INIT_AUTOMAKE([foreign tar-pax])
m4_ifdef([AM_SILENT_RULES],
	 [AM_SILENT_RULES([yes])
])
AX_PREFIX_CONFIG_H_G(src/ovis-ldms-config.h,,,[
#ifndef OVIS_FLEX
/* If OVIS_LDMS_FLEXIBLE_ARRAY_MEMBER is undefined or 1, we use 0
   for flexible array size on non ISO C compilers,
   else we use empty [] per c99.
   If a compiler is found not supporting both flex arrays and
   0 size array declarations, it will need an OVIS_FLEX value of 1
   and all sizeof calls on the affected structures will need
   offsetof instead, as outlined in ac_c_flexible_array_member source.
*/
#if (OVIS_LDMS_FLEXIBLE_ARRAY_MEMBER + 0)
#define OVIS_FLEX 0
#else
#define OVIS_FLEX
#endif
/* A union of flexible array types is not allowed by gcc 4.
   If this changes in a future compiler, this define may need changing.
   The ldms metric value union needs this.
*/
#define OVIS_FLEX_UNION 0
#endif
])
AM_PROG_LIBTOOL
AC_LIB_RPATH

dnl Checks for programs
AC_PROG_CC
AC_PROG_CXX
AC_CHECK_SIZEOF(long)
AC_CHECK_SIZEOF(long double)

dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_C_FLEXIBLE_ARRAY_MEMBER

dnl change sharedstatedir default
test "$sharedstatedir" = '${prefix}/com' && sharedstatedir='${prefix}/var/lib'

OVIS_PKGLIBDIR
OPTION_DEFAULT_ENABLE([scripts], [ENABLE_SCRIPTS])
OPTION_DEFAULT_DISABLE([slurmtest], [ENABLE_SLURMTEST])
OPTION_DEFAULT_DISABLE([developer], [ENABLE_DEVELOPER])
OPTION_DOC
OPTION_DEFAULT_DISABLE([etc], [ENABLE_ETC])
OPTION_DEFAULT_DISABLE([ldms-test], [ENABLE_LDMS_TEST])

OPTION_DEFAULT_ENABLE([core], [ENABLE_CORE])
OPTION_DEFAULT_ENABLE([mmap], [ENABLE_MMAP])
OPTION_DEFAULT_ENABLE([perf], [ENABLE_PERF])
OPTION_DEFAULT_DISABLE([yaml], [ENABLE_YAML])

dnl Options for store
OPTION_DEFAULT_ENABLE([store], [ENABLE_STORE])
OPTION_DEFAULT_ENABLE([flatfile], [ENABLE_FLATFILE])
OPTION_DEFAULT_ENABLE([csv], [ENABLE_CSV])
OPTION_DEFAULT_DISABLE([rabbitkw], [ENABLE_RABBITKW])
OPTION_DEFAULT_DISABLE([rabbitv3], [ENABLE_RABBITV3])

dnl AMQP
OPTION_DEFAULT_DISABLE([amqp], [ENABLE_AMQP])

dnl Options for contributed stores
OPTION_DEFAULT_DISABLE([tutorial-store],[ENABLE_TUTORIAL_STORE])

OPTION_DEFAULT_DISABLE([gpcdlocal], [ENABLE_GPCDLOCAL],[Required access to gpcd-support repository])
OPTION_WITH_OR_BUILD([gpcdlocal],[../gpcd-support],[gpcd],[gpcdlocal.sh], ,[gpcd])
OPTION_DEFAULT_DISABLE([sos], [ENABLE_SOS])
OPTION_WITH_OR_BUILD([sos],[../sos],[sos/src sos/include ods/src ods/include])

dnl Options for consumer
OPTION_DEFAULT_DISABLE([me], [ENABLE_ME])
OPTION_WITH([me], [ME], [/usr/local])

dnl Options for sampler
OPTION_DEFAULT_ENABLE([sampler], [ENABLE_SAMPLER])
OPTION_DEFAULT_DISABLE([kgnilnd], [ENABLE_KGNILND])
OPTION_DEFAULT_ENABLE([lustre], [ENABLE_LUSTRE])
OPTION_DEFAULT_DISABLE([jobid], [ENABLE_JOBID])
OPTION_DEFAULT_ENABLE([clock], [ENABLE_CLOCK])
OPTION_DEFAULT_ENABLE([synthetic], [ENABLE_SYNTHETIC])
OPTION_DEFAULT_ENABLE([varset], [ENABLE_VARSET])
OPTION_DEFAULT_ENABLE([lnet_stats], [ENABLE_LNET_STATS])
OPTION_DEFAULT_ENABLE([meminfo], [ENABLE_MEMINFO])
OPTION_DEFAULT_DISABLE([filesingle], [ENABLE_FILESINGLE])
OPTION_DEFAULT_DISABLE([msr_interlagos], [ENABLE_MSR_INTERLAGOS])
OPTION_DEFAULT_ENABLE([array_example], [ENABLE_ARRAY_EXAMPLE])
OPTION_DEFAULT_DISABLE([perfevent], [ENABLE_PERFEVENT])
OPTION_DEFAULT_DISABLE([rapl], [ENABLE_RAPL])
OPTION_DEFAULT_DISABLE([hweventpapi], [ENABLE_HWEVENTPAPI])
OPTION_DEFAULT_DISABLE([mpi_sampler], [ENABLE_MPI_SAMPLER])
OPTION_DEFAULT_DISABLE([mpi_noprofile], [ENABLE_MPI_NOPROFILE])
if test -z "$ENABLE_MPI_SAMPLER_TRUE" ; then
	AX_MPI([:],[ AC_MSG_ERROR([MPICC required by mpi_sampler ])])
fi
OPTION_WITH([libpapi], [LIBPAPI])
OPTION_DEFAULT_ENABLE([procinterrupts], [ENABLE_PROCINTERRUPTS])
OPTION_DEFAULT_ENABLE([procnetdev], [ENABLE_PROCNETDEV])
OPTION_DEFAULT_ENABLE([procnfs], [ENABLE_PROCNFS])
OPTION_DEFAULT_ENABLE([dstat], [ENABLE_DSTAT])
OPTION_DEFAULT_ENABLE([procstat], [ENABLE_PROCSTAT])
OPTION_DEFAULT_ENABLE([llnl-edac], [ENABLE_LLNL_EDAC])
AM_CONDITIONAL([ENABLE_LLNL], [test "x$ENABLE_LLNL_EDAC_FALSE" = "x#"])
OPTION_DEFAULT_DISABLE([fptrans], [ENABLE_FPTRANS])

OPTION_DEFAULT_ENABLE([tsampler], [ENABLE_TSAMPLER])
OPTION_DEFAULT_ENABLE([cray_power_sampler], [ENABLE_CRAY_POWER_SAMPLER])
dnl cray_power_sampler won't build with --disable-tsampler

OPTION_DEFAULT_DISABLE([sysclassib], [ENABLE_SYSCLASSIB])
OPTION_DEFAULT_DISABLE([opa2], [ENABLE_OPA2])
OPTION_DEFAULT_ENABLE([vmstat], [ENABLE_VMSTAT])
OPTION_DEFAULT_ENABLE([procdiskstats], [ENABLE_PROCDISKSTATS])
OPTION_DEFAULT_DISABLE([cray_system_sampler], [ENABLE_CRAY_SYSTEM_SAMPLER])
dnl spaceless names in the cray_system_sampler. Default is with spaces for reverse compatibility
OPTION_DEFAULT_ENABLE([spaceless_names], [ENABLE_SPACELESS_NAMES])
dnl aries_mmr is not part of the cray_system_sampler
OPTION_DEFAULT_DISABLE([aries-mmr], [ENABLE_ARIES_MMR], [Requires --enable-gpcd or --with-aries-libgpcd=libdir,incdir])
dnl linkstatus is not part of the cray_system_sampler
OPTION_DEFAULT_DISABLE([aries_linkstatus], [ENABLE_ARIES_LINKSTATUS], [Requires gpcdr to be set up with status metrics])
OPTION_DEFAULT_DISABLE([atasmart], [ENABLE_ATASMART])
OPTION_DEFAULT_ENABLE([generic_sampler], [ENABLE_GENERIC_SAMPLER])
OPTION_DEFAULT_DISABLE([switchx], [ENABLE_SWITCHX])
OPTION_WITH([switchx], [SWITCHX],[/usr/local])
OPTION_DEFAULT_DISABLE([kokkos], [ENABLE_KOKKOS])
OPTION_DEFAULT_ENABLE([jobinfo-sampler], [ENABLE_JOBINFO])
OPTION_DEFAULT_DISABLE([jobinfo-slurm], [ENABLE_SLURM_JOBINFO])
OPTION_DEFAULT_DISABLE([spank-plugin], [ENABLE_SPANK_PLUGIN])
OPTION_DEFAULT_ENABLE([slurm-sampler], [ENABLE_SLURM_SAMPLER])
OPTION_DEFAULT_DISABLE([papi-sampler], [ENABLE_PAPI_SAMPLER])
OPTION_DEFAULT_DISABLE([ibm_occ], [ENABLE_IBM_OCC_SAMPLER])
OPTION_DEFAULT_DISABLE([appinfo], [ENABLE_APPINFO])
OPTION_DEFAULT_DISABLE([test_sampler], [ENABLE_TEST_SAMPLER])
dnl test_sampler will also build with --enable-ldms-test
AM_CONDITIONAL([ENABLE_TEST_SAMPLER_LDMS_TEST], [test "x$ENABLE_LDMS_TEST_FALSE" = "x#" -o "x$ENABLE_TEST_SAMPLER_FALSE" = "x#"])
OPTION_DEFAULT_DISABLE([grptest], [ENABLE_GRPTEST])
dnl grptest will also build with --enable-ldms-test
AM_CONDITIONAL([ENABLE_GRPTEST_LDMS_TEST], [test "x$ENABLE_LDMS_TEST_FALSE" = "x#" -o "x$ENABLE_GRPTEST_FALSE" = "x#"])

dnl options for contributed samplers
OPTION_DEFAULT_DISABLE([ipmireader], [ENABLE_IPMIREADER])
OPTION_DEFAULT_DISABLE([tutorial-sampler],[ENABLE_TUTORIAL_SAMPLER])

dnl check for libcurl if influx is configured
OPTION_DEFAULT_ENABLE([influx], [ENABLE_INFLUX])
if test -z "$ENABLE_INFLUX_TRUE"; then
	TMPLIBS="$LIBS"
	LIBS=""
	AC_CHECK_LIB(curl, curl_version, [],
		AC_MSG_ERROR([libcurl not found (required by influx).]))
	AC_CHECK_HEADER(curl/curl.h, [],
		AC_MSG_ERROR([`curl.h` not found (required by influx).]))
	LIBS="$TMPLIBS"
fi

OPTION_WITH([libpfm], [LIBPFM])
OPTION_DEFAULT_DISABLE([syspapi-sampler], [ENABLE_SYSPAPI_SAMPLER])
if test -z "$ENABLE_SYSPAPI_SAMPLER_TRUE" -o -z "$ENABLE_PAPI_SAMPLER_TRUE"; then
	TMPLIBS="$LIBS"
	TMPCFLAGS="$CFLAGS"
	LIBS=""
	AC_CHECK_LIB(papi, PAPI_library_init, [],
		AC_MSG_ERROR([libpapi not found (required by papi-sampler/syspapi-sampler).]),
		$LIBPAPI_LIBDIR_FLAG $LIBPAPI_LIB64DIR_FLAG)
	LIBS=""
	dnl Check headers
	CFLAGS=$LIBPAPI_INCDIR_FLAG
	AC_CHECK_HEADER(papi.h, [],
		AC_MSG_ERROR([`papi.h` not found (required by papi-sampler/syspapi-sampler).]))
	LIBS="$TMPLIBS"
	CFLAGS="$TMPCFLAGS"
fi

if test -z "$ENABLE_SYSPAPI_SAMPLER_TRUE"; then
	TMPLIBS="$LIBS"
	TMPCFLAGS="$CFLAGS"
	LIBS=""
	AC_CHECK_LIB(pfm, pfm_initialize, [],
		AC_MSG_ERROR([libpfm not found (required by syspapi-sampler).]),
		$LIBPFM_LIBDIR_FLAG $LIBPFM_LIB64DIR_FLAG)
	LIBS=""
	dnl Check headers
	CFLAGS=$LIBPFM_INCDIR_FLAG
	AC_CHECK_HEADER(perfmon/pfmlib_perf_event.h, [],
		AC_MSG_ERROR([`perfmon/pfmlib_perf_event.h` not found (required by syspapi-sampler).]))
	LIBS="$TMPLIBS"
	CFLAGS="$TMPCFLAGS"
fi

OPTION_DEFAULT_ENABLE([ldmsd], [ENABLE_LDMSD])

dnl if LEX and/or YACC are not available, the configure still won't fail
AC_PROG_LEX
AC_PROG_YACC
if test -z "$ENABLE_KOKKOS_TRUE"; then
	dnl kokkos needs sos (not the storesos).
	CHECK_SOS=1
fi

dnl Other libraries
OPTION_DEFAULT_DISABLE([gemini-gpcdr], [ENABLE_GEMINI_GPCDR]) dnl use gpcdr for gemini (not mutually exclusive)
OPTION_DEFAULT_DISABLE([aries-gpcdr], [ENABLE_ARIES_GPCDR]) dnl use gpcdr for aries (not mutually exclusive)

OPTION_DEFAULT_DISABLE([cray-nvidia], [ENABLE_CRAY_NVIDIA])
OPTION_DEFAULT_DISABLE([cray-nvidia-inc], [ENABLE_CRAY_NVIDIA_INC])
OPTION_WITH([cray-nvidia-inc], [CRAY_NVIDIA_INC]) dnl for the path to nvidia include

dnl Will need to have the NVIDIA library in the LD_LIBRARY_PATH
OPTION_DEFAULT_DISABLE([cray-hss-devel], [ENABLE_CRAY_HSS_DEVEL])
OPTION_WITH([cray-hss-devel], [CRAY_HSS_DEVEL],[/usr])

# for aries_mmr
OPTION_ARIES_MMR

dnl munge
OPTION_DEFAULT_DISABLE([munge], [ENABLE_MUNGE])
OPTION_WITH([munge], [MUNGE])

OPTION_DEFAULT_ENABLE([ovis-lib], [ENABLE_OVIS_LIB])
# OPTION_WITH_OR_BUILD([ovis-lib],[../lib/src],[mmalloc third coll ovis_util zap ovis_ctrl ovis_event ovis_auth third/json_parser],[ovis-auth.sh],[ovis-lib],[ovis_auth])
OPTION_WITH_OR_BUILD([ovis-lib],[../lib/src],[mmalloc third json tada coll ovis_util zap ovis_ctrl ovis_event ovis_auth third/json_parser],[ovis-auth.sh],[ovis-lib],[ovis_auth])
dnl substitute values we need from ovis-auth.sh during joint configure
AC_SUBST(OVIS_AUTH_LIBS)

if test $(echo ${OVIS_LIB_LIBDIR} | wc -w) -gt 1 ; then
	# building with top build
	ZAP_LIBPATH=${libdir}/ovis-lib
elif test -d ${OVIS_LIB_LIB64DIR}/ovis-lib ; then
	ZAP_LIBPATH=${OVIS_LIB_LIB64DIR}/ovis-lib
else
	ZAP_LIBPATH=${OVIS_LIB_LIBDIR}/ovis-lib
fi
ZAP_LIBPATH=${ZAP_LIBPATH#*/rpm7/BUILDROOT}
ZAP_LIBPATH=${ZAP_LIBPATH#*/tmproot}
AC_SUBST(ZAP_LIBPATH)
LDMSD_PLUGIN_LIBPATH=${pkglibdir}
AC_SUBST(LDMSD_PLUGIN_LIBPATH)

OPTION_DEFAULT_ENABLE([ldms-python], [ENABLE_LDMS_PYTHON])

dnl Check for pthread support
AC_CHECK_LIB(pthread, pthread_mutex_init, [],
    AC_MSG_ERROR([pthread library not found.  ldms requires libpthread.]))
dnl save LIBS variable.
TMPLIBS="$LIBS"
LIBS=""

dnl no clock_gettime on osx. see
dnl https://developer.apple.com/library/mac/qa/qa1398/_index.html
AC_SEARCH_LIBS([clock_gettime],[rt posix4],[LDFLAGS_GETTIME=$LIBS])
LIBS=""
AC_SUBST([LDFLAGS_GETTIME])

dnl Check for libreadline
AX_LIB_READLINE
LDFLAGS_READLINE=$LIBS
AC_SUBST([LDFLAGS_READLINE])
LIBS=$TMPLIBS

dnl Munge library check
if test -z "$ENABLE_MUNGE_TRUE"; then
	AC_CHECK_LIB(munge, munge_encode, [], AC_MSG_ERROR([libmunge not found]))
	dnl Reset LIBS variable.
	LIBS=""

	AC_CHECK_HEADER(munge.h, [], AC_MSG_ERROR([munge.h not found]))
fi

dnl Checks for libraries
if test -z "$ENABLE_SYSCLASSIB_TRUE"; then
	AC_CHECK_LIB(ibmad, mad_rpc_open_port, [],
		AC_MSG_ERROR([mad_rpc_open_port() function not found. sysclassib sampler
		  requires libibmad 1.3.]))
	dnl Reset LIBS variable.
	LIBS=""

	AC_CHECK_HEADER(infiniband/mad.h, [],
		AC_MSG_ERROR([<infiniband/mad.h> not found.  Is libibmad-dev or
			libibmad-devel installed?]))

	AC_CHECK_LIB(ibumad, umad_get_port, [],
		AC_MSG_ERROR([umad_get_port() function not found. sysclassib sampler
			requires libibumad.]))
	dnl Reset LIBS variable.
	LIBS=""

	AC_CHECK_HEADER(infiniband/umad.h, [],
		AC_MSG_ERROR([<infiniband/umad.h> not found.  Is libibumad-dev or
			libibumad-devel installed?]))
fi

dnl Checks for slurm includes
OPTION_WITH([slurm], [SLURM], [/usr])
if test -z "$ENABLE_SLURM_JOBINFO_TRUE"; then
	OCFLAGS=$CFLAGS
	CFLAGS=$SLURM_INCDIR_FLAG
	AC_CHECK_HEADER(slurm/spank.h, [],
		AC_MSG_ERROR([<slurm/spank.h> not found.
			slurm installed?]))
	CFLAGS=$OCFLAGS
fi

if test "x$WITH_OVIS_LIB" != "xbuild" && test -z "$ENABLE_TSAMPLER_TRUE"; then
	dnl tsampler uses ovis_event (from lib/)
	OCFLAGS=$CFLAGS
	CFLAGS=$OVIS_LIB_INCDIR_FLAG
	AC_CHECK_HEADERS(ovis_event/ovis_event.h, [],
			 AC_MSG_FAILURE([ovis_event/ovis_event.h not found.])
			 )
	AC_CHECK_LIB(ovis_event, ovis_scheduler_new, [],
		     AC_MSG_ERROR([ovis_event library not found.]),
		     [ $OVIS_LIB_LIB64DIR_FLAG  $OVIS_LIB_LIBDIR_FLAG ]
		    )
	CFLAGS=$OCFLAGS
	LIBS=""
fi

if test -z "$ENABLE_SOS_TRUE"; then
	CHECK_SOS=1
fi

if test -n "$CHECK_SOS"; then
	if test "x$WITH_SOS" != "xbuild"; then
		OCFLAGS=$CFLAGS
		CFLAGS=$SOS_INCDIR_FLAG
		AC_CHECK_HEADERS(sos/sos.h,
			[],
			AC_MSG_FAILURE([sos/sos.h not found])
		)
		AC_CHECK_LIB( sos, sos_container_open,
			[],
			AC_MSG_FAILURE(libsos not found: required by either --enable-sos or --enable-kokkos),
			[ $SOS_LIB64DIR_FLAG $SOS_LIBDIR_FLAG ]
		)
		CFLAGS=$OCFLAGS
		LIBS=""
	else
		AC_MSG_NOTICE([Using staged ovis-sos $OVIS_SOS_LIB64DIR_FLAG $OVIS_SOS_LIBDIR_FLAG])
	fi
fi

if test -z "$ENABLE_ATASMART_TRUE" ; then
	AC_CHECK_LIB(atasmart, sk_disk_smart_read_data, [],
		AC_MSG_ERROR([libatasmart not found. sampler_atasmart requires libatasmart and libatasmart-devel.]))
fi


if test -z "$ENABLE_RABBITV3_TRUE" -o -z "$ENABLE_RABBITKW_TRUE"; then
	AC_CHECK_LIB(rabbitmq, amqp_version, [],
		AC_MSG_ERROR([librabbitmq not found. store_rabbitv3 requires librabbitmq and amqp headers.]))
	AC_LANG_PUSH([C])
	AC_COMPILE_IFELSE([AC_LANG_PROGRAM(
[[#include <amqp.h>
#if ((AMQP_VERSION_MINOR < 7) && (AMQP_VERSION_MAJOR < 1))
#error "librabbitmq version < 0.7 not supported"
#endif
]])],
	[AC_DEFINE([HAVE_RABBITMQ],[],[Is librabbitmq >= 0.7.0 available?])],
	[ AC_MSG_ERROR([librabbitmq version > 0.7 not found])])
	AC_LANG_POP([C])
fi

if test -z "$ENABLE_YAML_TRUE"; then
	AC_CHECK_LIB(yaml, yaml_parser_load, [],
		AC_MSG_ERROR([libyaml not found. please add --disable-yaml to disable yaml support.]))
	dnl Reset LIBS variable.
	LIBS=""
fi

dnl Check for mmalloc
if test "x$WITH_OVIS_LIB" != "xbuild"; then
	AC_CHECK_LIB(mmalloc, mm_init, [],
		AC_MSG_ERROR([libmmalloc not found. Please install ovis-lib.]),
		$OVIS_LIB_LIB64DIR_FLAG  $OVIS_LIB_LIBDIR_FLAG )
	dnl Reset LIBS variable.
	LIBS=""


	AC_CHECK_LIB(coll, idx_create, [],
		AC_MSG_ERROR([libcoll not found. Please install ovis-lib.]),
		$OVIS_LIB_LIB64DIR_FLAG $OVIS_LIB_LIBDIR_FLAG)
	dnl Reset LIBS variable.
	LIBS=""
else
	AC_MSG_NOTICE([Using staged ovis-lib $OVIS_LIB_LIB64DIR_FLAG $OVIS_LIB_LIBDIR_FLAG for LDMS.])
fi

dnl LDMS Swig
OPTION_DEFAULT_DISABLE([swig], [ENABLE_SWIG])
if test -z "$ENABLE_SWIG_TRUE"; then
	AC_PROG_SWIG
	SWIG_PYTHON
fi

if test -z "$ENABLE_SWIG_TRUE" || test -z "$ENABLE_LDMS_PYTHON_TRUE"
then
	AM_PATH_PYTHON(2.6)
	pkgpythondir="${pythondir}/ovis_ldms"
	pkgpyexecdir="${pkgpythondir}"
	AX_PYTHON_MODULE_VERSION(["argparse"], 1.1, "python")
fi

OPTION_WITH_PORT([LDMSD],[411])

OPTION_WITH_MAGIC([LDMS_MSG_MAX],[32768],[Maximum control message length allowed to ldmsd (min 4095)])

dnl if cray_sampler set some other variables
if test "x$enable_cray_system_sampler" = "xyes"
then

	if test -z "$ENABLE_SPACELESS_NAMES_TRUE"; then
	   AC_DEFINE([HAVE_SPACELESS_NAMES],[1],[cray_system_sampler: Using spaceless names.])
	fi

	if !(test -z "$ENABLE_GEMINI_GPCDR_TRUE") && !(test -z "$ENABLE_ARIES_GPCDR_TRUE")
	then
		AC_MSG_ERROR([Must enable at least one of gemini-gpcdr, and aries-gpcdr.])
	fi

	if test -z "$ENABLE_GEMINI_GPCDR_TRUE"
	then
	gpcdrfile="/sys/devices/virtual/gni/gpcdr0/metricsets/links/metrics"
	if ! test -f $gpcdrfile; then
	   AC_MSG_WARN([
	 ++++++++++++++++++++++++++++++++++++++++++++
	   GEMINI gpcdr interface not available:
	   $gpcdrfile
	   We hope your runtime environment has it.
	 ++++++++++++++++++++++++++++++++++++++++++++
	  ])
	  fi
	  AC_MSG_RESULT([Building gpcdr interface for GEMINI HSN metrics.])
	fi

	if test -z "$ENABLE_ARIES_GPCDR_TRUE"
	then
	gpcdrfile1="/sys/devices/virtual/gni/gpcdr0/metricsets/linktraffic/metrics"
	gpcdrfile2="/sys/devices/virtual/gni/gpcdr0/metricsets/linkstalled/metrics"
	gpcdrfile3="/sys/devices/virtual/gni/gpcdr0/metricsets/linksendstatus/metrics"
	gpcdrfile4="/sys/devices/virtual/gni/gpcdr0/metricsets/linkrecvstatus/metrics"
	if !(test -f $gpcdrfile1) || !(test -f $gpcdrfile2) || !(test -f $gpcdrfile3) || !(test -f $gpcdrfile4)
	then
	   AC_MSG_WARN([
	 ++++++++++++++++++++++++++++++++++++++++++++
	   ARIES gpcdr interface not available:
	   $gpcdrfile1 $gpcdrfile2 $gpcdrfile3 $gpcdrfile4
	   We hope your runtime environment has it.
	 ++++++++++++++++++++++++++++++++++++++++++++
	  ])
	  fi
	  AC_MSG_RESULT([Building gpcdr interface for ARIES HSN metrics.])
	fi

	if test -z "$ENABLE_CRAY_NVIDIA_TRUE"
	then
	  AC_DEFINE([HAVE_CRAY_NVIDIA],[1],[cray_system_sampler: Including option for NVIDIA metrics.])
	  AC_MSG_RESULT([cray_system_sampler: Including option for NVIDIA metrics.])
	else
	  AC_MSG_RESULT([cray_system_sampler: Not including option for NVIDIA metrics.])
	fi

	if test -z "$ENABLE_LUSTRE_TRUE"
	then
		AC_DEFINE([HAVE_LUSTRE],[1],[cray_system_sampler: Include option for LUSTRE metrics.])
		AC_MSG_RESULT([cray_system_sampler: Including option for LUSTRE metrics.])
	else
		AC_MSG_RESULT([cray_system_sampler: Not including option for LUSTRE metrics.])
	fi
fi

dnl Reset LIBS variable.

LIBS=""



OPTION_GITINFO
OPTION_HOSTINFO

# define substitutions for configvars and other sed-generated files.
# note carefully the escapes.
OVIS_DO_SUBST([LDMS_SUBST_RULE], ["sed \
-e 's,[[@]]mandir[[@]],\$(mandir),g' \
-e 's,[[@]]localedir[[@]],\$(localedir),g' \
-e 's,[[@]]libdir[[@]],\$(libdir),g' \
-e 's,[[@]]psdir[[@]],\$(psdir),g' \
-e 's,[[@]]pdfdir[[@]],\$(pdfdir),g' \
-e 's,[[@]]dvidir[[@]],\$(dvidir),g' \
-e 's,[[@]]htmldir[[@]],\$(htmldir),g' \
-e 's,[[@]]infodir[[@]],\$(infodir),g' \
-e 's,[[@]]docdir[[@]],\$(docdir),g' \
-e 's,[[@]]includedir[[@]],\$(includedir),g' \
-e 's,[[@]]localstatedir[[@]],\$(localstatedir),g' \
-e 's,[[@]]sharedstatedir[[@]],\$(sharedstatedir),g' \
-e 's,[[@]]sysconfdir[[@]],\$(sysconfdir),g' \
-e 's,[[@]]datadir[[@]],\$(datadir),g' \
-e 's,[[@]]datarootdir[[@]],\$(datarootdir),g' \
-e 's,[[@]]libexecdir[[@]],\$(libexecdir),g' \
-e 's,[[@]]sbindir[[@]],\$(sbindir),g' \
-e 's,[[@]]bindir[[@]],\$(bindir),g' \
-e 's,[[@]]prefix[[@]],\$(prefix),g' \
-e 's,[[@]]exec_prefix[[@]],\$(exec_prefix),g' \
-e 's,[[@]]LDMSD_PLUGIN_LIBPATH[[@]],\$(LDMSD_PLUGIN_LIBPATH),g' \
-e 's,[[@]]ZAP_LIBPATH[[@]],\$(ZAP_LIBPATH),g' \
-e 's,[[@]]pkglibdir[[@]],\$(pkglibdir),g' \
-e 's,[[@]]pythondir[[@]],\$(pythondir),g' \
-e 's,[[@]]SOS_LIB64DIR[[@]],\$(SOS_LIB64DIR),g' \
-e 's,[[@]]SOS_LIBDIR[[@]],\$(SOS_LIBDIR),g' \
"
])

AC_SUBST(ac_configure_args)
AC_SUBST(configure_input)

dnl handle test generation and chmod
OVIS_EXEC_SCRIPTS(
		 scripts/ldms-wrapper
		 scripts/ldms-static-test.sh
		 scripts/pll-ldms-static-test.sh
		 scripts/ldms_ban.sh
		 scripts/ldms-plugins.sh
		 scripts/ldms-py-subset_test.sh
		 scripts/ldms-py-varset.sh
		 scripts/ldms-py-syslog.sh
		 scripts/ldms-py-rename.sh
		 scripts/ldms-meminfo.sh
		 scripts/ldms_local_opa2test.sh
		 scripts/ldms-l2_test.sh
)

AC_CONFIG_FILES([Makefile src/Makefile src/core/Makefile
		 swig/Makefile
		 src/auth/Makefile
		 src/store/Makefile src/sampler/Makefile
		 src/contrib/Makefile
		 src/store/kokkos/Makefile
		 src/store/papi/Makefile
		 src/store/slurm/Makefile
		 src/store/influx/Makefile
		 src/store/store_flatfile/Makefile
		 src/contrib/store/Makefile
		 src/contrib/store/tutorial/Makefile
		 src/sampler/dstat/Makefile
		 src/sampler/filesingle/Makefile
		 src/sampler/lustre/Makefile
		 src/sampler/job_info/Makefile
		 src/sampler/job_info_slurm/Makefile
		 src/sampler/llnl/Makefile
		 src/sampler/shm/Makefile
		 src/sampler/shm/shm_util/Makefile
		 src/sampler/shm/mpi_profiler/Makefile
		 src/sampler/cray_system_sampler/Makefile
		 src/sampler/aries_mmr/Makefile
		 src/sampler/aries_mmr/aries_mmr_set_configs/Makefile
		 src/sampler/slurm/Makefile
		 src/sampler/spank/Makefile
		 src/sampler/papi/Makefile
		 src/sampler/appinfo_lib/Makefile
		 src/sampler/kgnilnd/Makefile
		 src/sampler/meminfo/Makefile
		 src/sampler/procinterrupts/Makefile
		 src/sampler/procstat/Makefile
		 src/sampler/vmstat/Makefile
		 src/sampler/examples/Makefile
		 src/sampler/examples/array_example/Makefile
		 src/sampler/examples/synthetic/Makefile
		 src/sampler/examples/test_sampler/Makefile
		 src/sampler/ibm_occ/Makefile
		 src/sampler/syspapi/Makefile
		 src/contrib/sampler/Makefile
		 src/contrib/sampler/ipmireader/Makefile
		 src/contrib/sampler/tutorial/Makefile
		 src/ldmsd/Makefile
		 src/ldmsd/test/Makefile
		 scripts/Makefile
		 src/test/Makefile
		 etc/Makefile
		 etc/systemd/Makefile
		 python/Makefile
		 python/ldmsd/Makefile
		 python/cmds/Makefile
		 Doxyfile
		 scripts/ldmsd
		 scripts/envldms.sh
		 ldms.spec
		 man/Makefile
])

AC_CONFIG_COMMANDS([scripts],[ echo fixing test script perms.
for i in $ovis_exec_scripts; do
	if test -f $ovis_exec_scripts_objdir/$i; then
		chmod a+x $ovis_exec_scripts_objdir/$i;
	else
		echo failing chmod on missing $ovis_exec_scripts_objdir/$i;
	fi
done
],[
	ovis_exec_scripts="$ovis_exec_scripts"
	ovis_extra_dist="$ovis_extra_dist"
	ovis_exec_scripts_objdir="$ac_pwd"
])
AC_OUTPUT

if test "x$enable_rpath" != "xyes"; then
echo "TURNING libtool rpath into no-ops"
sed -i 's|^hardcode_libdir_flag_spec=.*|hardcode_libdir_flag_spec=""|g' libtool
sed -i 's|^runpath_var=LD_RUN_PATH|runpath_var=DIE_RPATH_DIE|g' libtool
fi
