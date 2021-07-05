cmake_minimum_required (VERSION 3.15)

add_executable (${HILL_CLIMB}
  "HillClimb.h"
  "HillClimb.cpp" 
)

target_include_directories(${HILL_CLIMB} PRIVATE
  ${LIBPATH}/box2d-lite/include
  ${LIBPATH}/sfml-2.5.1/include
)

target_compile_definitions(${HILL_CLIMB}
  PRIVATE SFML_DINAMYC
)

if (CMAKE_BUILD_TYPE STREQUAL "Release")
  set(
    LIBS 
      ${LIBPATH}/sfml-2.5.1/bin/sfml-system.lib
      ${LIBPATH}/box2d-lite/bin/box2d-lite.lib
      ${LIBPATH}/sfml-2.5.1/bin/sfml-window.lib
      ${LIBPATH}/sfml-2.5.1/bin/sfml-graphics.lib
  )
  set(
    DLLS
      ${LIBPATH}/sfml-2.5.1/bin/sfml-system-2.dll
      ${LIBPATH}/sfml-2.5.1/bin/sfml-window-2.dll
      ${LIBPATH}/sfml-2.5.1/bin/sfml-graphics-2.dll
  )
else()
  set(
    LIBS 
      ${LIBPATH}/sfml-2.5.1/bin/sfml-system-d.lib
      ${LIBPATH}/box2d-lite/bin/box2d-lite.lib
      ${LIBPATH}/sfml-2.5.1/bin/sfml-window-d.lib
      ${LIBPATH}/sfml-2.5.1/bin/sfml-graphics-d.lib
  )
  set(
    DLLS
      ${LIBPATH}/sfml-2.5.1/bin/sfml-system-d-2.dll
      ${LIBPATH}/sfml-2.5.1/bin/sfml-window-d-2.dll
      ${LIBPATH}/sfml-2.5.1/bin/sfml-graphics-d-2.dll
  )
endif()

set(INSTALL_PATH ${OUTPATH}/${HILL_CLIMB})

set_target_properties(HillClimb PROPERTIES
  CXX_STANDARD 17
  CXX_STANDARD_REQUIRED yes
)

target_link_libraries(${HILL_CLIMB} LINK_PRIVATE ${LIBS})

install(
  TARGETS ${HILL_CLIMB}
  DESTINATION ${INSTALL_PATH}
)
install(
  FILES ${DLLS}
  DESTINATION "${INSTALL_PATH}"
)
