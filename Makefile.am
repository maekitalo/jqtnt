AUTOMAKE_OPTIONS = subdir-objects

bin_PROGRAMS = jqtnt

ecppSources = \
	index.ecpp \
	datepicker.ecpp \
	getproduct.ecpp \
	products.ecpp \
	page1.ecpp \
	page2.ecpp \
	mainpage.ecpp

jqtnt_SOURCES = \
	main.cpp \
	jquery.cpp \
	jqueryui.cpp \
	$(ecppSources)

BUILT_SOURCES = \
	jquery.cpp \
	jqueryui.cpp

jqtnt_LDFLAGS = -lcxxtools -ltntnet

CLEANFILES = $(ecppSources:.ecpp=.cpp) $(ecppSources:.ecpp=.deps) $(BUILT_SOURCES) resources.cpp

JQUERY=jquery-2.0.3.min.js
JQUERYUI=jquery-ui-1.10.3

jquery.cpp: jquery-2.0.3.min.js
	ecppc -b -z -n jquery $(JQUERY)

jqueryui.cpp: $(JQUERYUI)/stamp
	ecppc -bb -z -n jqueryui -p $$(for s in ui themes; do find $(JQUERYUI)/$$s -type f; done)

$(JQUERYUI)/stamp: $(JQUERYUI).zip
	unzip $(JQUERYUI).zip
	touch $(JQUERYUI)/stamp

#
# Rules for tntnet applications
#

SUFFIXES=.ecpp .ico .cpp .js

.ecpp.cpp:
	$(ECPPC) -I $(top_srcdir)/src -n $(basename $<) -o $@ $<
.ecpp.deps:
	$(ECPPC) -M -n $* -I $(srcdir) -I $(srcdir)/include $< | $(SED) '1s/\(.*\).cpp:/\1.cpp \1.deps:/' > $@
.ico.cpp:
	$(ECPPC) -b -m image/x-icon -o $@ $<
.js.cpp:
	$(ECPPC) -m application/x-javascript -b -o $@ $<

-include $(ecppSources:.ecpp=.deps)
