
cmake_minimum_required (VERSION 2.8)
cmake_policy(SET CMP0015 NEW)
project (vbsp)

set(INCLUDE_DIRS ../../public ../../public/tier0 ../../public/tier1 ../common)

set(SOURCES_PUBLIC ../../public/builddisp.cpp ../../public/chunkfile.cpp ../../public/collisionutils.cpp ../../public/disp_common.cpp ../../public/disp_powerinfo.cpp ../../public/filesystem_helpers.cpp ../../public/filesystem_init.cpp ../../public/loadcmdline.cpp ../../public/lumpfiles.cpp ../../public/zip_utils.cpp)
set(SOURCES_COMMON ../common/bsplib.cpp ../common/cmdlib.cpp ../common/filesystem_tools.cpp ../common/map_shared.cpp ../common/mstristrip.cpp ../common/pacifier.cpp ../common/physdll.cpp ../common/polylib.cpp ../common/scriplib.cpp ../common/threads.cpp ../common/utilmatlib.cpp ../common/tools_minidump.cpp)
set(SOURCES_VBSP boundbox.cpp brushbsp.cpp csg.cpp cubemap.cpp detail.cpp detailobjects.cpp disp_ivp.cpp disp_vbsp.cpp faces.cpp glfile.cpp ivp.cpp leakfile.cpp manifest.cpp map.cpp materialpatch.cpp materialsub.cpp nodraw.cpp normals.cpp overlay.cpp portals.cpp prtfile.cpp staticprop.cpp textures.cpp tree.cpp vbsp.cpp worldvertextransitionfixup.cpp writebsp.cpp)

set(SOURCES "${SOURCES_PUBLIC}" "${SOURCES_COMMON}" "${SOURCES_VBSP}")

set(CMAKE_BUILD_TYPE "Release")

set(CMAKE_C_FLAGS_RELEASE "-march=native -m32 -D_DLL_EXT=.so -DDX_TO_GL_ABSTRACTION -D_EXTERNAL_DLL_EXT=.so -DGL_GLEXT_PROTOTYPES -DGNUC -D_LINUX -DLINUX -DNDEBUG -DNO_HOOK_MALLOC -DNO_MALLOC_OVERRIDE -DNO_STRING_T -D_POSIX -DPOSIX -DPROTECTED_THINGS_ENABLE -D_snprintf=use_Q_snprintf_instead -Dstrncpy=use_Q_strncpy_instead -DUSE_SDL -DUSE_WEBM_FOR_REPLAY -DVECTOR -DVERSION_SAFE_STEAM_API_INTERFACES -DVPROF_LEVEL=1 -O2 -Wall -Wno-invalid-offsetof -Wno-unused-local-typedefs -Wno-unused-but-set-variable -Wno-unused-function -Wno-unused-value -Wno-unused-variable -Wextra -Wno-unused-parameter -Wno-ignored-qualifiers -Wno-missing-field-initializers -Wno-type-limits -Wno-comment" )
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE}")

#set(CMAKE_LINKER_FLAGS -L../../lib/linux32 -L../../lib/public/linux32 ../../lib/public/linux32/tier1.a ../../lib/public/linux32/tier2.a ../../lib/public/linux32/mathlib.a ../../lib/public/linux32/vtf.a ../../lib/public/linux32/bitmap.a  -ltier0 -lvstdlib)
include_directories(${INCLUDE_DIRS})

link_directories(../../lib/linux32 ../../lib/public/linux32)

add_executable(vbsp ${SOURCES})

target_link_libraries(vbsp /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32/tier1.a /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32//tier2.a /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32/mathlib.a /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32/vtf.a /home/salamanderrake/src/valve/sortie/mp/src/lib/public/linux32/bitmap.a  tier0 vstdlib)

