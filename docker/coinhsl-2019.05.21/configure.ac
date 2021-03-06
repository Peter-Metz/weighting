# Copyright (C) 2011 Science and Technology Facilities Council.

# Author:  Jonathan Hogg               STFC   2011-09-20

####################################################################

# initialise automake
AC_INIT(coinhsl, 2015.06.23, hsl@stfc.ac.uk)
AC_CONFIG_SRCDIR([hsl_ma86/hsl_ma86d.f90])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([subdir-objects])

# check for required programs
AC_PROG_FC
# Set f77 compiler to be same as f90 compiler unless explcitly told otherwise
if test "x$F77" = "x"; then
   F77="$FC"
fi
if test "x$FFLAGS" = "x"; then
   FFLAGS="$FCFLAGS"
fi
AC_PROG_F77
AC_PROG_CC
AC_PROG_LIBTOOL

# Define a macros to state availability, as per coin expectations
AC_DEFUN([HSL_CHECK_PKG],[
   pkg=$1
   AC_MSG_CHECKING([for $2])
   if test -r "$srcdir/$pkg/${pkg}d.f"; then
      AC_DEFINE(COINHSL_HAS_$2, [1], [Define to 1 if $2 is available.])
      coin_has_$1=yes
      AC_MSG_RESULT([yes])
   else
      coin_has_$1=no
      AC_MSG_RESULT([no])
   fi
   AM_CONDITIONAL(HAVE_$2, test x$coin_has_$1 = xyes)
   ])
AC_DEFUN([HSL_CHECK_PKG_F90],[
   pkg=$1
   AC_MSG_CHECKING([for $2])
   if test -r "$srcdir/$pkg/${pkg}d.f90"; then
      AC_DEFINE(COINHSL_HAS_$2, [1], [Define to 1 if $2 is available.])
      coin_has_$1=yes
      AC_MSG_RESULT([yes])
   else
      coin_has_$1=no
      AC_MSG_RESULT([no])
   fi
   AM_CONDITIONAL(HAVE_$2, test x$coin_has_$1 = xyes)
   ])

HSL_CHECK_PKG(mc19,MC19)
HSL_CHECK_PKG(ma27,MA27)
HSL_CHECK_PKG(ma28,MA28)
HSL_CHECK_PKG(ma57,MA57)
HSL_CHECK_PKG_F90(hsl_ma77,MA77)
HSL_CHECK_PKG_F90(hsl_ma86,MA86)
HSL_CHECK_PKG_F90(hsl_ma97,MA97)

# HSL_MC68 is an i.f90 not a d.f90 so can't use HSL_CHECK_PKG_F90
AC_MSG_CHECKING([for MC68])
if test -r "$srcdir/hsl_mc68/C/hsl_mc68i_ciface.f90"; then
   AC_DEFINE(COINHSL_HAS_MC68, [1], [Define to 1 if MC68 is available.])
   coin_has_hsl_mc68=yes
   AC_MSG_RESULT([yes])
else
   coin_has_hsl_mc68=no
   AC_MSG_RESULT([no])
fi
AM_CONDITIONAL(HAVE_MC68, test x$coin_has_hsl_mc68 = xyes)

# Look for a metis we can compile
AC_MSG_CHECKING([for metis to compile])
if test -r "$srcdir/metis-4.0.3/Lib/balance.c"; then
   AC_DEFINE(COINHSL_HAS_METIS, [1], [Define to 1 if METIS is available to compile.])
   coin_has_metis=yes
   AC_MSG_RESULT([yes])
else
   coin_has_metis=no
   AC_MSG_RESULT([no])
fi
AM_CONDITIONAL(HAVE_METIS, test x$coin_has_metis = xyes)

# Check if we're on Windows and have to do extra legwork for DLLs
AC_CHECK_HEADERS(windows.h)
AM_CONDITIONAL(TARGET_DLL, test x$ac_cv_header_windows_h = xyes)

# Check if we have BLAS (only used for windows as dep of dll)
AX_BLAS

# output data
AC_CONFIG_FILES([Makefile coinhsl.pc])
AC_CONFIG_HEADER(config.h CoinHslConfig.h)
AC_OUTPUT
