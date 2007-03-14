AC_INIT(README)
AC_CANONICAL_SYSTEM
AM_INIT_AUTOMAKE(jscall-sharp, 0.0.2)
AM_MAINTAINER_MODE

AM_PROG_LIBTOOL
AC_PROG_INSTALL
AC_PROG_CXX

### Dependency version numbers

MONO_REQUIRED_VERSION=1.1.9
GTKSHARP_REQUIRED_VERSION=2.4
GECKOSHARP_REQUIRED_VERSION=0.10

m4_define(gtk_required_version,               2.6.0)
m4_define(mozilla_required_version,           1.6)
m4_define(firefox_required_version,           1.0)
m4_define(xulrunner_required_version,         1.8)
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

### Check for C++/Mozilla dependencies (inspired by gnome-python-extras)
AC_ARG_WITH(gtkmozembed, AS_HELP_STRING(
                         [--with-gtkmozembed=mozilla|firefox],
                         [package that provides libgtkmozembed]),
            [mozpackage=$withval], [mozpackage=any])

if test $mozpackage = any ; then
	AC_MSG_CHECKING(for Gecko development files)
	if $PKG_CONFIG --exists mozilla-gtkmozembed; then
	    AC_MSG_RESULT([Mozilla detected])
	    mozpackage=mozilla
	else
	    if $PKG_CONFIG --exists firefox-gtkmozembed; then
	        AC_MSG_RESULT([Firefox detected])
	        mozpackage=firefox
	    else
		if $PKG_CONFIG --exists xulrunner-gtkmozembed; then
		  AC_MSG_RESULT([XulRunner detected])
		  mozpackage=xulrunner
		else
	          AC_MSG_ERROR([Neither Firefox nor Mozilla development packages were detected])
	        fi
	    fi
	fi
fi

case $mozpackage in
     firefox) mozpackage_required_version=firefox_required_version ;;
     mozilla) mozpackage_required_version=mozilla_required_version ;;
     xulrunner) mozpackage_required_version=xulrunner_required_version ;;
     *) AC_MSG_ERROR([--with-gtkmozembed argument must be either 'mozilla' or 'firefox'])
esac

MOZILLA_HOME="`$PKG_CONFIG --variable=libdir $mozpackage-gtkmozembed`"
AC_SUBST(MOZILLA_HOME)

PKG_CHECK_MODULES(JSGLUEDEPS, [$mozpackage-gtkmozembed >= $mozpackage_required_version,
                               $mozpackage-xpcom >= $mozpackage_required_version
                               gtk+-2.0                >= gtk_required_version])

AC_OUTPUT([
Makefile
jscall-sharp.pc
src/Makefile
src/jscallglue/Makefile
src/AssemblyInfo.cs
src/jscall.dll.config
])

echo ""
echo "Configuration summary"
echo ""
echo "   * Installation prefix = $prefix"
echo "   * C# compiler = $MCS"
echo "   * C# compiler options = $MCS_OPTIONS"
echo "   * Gecko libraries from:  $mozpackage"
echo "   * $mozpackage home: $MOZILLA_HOME"
echo ""
