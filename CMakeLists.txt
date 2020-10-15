cmake_minimum_required(VERSION 3.0)
project(app)

set(SOURCES app.cpp)
set(LIB_ADD_DIR add)

# Include add project.
add_subdirectory(${LIB_ADD_DIR})

# A library and a header are generated in the binary directory.
include_directories(${CMAKE_CURRENT_BINARY_DIR}/${LIB_ADD_DIR})
link_directories(${CMAKE_CURRENT_BINARY_DIR}/${LIB_ADD_DIR})

add_executable(app ${SOURCES})
add_dependencies(app ${TARGET_LIB_ADD})
target_link_libraries(app add pthread)
