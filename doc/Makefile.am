#  Copyright (c) 2018, Michael B Tegtmeyer
#  Copyright (c) 2016, Robert van Engelen, Genivia Inc.
#
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



# Only try and build and distribute manfiles if HAVE_HELP2MAN is set
dist_man_MANS = reflex.1

reflex.1: $(top_srcdir)/src/reflex.cpp $(top_srcdir)/configure.ac
	cd $(top_builddir)/src/ && $(MAKE) $(AM_MAKEFLAGS) reflex$(EXEEXT)
	-$(HELP2MAN) --output=$@ --no-info $(top_builddir)/src/reflex$(EXEEXT)


docpkg = $(PACKAGE_TARNAME)-doxy-$(PACKAGE_VERSION).tar.gz

doc_DATA = $(docpkg)

$(docpkg): doxygen.stamp
	tar chof - html | gzip -9 -c >$@


doxygen.stamp: Doxyfile
	$(DOXYGEN) $(DOXYFLAGS) $<
	echo Timestamp > $@

uninstall-hook:
	cd $(DESTDIR)$(docdir) && rm -rf html

clean-local:
	rm -rf html


EXTRA_DIST= \
  Doxyfile.in \
  README.md \
  doxygen_content.css \
  doxygen_tabs.css \
  header.html \
  footer.html \
  index.md \
  reflex-logo.pdf \
  reflex-logo.png

CLEANFILES= \
  doxywarn.txt \
  doxygen.stamp \
  $(docpkg)

MAINTAINERCLEANFILES= \
  reflex.1


install-data-hook:
	cd $(DESTDIR)$(docdir) && tar xf $(docpkg)
