set(FILE_LIST
    libSDL2-2.0.so.0
    libSDL2.so
    libtier0.so
    libvstdlib.so )

install(FILES ${FILE_LIST} DESTINATION ${CMAKE_SOURCE_DIR}/../game/bin)

