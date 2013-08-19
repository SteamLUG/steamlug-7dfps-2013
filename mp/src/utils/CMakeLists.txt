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

add_subdirectory(vbsp)
add_subdirectory(vvis)
add_subdirectory(vrad)
