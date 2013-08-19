
cmake_minimum_required (VERSION 2.8)
#-----------------------------------------------------------------------------
# Set policy

# see "cmake --help-policy CMP0003"
# So library linking is more sane
cmake_policy(SET CMP0003 NEW)

#
cmake_policy(SET CMP0005 NEW)

# So syntax problems are errors
cmake_policy(SET CMP0010 NEW)

# Input directories must have CMakeLists.txt
cmake_policy(SET CMP0014 NEW)

#
cmake_policy(SET CMP0015 NEW)

#-----------------------------------------------------------------------------

SET(CMAKE_FIND_LIBRARY_PREFIXES "")
SET(CMAKE_FIND_LIBRARY_SUFFIXES ".a")

#-----------------------------------------------------------------------------

project (vbsp)

set(CMAKE_BUILD_TYPE "Release")

# INC
set(INC
    ../../public
    ../../public/tier0
    ../../public/tier1
    ../common ) # End INC

# SRC
set(SRC

    # Public Sources
    ../../public/builddisp.cpp
    ../../public/chunkfile.cpp
    ../../public/collisionutils.cpp
    ../../public/disp_common.cpp
    ../../public/disp_powerinfo.cpp
    ../../public/filesystem_helpers.cpp
    ../../public/filesystem_init.cpp
    ../../public/loadcmdline.cpp
    ../../public/lumpfiles.cpp
    ../../public/zip_utils.cpp

    # Common Sources
    ../common/bsplib.cpp
    ../common/cmdlib.cpp
    ../common/filesystem_tools.cpp
    ../common/map_shared.cpp
    ../common/mstristrip.cpp
    ../common/pacifier.cpp
    ../common/physdll.cpp
    ../common/polylib.cpp
    ../common/scriplib.cpp
    ../common/threads.cpp
    ../common/utilmatlib.cpp
    ../common/tools_minidump.cpp

    # Vbsp Sources
    boundbox.cpp
    brushbsp.cpp
    csg.cpp
    cubemap.cpp
    detail.cpp
    detailobjects.cpp
    disp_ivp.cpp
    disp_vbsp.cpp
    faces.cpp
    glfile.cpp
    ivp.cpp
    leakfile.cpp
    manifest.cpp
    map.cpp
    materialpatch.cpp
    materialsub.cpp
    nodraw.cpp
    normals.cpp
    overlay.cpp
    portals.cpp
    prtfile.cpp
    staticprop.cpp
    textures.cpp
    tree.cpp
    vbsp.cpp
    worldvertextransitionfixup.cpp
    writebsp.cpp
    ) # End SRC

# C_FLAGS
set(CMAKE_C_FLAGS_RELEASE "-march=native -m32 -O2")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -D_DLL_EXT=.so -DDX_TO_GL_ABSTRACTION -D_EXTERNAL_DLL_EXT=.so -DGL_GLEXT_PROTOTYPES")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DGNUC -D_LINUX -DLINUX -DNDEBUG -DNO_HOOK_MALLOC -DNO_MALLOC_OVERRIDE -DNO_STRING_T")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -D_POSIX -DPOSIX -DPROTECTED_THINGS_ENABLE")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -D_snprintf=use_Q_snprintf_instead -Dstrncpy=use_Q_strncpy_instead")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DUSE_SDL -DUSE_WEBM_FOR_REPLAY -DVECTOR -DVERSION_SAFE_STEAM_API_INTERFACES -DVPROF_LEVEL=1")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -Wall -Wno-invalid-offsetof -Wno-unused-local-typedefs -Wno-unused-but-set-variable -Wno-unused-function")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -Wno-unused-value -Wno-unused-variable -Wextra -Wno-unused-parameter -Wno-ignored-qualifiers")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -Wno-missing-field-initializers -Wno-type-limits -Wno-comment" ) # End C_FLAGS

# CXX_FLAGS
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE}") # End CXX_FLAGS

include_directories(${INC})

# Link Directores
link_directories(
    ../../lib/linux32
    ../../lib/public/linux32) # End Link Directories

add_executable(vbsp ${SRC})

# LINK_LIBS
set(LINK_LIBS
    ${CMAKE_SOURCE_DIR}/lib/public/linux32/tier1.a
    ${CMAKE_SOURCE_DIR}/lib/public/linux32/tier2.a
    ${CMAKE_SOURCE_DIR}/lib/public/linux32/mathlib.a
    ${CMAKE_SOURCE_DIR}/lib/public/linux32/vtf.a
    ${CMAKE_SOURCE_DIR}/lib/public/linux32//bitmap.a
    tier0 vstdlib) # End LINK_LIBS

target_link_libraries(vbsp ${LINK_LIBS})
