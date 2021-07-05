cmake_minimum_required (VERSION 3.15)

function(set_version PROJECT MAJOR MINOR)
  execute_process(
    COMMAND git rev-list HEAD --count --${PROJECT}
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    OUTPUT_VARIABLE GIT_RESULT
  )
  string(STRIP ${GIT_RESULT} PATCH)
  
  set(${PROJECT}_VERSION_MAJOR ${MAJOR})
  set(${PROJECT}_VERSION_MINOR ${MINOR})
  set(${PROJECT}_VERSION_PATCH ${PATCH})
endfunction()

set(LIBPATH ${CMAKE_CURRENT_SOURCE_DIR}/libs)
if (CMAKE_BUILD_TYPE STREQUAL "Release")
  set(OUTPATH ${CMAKE_CURRENT_SOURCE_DIR}/bin_Release)
else()
  set(OUTPATH ${CMAKE_CURRENT_SOURCE_DIR}/bin_Debug)
endif()

####################################################
# Project Hill Climb

set(HILL_CLIMB HillClimb)
project (${HILL_CLIMB})
set_version(${HILL_CLIMB} 1 0)

add_subdirectory (${HILL_CLIMB})
####################################################
