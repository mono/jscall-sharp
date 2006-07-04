### Names ###

ASSEMBLY_NAME = jscall
ASSEMBLY = $(ASSEMBLY_NAME).dll
GLUELIB = lib$(ASSEMBLY_NAME)glue.dll.so


### Source files and refs ###

ASSEMBLY_CSFILES = \
	AssemblyInfo.cs \
	AspNetEdit.JSCall/CommandManager.cs \
	AspNetEdit.JSCall/InvalidJSArgumentException.cs
	
ASSEMBLY_REFERENCES = \
	$(GTKSHARP_LIBS) \
	$(GECKOSHARP_LIBS)

GLUELIB_CPPFILES = \
	jscallglue/jscallglue.cpp

CXXFLAGS = -shared -g -fPIC -fno-rtti $(JSGLUEDEPS_CFLAGS)
LDFLAGS = $(JSGLUEDEPS_CFLAGS)

JS_FILES = \
	Resources/JSCall.js

DOC_FILES = \
	jscallglue/README


### Install locations, files ###

jscalldir=$(pkglibdir)
jscall_SCRIPTS = $(ASSEMBLY) $(GLUELIB) $(JS_FILES)
jscall_DATA = $(ASSEMBLY).mdb


### Build rules ###

all: $(ASSEMBLY)


$(ASSEMBLY): $(ASSEMBLY_CSFILES)
	$(MCS) $(MCS_OPTIONS) $(ASSEMBLY_REFERENCES) -debug -target:library -out:$@ $^

$(ASSEMBLY).mdb: $(ASSEMBLY)


$(GLUELIB): $(GLUELIB_CPPFILES)
	$(CXX) $(CXXFLAGS) -o $@ $^ $(LDFLAGS)


### Extra dist and clean info ###

EXTRA_DIST = $(ASSEMBLY_CSFILES) $(GLUELIB_CPPFILES) $(JS_FILES) $(DOC_FILES)
CLEANFILES = $(ASSEMBLY) $(ASSEMBLY).mdb $(GLUELIB)
