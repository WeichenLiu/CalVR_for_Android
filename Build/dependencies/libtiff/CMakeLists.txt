
file(GLOB libtiff_srcs "${LIBTIFF_SOURCE_DIR}/*.c" "${LIBTIFF_SOURCE_DIR}/*.cpp")
file(GLOB libtiff_int_hdrs "${LIBTIFF_SOURCE_DIR}/*.h*")

add_library( # Specifies the name of the library.
             tiff

             # Sets the library as a shared library.
             STATIC

             ${libtiff_srcs}
             )



# Links your native library against one or more other native libraries.
target_link_libraries( # Specifies the target library.
                       tiff

                       # Links the log library to the target library.
                       ${log-lib} )