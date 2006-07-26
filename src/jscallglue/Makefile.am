ASSEMBLY_NAME=jscall
GLUELIB=libjscallglue.la

libjscallglue_la_LDFLAGS = -module -no-undefined -avoid-version -release $(VERSION)
libjscallglue_la_LIBADD = $(JSGLUEDEPS_LIBS)
libjscallglue_la_CXXFLAGS = -fno-rtti 
INCLUDES=$(JSGLUEDEPS_CFLAGS)

libjscallglue_la_SOURCES = \
	jscallglue.cpp

lib_LTLIBRARIES=$(GLUELIB)

EXTRA_DIST = $(ASSEMBLY_CSFILES) $(glue_CPPFILES)
CLEANFILES = lib*.a lib*.o lib*.lo lib*.la
