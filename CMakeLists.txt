cmake_minimum_required(VERSION 3.26)

project(valhalla
  VERSION 0.0.1
  DESCRIPTION ""
  LANGUAGES C CXX)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 20)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set(CMAKE_MODULE_PATH 
  "${PROJECT_SOURCE_DIR}/cmake"
  ${CMAKE_MODULE_PATH}
  )

include(LibUtils)

#Note: When using target_compile options all options need to be ; separated with NO spaces!!
#(although I imagine cmake list commands may have done this automatically we got a lot of errors
#using no spaces and then some warning with ; and space)
if (MSVC)
  set(VALHALLA_COMPILE_OPTIONS "/W4;/WX;/permissive-")
else()
  set(VALHALLA_COMPILE_OPTIONS "-Wall;-Wextra;-pedantic;-Werror;-Wno-comment;-Wno-unknown-pragmas")
endif()

# option(VALHALLA_BUILD_DOCS "Whether or not to build documentation.")
# option(VALHALLA_BUILD_TESTS "Whether or not to build tests.")

set(MODULE_ROOT "${PROJECT_SOURCE_DIR}/include")

add_subdirectory(lib)
add_subdirectory(valhalla)
add_subdirectory(app)

#if(VALHALLA_BUILD_TESTS)
#  enable_testing()
#  add_subdirectory(tests)
#endif()

#if(VALHALLA_BUILD_DOCS)
#  add_subdirectory(docs)
#  #Do I need to add pulse's dependancies as well or is that transitive!?
#  # add_dependencies(Doxygen <Target_dependancies>)
#endif()


