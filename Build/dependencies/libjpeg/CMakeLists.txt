

file(GLOB libjpeg_srcs "${LIBJPEG_SOURCE_DIR}/*.c" "${LIBJPEG_SOURCE_DIR}/*.cpp")
file(GLOB libjpeg_int_hdrs "${LIBJPEG_SOURCE_DIR}/*.h*")

add_library( # Specifies the name of the library.
             jpeg

             # Sets the library as a shared library.
             STATIC

             ${libjpeg_srcs}
             )


# Links your native library against one or more other native libraries.
target_link_libraries( # Specifies the target library.
                       jpeg

                       # Links the log library to the target library.
                       ${log-lib} )
                       
