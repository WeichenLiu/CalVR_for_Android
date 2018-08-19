

file(GLOB libpng_srcs "${LIBPNG_SOURCE_DIR}/*.c" "${LIBPNG_SOURCE_DIR}/*.cpp")
file(GLOB libpng_int_hdrs "${LIBPNG_SOURCE_DIR}/*.h*")

add_library( # Specifies the name of the library.
             png

             # Sets the library as a shared library.
             STATIC

             ${libpng_srcs}
             )



# Links your native library against one or more other native libraries.
target_link_libraries( # Specifies the target library.
                       png

                       # Links the log library to the target library.
                       ${log-lib} )