AC_INIT(README)
AC_CANONICAL_SYSTEM
AM_INIT_AUTOMAKE(jscall-sharp, 0.0.3)
AM_MAINTAINER_MODE

AC_PROG_INSTALL

### Dependency version numbers

MONO_REQUIRED_VERSION=1.1.9
GTKSHARP_REQUIRED_VERSION=2.4
GECKOSHARP_REQUIRED_VERSION=0.10

### Check for pkg-config
AC_PATH_PROG(PKG_CONFIG, pkg-config, no)
if test "x$PKG_CONFIG" = "xno"; then
	AC_MSG_ERROR([You need to install pkg-config])
fi

### Check mono version
PKG_CHECK_MODULES(MONO, mono >= $MONO_REQUIRED_VERSION)

#Check for C# compiler
AC_PATH_PROG(CSC, csc, no)
AC_PATH_PROG(MCS, mcs, no)
AC_PATH_PROG(MONO, mono, no)

### Find a c# compiler 

CS="C#"
if test "x$CSC" = "xno" -a "x$MCS" = "xno"  ; then
	dnl AC_MSG_ERROR([You need to install a C# compiler])
	AC_MSG_ERROR([No $CS compiler found])
fi

if test "x$MCS" = "xno" ; then
	MCS=$CSC
fi

if test "x$MONO" = "xno"; then
	AC_MSG_ERROR([No mono runtime found])
fi

AC_SUBST(MCS)

MCS_OPTIONS="-d:TRACE"
AC_SUBST(MCS_OPTIONS)

### The GAC tool

AC_PATH_PROG(GACUTIL, gacutil, no)
if test "x$GACUTIL" = "xno" ; then
        AC_MSG_ERROR([No gacutil tool found])
fi

AC_SUBST(GACUTIL)

GACUTIL_FLAGS='/gacdir $(DESTDIR)$(prefix)'
AC_SUBST(GACUTIL_FLAGS)

### Check c# dependencies

PKG_CHECK_MODULES(GTKSHARP, gtk-sharp-2.0 >= $GTKSHARP_REQUIRED_VERSION)
PKG_CHECK_MODULES(GECKOSHARP, gecko-sharp-2.0 >= $GECKOSHARP_REQUIRED_VERSION)

AC_OUTPUT([
Makefile
jscall-sharp.pc
src/Makefile
src/AssemblyInfo.cs
src/jscall.dll.config
])

echo ""
echo "Configuration summary"
echo ""
echo "   * Installation prefix = $prefix"
echo "   * C# compiler = $MCS"
echo "   * C# compiler options = $MCS_OPTIONS"
echo ""
