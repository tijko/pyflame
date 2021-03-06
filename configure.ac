AC_PREREQ([2.68])
AC_INIT([pyflame], [1.1.1], [evan@uber.com])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_HEADERS([src/config.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_SRCDIR([src/pyflame.cc])

AM_INIT_AUTOMAKE([dist-bzip2 foreign subdir-objects -Wall -Werror])

# Checks for programs.
AC_PROG_CXX
AC_PROG_CC
AC_PROG_INSTALL

# Fail early if the user tries to build on OS X
AC_CHECK_HEADERS([linux/ptrace.h], [], [AC_MSG_ERROR([Pyflame only supports Linux hosts])])

# This is commented out because it doesn't work right on Ubuntu 12.04 (Precise)
# AX_CXX_COMPILE_STDCXX_11
AX_CHECK_COMPILE_FLAG(["-std=c++11"],
                      [AX_APPEND_FLAG(["-std=c++11"], [CXXFLAGS])],
                      [AX_CHECK_COMPILE_FLAG(["-std=c++0x"],
                                             [AX_APPEND_FLAG(["-std=c++0x"], [CXXFLAGS])],
                                             [AC_MSG_ERROR([failed to detect C++11 support])])])

AX_CHECK_COMPILE_FLAG([-Wall],
                      [AX_APPEND_FLAG([-Wall], [CXXFLAGS])])

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.
# AC_CHECK_HEADER_STDBOOL

# Checks for library functions.

AC_ARG_WITH([python],
            [AS_HELP_STRING([--with-python], [specify python or python3 @<:@default=python@:>@])],
            [],
            [with_python="python"])

PKG_CHECK_MODULES([PYTHON], ["$with_python"])
AC_SUBST([PYTHON])

AC_CONFIG_FILES([Makefile
                 src/Makefile])
AC_REVISION([m4_esyscmd_s([git describe --always])])
AC_OUTPUT
