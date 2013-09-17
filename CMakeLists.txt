cmake_minimum_required (VERSION 2.8)
project (git_cmake)

# Appends the cmake/modules path to MAKE_MODULE_PATH variable.
set (CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

# Make a version file containing the current version from git.
include (GetGitRevisionDescription)
get_git_head_revision (refspec hash)

configure_file (${CMAKE_SOURCE_DIR}/version.h.in
  ${CMAKE_BINARY_DIR}/version.h)

include_directories (${CMAKE_BINARY_DIR})

# Add the version_file to the project build.
add_executable (${PROJECT_NAME} main.c)

add_custom_target (run
  COMMAND ${PROJECT_NAME}
  DEPENDS ${PROJECT_NAME}
  WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
  )
