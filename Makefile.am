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

ACLOCAL_AMFLAGS = --install -I m4

# Leave examples off of DIST_SUBDIRS on purpose
SUBDIRS = src include tests doc


# Make sure the top level files and the files necessary to build the
# documentation are included in the distribution. Generated man files are
# included in the documentation but the Doxygen content is not.
EXTRA_DIST= \
  examples/Makefile.in.in \
  examples/flexexample10.test.in \
  examples/flexexample10a.test.in \
  examples/ctokens.l.in \
  examples/jtokens.l.in \
  examples/ptokens.l.in \
  CODE_OF_CONDUCT.md \
  CONTRIBUTING.md \
  INSTALL.md \
  LICENSE.txt \
  README.md

DISTCLEANFILES= \
  examples/Makefile.in \
  examples/Makefile \
  examples/flexexample10.test \
  examples/flexexample10a.test \
  examples/ctokens.l \
  examples/jtokens.l \
  examples/ptokens.l






# examples are complicated. On one hand, the examples need to be
# installed into $(docdir) along with a makefile that builds the
# examples using the installed version of reflex. Ie so a user who just
# wants to get up and running quickly without having to mess around with
# automake can simply copy the installed examples directory, run make in
# it, and assuming the users build environment is sane, all the examples
# will build and link correctly. On the other hand, there needs to be be
# a way to build and link the examples against the version of reflex in
# this distribution to check for errors in the examples before they are
# installed. These two makefiles need to either be the same or as close
# to the same as possible. The nobase_dist_doc_DATA below simply
# installs the version of the examples that build against the installed
# version of reflex
if EXAMPLES
check-local:
	cd examples && $(MAKE) $(AM_MAKEFLAGS) all

clean-local:
	cd examples && $(MAKE) $(AM_MAKEFLAGS) clean
endif

nobase_dist_doc_DATA= \
  examples/README.md \
  examples/braille.l \
  examples/calc.l \
  examples/calc.y \
  examples/cards.cpp \
  examples/cdefs.l \
  examples/cow.l \
  examples/cows.l \
  examples/csv.l \
  examples/echo.l \
  examples/flexexample1.l \
  examples/flexexample2.l \
  examples/flexexample3.lxx \
  examples/flexexample3.test \
  examples/flexexample3.yxx \
  examples/flexexample3.l \
  examples/flexexample3.y \
  examples/flexexample4.l \
  examples/flexexample4.lxx \
  examples/flexexample4.test \
  examples/flexexample4.y \
  examples/flexexample4.yxx \
  examples/flexexample5.l \
  examples/flexexample5.lxx \
  examples/flexexample5.test \
  examples/flexexample5.y \
  examples/flexexample5.yxx \
  examples/flexexample6.l \
  examples/flexexample7.l \
  examples/flexexample7.lxx \
  examples/flexexample7.test \
  examples/flexexample7.y \
  examples/flexexample7.yxx \
  examples/flexexample8.l \
  examples/flexexample8.lxx \
  examples/flexexample8.test \
  examples/flexexample8.y \
  examples/flexexample8.yxx \
  examples/flexexample9.lxx \
  examples/flexexample9.test \
  examples/flexexample9.yxx \
  examples/flexexample10.l \
  examples/flexexample10b.test \
  examples/indent.l \
  examples/jdefs.l \
  examples/json.l \
  examples/pdefs.l \
  examples/readline.l \
  examples/reflexexample3.l \
  examples/reflexexample3.lxx \
  examples/reflexexample3.y \
  examples/reflexexample3.yxx \
  examples/reflexexample4.l \
  examples/reflexexample4.lxx \
  examples/reflexexample5.l \
  examples/reflexexample5.lxx \
  examples/reflexexample6.l \
  examples/reflexexample7.l \
  examples/reflexexample7.lxx \
  examples/reflexexample8.l \
  examples/reflexexample8.lxx \
  examples/reflexexample9.lxx \
  examples/reflexexample10.l \
  examples/tag.l \
  examples/tag_lazy.l \
  examples/tag_lazystates.l \
  examples/tag_tidy.l \
  examples/tag_unicode.l \
  examples/unicode.l \
  examples/url.cpp \
  examples/wc.l \
  examples/wcpp.l \
  examples/wcu.l \
  examples/wcwc.l

uninstall-hook:
	rm -R -f $(DESTDIR)$(docdir)

makefile_subs = sed -e ' s/[@]REFLEX[@]/reflex/g' \
                    -e ' s/[@]LIBREFLEX[@]/-lreflex/g' \
                    -e ' s/[@]YACC[@]/bison -y/g' \
                    -e ' s/[@]BISON[@]/bison/g' \
                    -e ' s/[@]LIBREADLINE[@]/-lreadline/g' \
                    -e ' s/[@]CC[@]/cc/g' \
                    -e ' s/[@]CXX[@]/c++/g' \
                    -e ' s|[@]srcdir[@]/||g' \
                    -e ' s|[@]builddir[@]/||g' \
                    -e ' s/[@].*[@]//g'

example_subs = sed -e ' s|[@]builddir[@]/||g' \
                   -e ' s|[@]srcdir[@]/||g'
install-data-hook:
	$(makefile_subs) $(top_srcdir)/examples/Makefile.in.in > $(DESTDIR)$(docdir)/examples/Makefile
	$(example_subs) $(top_srcdir)/examples/flexexample10.test.in > $(DESTDIR)$(docdir)/examples/flexexample10.test
	$(example_subs) $(top_srcdir)/examples/flexexample10a.test.in > $(DESTDIR)$(docdir)/examples/flexexample10a.test
	$(example_subs) $(top_srcdir)/examples/ctokens.l.in > $(DESTDIR)$(docdir)/examples/ctokens.l
	$(example_subs) $(top_srcdir)/examples/jtokens.l.in > $(DESTDIR)$(docdir)/examples/jtokens.l
	$(example_subs) $(top_srcdir)/examples/ptokens.l.in > $(DESTDIR)$(docdir)/examples/ptokens.l
	@echo " ______________________________________________________ "; \
	 echo "|                                                      |"; \
	 echo "| You have successfully built and installed reflex.    |"; \
	 echo "|                                                      |"; \
	 echo "| You can use the reflex command to generate scanners. |"; \
	 echo "| Link your generated scanner with -lreflex.           |"; \
	 echo "|                                                      |"; \
	 echo "| Thanks for using reflex.                             |"; \
	 echo "|                                                      |"; \
	 echo "|             https://github.com/Genivia/RE-flex       |"; \
	 echo "|             https://sourceforge.net/projects/re-flex |"; \
	 echo "|______________________________________________________|";
