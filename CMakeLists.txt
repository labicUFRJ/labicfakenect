######################################################################################
# Fakenect Mock Library
######################################################################################
cmake_minimum_required(VERSION 2.8)

SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
SET(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/lib/labicfakenect)
add_library (labicfakenect SHARED fakenect.c)
set_target_properties ( labicfakenect PROPERTIES
  VERSION ${PROJECT_VER}
  SOVERSION ${PROJECT_APIVER}
  OUTPUT_NAME freenect)
target_link_libraries(labicfakenect ${MATH_LIB})

install (TARGETS labicfakenect
  DESTINATION "${PROJECT_LIBRARY_INSTALL_DIR}/labicfakenect")

add_executable(labicrecord record.c)
target_link_libraries(labicrecord freenect)
install (TARGETS labicrecord
  DESTINATION bin)

CONFIGURE_FILE("fakenect.sh.in"
  "labicfakenect.sh"
  IMMEDIATE @ONLY)
install (PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/labicfakenect.sh
  DESTINATION bin
  RENAME fakenect)
