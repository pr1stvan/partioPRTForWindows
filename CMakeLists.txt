cmake_minimum_required (VERSION 3.5)
project (partioPRTForWindows)

set(CompilerFlags
        CMAKE_CXX_FLAGS
        CMAKE_CXX_FLAGS_DEBUG
        CMAKE_CXX_FLAGS_RELEASE
        CMAKE_C_FLAGS
        CMAKE_C_FLAGS_DEBUG
        CMAKE_C_FLAGS_RELEASE
        )
foreach(CompilerFlag ${CompilerFlags})
  string(REPLACE "/MD" "/MT" ${CompilerFlag} "${${CompilerFlag}}")
endforeach()

IF (WIN32)
  add_definitions(-DPARTIO_WIN32)
ELSE()
  # set stuff for other systems
ENDIF()

include_directories ("${PROJECT_SOURCE_DIR}/include")

include_directories ("${PROJECT_SOURCE_DIR}/dependencies/zlib")

add_subdirectory (dependencies/zlib)
set (EXTRA_LIBS ${EXTRA_LIBS} zlibstatic)


add_library(partioPRTForWindows 
    src/Particle.cpp
    src/ParticleCaching.cpp
    src/ParticleHeaders.cpp
    src/ParticleIO.cpp
    src/ParticleSimple.cpp
    src/ParticleSimpleInterleave.cpp
    src/PRT.cpp
    src/ZIP.cpp
    )


ADD_DEFINITIONS (-DPARTIO_USE_ZLIB)

target_link_libraries(partioPRTForWindows ${EXTRA_LIBS})

include_directories ("${CMAKE_CURRENT_BINARY_DIR}/dependencies/zlib")

install(TARGETS partioPRTForWindows DESTINATION ${PROJECT_SOURCE_DIR}/bin)
