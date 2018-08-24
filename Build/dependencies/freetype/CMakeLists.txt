

set(freetype_srcs 
	"${FREETYPE_SOURCE_DIR}/src/base/ftbbox.c"
	"${FREETYPE_SOURCE_DIR}/src/base/ftbitmap.c"
	"${FREETYPE_SOURCE_DIR}/src/base/ftglyph.c"
	"${FREETYPE_SOURCE_DIR}/src/base/ftstroke.c"
	"${FREETYPE_SOURCE_DIR}/src/base/ftxf86.c"
	"${FREETYPE_SOURCE_DIR}/src/base/ftbase.c"
	"${FREETYPE_SOURCE_DIR}/src/base/ftsystem.c"
	"${FREETYPE_SOURCE_DIR}/src/base/ftinit.c"
	"${FREETYPE_SOURCE_DIR}/src/base/ftgasp.c"
	"${FREETYPE_SOURCE_DIR}/src/raster/raster.c"
	"${FREETYPE_SOURCE_DIR}/src/sfnt/sfnt.c"
	"${FREETYPE_SOURCE_DIR}/src/smooth/smooth.c"
	"${FREETYPE_SOURCE_DIR}/src/autofit/autofit.c"
	"${FREETYPE_SOURCE_DIR}/src/truetype/truetype.c"
	"${FREETYPE_SOURCE_DIR}/src/cff/cff.c"
	"${FREETYPE_SOURCE_DIR}/src/psnames/psnames.c"
	"${FREETYPE_SOURCE_DIR}/src/pshinter/pshinter.c"
)

ADD_DEFINITIONS (-DDARWIN_NO_CARBON -DFT2_BUILD_LIBRARY)

add_library( # Specifies the name of the library.
             freetype

             # Sets the library as a shared library.
             STATIC

             ${freetype_srcs}
             )


# Links your native library against one or more other native libraries.
target_link_libraries( # Specifies the target library.
                       freetype

                       # Links the log library to the target library.
                       ${log-lib} )
                       
