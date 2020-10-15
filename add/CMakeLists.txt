cmake_minimum_required(VERSION 3.0)
project(add)

set(TARGET_LIB add.lib)

# Go configurations.
set(GO_LIBNAME libadd.a)

# List all .go files.
file(GLOB_RECURSE GO_SOURCES ./**.go)

# Make .go files visible for QtCreator.
add_custom_target(src SOURCES ${GO_SOURCES})

set(GO_BUILD_COMMAND go build -buildmode=c-archive -o "${CMAKE_CURRENT_BINARY_DIR}/${GO_LIBNAME}" ${CMAKE_GO_FLAGS})

# Custom command for 'go build -buildmode=c-archive ...'
# to create a library from Go codes.
add_custom_command(
  OUTPUT ${GO_LIBNAME}
  DEPENDS ${GO_SOURCES}
  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  COMMAND ${GO_BUILD_COMMAND}
  COMMENT "Building Go library"
  )

# Add a custom target for the library.
add_custom_target(${TARGET_LIB} DEPENDS ${GO_LIBNAME})

# Export target name of the library.
set(TARGET_LIB_ADD ${TARGET_LIB} PARENT_SCOPE)

