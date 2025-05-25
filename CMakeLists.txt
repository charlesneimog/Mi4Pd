cmake_minimum_required(VERSION 3.5)

project(Mi4Pd)

set(PDCMAKE_FILE ${CMAKE_BINARY_DIR}/pd.cmake)
set(PDCMAKE_VERSION "v0.2.0")
if(NOT EXISTS "${PDCMAKE_FILE}")
    file(DOWNLOAD https://raw.githubusercontent.com/pure-data/pd.cmake/refs/tags/${PDCMAKE_VERSION}/pd.cmake ${PDCMAKE_FILE})
endif()
include(${PDCMAKE_FILE})

if(CMAKE_SYSTEM_PROCESSOR MATCHES "arm" OR CMAKE_SYSTEM_PROCESSOR MATCHES "aarch64")
    message(STATUS "Target is ARM")
else()
    message(STATUS "Not ARM build is experimental")
    add_definitions(-DTEST)
endif()

add_subdirectory(mi)
set_target_properties(MILib PROPERTIES POSITION_INDEPENDENT_CODE ON)
include_directories(mi)

pd_add_external(brds~ "${CMAKE_CURRENT_SOURCE_DIR}/brds/brds~.cpp" LINK_LIBRARIES MILib)
pd_add_external(clds~ "${CMAKE_CURRENT_SOURCE_DIR}/clds/clds~.cpp" LINK_LIBRARIES MILib)
pd_add_external(clds_reverb~ "${CMAKE_CURRENT_SOURCE_DIR}/clds_reverb/clds_reverb~.cpp" LINK_LIBRARIES MILib)
pd_add_external(grds~ "${CMAKE_CURRENT_SOURCE_DIR}/grds/grids.cpp" LINK_LIBRARIES MILib)
pd_add_external(lmnts~ "${CMAKE_CURRENT_SOURCE_DIR}/lmnts/lmnts~.cpp" LINK_LIBRARIES MILib)
pd_add_external(rngs~ "${CMAKE_CURRENT_SOURCE_DIR}/rngs/rngs~.cpp" LINK_LIBRARIES MILib)
pd_add_external(rngs_chorus~ "${CMAKE_CURRENT_SOURCE_DIR}/rngs_chorus/rngs_chorus~.cpp" LINK_LIBRARIES MILib)
pd_add_external(rngs_ensemble~ "${CMAKE_CURRENT_SOURCE_DIR}/rngs_ensemble/rngs_ensemble~.cpp" LINK_LIBRARIES MILib)
pd_add_external(rngs_reverb~ "${CMAKE_CURRENT_SOURCE_DIR}/rngs_reverb/rngs_reverb~.cpp" LINK_LIBRARIES MILib)
pd_add_external(wrps~ "${CMAKE_CURRENT_SOURCE_DIR}/wrps/wrps~.cpp" LINK_LIBRARIES MILib)

