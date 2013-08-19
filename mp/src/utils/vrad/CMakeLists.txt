cmake_minimum_required (VERSION 2.8)
cmake_policy(SET CMP0015 NEW)
project (vrad)

set(INCLUDE_DIRS ../../public ../../public/tier0 ../../public/tier1 ../common ../vmpi )

set(SOURCES_PUBLIC  ../../public/bsptreedata.cpp ../../public/builddisp.cpp ../../public/chunkfile.cpp ../../public/collisionutils.cpp)
set(SOURCES_PUBLIC ${SOURCES_PUBLIC}  ../../public/dispcoll_common.cpp ../../public/disp_common.cpp ../../public/disp_powerinfo.cpp)
set(SOURCES_PUBLIC ${SOURCES_PUBLIC} ../../public/filesystem_helpers.cpp ../../public/filesystem_init.cpp ../../public/loadcmdline.cpp)
set(SOURCES_PUBLIC ${SOURCES_PUBLIC} ../../public/lumpfiles.cpp ../../public/scratchpad3d.cpp ../../public/zip_utils.cpp)

set(SOURCES_COMMON ../common/bsplib.cpp ../common/cmdlib.cpp ../common/filesystem_tools.cpp ../common/map_shared.cpp ../common/pacifier.cpp)
set(SOURCES_COMMON ${SOURCES_COMMON} ../common/physdll.cpp ../common/polylib.cpp ../common/scriplib.cpp ../common/threads.cpp)
set(SOURCES_COMMON ${SOURCES_COMMON} ../common/tools_minidump.cpp ../common/utilmatlib.cpp)

set(SOURCES_VRAD disp_vrad.cpp leaf_ambient_lighting.cpp samplehash.cpp vrad.cpp vraddisps.cpp imagepacker.cpp lightmap.cpp origface.cpp)
set(SOURCES_VRAD ${SOURCES_VRAD} trace.cpp vrad_dispcoll.cpp vraddll.cpp incremental.cpp macro_texture.cpp radial.cpp vismat.cpp vraddetailprops.cpp vradstaticprops.cpp)

set(SOURCES "${SOURCES_PUBLIC}" "${SOURCES_COMMON}" "${SOURCES_VRAD}")

set(CMAKE_BUILD_TYPE "Release")

set(CMAKE_C_FLAGS_RELEASE "-march=native -m32 -D_DLL_EXT=.so -DDX_TO_GL_ABSTRACTION -D_EXTERNAL_DLL_EXT=.so -DGL_GLEXT_PROTOTYPES -DGNUC")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -D_LINUX -DLINUX -DNDEBUG -DNO_HOOK_MALLOC -DNO_MALLOC_OVERRIDE -DNO_STRING_T -D_POSIX")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DPOSIX -DPROTECTED_THINGS_ENABLE -D_snprintf=use_Q_snprintf_instead -Dstrncpy=use_Q_strncpy_instead")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DUSE_SDL -DUSE_WEBM_FOR_REPLAY -DVECTOR -DVERSION_SAFE_STEAM_API_INTERFACES -DVPROF_LEVEL=1")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -DRAD_TELEMETRY_DISABLED=1 -O2 -Wall -Wno-invalid-offsetof -Wno-unused-local-typedefs")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE}  -Wno-unused-but-set-variable -Wno-unused-function -Wno-unused-value -Wno-unused-variable")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -Wextra -Wno-unused-parameter -Wno-ignored-qualifiers -Wno-missing-field-initializers -Wno-type-limits -Wno-comment" )

set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE}")

include_directories(${INCLUDE_DIRS})

link_directories(../../lib/linux32 ../../lib/public/linux32)

add_executable(vrad ${SOURCES})
# So far cmake does not like relitive linking to static libs
set(TARGET_LINK_LIBS /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32/tier1.a /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32//tier2.a)
set(TARGET_LINK_LIBS ${TARGET_LINK_LIBS} /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32/mathlib.a /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32/vtf.a)
set(TARGET_LINK_LIBS ${TARGET_LINK_LIBS} /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32/bitmap.a  tier0 vstdlib)

target_link_libraries(vrad ${TARGET_LINK_LIBS})
