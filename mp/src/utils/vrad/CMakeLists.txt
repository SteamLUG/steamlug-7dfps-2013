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

project (vrad)

set(CMAKE_BUILD_TYPE "Release")

# INC
set(INC
    ../../public
    ../../public/tier0
    ../../public/tier1
    ../common
    ../vmpi ) # End INC

# SRC
set(SRC

    # Public Sources
    ../../public/bsptreedata.cpp
    ../../public/builddisp.cpp
    ../../public/chunkfile.cpp
    ../../public/collisionutils.cpp
    ../../public/dispcoll_common.cpp
    ../../public/disp_common.cpp
    ../../public/disp_powerinfo.cpp
    ../../public/filesystem_helpers.cpp
    ../../public/filesystem_init.cpp
    ../../public/loadcmdline.cpp
    ../../public/lumpfiles.cpp
    ../../public/scratchpad3d.cpp
    ../../public/zip_utils.cpp

    # Common Sources
    ../common/bsplib.cpp
    ../common/cmdlib.cpp
    ../common/filesystem_tools.cpp
    ../common/map_shared.cpp
    ../common/pacifier.cpp
    ../common/physdll.cpp
    ../common/polylib.cpp
    ../common/scriplib.cpp
    ../common/threads.cpp
    ../common/tools_minidump.cpp
    ../common/utilmatlib.cpp

    # Vrad Sources
    disp_vrad.cpp
    leaf_ambient_lighting.cpp
    samplehash.cpp
    vrad.cpp
    vraddisps.cpp
    imagepacker.cpp
    lightmap.cpp
    origface.cpp
    trace.cpp
    vrad_dispcoll.cpp
    vraddll.cpp
    incremental.cpp
    macro_texture.cpp
    radial.cpp
    vismat.cpp
    vraddetailprops.cpp
    vradstaticprops.cpp) # End SRC

# C_FLAGS
set(CMAKE_C_FLAGS_RELEASE "-march=native -m32 -O2")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -D_DLL_EXT=.so -DDX_TO_GL_ABSTRACTION -D_EXTERNAL_DLL_EXT=.so -DGL_GLEXT_PROTOTYPES -DGNUC")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -D_LINUX -DLINUX -DNDEBUG -DNO_HOOK_MALLOC -DNO_MALLOC_OVERRIDE -DNO_STRING_T -D_POSIX")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DPOSIX -DPROTECTED_THINGS_ENABLE -D_snprintf=use_Q_snprintf_instead -Dstrncpy=use_Q_strncpy_instead")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DUSE_SDL -DUSE_WEBM_FOR_REPLAY -DVECTOR -DVERSION_SAFE_STEAM_API_INTERFACES -DVPROF_LEVEL=1")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DRAD_TELEMETRY_DISABLED=1 -O2 -Wall -Wno-invalid-offsetof -Wno-unused-local-typedefs")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -Wno-unused-but-set-variable -Wno-unused-function -Wno-unused-value -Wno-unused-variable")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -Wextra -Wno-unused-parameter -Wno-ignored-qualifiers -Wno-missing-field-initializers -Wno-type-limits -Wno-comment" ) # End C_FLAGS

# CXX_FLAGS
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE}") # End CXX_FLAGS

include_directories(${INC})

# Link Directories
link_directories(
    ../../lib/linux32
    ../../lib/public/linux32) # End Link Directories

add_executable(vrad ${SRC})

# LINK_LIBS
set(LINK_LIBS
    ${CMAKE_SOURCE_DIR}/lib/public/linux32/tier1.a
    ${CMAKE_SOURCE_DIR}/lib/public/linux32/tier2.a
    ${CMAKE_SOURCE_DIR}/lib/public/linux32/mathlib.a
    ${CMAKE_SOURCE_DIR}/lib/public/linux32/vtf.a
    ${CMAKE_SOURCE_DIR}/lib/public/linux32//bitmap.a
    tier0 vstdlib) # End LINK_LIBS

target_link_libraries(vrad ${LINK_LIBS})

install(TARGETS vrad DESTINATION ${CMAKE_SOURCE_DIR}/../game/bin)
