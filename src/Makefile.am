### Names ###

ASSEMBLY_NAME=jscall
ASSEMBLY=$(ASSEMBLY_NAME).dll
ASSEMBLY_CONFIG=$(ASSEMBLY_NAME).dll.config
SNK=$(ASSEMBLY_NAME).key


### Source files and refs ###

ASSEMBLY_CSFILES = \
	$(srcdir)/AssemblyInfo.cs \
	$(srcdir)/AspNetEdit.JSCall/CommandManager.cs \
	$(srcdir)/AspNetEdit.JSCall/InvalidJSArgumentException.cs

ASSEMBLY_REFERENCES = \
	$(GTKSHARP_LIBS) \
	$(GECKOSHARP_LIBS)

JS_FILES = \
	Resources/JSCall.js


### Install locations, files ###

jscalldir=$(pkglibdir)
jscall_SCRIPTS = $(ASSEMBLY) $(JS_FILES) $(ASSEMBLY_CONFIG)
jscall_DATA = $(ASSEMBLY).mdb


### Build rules ###

all: $(ASSEMBLY)

$(ASSEMBLY): $(ASSEMBLY_CSFILES) $(SNK)
	$(MCS) $(MCS_OPTIONS) $(ASSEMBLY_REFERENCES) -debug -target:library -out:$@ $(ASSEMBLY_CSFILES)

$(ASSEMBLY).mdb: $(ASSEMBLY)

$(SNK): $(top_srcdir)/$(SNK)
	cp $(top_srcdir)/$(SNK) .

### Extra dist and clean info ###

EXTRA_DIST = $(ASSEMBLY_CSFILES) $(JS_FILES)
CLEANFILES = $(ASSEMBLY) $(ASSEMBLY).mdb $(GLUELIB) $(SNK)

### GAC install rules ###

install-data-local:
	echo "$(GACUTIL) /i $(ASSEMBLY) $(GACUTIL_FLAGS)";  \
        $(GACUTIL) /i $(ASSEMBLY) $(GACUTIL_FLAGS) || exit 1;

uninstall-local:
	echo "$(GACUTIL) /u $(ASSEMBLY_NAME) $(GACUTIL_FLAGS)"; \
        $(GACUTIL) /u $(ASSEMBLY_NAME) $(GACUTIL_FLAGS) || exit 1;
