#  Copyright (c) 2018, Michael B Tegtmeyer
#  All rights reserved.
#  Redistribution and use in source and binary forms, with or without
#  modification, are permitted provided that the following conditions are met:
#
#      * Redistributions of source code must retain the above copyright
#        notice, this list of conditions and the following disclaimer.
#      * Redistributions in binary form must reproduce the above copyright
#        notice, this list of conditions and the following disclaimer in the
#        documentation and/or other materials provided with the distribution.
#      * Neither the name of the author nor the names of its contributors may
#        be used to endorse or promote products derived from this software
#        without specific prior written permission.
#
#  THIS SOFTWARE IS PROVIDED BY THE AUTHOR AND CONTRIBUTORS ``AS IS'' AND ANY
#  EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
#  WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
#  DISCLAIMED. IN NO EVENT SHALL THE REGENTS AND CONTRIBUTORS BE LIABLE FOR ANY
#  DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
#  (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
#  LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
#  ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
#  (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF
#  THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

AC_PREREQ([2.69])
AC_INIT([reflex],[1.1.2],[github.com/tegtmeye/re-flex])
AC_CONFIG_SRCDIR([Makefile.am])
AM_CONFIG_HEADER(config.h)
AC_CONFIG_AUX_DIR(config)
AM_INIT_AUTOMAKE([foreign std-options])
AC_CONFIG_MACRO_DIR([m4])


# checks for programs
AC_PROG_INSTALL
AC_PROG_CXX
AC_PROG_LIBTOOL




# Since reflex poses as a substitute to LEX/FLEX, just make sure the LEX is
# properly defined


# Check for maintainer-specific programs
AM_MISSING_PROG([HELP2MAN], [help2man], [$missing_dir])

# html documentation is only built if requested '--with-doxygen'. Since the
# resulting html is distributed, we only actually need doxygen and dot if
# a source file changes though
AC_ARG_WITH([doxygen],
  [AS_HELP_STRING([--with-doxygen],
    [build html documentation using doxygen @<:@default=yes@:>@])],
  [AS_CASE([$withval],
    [yes],[],
    [no],[],
    [AC_MSG_ERROR([bad value ${withval} for --with-doxygen])])
  ],
  [with_doxygen=yes])

if test "x$with_doxygen" = xyes; then
  AM_MISSING_PROG([DOXYGEN], [doxygen], [$missing_dir])
  AC_CHECK_PROG([HAVE_DOT],[dot],[YES],[NO])
  AC_CONFIG_FILES([doc/Doxyfile])
fi




# checks for libraries
# Check for boost
AX_BOOST_BASE
AX_BOOST_REGEX

# checks for header files
AC_HEADER_TIME

# checks for types

# checks for structures

# checks for compiler characteristics
# Check for C++11 compiler
AX_CXX_COMPILE_STDCXX([11],[noext],[mandatory])

# checks for library functions

# checks for system services




# Examples are only built if requested '--with-examples' and if GNU bison, flex,
# and readline are available
AC_ARG_WITH([examples],
  [AS_HELP_STRING([--with-examples],
    [build examples @<:@default=yes@:>@])],
  [AS_CASE([$withval],
    [yes],[],
    [no],[],
    [AC_MSG_ERROR([bad value ${withval} for --with-examples])])
  ],
  [with_examples=yes])

if test "x$with_examples" = xyes; then
    AC_PROG_LEX
    if test "x$LEX" != xflex; then
        AC_MSG_WARN([--with-examples is requested but flex is required to build the examples and is not found. Skipping.])
        with_examples=no
    else
      AX_PROG_BISON(
        [
          AC_SUBST([BISON],[bison])
          AX_LIB_READLINE
          if test "x$ax_cv_lib_readline" != "xno"; then
            AC_SUBST([LIBREADLINE],[$ax_cv_lib_readline])
          else
            AC_MSG_WARN([--with-examples is requested but readline is required to build the examples it is not found. Skipping.])
            with_examples=no
          fi
        ],
        [
          AC_MSG_WARN([--with-examples is requested but GNU bison is required to build the examples and is not found. Skipping.])
          [with_examples=no]
        ]
      )
    fi
fi

AM_CONDITIONAL([EXAMPLES], [test x"$with_examples" = x"yes"])



# These are used to build the examples makefile which is overly simplistic
# for the benefit of new users. This always happens whether or not
# --with-examples is set or not
AC_SUBST([REFLEX],['@top_builddir@/src/reflex'])
AC_SUBST([REFLEX_INC],['-I@top_srcdir@/include'])
AC_SUBST([LIBREFLEX],['@top_builddir@/src/.libs/libreflex.a'])

# Needed because the example directory is not included in the subdirs
AC_SUBST([CONFIG_STATUS_DEPENDENCIES],
  ['$(top_srcdir)/examples/Makefile.in.in \
  $(top_srcdir)/examples/flexexample10.test.in \
  $(top_srcdir)/examples/flexexample10a.test.in \
  $(top_srcdir)/examples/ctokens.l.in \
  $(top_srcdir)/examples/jtokens.l.in \
  $(top_srcdir)/examples/ptokens.l.in'])

AC_CONFIG_FILES( \
  Makefile \
  include/Makefile \
  src/Makefile \
  tests/Makefile \
  doc/Makefile \
  examples/Makefile.in \
  examples/Makefile \
  examples/flexexample10.test \
  examples/flexexample10a.test \
  examples/ctokens.l \
  examples/jtokens.l \
  examples/ptokens.l)


AC_OUTPUT

