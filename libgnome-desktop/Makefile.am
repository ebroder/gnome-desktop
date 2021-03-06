CLEANFILES =

lib_LTLIBRARIES = libgnome-desktop-3.la

AM_CPPFLAGS =							\
	-I$(top_srcdir)						\
	$(GNOME_DESKTOP_CFLAGS)					\
	$(XLIB_CFLAGS)						\
	-DG_LOG_DOMAIN=\"GnomeDesktop\"				\
	-DGNOMELOCALEDIR=\""$(prefix)/$(DATADIRNAME)/locale\""	\
	-DPNP_IDS=\""$(PNP_IDS)"\"				\
	$(DISABLE_DEPRECATED_CFLAGS)

AM_CFLAGS = $(WARN_CFLAGS)

introspection_sources = 		\
	gnome-desktop-utils.c		\
	gnome-desktop-thumbnail.c 	\
	gnome-thumbnail-pixbuf-utils.c 	\
	gnome-bg.c			\
	gnome-bg-crossfade.c		\
	display-name.c			\
	gnome-rr.c			\
	gnome-rr-config.c		\
	gnome-rr-output-info.c		\
	gnome-rr-labeler.c		\
	gnome-tz-monitor.c		\
	edid-parse.c

libgnome_desktop_3_la_SOURCES = 	\
	$(introspection_sources)	\
	gnome-rr-private.h		\
	edid.h				\
	private.h

libgnome_desktop_3_la_LIBADD =	\
	$(XLIB_LIBS)		\
	$(GNOME_DESKTOP_LIBS)

libgnome_desktop_3_la_LDFLAGS = \
	-version-info $(LT_VERSION) \
	-export-symbols-regex "^gnome_.*" \
	-no-undefined

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = gnome-desktop-3.0.pc

libgnome_desktopdir = $(includedir)/gnome-desktop-3.0/libgnome-desktop
libgnome_desktop_HEADERS = \
        gnome-bg.h                      \
        gnome-bg-crossfade.h            \
        gnome-desktop-utils.h           \
        gnome-desktop-thumbnail.h       \
        gnome-rr.h                      \
        gnome-rr-config.h               \
        gnome-rr-labeler.h		\
        gnome-tz-monitor.h

if USE_INTERNAL_PNP_IDS
pnpdatadir = $(datadir)/libgnome-desktop-3.0
pnpdata_DATA = pnp.ids
endif
pnpdata_DATA_dist = pnp.ids

check:
	test -s $(top_srcdir)/libgnome-desktop/pnp.ids

-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS = --add-include-path=$(srcdir) --warn-all
INTROSPECTION_COMPILER_ARGS = --includedir=$(srcdir)

if HAVE_INTROSPECTION

GnomeDesktop-3.0.gir: libgnome-desktop-3.la
GnomeDesktop_3_0_gir_INCLUDES = GObject-2.0 Gtk-3.0
GnomeDesktop_3_0_gir_PACKAGES = gdk-pixbuf-2.0 glib-2.0 gobject-2.0 gio-2.0 gtk+-3.0 gsettings-desktop-schemas
GnomeDesktop_3_0_gir_CFLAGS = -DGNOME_DESKTOP_USE_UNSTABLE_API -I$(top_srcdir)
GnomeDesktop_3_0_gir_LIBS = libgnome-desktop-3.la
GnomeDesktop_3_0_gir_FILES = $(introspection_sources) $(libgnome_desktop_HEADERS)
GnomeDesktop_3_0_gir_SCANNERFLAGS = --identifier-prefix=Gnome --symbol-prefix=gnome_
INTROSPECTION_SCANNER_ARGS += $(patsubst %,--c-include='libgnome-desktop/%',$(libgnome_desktop_HEADERS))
INTROSPECTION_GIRS += GnomeDesktop-3.0.gir

girdir = $(datadir)/gir-1.0
gir_DATA = $(INTROSPECTION_GIRS)

typelibdir = $(libdir)/girepository-1.0
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

CLEANFILES += $(gir_DATA) $(typelib_DATA)
endif

EXTRA_DIST = \
	gnome-desktop-3.0.pc.in			\
	gnome-desktop-3.0-uninstalled.pc.in	\
	$(pnpdata_DATA_dist)

MAINTAINERCLEANFILES = \
	pnp.ids

-include $(top_srcdir)/git.mk
