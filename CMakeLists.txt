cmake_minimum_required(VERSION 3.7.2)
project(boilerplate)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "-Wall -g")

# Add SFML
find_package(SFML 2 COMPONENTS graphics window system REQUIRED)
include_directories(${SFML_INCLUDE_DIR})

set(HEADER_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include)
set(MAIN_FILE ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp)
file(GLOB SOURCE_FILES "src/*.cpp")
list(REMOVE_ITEM SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp)
file(GLOB HEADER_FILES "include/*.h")

# Main executable
add_executable(main ${SOURCE_FILES} ${MAIN_FILE} ${HEADER_FILES})
target_include_directories(main PRIVATE ${HEADER_DIRECTORY} ${SFML_INCLUDE_DIR})
target_link_libraries(main ${SFML_LIBRARIES})

# Tests executable
file(GLOB TESTS "test/*.cpp")
add_executable(tests ${TESTS} ${SOURCE_FILES} ${HEADER_FILES})
target_include_directories(tests PRIVATE ${HEADER_DIRECTORY})
