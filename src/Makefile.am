SUBDIRS = jscallglue

### Names ###

ASSEMBLY_NAME=jscall
ASSEMBLY=$(ASSEMBLY_NAME).dll
ASSEMBLY_CONFIG=$(ASSEMBLY_NAME).dll.config
SNK=$(ASSEMBLY_NAME).key


### Source files and refs ###

ASSEMBLY_CSFILES = \
	AssemblyInfo.cs \
	AspNetEdit.JSCall/CommandManager.cs \
	AspNetEdit.JSCall/InvalidJSArgumentException.cs
	
ASSEMBLY_REFERENCES = \
	$(GTKSHARP_LIBS) \
	$(GECKOSHARP_LIBS)

JS_FILES = \
	Resources/JSCall.js

DOC_FILES = \
	jscallglue/README


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

EXTRA_DIST = $(ASSEMBLY_CSFILES) $(JS_FILES) $(DOC_FILES)
CLEANFILES = $(ASSEMBLY) $(ASSEMBLY).mdb $(GLUELIB) $(SNK)

### GAC install rules ###

install-data-local:
	echo "$(GACUTIL) /i $(ASSEMBLY)";  \
        $(GACUTIL) /i $(ASSEMBLY) || exit 1;

uninstall-local:
	echo "$(GACUTIL) /u $(ASSEMBLY_NAME)"; \
        $(GACUTIL) /u $(ASSEMBLY_NAME) || exit 1;
